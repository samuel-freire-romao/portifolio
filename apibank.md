<?php
session_start();
require_once __DIR__ . '/config.php';

header('Content-Type: application/json; charset=utf-8');

function respond(int $status, array $payload): void
{
    http_response_code($status);
    echo json_encode($payload, JSON_UNESCAPED_UNICODE | JSON_INVALID_UTF8_SUBSTITUTE);
    exit;
}

function hasValidTextLength(string $value, int $maxLength): bool
{
    $length = preg_match_all('/./us', $value);
    return $length !== false && $length <= $maxLength;
}

$action = (string)($_GET['action'] ?? $_POST['action'] ?? '');

if ($action === 'logout') {
    session_unset();
    session_destroy();
    respond(200, ['success' => true]);
}

$db = $conexao;
if (!($db instanceof mysqli)) {
    respond(503, ['success' => false, 'message' => 'Banco de dados indisponível.']);
}

try {
    $user = $_SESSION['user'] ?? null;
    $userId = filter_var($user['id'] ?? null, FILTER_VALIDATE_INT);
    if (!$userId || $userId < 1) {
        respond(401, ['success' => false, 'message' => 'Acesso administrativo necessário.']);
    }

    $authStmt = $db->prepare('SELECT id, email, tipo_usuario FROM usuarios WHERE id = ? LIMIT 1');
    $authStmt->bind_param('i', $userId);
    $authStmt->execute();
    $currentUser = $authStmt->get_result()->fetch_assoc();
    $authStmt->close();
    if (!$currentUser || $currentUser['tipo_usuario'] !== 'admin') {
        session_unset();
        session_destroy();
        respond(401, ['success' => false, 'message' => 'Acesso administrativo necessário.']);
    }
    $user = $currentUser;

    if ($action === 'session') {
        respond(200, ['success' => true, 'id' => $user['id'], 'email' => $user['email'] ?? '']);
    }

    if ($action === 'users') {
        $result = $db->query('SELECT id, nome, telefone, email, tipo_usuario, criado_em FROM usuarios ORDER BY criado_em DESC');
        respond(200, ['success' => true, 'users' => $result->fetch_all(MYSQLI_ASSOC)]);
    }

    if ($action === 'user-create') {
        $name = trim((string)($_POST['nome'] ?? ''));
        $phone = trim((string)($_POST['telefone'] ?? ''));
        $email = strtolower(trim((string)($_POST['email'] ?? '')));
        $password = (string)($_POST['password'] ?? '');
        $role = (string)($_POST['tipo_usuario'] ?? 'cliente');

        if (
            $name === '' || !hasValidTextLength($name, 150) ||
            $phone === '' || !hasValidTextLength($phone, 50) ||
            !hasValidTextLength($email, 150) || !filter_var($email, FILTER_VALIDATE_EMAIL) ||
            strlen($password) < 6 || !in_array($role, ['cliente', 'admin'], true)
        ) {
            respond(400, ['success' => false, 'message' => 'Confira nome, e-mail, telefone, perfil e senha (mínimo de 6 caracteres).']);
        }

        $passwordHash = password_hash($password, PASSWORD_DEFAULT);
        $stmt = $db->prepare('INSERT INTO usuarios (nome, telefone, email, senha, tipo_usuario) VALUES (?, ?, ?, ?, ?)');
        $stmt->bind_param('sssss', $name, $phone, $email, $passwordHash, $role);
        $stmt->execute();
        $stmt->close();
        respond(201, ['success' => true]);
    }

    if ($action === 'user-delete') {
        $id = filter_var($_POST['id'] ?? null, FILTER_VALIDATE_INT);
        if (!$id || $id < 1) {
            respond(400, ['success' => false, 'message' => 'Usuário inválido.']);
        }
        if ((int)$user['id'] === $id) {
            respond(400, ['success' => false, 'message' => 'Não é possível remover a conta administrativa em uso.']);
        }

        $stmt = $db->prepare('DELETE FROM usuarios WHERE id = ?');
        $stmt->bind_param('i', $id);
        $stmt->execute();
        $deleted = $stmt->affected_rows > 0;
        $stmt->close();
        if (!$deleted) {
            respond(404, ['success' => false, 'message' => 'Usuário não encontrado.']);
        }

        respond(200, ['success' => true]);
    }

    if ($action === 'user-update') {
        $id = filter_var($_POST['id'] ?? null, FILTER_VALIDATE_INT);
        $name = trim((string)($_POST['nome'] ?? ''));
        $phone = trim((string)($_POST['telefone'] ?? ''));
        $email = strtolower(trim((string)($_POST['email'] ?? '')));
        $role = (string)($_POST['tipo_usuario'] ?? '');
        $newPassword = (string)($_POST['new_password'] ?? '');

        if (!$id || $id < 1 || $name === '' || $phone === '' || !filter_var($email, FILTER_VALIDATE_EMAIL)) {
            respond(400, ['success' => false, 'message' => 'Confira os dados obrigatórios do usuário.']);
        }
        if (!in_array($role, ['cliente', 'admin'], true)) {
            respond(400, ['success' => false, 'message' => 'Perfil inválido.']);
        }
        if ($newPassword !== '' && strlen($newPassword) < 6) {
            respond(400, ['success' => false, 'message' => 'A nova senha deve ter pelo menos 6 caracteres.']);
        }
        if ((int)$user['id'] === $id && $role !== 'admin') {
            respond(400, ['success' => false, 'message' => 'Não é possível remover seu próprio acesso administrativo.']);
        }

        $check = $db->prepare('SELECT id FROM usuarios WHERE id = ? LIMIT 1');
        $check->bind_param('i', $id);
        $check->execute();
        $check->store_result();
        $exists = $check->num_rows > 0;
        $check->close();
        if (!$exists) {
            respond(404, ['success' => false, 'message' => 'Usuário não encontrado.']);
        }

        if ($newPassword !== '') {
            $passwordHash = password_hash($newPassword, PASSWORD_DEFAULT);
            $stmt = $db->prepare('UPDATE usuarios SET nome = ?, telefone = ?, email = ?, tipo_usuario = ?, senha = ? WHERE id = ?');
            $stmt->bind_param('sssssi', $name, $phone, $email, $role, $passwordHash, $id);
        } else {
            $stmt = $db->prepare('UPDATE usuarios SET nome = ?, telefone = ?, email = ?, tipo_usuario = ? WHERE id = ?');
            $stmt->bind_param('ssssi', $name, $phone, $email, $role, $id);
        }
        $stmt->execute();
        $stmt->close();
        if ((int)$user['id'] === $id) {
            $_SESSION['user']['nome'] = $name;
            $_SESSION['user']['telefone'] = $phone;
            $_SESSION['user']['email'] = $email;
        }
        respond(200, ['success' => true]);
    }

    if ($action === 'orders') {
        $result = $db->query('SELECT id, nome, email, tipo_servico, prazo, descricao, status, valor, created_at FROM pedidos ORDER BY created_at DESC');
        respond(200, ['success' => true, 'orders' => $result->fetch_all(MYSQLI_ASSOC)]);
    }

    if ($action === 'order-update') {
        $id = filter_var($_POST['id'] ?? null, FILTER_VALIDATE_INT);
        $name = trim((string)($_POST['nome'] ?? ''));
        $email = strtolower(trim((string)($_POST['email'] ?? '')));
        $service = trim((string)($_POST['tipo_servico'] ?? ''));
        $deadline = trim((string)($_POST['prazo'] ?? ''));
        $description = trim((string)($_POST['descricao'] ?? ''));

        if (!$id || $id < 1 || $name === '' || !filter_var($email, FILTER_VALIDATE_EMAIL) || $service === '' || $deadline === '' || strlen($description) < 10) {
            respond(400, ['success' => false, 'message' => 'Confira nome, e-mail, serviço, prazo e descrição do pedido.']);
        }

        $stmt = $db->prepare('UPDATE pedidos SET nome = ?, email = ?, tipo_servico = ?, prazo = ?, descricao = ? WHERE id = ?');
        $stmt->bind_param('sssssi', $name, $email, $service, $deadline, $description, $id);
        $stmt->execute();
        if ($stmt->affected_rows === 0) {
            $check = $db->prepare('SELECT id FROM pedidos WHERE id = ? LIMIT 1');
            $check->bind_param('i', $id);
            $check->execute();
            $check->store_result();
            $exists = $check->num_rows > 0;
            $check->close();
            if (!$exists) {
                $stmt->close();
                respond(404, ['success' => false, 'message' => 'Pedido não encontrado.']);
            }
        }
        $stmt->close();
        respond(200, ['success' => true]);
    }

    if ($action === 'order-delete') {
        $id = filter_var($_POST['id'] ?? null, FILTER_VALIDATE_INT);
        if (!$id || $id < 1) {
            respond(400, ['success' => false, 'message' => 'Pedido inválido.']);
        }

        $stmt = $db->prepare('DELETE FROM pedidos WHERE id = ?');
        $stmt->bind_param('i', $id);
        $stmt->execute();
        $deleted = $stmt->affected_rows > 0;
        $stmt->close();
        if (!$deleted) {
            respond(404, ['success' => false, 'message' => 'Pedido não encontrado.']);
        }
        respond(200, ['success' => true]);
    }

    if ($action === 'update') {
        $id = filter_var($_POST['id'] ?? null, FILTER_VALIDATE_INT);
        if (!$id || $id < 1) {
            respond(400, ['success' => false, 'message' => 'Pedido inválido.']);
        }

        if (array_key_exists('status', $_POST)) {
            $status = (string)$_POST['status'];
            $validStatuses = ['recebido', 'em_andamento', 'pronto', 'cancelado'];
            if (!in_array($status, $validStatuses, true)) {
                respond(400, ['success' => false, 'message' => 'Status inválido.']);
            }
            $stmt = $db->prepare('UPDATE pedidos SET status = ? WHERE id = ?');
            $stmt->bind_param('si', $status, $id);
        } elseif (array_key_exists('valor', $_POST)) {
            $value = filter_var($_POST['valor'], FILTER_VALIDATE_FLOAT);
            if ($value === false || $value < 0) {
                respond(400, ['success' => false, 'message' => 'Valor inválido.']);
            }
            $stmt = $db->prepare('UPDATE pedidos SET valor = ? WHERE id = ?');
            $stmt->bind_param('di', $value, $id);
        } else {
            respond(400, ['success' => false, 'message' => 'Nenhuma alteração informada.']);
        }

        $stmt->execute();
        if ($stmt->affected_rows === 0) {
            $check = $db->prepare('SELECT id FROM pedidos WHERE id = ?');
            $check->bind_param('i', $id);
            $check->execute();
            $check->store_result();
            $exists = $check->num_rows > 0;
            $check->close();
            if (!$exists) {
                $stmt->close();
                respond(404, ['success' => false, 'message' => 'Pedido não encontrado.']);
            }
        }
        $stmt->close();
        respond(200, ['success' => true]);
    }

    respond(400, ['success' => false, 'message' => 'Ação inválida.']);
} catch (Throwable $error) {
    error_log('Admin API error: ' . $error->getMessage());
    if ($error instanceof mysqli_sql_exception && (int)$error->getCode() === 1062) {
        respond(409, ['success' => false, 'message' => 'Este e-mail já está associado a outra conta.']);
    }
    respond(500, ['success' => false, 'message' => 'Não foi possível processar a solicitação.']);
}
