<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="referrer" content="no-referrer">
    <meta name="theme-color" content="#080B14">
    <title>Novo pedido — SiteLab</title>
    <meta name="description" content="Conte à SiteLab sobre o projeto que você precisa e receba uma proposta de escopo e prazo.">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        :root {
            color-scheme: dark;
            --bg: #080B14;
            --panel: #0F1526;
            --panel-raised: #131B31;
            --primary: #00D9C0;
            --primary-dark: #06231F;
            --secondary: #FFB454;
            --text: #E8ECF4;
            --muted: #8B95AC;
            --faint: #5C6478;
            --border: rgba(232, 236, 244, 0.12);
            --border-strong: rgba(232, 236, 244, 0.2);
        }

        *, *::before, *::after { box-sizing: border-box; }
        body {
            min-height: 100vh;
            margin: 0;
            color: var(--text);
            background:
                radial-gradient(ellipse at 12% 16%, rgba(0, 217, 192, 0.11), transparent 34rem),
                radial-gradient(ellipse at 88% 82%, rgba(255, 180, 84, 0.08), transparent 30rem),
                var(--bg);
            font-family: 'Inter', system-ui, sans-serif;
            line-height: 1.6;
            -webkit-font-smoothing: antialiased;
        }
        a { color: inherit; text-decoration: none; }
        button, input, select, textarea { font: inherit; }
        .container { width: min(100% - 2.5rem, 1000px); margin-inline: auto; }
        .site-header { border-bottom: 1px solid var(--border); background: rgba(8, 11, 20, 0.84); backdrop-filter: blur(14px); }
        .nav-inner { min-height: 76px; display: flex; align-items: center; justify-content: space-between; gap: 1rem; }
        .logo { display: inline-flex; align-items: center; gap: .55rem; font: 700 1.25rem 'Space Grotesk', sans-serif; }
        .logo > span:last-child { color: var(--primary); }
        .logo-mark { display: grid; place-items: center; width: 34px; height: 34px; border-radius: 9px; color: var(--primary-dark); background: linear-gradient(135deg, var(--primary), #00A78F); font: 500 1rem 'IBM Plex Mono', monospace; }
        .back-link { display: inline-flex; align-items: center; gap: .55rem; min-height: 42px; padding: .55rem .9rem; border: 1px solid var(--border-strong); border-radius: 999px; color: var(--text); font-size: .86rem; font-weight: 600; transition: border-color .2s, color .2s; }
        .back-link:hover { color: var(--primary); border-color: var(--primary); }
        main { padding: clamp(3rem, 8vh, 6rem) 0 5rem; }
        .page-heading { max-width: 680px; margin: 0 auto 2.5rem; text-align: center; }
        .eyebrow { display: inline-flex; align-items: center; gap: .5rem; color: var(--primary); font: 500 .75rem 'IBM Plex Mono', monospace; letter-spacing: .12em; text-transform: uppercase; }
        .eyebrow::before { width: 6px; height: 6px; border-radius: 50%; background: var(--primary); box-shadow: 0 0 8px var(--primary); content: ''; }
        h1 { margin: .8rem 0 0; font: 600 clamp(2rem, 5vw, 3rem)/1.1 'Space Grotesk', sans-serif; }
        .page-heading p { margin: 1rem 0 0; color: var(--muted); font-size: 1rem; }
        .order-shell { max-width: 760px; margin-inline: auto; padding: clamp(1.25rem, 5vw, 2.2rem); border: 1px solid var(--border); border-radius: 18px; background: linear-gradient(145deg, rgba(19, 27, 49, .96), rgba(15, 21, 38, .96)); box-shadow: 0 24px 60px rgba(0, 0, 0, .3), 0 0 36px rgba(0, 217, 192, .08); }
        .order-form { display: grid; gap: 1.2rem; }
        .order-row { display: grid; grid-template-columns: 1fr; gap: 1.2rem; }
        .input-group { display: grid; gap: .5rem; }
        label { color: var(--text); font-size: .88rem; font-weight: 600; }
        input, select, textarea { width: 100%; min-height: 48px; padding: .8rem .95rem; border: 1px solid var(--border-strong); border-radius: 9px; outline: none; background: rgba(255, 255, 255, .025); color: var(--text); transition: border-color .2s, box-shadow .2s; }
        input:focus, select:focus, textarea:focus { border-color: var(--primary); box-shadow: 0 0 0 3px rgba(0, 217, 192, .12); }
        select option { background: var(--panel); color: var(--text); }
        textarea { min-height: 142px; resize: vertical; }
        textarea::placeholder { color: var(--faint); }
        .submit-button { display: inline-flex; align-items: center; justify-content: center; gap: .6rem; justify-self: start; min-height: 48px; padding: .8rem 1.4rem; border: 0; border-radius: 999px; background: var(--primary); color: var(--primary-dark); font-weight: 700; cursor: pointer; transition: transform .2s, box-shadow .2s; }
        .submit-button:hover { transform: translateY(-2px); box-shadow: 0 10px 24px rgba(0, 217, 192, .2); }
        .submit-button:disabled { cursor: wait; opacity: .65; transform: none; }
        .order-msg { padding: .9rem 1rem; border-radius: 9px; font-size: .9rem; }
        .order-msg.ok { border: 1px solid rgba(0, 217, 192, .3); background: rgba(0, 217, 192, .1); color: var(--primary); }
        .order-msg.error { border: 1px solid rgba(255, 95, 87, .3); background: rgba(255, 95, 87, .1); color: #FF8A84; }
        .hidden { display: none !important; }
        .quote-panel { margin-top: 1.5rem; padding: 1.4rem; border: 1px solid rgba(0, 217, 192, .28); border-radius: 12px; background: rgba(0, 217, 192, .07); }
        .quote-label { color: var(--muted); font-size: .82rem; }
        .quote-value { display: block; margin-top: .25rem; color: var(--primary); font: 600 1.8rem/1.2 'Space Grotesk', sans-serif; }
        .quote-note { margin-top: .55rem; color: var(--muted); font-size: .86rem; }
        .tracking-details { display: grid; grid-template-columns: 1fr; gap: .8rem; margin: 1.5rem 0; }
        .tracking-details div { padding-bottom: .7rem; border-bottom: 1px solid var(--border); }
        .tracking-details dt { color: var(--muted); font-size: .78rem; }
        .tracking-details dd { margin: .2rem 0 0; overflow-wrap: anywhere; }
        .tracking-actions { display: flex; gap: .75rem; flex-wrap: wrap; margin-top: 1.4rem; }
        .tracking-button { display: inline-flex; align-items: center; justify-content: center; gap: .55rem; min-height: 46px; padding: .7rem 1.15rem; border: 1px solid var(--border-strong); border-radius: 999px; background: transparent; color: var(--text); font-weight: 600; cursor: pointer; }
        .tracking-button:hover { border-color: var(--primary); color: var(--primary); }
        .tracking-button:disabled { cursor: wait; opacity: .6; }
        :focus-visible { outline: 2px solid var(--primary); outline-offset: 3px; }
        @media (min-width: 640px) { .order-row { grid-template-columns: 1fr 1fr; } .tracking-details { grid-template-columns: 1fr 1fr; } }
        @media (max-width: 480px) {
            .container { width: min(100% - 1.5rem, 1000px); }
            .nav-inner { min-height: 68px; }
            .back-link { width: 42px; justify-content: center; padding: 0; overflow: hidden; font-size: 0; }
            .back-link i { font-size: .9rem; }
            .submit-button { width: 100%; }
        }
        @media (prefers-reduced-motion: reduce) { *, *::before, *::after { scroll-behavior: auto !important; transition-duration: .01ms !important; } }
    </style>
</head>
<body>
    <header class="site-header">
        <div class="container nav-inner">
            <a href="sitelabcliente.html" class="logo" aria-label="SiteLab, voltar ao início">
                <span class="logo-mark">S</span>Site<span>Lab</span>
            </a>
            <a href="sitelabcliente.html" class="back-link"><i class="fa-solid fa-arrow-left" aria-hidden="true"></i> Voltar ao site</a>
        </div>
    </header>
    <main id="main">
        <div class="container">
            <div class="page-heading" id="page-heading">
                <span class="eyebrow">Novo pedido</span>
                <h1>Conte o que você precisa</h1>
                <p>Descreva o projeto e retornamos com escopo e prazo em até 1 dia útil.</p>
            </div>
            <div class="order-shell" id="form-shell">
                <form class="order-form" id="order-form">
                    <div class="order-row">
                        <div class="input-group">
                            <label for="ped-nome">Nome</label>
                            <input id="ped-nome" name="nome" autocomplete="name" required>
                        </div>
                        <div class="input-group">
                            <label for="ped-email">E-mail</label>
                            <input id="ped-email" name="email" type="email" autocomplete="email" required>
                        </div>
                    </div>
                    <div class="order-row">
                        <div class="input-group">
                            <label for="ped-tipo">Tipo de serviço</label>
                            <select id="ped-tipo" name="tipo">
                                <option>Sites institucionais</option>
                                <option>Lojas virtuais</option>
                                <option>Sistemas sob medida</option>
                                <option>Automação de processos</option>
                                <option>Painéis administrativos</option>
                                <option>Manutenção &amp; suporte</option>
                            </select>
                        </div>
                        <div class="input-group">
                            <label for="ped-prazo">Prazo desejado</label>
                            <select id="ped-prazo" name="prazo">
                                <option>Sem pressa</option>
                                <option>Até 1 mês</option>
                                <option>Até 15 dias</option>
                                <option>Urgente (menos de 7 dias)</option>
                            </select>
                        </div>
                    </div>
                    <div class="input-group">
                        <label for="ped-desc">Descrição do pedido</label>
                        <textarea id="ped-desc" name="descricao" required minlength="10" placeholder="Ex.: preciso de uma loja virtual para vender roupas, com pagamento por Pix e cartão."></textarea>
                    </div>
                    <div class="order-msg error" id="order-error" role="alert" hidden>Não foi possível enviar. Tente novamente.</div>
                    <button type="submit" class="submit-button" id="submit-button">Enviar pedido <i class="fa-solid fa-paper-plane" aria-hidden="true"></i></button>
                </form>
            </div>
            <section class="order-shell hidden" id="tracking-shell" aria-labelledby="tracking-title">
                <span class="eyebrow">Acompanhamento</span>
                <h1 id="tracking-title" style="font-size: 1.7rem; margin-top: .6rem;">Seu pedido</h1>
                <div class="quote-panel">
                    <span class="quote-label">Preço do pedido</span>
                    <strong class="quote-value" id="tracking-price">Carregando...</strong>
                    <p class="quote-note" id="tracking-price-note"></p>
                </div>
                <dl class="tracking-details">
                    <div><dt>Serviço</dt><dd id="tracking-service"></dd></div>
                    <div><dt>Status</dt><dd id="tracking-status"></dd></div>
                    <div><dt>Prazo solicitado</dt><dd id="tracking-deadline"></dd></div>
                    <div><dt>Pedido criado</dt><dd id="tracking-created"></dd></div>
                    <div><dt>Descrição</dt><dd id="tracking-description"></dd></div>
                </dl>
                <div class="order-msg error hidden" id="tracking-error" role="alert"></div>
                <div class="tracking-actions">
                    <button class="tracking-button" type="button" id="refresh-tracking"><i class="fa-solid fa-rotate" aria-hidden="true"></i> Atualizar preço</button>
                    <button class="tracking-button" type="button" id="copy-tracking-link"><i class="fa-solid fa-link" aria-hidden="true"></i> Copiar link</button>
                    <a href="pedido.html" class="tracking-button">Fazer outro pedido</a>
                </div>
            </section>
        </div>
    </main>
    <script>
        const form = document.getElementById('order-form');
        const submitButton = document.getElementById('submit-button');
        const errorMessage = document.getElementById('order-error');
        const trackingParams = new URLSearchParams(window.location.search);
        let trackingId = trackingParams.get('pedido');
        let trackingToken = trackingParams.get('token');
        const statusLabels = {
            recebido: 'Recebido',
            em_andamento: 'Em andamento',
            pronto: 'Pronto',
            cancelado: 'Cancelado',
        };

        async function readApiResponse(response) {
            let result;
            try {
                result = await response.json();
            } catch (error) {
                throw new Error('Não foi possível conectar ao servidor do pedido. Abra o site pelo servidor web e tente novamente.');
            }
            if (!response.ok || !result.success) throw new Error(result.message || 'Não foi possível consultar o pedido.');
            return result;
        }

        const formatCurrency = (amount) => Number(amount).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
        const formatDate = (value) => {
            const date = new Date(value);
            return Number.isNaN(date.getTime()) ? '—' : date.toLocaleString('pt-BR');
        };

        try {
            const session = JSON.parse(localStorage.getItem('sitelab-demo-session') || 'null');
            const name = session?.full_name || session?.user_metadata?.full_name || (session?.email ? session.email.split('@')[0] : '');
            if (name) document.getElementById('ped-nome').value = name;
            if (session?.email) document.getElementById('ped-email').value = session.email;
        } catch (error) {
            console.warn('Não foi possível carregar os dados da sessão.', error);
        }

        form.addEventListener('submit', async (event) => {
            event.preventDefault();
            errorMessage.hidden = true;
            submitButton.disabled = true;
            submitButton.innerHTML = 'Enviando...';
            const values = Object.fromEntries(new FormData(form));

            try {
                const response = await fetch('pedido_api.php', {
                    method: 'POST',
                    credentials: 'same-origin',
                    headers: { 'Content-Type': 'application/x-www-form-urlencoded;charset=UTF-8' },
                    body: new URLSearchParams({ action: 'create', ...values }),
                });
                const result = await readApiResponse(response);
                trackingId = String(result.order_id);
                trackingToken = result.tracking_token;
                const url = new URL(window.location.href);
                url.searchParams.set('pedido', result.order_id);
                url.searchParams.set('token', result.tracking_token);
                window.history.replaceState({}, '', url);
                await loadTracking();
            } catch (error) {
                console.error(error);
                errorMessage.textContent = error.message || 'Não foi possível enviar. Tente novamente.';
                errorMessage.hidden = false;
            } finally {
                submitButton.disabled = false;
                submitButton.innerHTML = 'Enviar pedido <i class="fa-solid fa-paper-plane" aria-hidden="true"></i>';
            }
        });

        async function loadTracking() {
            const shell = document.getElementById('tracking-shell');
            const refreshButton = document.getElementById('refresh-tracking');
            const trackingError = document.getElementById('tracking-error');
            shell.classList.remove('hidden');
            document.getElementById('form-shell').classList.add('hidden');
            document.getElementById('page-heading').classList.add('hidden');
            document.getElementById('tracking-title').textContent = `Pedido #${trackingId}`;
            trackingError.classList.add('hidden');
            refreshButton.disabled = true;

            try {
                const query = new URLSearchParams({ action: 'status', id: trackingId, token: trackingToken });
                const response = await fetch(`pedido_api.php?${query}`, { credentials: 'same-origin', cache: 'no-store' });
                const result = await readApiResponse(response);
                const order = result.order;
                const price = Number(order.valor);
                document.getElementById('tracking-price').textContent = price > 0 ? formatCurrency(price) : 'Aguardando orçamento';
                document.getElementById('tracking-price-note').textContent = price > 0
                    ? 'Valor informado pela equipe SiteLab para este pedido.'
                    : 'A equipe analisará os detalhes e atualizará o preço nesta página.';
                document.getElementById('tracking-service').textContent = order.tipo_servico;
                document.getElementById('tracking-status').textContent = statusLabels[order.status] || order.status;
                document.getElementById('tracking-deadline').textContent = order.prazo;
                document.getElementById('tracking-created').textContent = formatDate(order.created_at);
                document.getElementById('tracking-description').textContent = order.descricao;
                document.title = `Pedido #${trackingId} — SiteLab`;
            } catch (error) {
                trackingError.textContent = error.message || 'Não foi possível carregar o acompanhamento do pedido.';
                trackingError.classList.remove('hidden');
            } finally {
                refreshButton.disabled = false;
            }
        }

        document.getElementById('refresh-tracking').addEventListener('click', loadTracking);
        document.getElementById('copy-tracking-link').addEventListener('click', async (event) => {
            try {
                await navigator.clipboard.writeText(window.location.href);
                event.currentTarget.innerHTML = '<i class="fa-solid fa-check" aria-hidden="true"></i> Link copiado';
            } catch (error) {
                const trackingError = document.getElementById('tracking-error');
                trackingError.textContent = 'Não foi possível copiar. Copie o endereço desta página para voltar ao orçamento.';
                trackingError.classList.remove('hidden');
            }
        });

        if (trackingId || trackingToken) {
            loadTracking();
        }
    </script>
</body>
</html>
