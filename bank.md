<?php
session_start();
header('Content-Type: application/json; charset=utf-8');

require_once __DIR__ . '/config.php';
require_once __DIR__ . '/password_utils.php';

function responder(int $status, array $data): void
{
    http_response_code($status);
    echo json_encode($data, JSON_UNESCAPED_UNICODE | JSON_INVALID_UTF8_SUBSTITUTE);
    exit;
}

if ($_SERVER['REQUEST_METHOD'] !== 'POST') {
    responder(405, ['ok' => false, 'mensagem' => 'Método não permitido.']);
}

$dados = json_decode(file_get_contents('php://input'), true);
if (!is_array($dados)) {
    responder(400, ['ok' => false, 'mensagem' => 'Dados inválidos.']);
}

$acao = (string)($dados['acao'] ?? '');

if ($acao === 'logout') {
    $_SESSION = [];
    session_destroy();
    responder(200, ['ok' => true]);
}

if (!isset($conexao) || !($conexao instanceof mysqli)) {
    responder(503, ['ok' => false, 'mensagem' => 'Banco de dados indisponível.']);
}

try {
    if ($acao === 'login') {
        $email = strtolower(trim((string)($dados['email'] ?? '')));
        $senha = (string)($dados['senha'] ?? '');

        if (!filter_var($email, FILTER_VALIDATE_EMAIL) || $senha === '') {
            responder(400, ['ok' => false, 'mensagem' => 'Informe e-mail e senha válidos.']);
        }

        $consulta = $conexao->prepare(
            'SELECT id, nome, email, senha, tipo_usuario FROM usuarios WHERE email = ? LIMIT 1'
        );
        $consulta->bind_param('s', $email);
        $consulta->execute();
        $usuario = $consulta->get_result()->fetch_assoc();
        $consulta->close();

        if (!$usuario || !userPasswordVerify($senha, $usuario['senha'])) {
            responder(401, ['ok' => false, 'mensagem' => 'E-mail ou senha inválidos.']);
        }

        session_regenerate_id(true);
        $_SESSION['user'] = [
            'id' => (int)$usuario['id'],
            'email' => $usuario['email'],
            'tipo_usuario' => $usuario['tipo_usuario'],
        ];

        responder(200, [
            'ok' => true,
            'mensagem' => 'Login realizado com sucesso!',
            'usuario' => [
                'id' => (int)$usuario['id'],
                'email' => $usuario['email'],
                'contato' => $usuario['nome'],
            ],
            'redirect' => $usuario['tipo_usuario'] === 'admin'
                ? 'sitelabadmin.html'
                : 'sitelabcliente.html',
        ]);
    }

    if ($acao === 'cadastro') {
        $nome = trim((string)($dados['nome'] ?? ''));
        $empresa = trim((string)($dados['empresa'] ?? ''));
        $telefone = trim((string)($dados['telefone'] ?? ''));
        $email = strtolower(trim((string)($dados['email'] ?? '')));
        $senha = (string)($dados['senha'] ?? '');

        if ($nome === '') {
            responder(400, ['ok' => false, 'mensagem' => 'Preencha seu nome.']);
        }

        if ($empresa === '') {
            responder(400, ['ok' => false, 'mensagem' => 'Preencha o nome da empresa.']);
        }

        if ($telefone === '') {
            responder(400, ['ok' => false, 'mensagem' => 'Preencha seu telefone.']);
        }

        if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
            responder(400, ['ok' => false, 'mensagem' => 'Informe um endereço de e-mail válido.']);
        }

        if (userPasswordCharacterLength($senha) < 6) {
            responder(400, ['ok' => false, 'mensagem' => 'A senha precisa ter pelo menos 6 caracteres.']);
        }

        $hash = userPasswordHash($senha);
        $consulta = $conexao->prepare(
            "INSERT INTO usuarios (nome, empresa, telefone, email, senha, tipo_usuario)
             VALUES (?, ?, ?, ?, ?, 'cliente')"
        );
        $consulta->bind_param('sssss', $nome, $empresa, $telefone, $email, $hash);
        $consulta->execute();
        $id = (int)$consulta->insert_id;
        $consulta->close();

        session_regenerate_id(true);
        $_SESSION['user'] = [
            'id' => $id,
            'email' => $email,
            'tipo_usuario' => 'cliente',
        ];

        responder(201, [
            'ok' => true,
            'mensagem' => 'Cadastro realizado com sucesso!',
            'usuario' => [
                'id' => $id,
                'email' => $email,
                'contato' => $nome,
            ],
            'redirect' => 'sitelabcliente.html',
        ]);
    }

    responder(400, ['ok' => false, 'mensagem' => 'Ação inválida.']);
} catch (mysqli_sql_exception $erro) {
    if ($acao === 'cadastro' && (int)$erro->getCode() === 1062) {
        responder(409, ['ok' => false, 'mensagem' => 'Este e-mail já está cadastrado.']);
    }

    error_log('Erro de autenticação: ' . $erro->getMessage());
    responder(500, ['ok' => false, 'mensagem' => 'Erro ao processar a solicitação.']);
} catch (RuntimeException $erro) {
    error_log('Erro de autenticação: ' . $erro->getMessage());
    responder(500, ['ok' => false, 'mensagem' => 'Erro ao processar a solicitação.']);
}
