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

$db = $conexao ?? null;
if (!($db instanceof mysqli)) {
    respond(503, ['success' => false, 'message' => 'Banco de dados indisponível.']);
}

$action = (string)($_GET['action'] ?? $_POST['action'] ?? '');

try {
    if ($action === 'mine') {
        $sessionUser = $_SESSION['user'] ?? null;
        if (!$sessionUser || ($sessionUser['tipo_usuario'] ?? '') !== 'cliente' || empty($sessionUser['id'])) {
            respond(401, ['success' => false, 'message' => 'Entre na sua conta de cliente para ver seus pedidos.']);
        }

        $clientId = (int)$sessionUser['id'];
        $clientEmail = strtolower(trim((string)($sessionUser['email'] ?? '')));
        $stmt = $db->prepare('SELECT id, tipo_servico, prazo, descricao, status, valor, created_at FROM pedidos WHERE cliente_id = ? OR (cliente_id IS NULL AND LOWER(email) = ?) ORDER BY created_at DESC');
        $stmt->bind_param('is', $clientId, $clientEmail);
        $stmt->execute();
        $result = $stmt->get_result();
        $orders = $result->fetch_all(MYSQLI_ASSOC);
        $stmt->close();
        respond(200, ['success' => true, 'orders' => $orders]);
    }

    if ($action === 'health') {
        $db->query('SELECT id, nome, email, tipo_servico, prazo, descricao, status, valor, tracking_token_hash, created_at FROM pedidos LIMIT 0');
        respond(200, ['success' => true, 'message' => 'Conexão com o banco e tabela pedidos confirmadas.']);
    }

    if ($action === 'create') {
        $name = trim((string)($_POST['nome'] ?? ''));
        $email = strtolower(trim((string)($_POST['email'] ?? '')));
        $service = trim((string)($_POST['tipo'] ?? ''));
        $deadline = trim((string)($_POST['prazo'] ?? ''));
        $description = trim((string)($_POST['descricao'] ?? ''));

        if ($name === '' || $service === '' || $deadline === '' || strlen($description) < 10 || !filter_var($email, FILTER_VALIDATE_EMAIL)) {
            respond(400, ['success' => false, 'message' => 'Confira os dados do pedido e tente novamente.']);
        }

        $clientId = null;
        $sessionUser = $_SESSION['user'] ?? null;
        if (($sessionUser['tipo_usuario'] ?? '') === 'cliente' && !empty($sessionUser['id'])) {
            $clientId = (int)$sessionUser['id'];
        }

        $trackingToken = bin2hex(random_bytes(32));
        $trackingHash = hash('sha256', $trackingToken);
        $status = 'recebido';
        $value = 0.00;
        $stmt = $db->prepare('INSERT INTO pedidos (cliente_id, nome, email, tipo_servico, prazo, descricao, status, valor, tracking_token_hash) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)');
        $stmt->bind_param('issssssds', $clientId, $name, $email, $service, $deadline, $description, $status, $value, $trackingHash);
        $stmt->execute();
        $orderId = (int)$stmt->insert_id;
        $stmt->close();

        respond(201, [
            'success' => true,
            'message' => 'Pedido enviado. Você pode acompanhar o orçamento neste link.',
            'order_id' => $orderId,
            'tracking_token' => $trackingToken,
        ]);
    }

    if ($action === 'status') {
        $orderId = filter_var($_GET['id'] ?? null, FILTER_VALIDATE_INT);
        $trackingToken = (string)($_GET['token'] ?? '');
        if (!$orderId || $orderId < 1 || !preg_match('/^[a-f0-9]{64}$/', $trackingToken)) {
            respond(400, ['success' => false, 'message' => 'Link de acompanhamento inválido.']);
        }

        $trackingHash = hash('sha256', $trackingToken);
        $stmt = $db->prepare('SELECT tipo_servico, prazo, descricao, status, valor, created_at FROM pedidos WHERE id = ? AND tracking_token_hash = ? LIMIT 1');
        $stmt->bind_param('is', $orderId, $trackingHash);
        $stmt->execute();
        $service = '';
        $deadline = '';
        $description = '';
        $status = '';
        $value = '0.00';
        $createdAt = '';
        $stmt->bind_result($service, $deadline, $description, $status, $value, $createdAt);
        $found = $stmt->fetch();
        $stmt->close();

        if (!$found) {
            respond(404, ['success' => false, 'message' => 'Pedido não encontrado. Verifique o link de acompanhamento.']);
        }

        respond(200, [
            'success' => true,
            'order' => [
                'id' => $orderId,
                'tipo_servico' => $service,
                'prazo' => $deadline,
                'descricao' => $description,
                'status' => $status,
                'valor' => (float)$value,
                'created_at' => $createdAt,
            ],
        ]);
    }

    respond(400, ['success' => false, 'message' => 'Ação inválida.']);
} catch (Throwable $error) {
    error_log('Order API error: ' . $error->getMessage());
    if ($error instanceof mysqli_sql_exception && in_array((int)$error->getCode(), [1054, 1146], true)) {
        respond(503, ['success' => false, 'message' => 'A tabela pedidos está ausente ou sem as colunas necessárias. Execute pedidos_schema.sql no banco configurado em config.php.']);
    }
    respond(500, ['success' => false, 'message' => 'Não foi possível processar o pedido.']);
}
