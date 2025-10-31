<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema Metanol</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0d1117;
            --border-color: #30363d;
            --text-color: #c9d1d9;
            --green-accent: #238636;
            --green-glow: #2ea043;
            --card-bg: rgba(22, 27, 34, 0.85);
            --red-accent: #da3633;
            --purple-accent: #8957e5;
            --purple-glow: #a77dff;
            --blue-accent: #1f6feb;
            --blue-glow: #388bfd;
        }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
        @keyframes backgroundShine {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        @keyframes float-icon {
            0% { transform: translateY(0px) rotate(-5deg); }
            50% { transform: translateY(-8px) rotate(5deg); }
            100% { transform: translateY(0px) rotate(-5deg); }
        }
        
        @keyframes rotate-scanner {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        @keyframes rotate-scanner-reverse {
            from { transform: rotate(360deg); }
            to { transform: rotate(0deg); }
        }

        .scanner-animation {
            filter: drop-shadow(0 0 15px var(--purple-glow));
        }
        .scanner-outer-ring {
            transform-origin: center;
            animation: rotate-scanner 10s linear infinite;
        }
        .scanner-inner-ring {
            transform-origin: center;
            animation: rotate-scanner-reverse 15s linear infinite;
        }

        @keyframes pulse-glow {
            0%, 100% {
                transform: scale(1);
                opacity: 0.8;
            }
            50% {
                transform: scale(1.05);
                opacity: 1;
            }
        }

        @keyframes card-entry {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .card-entry-animation {
            animation: card-entry 0.5s ease-out forwards;
            opacity: 0; /* Começa invisível para a animação */
        }

        body {
            font-family: 'Poppins', sans-serif;
            background-color: #0A090F;
            color: var(--text-color);
            overflow-x: hidden;
        }

        #menu-principal {
            background-image: 
                radial-gradient(ellipse at 10% 20%, rgba(46, 160, 67, 0.2) 0%, transparent 50%),
                radial-gradient(ellipse at 95% 80%, rgba(137, 87, 229, 0.2) 0%, transparent 50%);
        }

        .placar, .elenco-box, .console-sistema, .modal-content, .card-historico {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            backdrop-filter: blur(12px);
            animation: fadeIn 0.5s ease-out forwards;
        }
        .console-sistema {
            border: 1px solid var(--green-accent);
            box-shadow: 0 0 20px rgba(35, 134, 54, 0.4);
        }
        #mensagens-sistema, #historico-content {
            height: 500px;
            overflow-y: auto;
            border-bottom: 1px solid var(--border-color);
            scrollbar-width: thin;
            scrollbar-color: var(--green-accent) var(--bg-color);
        }
        #historico-content {
             height: 70vh;
             border: 1px solid var(--border-color);
             border-radius: 8px;
        }
        #mensagens-sistema p { margin-bottom: 0.5rem; }
        .action-button, .diretrizes-btn {
            transition: all 0.3s ease;
            text-transform: uppercase;
            font-weight: 600;
            letter-spacing: 0.5px;
            border-radius: 8px;
        }
        .action-button:hover:not(:disabled) {
            transform: scale(1.03);
            box-shadow: 0 0 15px var(--green-glow);
        }
        .action-button:disabled { opacity: 0.5; cursor: not-allowed; }
        .btn-primary {
            background: linear-gradient(45deg, var(--green-accent), var(--green-glow));
            background-size: 200% 200%;
            border: none;
            color: white;
            animation: backgroundShine 5s linear infinite;
        }
        .btn-danger {
            background: linear-gradient(45deg, var(--red-accent), #ff5e5b); 
            box-shadow: 0 0 15px var(--red-accent);
        }
         .btn-danger:hover:not(:disabled) {
             box-shadow: 0 0 15px #ff5e5b;
         }
        .btn-secondary {
            background-color: transparent;
            border: 1px solid var(--green-accent);
            color: var(--green-glow);
        }
        .btn-secondary:hover:not(:disabled) {
             background-color: var(--green-accent);
             color: white;
        }
        .btn-purple {
            background-color: var(--purple-accent);
            border: 1px solid var(--purple-glow);
            color: white;
        }
         .btn-purple:hover:not(:disabled) {
             box-shadow: 0 0 15px var(--purple-glow);
             background-color: var(--purple-glow);
         }
        .btn-pact {
            background: linear-gradient(45deg, #c31432, #ff416c);
            border: none;
            color: white;
            box-shadow: 0 0 15px #ff416c;
            animation: backgroundShine 3s linear infinite;
        }
        .btn-pact:hover {
            box-shadow: 0 0 25px #ff416c !important;
        }
        .player-choice-btn {
            background: rgba(33, 38, 45, 0.7);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            backdrop-filter: blur(5px);
            transition: all 0.2s ease-in-out;
        }
        .player-choice-btn:hover {
            border-color: var(--green-glow);
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(46, 160, 67, 0.2);
        }
        .diretrizes-btn {
            background: none; border: none;
            color: var(--green-glow);
            text-decoration: underline;
            cursor: pointer; font-weight: bold;
        }
        /* CORREÇÃO: Efeito de brilho adicionado a todas as raridades de texto */
        .rarity-diamante { color: #b9f2ff; text-shadow: 0 0 5px #b9f2ff; }
        .rarity-ouro { color: #ffd700; text-shadow: 0 0 5px #ffd700; }
        .rarity-prata { color: #c0c0c0; text-shadow: 0 0 5px #c0c0c0; }
        .rarity-bronze { color: #cd7f32; text-shadow: 0 0 5px #cd7f32; }
        
        .menu-title {
            background: linear-gradient(to right, #e0e0e0, #ffffff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .menu-button-primary, .menu-button-secondary {
            display: flex;
            align-items: center;
            width: 100%;
            padding: 1rem;
            border-radius: 0.75rem; /* 12px */
            transition: all 0.2s ease-in-out;
            border: 1px solid transparent;
            gap: 1rem; /* 16px */
        }
        .menu-button-primary {
            background-color: var(--green-glow);
            color: #0A090F;
            border-color: var(--green-glow);
            box-shadow: 0 5px 20px rgba(46, 160, 67, 0.4);
        }
        .menu-button-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(46, 160, 67, 0.5);
        }
        .menu-button-secondary {
            background-color: rgba(255, 255, 255, 0.03);
            border-color: rgba(255, 255, 255, 0.1);
            color: var(--text-color);
        }
        .menu-button-secondary:hover {
            background-color: rgba(255, 255, 255, 0.07);
            border-color: rgba(255, 255, 255, 0.2);
        }

        .menu-button-purple {
            background-color: rgba(137, 87, 229, 0.15);
            border-color: rgba(137, 87, 229, 0.3);
            color: var(--purple-glow);
        }
        .menu-button-purple:hover {
            background-color: rgba(137, 87, 229, 0.25);
            border-color: var(--purple-glow);
            box-shadow: 0 0 15px rgba(167, 125, 255, 0.3);
        }

        .modal { background-color: rgba(0,0,0,0.8); backdrop-filter: blur(5px); }
        .modal-content {
            max-height: 90vh;
            /* Estilos padrão agora são aplicados via seletor :not() para evitar conflitos */
        }
        /* Novo: Estilo padrão do modal */
        .modal-content:not([class*="modal-rarity-"]) {
             border: 1px solid var(--green-glow);
             box-shadow: 0 0 25px rgba(46, 160, 67, 0.5);
        }
        /* Novos Brilhos de Raridade para Modals */
        .modal-rarity-diamond {
            border: 1px solid #b9f2ff;
            box-shadow: 0 0 25px rgba(185, 242, 255, 0.5), 0 0 40px rgba(185, 242, 255, 0.3) inset;
        }
        .modal-rarity-gold {
            border: 1px solid #ffd700;
            box-shadow: 0 0 25px rgba(255, 215, 0, 0.5), 0 0 40px rgba(255, 215, 0, 0.3) inset;
        }
        .modal-rarity-silver {
            border: 1px solid #c0c0c0;
            box-shadow: 0 0 25px rgba(192, 192, 192, 0.5), 0 0 40px rgba(192, 192, 192, 0.3) inset;
        }
        .modal-rarity-bronze {
            border: 1px solid #cd7f32;
            box-shadow: 0 0 25px rgba(205, 127, 50, 0.5), 0 0 40px rgba(205, 127, 50, 0.3) inset;
        }
        .modal-rarity-pact { /* Para eventos perigosos/arriscados */
            border: 1px solid var(--red-accent);
            box-shadow: 0 0 25px rgba(218, 54, 51, 0.6), 0 0 40px rgba(218, 54, 51, 0.3) inset;
        }
        .modal-rarity-success { /* Para eventos positivos */
            border: 1px solid var(--green-glow);
            box-shadow: 0 0 25px rgba(46, 160, 67, 0.6), 0 0 40px rgba(46, 160, 67, 0.3) inset;
        }
        .modal-rarity-purple {
            border: 1px solid var(--purple-glow);
            box-shadow: 0 0 25px rgba(167, 125, 255, 0.5), 0 0 40px rgba(137, 87, 229, 0.3) inset;
        }

        #jogo-rapido-container {
            background-image:
                radial-gradient(ellipse at center, rgba(13, 17, 23, 0) 0%, var(--bg-color) 70%),
                linear-gradient(rgba(137, 87, 229, 0.15), rgba(13, 17, 23, 1) 80%);
        }

        .btn-jogo-rapido-win {
            transition: all 0.3s ease;
            border-radius: 8px;
            font-weight: 700;
            text-transform: uppercase;
            padding: 1rem;
            color: white;
        }

        .btn-win-caio {
            background: linear-gradient(45deg, var(--blue-accent), var(--blue-glow));
            box-shadow: 0 0 15px var(--blue-glow);
        }
        .btn-win-caio:hover {
            box-shadow: 0 0 25px var(--blue-glow);
        }

        .btn-win-ricardo {
            background: linear-gradient(45deg, var(--red-accent), #ff5e5b);
            box-shadow: 0 0 15px var(--red-accent);
        }
        .btn-win-ricardo:hover {
            box-shadow: 0 0 25px #ff5e5b;
        }

        .dossier-section {
            margin-bottom: 1.5rem;
        }
        .dossier-card {
            background-color: rgba(33, 38, 45, 0.9);
            border: 1px solid var(--border-color);
            padding: 1rem;
            border-radius: 8px;
        }
        .dossier-card-title {
            color: var(--green-glow);
            font-weight: 600;
            text-transform: uppercase;
            font-size: 0.8rem;
            letter-spacing: 0.5px;
            margin-bottom: 0.5rem;
        }

        .player-card-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: rgba(255, 255, 255, 0.05);
            padding: 0.75rem;
            border-radius: 12px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s ease; /* Adicionando transição para suavidade */
        }

        /* CORREÇÃO: Novas classes de brilho para os cards de jogadores */
        /* Os nomes das classes foram traduzidos para corresponder aos dados em JavaScript */
        .card-glow-diamante {
            border-color: rgba(185, 242, 255, 0.5);
            box-shadow: 0 2px 15px rgba(185, 242, 255, 0.2);
        }
        .card-glow-ouro {
            border-color: rgba(255, 215, 0, 0.5);
            box-shadow: 0 2px 15px rgba(255, 215, 0, 0.2);
        }
        .card-glow-prata {
            border-color: rgba(192, 192, 192, 0.5);
            box-shadow: 0 2px 15px rgba(192, 192, 192, 0.2);
        }
        .card-glow-bronze {
            border-color: rgba(205, 127, 50, 0.5);
            box-shadow: 0 2px 15px rgba(205, 127, 50, 0.2);
        }

        .player-card-info {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .player-card-ovr {
            font-size: 1.25rem;
            font-weight: 700;
            padding: 0.5rem 0.75rem;
            border-radius: 8px;
            background: rgba(0,0,0,0.3);
        }

        .fire-border {
            border: 2px solid transparent;
            position: relative;
        }
        .fire-border::before {
            content: '';
            position: absolute;
            top: -2px; left: -2px; right: -2px; bottom: -2px;
            border-radius: 8px;
            background: linear-gradient(45deg, #ff6600, #ff4500, #ff8c00, #ff4500);
            background-size: 400%;
            z-index: -1;
            animation: fire-glow 8s linear infinite;
        }
        @keyframes fire-glow {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

    </style>
</head>
<body>

    <!-- Menu Principal -->
    <div id="menu-principal" class="relative flex flex-col items-center justify-center min-h-screen p-4">
        
        <div class="text-center w-full max-w-md">
            <svg class="mx-auto mb-4" width="80" height="80" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg" style="animation: float-icon 6s ease-in-out infinite;">
                <defs>
                    <filter id="neon-glow" x="-50%" y="-50%" width="200%" height="200%">
                        <feGaussianBlur in="SourceGraphic" stdDeviation="3" result="blur"></feGaussianBlur>
                        <feMerge>
                            <feMergeNode in="blur"></feMergeNode>
                            <feMergeNode in="SourceGraphic"></feMergeNode>
                        </feMerge>
                    </filter>
                </defs>
                <g style="filter: url(#neon-glow);">
                    <path d="M41.7586 6.00012H22.2414C21.0034 6.00012 20 7.00355 20 8.2415V48.1105C20 54.3411 25.1822 59.2787 31.3672 58.9953C37.496 58.7145 42.022 53.6062 42.022 47.465V8.2415C42.022 7.00355 41.0186 6.00012 39.7586 6.00012H41.7586Z" stroke="#9FA8DA" stroke-width="3" fill="rgba(30, 30, 45, 0.3)"></path>
                    <path d="M24 38.0001C24 36.3433 25.3431 35.0001 27 35.0001H37C38.6569 35.0001 40 36.3433 40 38.0001V47.465C40 52.5401 35.4191 56.702 30.3621 56.984C25.3582 57.2625 24 52.8872 24 48.1105V38.0001Z" fill="#2ea043"></path>
                    <path d="M28 43L36 43" stroke="#0d1117" stroke-width="2" stroke-linecap="round"></path>
                    <path d="M28 48L36 48" stroke="#0d1117" stroke-width="2" stroke-linecap="round"></path>
                     <path d="M22 6L42 6" stroke="#c9d1d9" stroke-width="4" stroke-linecap="round"></path>
                </g>
            </svg>

            <h1 class="text-4xl md:text-5xl font-bold text-white uppercase tracking-widest menu-title mb-2">
                Sistema Metanol
            </h1>
            <p class="text-sm text-gray-400 mb-10">Onde lendas são forjadas e rivalidades eternizadas.</p>
            
            <div class="flex flex-col space-y-3 w-full">
                <button id="btn-jogar" class="menu-button-primary">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                    <div class="text-left flex flex-col">
                        <span class="font-semibold leading-tight">Jogar</span>
                        <span class="text-xs opacity-70 leading-tight">Iniciar nova temporada</span>
                    </div>
                    <svg class="w-5 h-5 ml-auto opacity-80" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                </button>
                <button id="btn-historico" class="menu-button-secondary">
                    <svg class="w-6 h-6 opacity-80" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                    <div class="text-left flex flex-col">
                        <span class="font-semibold leading-tight">Histórico</span>
                        <span class="text-xs opacity-70 leading-tight">Ver temporadas anteriores</span>
                    </div>
                     <svg class="w-5 h-5 ml-auto opacity-50" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                </button>
                <button id="btn-regras" class="menu-button-secondary">
                   <svg class="w-6 h-6 opacity-80" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v11.494M12 6.253A4.5 4.5 0 007.5 1.753V3.75a4.5 4.5 0 014.5 4.5V6.253zM12 6.253A4.5 4.5 0 0116.5 1.753V3.75a4.5 4.5 0 00-4.5 4.5V6.253z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.75 6.75h16.5v11.5a2 2 0 01-2 2H5.75a2 2 0 01-2-2V6.75z"></path></svg>
                    <div class="text-left flex flex-col">
                        <span class="font-semibold leading-tight">Manual de Regras</span>
                        <span class="text-xs opacity-70 leading-tight">Entenda como jogar</span>
                    </div>
                     <svg class="w-5 h-5 ml-auto opacity-50" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                </button>
                <button id="btn-modos-jogo" class="menu-button-secondary menu-button-purple">
                    <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 3.104v5.714a2.25 2.25 0 01-.659 1.591L5 14.5M9.75 3.104c-.251.023-.501.05-.75.082m.75-.082a24.301 24.301 0 014.5 0m0 0v5.714c0 .597.237 1.17.659 1.591L19 14.5M14.25 3.104c.251.023.501.05.75.082M19 14.5h-14a1 1 0 00-1 1v4.5A2.25 2.25 0 006.25 22h11.5A2.25 2.25 0 0020 19.5v-4.5a1 1 0 00-1-1z" />
                    </svg>
                    <div class="text-left flex flex-col">
                        <span class="font-semibold leading-tight">Modos de Jogo</span>
                        <span class="text-xs opacity-70 leading-tight">Explore outras formas de jogar</span>
                    </div>
                     <svg class="w-5 h-5 ml-auto opacity-50" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                </button>
            </div>
        </div>
        
        <div class="absolute bottom-8">
             <button id="admin-btn-menu" class="flex items-center space-x-2 text-sm text-gray-500 hover:text-white transition-colors">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path></svg>
                <span>Administração</span>
            </button>
        </div>
    </div>

    <!-- Container do Jogo -->
    <div id="jogo-container" class="hidden relative">
        <button id="btn-voltar-menu-jogo" class="absolute top-6 left-6 py-1 px-3 text-sm action-button btn-secondary z-20">Voltar ao Menu</button>
        
        <div class="container mx-auto max-w-7xl">
            <header class="text-center mb-4 pt-8">
                <h1 class="text-3xl md:text-5xl font-bold text-white mb-4" style="text-shadow: 0 0 10px var(--green-glow);">
                    🧪 SISTEMA METANOL 🧪
                </h1>
            </header>

            <div id="placar-temporada" class="placar p-3 rounded-lg text-lg text-center mb-8">⚔️ TEMPORADA ATUAL: CAIO 0 x 0 RICARDO ⚔️ (MD7)</div>

            <main class="grid grid-cols-1 lg:grid-cols-4 gap-8">
                <!-- Time Caio (Esquerda) -->
                <!-- CORREÇÃO: Adicionado 'flex flex-col' para corrigir a diagramação da lista de jogadores -->
                <div id="elenco-caio" class="elenco-box p-4 rounded-lg lg:col-span-1 flex flex-col">
                    <div id="header-caio" class="mb-4"></div>
                    <div id="tatica-caio" class="text-center text-sm text-green-400 font-bold mb-4 h-6 flex-shrink-0"></div>
                    <!-- CORREÇÃO: Adicionado 'flex-grow overflow-y-auto min-h-0' para a lista rolar corretamente -->
                    <ul id="lista-caio" class="space-y-2 mt-4 flex-grow overflow-y-auto min-h-0"></ul>
                </div>

                <!-- Console Central -->
                <div class="lg:col-span-2 console-sistema p-4 rounded-lg flex flex-col">
                    <div id="mensagens-sistema" class="p-2 mb-4 text-sm md:text-base flex-grow"></div>
                    <div id="area-de-escolha" class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4"></div>
                    <div id="area-de-decisao" class="text-center mb-4"></div>
                    <div id="area-de-comandos" class="mt-auto pt-4 border-t border-gray-700"></div>
                </div>

                <!-- Time Ricardo (Direita) -->
                 <!-- CORREÇÃO: Adicionado 'flex flex-col' para corrigir a diagramação da lista de jogadores -->
                <div id="elenco-ricardo" class="elenco-box p-4 rounded-lg lg:col-span-1 flex flex-col">
                    <div id="header-ricardo" class="mb-4"></div>
                    <div id="tatica-ricardo" class="text-center text-sm text-green-400 font-bold mb-4 h-6 flex-shrink-0"></div>
                    <!-- CORREÇÃO: Adicionado 'flex-grow overflow-y-auto min-h-0' para a lista rolar corretamente -->
                    <ul id="lista-ricardo" class="space-y-2 mt-4 flex-grow overflow-y-auto min-h-0"></ul>
                </div>
            </main>

            <footer class="text-center mt-8">
                <div id="placar-geral" class="placar p-3 rounded-lg text-lg inline-block">🏆 PLACAR GERAL: CAIO 0 x 0 RICARDO 🏆</div>
            </footer>
        </div>
    </div>
    
    <!-- Container do Histórico -->
    <div id="historico-container" class="hidden">
         <div class="container mx-auto max-w-4xl">
              <div class="text-center mb-8">
                <h1 class="text-3xl md:text-5xl font-bold text-white mb-4" style="text-shadow: 0 0 10px var(--green-glow);">
                    🏆 Hall dos Campeões 🏆
                </h1>
            </div>
            <div id="historico-content" class="p-4 space-y-6"></div>
            <div class="text-center mt-8">
                 <button id="btn-voltar-menu" class="py-3 px-6 text-lg action-button btn-secondary">Voltar ao Menu</button>
            </div>
         </div>
    </div>

    <!-- Container Jogo Rápido -->
    <div id="jogo-rapido-container" class="hidden">
        <!-- Layout será gerado via JS -->
    </div>
    <!-- Container Sorteio de Times -->
    <div id="sorteio-times-container" class="hidden">
        <!-- Layout será gerado via JS -->
    </div>


    <!-- Modal -->
    <div id="modal" class="fixed inset-0 z-50 items-center justify-center p-4 hidden">
        <div class="modal-backdrop fixed inset-0"></div>
        <div class="modal-content relative w-full max-w-2xl p-6 rounded-lg overflow-y-auto">
            <h2 id="modal-title" class="text-2xl font-bold mb-4 text-green-400"></h2>
            <div id="modal-body" class="text-base"></div>
            <button id="modal-close-btn" class="absolute top-4 right-4 text-gray-400 hover:text-white text-2xl">&times;</button>
        </div>
    </div>

    <script>
        // --- BANCO DE DADOS ---
        let playersDB = {
            diamante: [], ouro: [], prata: [], bronze: []
        };

        const csvData = `Overall,Nome,Time,Liga,PlayStyles
💎 91,Kylian Mbappé,Real Madrid,LALIGA EA SPORTS,"Quick Step+, Acrobatic, Finesse Shot, Flair, Rapid, Trivela"
💎 91,Rodri,Manchester City,Premier League,"Tiki Taka+, Aerial, Bruiser, Long Ball Pass, Power Shot, Press Proven"
💎 91,Erling Haaland,Manchester City,Premier League,"Acrobatic+, Bruiser, Power Header, Power Shot, Press Proven"
💎 90,Jude Bellingham,Real Madrid,LALIGA EA SPORTS,"Relentless+, Flair, Intercept, Slide Tackle, Technical"
💎 90,Vini Jr.,Real Madrid,LALIGA EA SPORTS,"Quick Step+, Chip Shot, Finesse Shot, First Touch, Flair, Rapid, Trivela"
💎 90,Kevin De Bruyne,Manchester City,Premier League,"Incisive Pass+, Dead Ball, Long Ball Pass, Pinged Pass, Trivela, Whipped Pass"
💎 90,Harry Kane,FC Bayern München,Bundesliga,"Finesse Shot+, First Touch, Incisive Pass, Long Ball Pass, Power Header, Trivela"
💎 89,Martin Ødegaard,Arsenal,Premier League,"Incisive Pass+, First Touch, Flair, Pinged Pass, Technical, Trivela, Whipped Pass"
💎 89,Gianluigi Donnarumma,Paris SG,Ligue 1 McDonald's,"Deflector+, Footwork"
💎 89,Alisson,Liverpool,Premier League,"Deflector+, 1v1 Close Down, Far Throw"
💎 89,Thibaut Courtois,Real Madrid,LALIGA EA SPORTS,"1v1 Close Down+, Cross Claimer, Far Throw"
💎 89,Lautaro Martínez,Lombardia FC,Serie A Enilive,"Finesse Shot+, Power Shot, Relentless, Technical"
💎 89,Virgil van Dijk,Liverpool,Premier League,"Aerial+, Anticipate, Block, Bruiser, Jockey, Long Ball Pass, Power Header"
💎 89,Marc-André ter Stegen,FC Barcelona,LALIGA EA SPORTS,"Footwork+, 1v1 Close Down"
💎 89,Mohamed Salah,Liverpool,Premier League,"Finesse Shot+, Chip Shot, Rapid, Trivela"
🥇 88,Phil Foden,Manchester City,Premier League,"Technical+, First Touch, Flair"
🥇 88,Lionel Messi,Inter Miami CF,MLS,"Technical+, Dead Ball, Finesse Shot, Incisive Pass, Quick Step, Tiki Taka, Trivela"
🥇 88,Antoine Griezmann,Atlético de Madrid,LALIGA EA SPORTS,"Finesse Shot+, Acrobatic, Chip Shot, Flair, Incisive Pass, Technical, Trivela"
🥇 88,Rúben Dias,Manchester City,Premier League,"Bruiser+, Power Header"
🥇 88,Robert Lewandowski,FC Barcelona,LALIGA EA SPORTS,"Chip Shot+, Finesse Shot, First Touch, Incisive Pass, Power Header, Power Shot, Trivela"
🥇 88,Federico Valverde,Real Madrid,LALIGA EA SPORTS,"Power Shot+, Long Ball Pass, Rapid, Relentless, Trivela"
🥇 88,Ederson,Manchester City,Premier League,"Long Ball Pass+, Cross Claimer, Pinged Pass"
🥇 88,Bernardo Silva,Manchester City,Premier League,"Technical+, Flair, Relentless, Tiki Taka, Trivela, Whipped Pass"
🥇 88,Jan Oblak,Atlético de Madrid,LALIGA EA SPORTS,"Far Reach+, Cross Claimer, Far Throw"
🥇 88,Antonio Rüdiger,Real Madrid,LALIGA EA SPORTS,"Bruiser+, Acrobatic, Aerial, Block, Jockey"
🥇 88,Florian Wirtz,Leverkusen,Bundesliga,"Incisive Pass+, Chip Shot, Finesse Shot, First Touch, Flair, Technical, Trivela"
🥇 88,Gregor Kobel,Borussia Dortmund,Bundesliga,"1v1 Close Down+, Deflector, Far Throw"
🥇 87,William Saliba,Arsenal,Premier League,"Anticipate+, Jockey"
🥇 87,Victor Osimhen,SSC Napoli,Serie A Enilive,"Acrobatic, Chip Shot, Power Header, Rapid"
🥇 87,Jamal Musiala,FC Bayern München,Bundesliga,"Technical+, Flair, Incisive Pass, Trickster"
🥇 87,Bukayo Saka,Arsenal,Premier League,"Finesse Shot, Flair, Technical, Whipped Pass"
🥇 87,Paulo Dybala,AS Roma,Serie A Enilive,"First Touch+, Dead Ball, Finesse Shot, Flair, Incisive Pass, Technical, Trivela"
🥇 87,Theo Hernández,Milano FC,Serie A Enilive,"Bruiser+, Anticipate, Long Throw, Quick Step, Rapid, Relentless"
🥇 87,Neymar Jr,Al Hilal,ROSHN Saudi League,"Trickster+, First Touch, Flair, Incisive Pass, Technical, Trivela"
🥇 87,Declan Rice,Arsenal,Premier League,"Block, Intercept, Long Ball Pass, Press Proven"
🥇 87,Frenkie de Jong,FC Barcelona,LALIGA EA SPORTS,"Trivela+, Flair, Incisive Pass, Long Ball Pass, Press Proven, Tiki Taka"
🥇 87,Mike Maignan,Milano FC,Serie A Enilive,"Deflector+, Cross Claimer, Far Throw"
🥇 87,Bruno Fernandes,Man Utd,Premier League,"Long Ball Pass+, Dead Ball, First Touch, Flair, Incisive Pass, Pinged Pass, Relentless"
🥇 87,Heung Min Son,Spurs,Premier League,"Finesse Shot+, Quick Step, Rapid"
🥇 87,Marquinhos,Paris SG,Ligue 1 McDonald's,"Intercept+, Aerial, Anticipate, Jockey, Power Header"
🥇 87,Alessandro Bastoni,Lombardia FC,Serie A Enilive,"Intercept+, Anticipate, Jockey, Long Ball Pass, Pinged Pass"
🥇 87,İlkay Gündoğan,Manchester City,Premier League,"First Touch+, Incisive Pass, Press Proven, Tiki Taka"
🥇 87,Emiliano Martínez,Aston Villa,Premier League,"1v1 Close Down+, Footwork"
🥇 87,Nicolò Barella,Lombardia FC,Serie A Enilive,"Relentless+, Anticipate, Intercept, Pinged Pass, Press Proven, Slide Tackle"
🥇 87,Yann Sommer,Lombardia FC,Serie A Enilive,"Far Reach+"
🥇 86,Cristiano Ronaldo,Al Nassr,ROSHN Saudi League,"Power Shot+, Acrobatic, Aerial, Flair, Power Header, Trickster, Trivela"
🥇 86,Gabriel,Arsenal,Premier League,"Bruiser+, Aerial, Power Header"
🥇 86,Granit Xhaka,Leverkusen,Bundesliga,"Long Ball Pass+, Bruiser, Finesse Shot, Incisive Pass, Power Shot, Slide Tackle"
🥇 86,Rodrygo,Real Madrid,LALIGA EA SPORTS,"Dead Ball, Finesse Shot, Flair, Technical"
🥇 86,João Cancelo,Al Hilal,ROSHN Saudi League,"Block, First Touch, Flair, Technical, Trivela, Whipped Pass"
🥇 86,Rafael Leão,Milano FC,Serie A Enilive,"Rapid+, Finesse Shot, Flair, Incisive Pass, Quick Step, Trickster, Whipped Pass"
🥇 86,Grimaldo,Leverkusen,Bundesliga,"Whipped Pass+, Dead Ball, Finesse Shot"
🥇 86,Luka Modrić,Real Madrid,LALIGA EA SPORTS,"Trivela+, Incisive Pass, Long Ball Pass, Technical, Whipped Pass"
🥇 86,Alexis Mac Allister,Liverpool,Premier League,"Pinged Pass+, Dead Ball, Incisive Pass, Power Shot, Press Proven"
🥇 86,Carvajal,Real Madrid,LALIGA EA SPORTS,"Block, Whipped Pass"
🥇 86,Ousmane Dembélé,Paris SG,Ligue 1 McDonald's,"Rapid+, Flair, Pinged Pass, Quick Step, Trickster"
🥇 86,Trent Alexander-Arnold,Liverpool,Premier League,"Whipped Pass+, Dead Ball, Incisive Pass, Long Ball Pass, Relentless"
🥇 86,Pedri,FC Barcelona,LALIGA EA SPORTS,"Incisive Pass+, First Touch, Long Ball Pass, Relentless, Technical, Tiki Taka"
🥇 86,Jonathan Tah,Leverkusen,Bundesliga,Aerial
🥇 86,Karim Benzema,Al Ittihad,ROSHN Saudi League,"Finesse Shot, First Touch, Incisive Pass, Relentless, Trivela"
🥇 86,Bremer,Juventus,Serie A Enilive,"Aerial, Block, Bruiser, Intercept, Long Ball Pass, Power Header"
🥇 86,Joshua Kimmich,FC Bayern München,Bundesliga,"Long Ball Pass+, Anticipate, Finesse Shot, Press Proven, Relentless, Whipped Pass"
🥇 86,Unai Simón,Athletic Club,LALIGA EA SPORTS,"1v1 Close Down, Footwork, Long Ball Pass, Pinged Pass"
🥇 86,Manuel Neuer,FC Bayern München,Bundesliga,"Pinged Pass+, Far Throw, Long Ball Pass"
🥇 86,Hakan Çalhanoğlu,Lombardia FC,Serie A Enilive,"Incisive Pass+, Anticipate, First Touch, Technical"
🥇 85,David Alaba,Real Madrid,LALIGA EA SPORTS,"Anticipate, Dead Ball, Long Ball Pass"
🥇 85,Ronald Araujo,FC Barcelona,LALIGA EA SPORTS,"Block+, Acrobatic, Anticipate, Jockey, Power Header, Slide Tackle"
🥇 85,Julian Brandt,Borussia Dortmund,Bundesliga,"Tiki Taka+, Dead Ball, First Touch, Flair, Incisive Pass, Technical, Trivela"
🥇 85,Éder Militão,Real Madrid,LALIGA EA SPORTS,"Aerial, Block, Intercept, Long Ball Pass, Power Header"
🥇 85,Bruno Guimarães,Newcastle Utd,Premier League,"Trivela+, Flair, Incisive Pass, Long Ball Pass, Press Proven"
🥇 85,Alexander Isak,Newcastle Utd,Premier League,"Finesse Shot, First Touch, Flair, Rapid"
🥇 85,N'Golo Kanté,Al Ittihad,ROSHN Saudi League,"Intercept+, Press Proven, Relentless"
🥇 85,Jules Koundé,FC Barcelona,LALIGA EA SPORTS,"Jockey+, Quick Step, Relentless, Slide Tackle"
🥇 85,Khvicha Kvaratskhelia,SSC Napoli,Serie A Enilive,"Finesse Shot, Flair, Incisive Pass, Technical, Trickster, Trivela"
🥇 85,Vitinha,Paris SG,Ligue 1 McDonald's,"Tiki Taka+, Finesse Shot, Intercept, Technical"
🥇 85,James Maddison,Spurs,Premier League,"Dead Ball, Finesse Shot, Flair, Incisive Pass, Trivela"
🥇 85,Riyad Mahrez,Al Ahli,ROSHN Saudi League,"Finesse Shot, First Touch, Flair, Technical"
🥇 85,Giorgi Mamardashvili,Valencia CF,LALIGA EA SPORTS,"Cross Claimer, Far Throw"
🥇 85,Mikel Merino,Arsenal,Premier League,"Aerial, Incisive Pass, Power Shot, Relentless"
🥇 85,Sergej Milinković-Savić,Al Hilal,ROSHN Saudi League,"Aerial, First Touch, Incisive Pass, Power Header, Relentless, Trivela"
🥇 85,Loïs Openda,RB Leipzig,Bundesliga,"Finesse Shot, Quick Step, Rapid, Trivela"
🥇 85,Palhinha,FC Bayern München,Bundesliga,"Bruiser+, Long Ball Pass, Slide Tackle"
🥇 85,Cole Palmer,Chelsea,Premier League,"Finesse Shot, First Touch, Flair, Incisive Pass, Technical, Whipped Pass"
🥇 85,Andrew Robertson,Liverpool,Premier League,"Relentless+, Rapid, Whipped Pass"
🥇 85,Leroy Sané,FC Bayern München,Bundesliga,"Finesse Shot, Flair, Power Shot, Quick Step, Rapid"
🥇 85,Nico Schlotterbeck,Borussia Dortmund,Bundesliga,"Slide Tackle+, Anticipate, Block, Jockey, Long Ball Pass, Power Header"
🥇 85,John Stones,Manchester City,Premier League,"Aerial, Long Throw"
🥇 85,Aurélien Tchouaméni,Real Madrid,LALIGA EA SPORTS,"Aerial, Anticipate, Bruiser, Intercept, Jockey, Long Ball Pass, Relentless"
🥇 85,Diogo Jota,Liverpool,Premier League,"Rapid, Relentless"
🥇 85,Sandro Tonali,Newcastle Utd,Premier League,"Long Ball Pass, Relentless, Slide Tackle"
🥇 85,Ollie Watkins,Aston Villa,Premier League,"Chip Shot, Rapid, Relentless"
🥇 85,Nico Williams,Athletic Club,LALIGA EA SPORTS,"Rapid+, Finesse Shot, Flair, Quick Step, Relentless, Trivela"
🥈 84,Francesco Acerbi,Lombardia FC,Serie A Enilive,"Aerial, Intercept, Jockey"
🥈 84,Julián Álvarez,Atlético de Madrid,LALIGA EA SPORTS,"Press Proven+, Finesse Shot, Flair"
🥈 84,Iago Aspas,RC Celta,LALIGA EA SPORTS,"Chip Shot+, Dead Ball, Finesse Shot, Incisive Pass, Trivela"
🥈 84,Yassine Bounou,Al Hilal,ROSHN Saudi League,"Far Throw+, Cross Claimer, Footwork"
🥈 84,Federico Chiesa,Liverpool,Premier League,"Finesse Shot, Flair, Quick Step, Rapid, Trivela"
🥈 84,Kingsley Coman,FC Bayern München,Bundesliga,"Rapid+, Acrobatic, First Touch, Flair, Quick Step"
🥈 84,Rúben Neves,Al Hilal,ROSHN Saudi League,"Dead Ball, Long Ball Pass, Power Shot, Whipped Pass"
🥈 84,Matthijs de Ligt,Man Utd,Premier League,"Block, Bruiser, Long Ball Pass, Power Shot"
🥈 84,Rodrigo De Paul,Atlético de Madrid,LALIGA EA SPORTS,"Finesse Shot, Incisive Pass, Long Ball Pass, Technical"
🥈 84,Raphinha,FC Barcelona,LALIGA EA SPORTS,"Finesse Shot, Flair, Power Shot, Quick Step, Rapid, Relentless, Trickster"
🥈 84,Luis Díaz,Liverpool,Premier League,"Flair, Quick Step, Technical"
🥈 84,Federico Dimarco,Lombardia FC,Serie A Enilive,"Finesse Shot, First Touch, Incisive Pass, Long Ball Pass, Power Shot, Whipped Pass"
🥈 84,Artem Dovbyk,AS Roma,Serie A Enilive,"Power Header"
🥈 84,Jeremie Frimpong,Leverkusen,Bundesliga,"Flair, Quick Step, Rapid"
🥈 84,Aleix García,Leverkusen,Bundesliga,"Press Proven+, Dead Ball, Tiki Taka"
🥈 84,Jack Grealish,Manchester City,Premier League,"Press Proven+, Finesse Shot, First Touch, Flair"
🥈 84,Serhou Guirassy,Borussia Dortmund,Bundesliga,"Chip Shot+, Aerial, Finesse Shot, First Touch, Power Header, Trivela"
🥈 84,Viktor Gyökeres,Sporting CP,Liga Portugal,"Press Proven"
🥈 84,Achraf Hakimi,Paris SG,Ligue 1 McDonald's,"Quick Step, Whipped Pass"
🥈 84,Kalidou Koulibaly,Al Hilal,ROSHN Saudi League,"Anticipate, Block, Bruiser, Power Header"
🥈 84,Sadio Mané,Al Nassr,ROSHN Saudi League,"Flair, Rapid"
🥈 84,Lisandro Martínez,Man Utd,Premier League,"Bruiser, Long Ball Pass, Slide Tackle"
🥈 84,Diogo Costa,FC Porto,Liga Portugal,"1v1 Close Down, Far Throw, Long Ball Pass"
🥈 84,Ferland Mendy,Real Madrid,LALIGA EA SPORTS,"Block, Rapid"
🥈 84,Christopher Nkunku,Chelsea,Premier League,"Finesse Shot, First Touch, Flair, Incisive Pass, Technical, Trivela"
🥈 84,Dani Olmo,FC Barcelona,LALIGA EA SPORTS,"Finesse Shot, First Touch, Flair, Incisive Pass, Technical, Tiki Taka, Trivela"
🥈 84,Exequiel Palacios,Leverkusen,Bundesliga,"Anticipate, Intercept"
🥈 84,Benjamin Pavard,Lombardia FC,Serie A Enilive,"Jockey+, Intercept"
🥈 84,Álex Remiro,Real Sociedad,LALIGA EA SPORTS,"Far Throw, Footwork"
🥈 84,Cristian Romero,Spurs,Premier League,"Aerial, Bruiser, Intercept, Slide Tackle"
🥈 84,Marcel Sabitzer,Borussia Dortmund,Bundesliga,"Finesse Shot, Pinged Pass, Power Shot, Trivela"
🥈 84,Casemiro,Man Utd,Premier League,"Block, Bruiser, Long Ball Pass, Slide Tackle"
🥈 84,Guglielmo Vicario,Spurs,Premier League,Footwork
🥈 84,Dušan Vlahović,Juventus,Serie A Enilive,"Chip Shot, Dead Ball, Finesse Shot, Flair"
🥈 84,Kyle Walker,Manchester City,Premier League,"Jockey, Long Throw, Rapid"
🥈 84,Benjamin White,Arsenal,Premier League,Block
🥈 83,Marcos Acuña,River Plate,Libertadores,"Anticipate, Bruiser, Flair, Long Ball Pass, Power Shot, Relentless, Trivela"
🥈 83,Robert Andrich,Leverkusen,Bundesliga,"Bruiser, Power Shot, Relentless"
🥈 83,Ismaël Bennacer,Milano FC,Serie A Enilive,"Incisive Pass, Technical, Tiki Taka"
🥈 83,Domenico Berardi,Sassuolo,Serie BKT,"Dead Ball, Flair, Incisive Pass, Technical, Trivela"
🥈 83,Eduardo Camavinga,Real Madrid,LALIGA EA SPOI,"Block, Bruiser, Flair, Jockey, Technical"
🥈 83,Yannick Carrasco,Al Shabab,ROSHN Saudi League,"Flair, Technical, Trivela, Whipped Pass"
🥈 83,Stefan de Vrij,Lombardia FC,Serie A Enilive,"Aerial, Jockey"
🥈 83,Ángel Di María,SL Benfica,Liga Portugal,"Chip Shot, Finesse Shot, Flair, Incisive Pass, Technical, Trickster, Trivela"
🥈 83,Moussa Diaby,Al Ittihad,ROSHN Saudi League,"Quick Step+, First Touch, Rapid"
🥈 83,Youssef En-Nesyri,Fenerbahçe,Trendyol Süper Lig,"Power Header+, Aerial, Quick Step, Rapid, Relentless"
🥈 83,Rafa,Beşiktaş,Trendyol Süper Lig,"Acrobatic, First Touch, Flair, Quick Step, Rapid, Trivela"
🥈 83,Cody Gakpo,Liverpool,Premier League,"Press Proven, Trivela"
🥈 83,José María Giménez,Atlético de Madrid,LALIGA EA SPOI,"Aerial, Power Header, Slide Tackle"
🥈 83,Olivier Giroud,LAFC,MLS,"Aerial, Power Header, Trivela"
🥈 83,Leon Goretzka,FC Bayern München,Bundesliga,"Bruiser, Incisive Pass, Power Shot"
🥈 83,Joško Gvardiol,Manchester City,Premier League,"Block+, Jockey, Long Ball Pass, Pinged Pass, Power Header"
🥈 83,Kai Havertz,Arsenal,Premier League,"Aerial, Chip Shot, First Touch, Technical, Trivela"
🥈 83,Lucas Hernández,Paris SG,Ligue 1 McDonald's,"Bruiser, Slide Tackle"
🥈 83,Mauro Icardi,Galatasaray,Trendyol Süper Lig,"Chip Shot+, Aerial, Flair, Incisive Pass, Power Header, Trivela"
🥈 83,Kim Min Jae,FC Bayern München,Bundesliga,"Aerial, Block, Intercept, Power Header, Slide Tackle"
🥈 83,Ibrahima Konaté,Liverpool,Premier League,"Aerial, Block, Bruiser"
🥈 83,Teun Koopmeiners,Juventus,Serie A Enilive,"Anticipate, Relentless"
🥈 83,Mateo Kovačić,Manchester City,Premier League,"Flair, Incisive Pass, Pinged Pass, Press Proven"
🥈 83,Konrad Laimer,FC Bayern München,Bundesliga,"Block+, Bruiser, Relentless"
🥈 83,Aymeric Laporte,Al Nassr,ROSHN Saudi League,"Aerial, Long Ball Pass"
🥈 83,Robin Le Normand,Atlético de Madrid,LALIGA EA SPOI,"Aerial, Power Header, Slide Tackle"
🥈 83,Marcos Llorente,Atlético de Madrid,LALIGA EA SPOI,"Power Shot, Quick Step, Rapid, Relentless, Whipped Pass"
🥈 83,Manuel Locatelli,Juventus,Serie A Enilive,"Anticipate, Long Ball Pass, Relentless"
🥈 83,Donyell Malen,Borussia Dortmund,Bundesliga,"First Touch, Flair, Quick Step, Technical, Trivela"
🥈 83,Gabriel Martinelli,Arsenal,Premier League,"Finesse Shot, Flair, Quick Step, Technical, Trivela, Whipped Pass"
🥈 83,Henrikh Mkhitaryan,Lombardia FC,Serie A Enilive,"Anticipate, Finesse Shot, Flair, Incisive Pass, Technical"
🥈 83,Morata,Milano FC,Serie A Enilive,"Rapid, Relentless"
🥈 83,Gerard Moreno,Villarreal CF,LALIGA EA SPOI,"Finesse Shot, Power Shot, Trivela"
🥈 83,André Onana,Man Utd,Premier League,"1v1 Close Down, Footwork"
🥈 83,Willi Orban,RB Leipzig,Bundesliga,"Bruiser, Power Header"
🥈 83,Gavi,FC Barcelona,LALIGA EA SPOI,"Rapid, Relentless, Slide Tackle, Tiki Taka"
🥈 83,Parejo,Villarreal CF,LALIGA EA SPOI,"Dead Ball+, Long Ball Pass, Pinged Pass, Press Proven"
🥈 83,Lorenzo Pellegrini,AS Roma,Serie A Enilive,"Finesse Shot, Incisive Pass, Press Proven"
🥈 83,Pedro Gonçalves,Sporting CP,Liga Portugal,"Tiki Taka+, Dead Ball, Finesse Shot, Flair, Incisive Pass, Technical, Whipped Pass"
🥈 83,Jordan Pickford,Everton,Premier League,"Far Throw, Footwork, Long Ball Pass"
🥈 83,Nick Pope,Newcastle Utd,Premier League,Footwork
🥈 83,Pedro Porro,Spurs,Premier League,"Rapid, Relentless, Whipped Pass"
🥈 83,Ivan Provedel,Latium,Serie A Enilive,"Deflector, Far Throw, Footwork"
🥈 83,Christian Pulisic,Milano FC,Serie A Enilive,"Finesse Shot, Flair, Rapid"
🥈 83,David Raya,Arsenal,Premier League,"Cross Claimer"
🥈 83,Koke,Atlético de Madrid,LALIGA EA SPOI,"Long Ball Pass, Relentless"
🥈 83,Guido Rodríguez,West Ham,Premier League,"Anticipate+, Bruiser, Slide Tackle, Tiki Taka"
🥈 83,Alessio Romagnoli,Latium,Serie A Enilive,"Aerial, Bruiser"
🥈 83,Xavi Simons,RB Leipzig,Bundesliga,"Finesse Shot, First Touch, Flair, Incisive Pass, Technical, Tiki Taka, Trivela"
🥈 83,Douglas Luiz,Juventus,Serie A Enilive,"Dead Ball, Flair, Press Proven"
🥈 83,Dušan Tadić,Fenerbahçe,Trendyol Süper Lig,"Chip Shot, First Touch, Flair, Press Proven, Trivela, Whipped Pass"
🥈 83,Edmond Tapsoba,Leverkusen,Bundesliga,"Long Ball Pass, Pinged Pass, Power Header"
🥈 83,Nuno Mendes,Paris SG,Ligue 1 McDonald's,"Pinged Pass, Quick Step, Rapid, Whipped Pass"
🥈 83,Marcus Thuram,Lombardia FC,Serie A Enilive,"Aerial, Quick Step, Relentless"
🥈 83,Fikayo Tomori,Milano FC,Serie A Enilive,"Block+, Anticipate, Long Ball Pass"
🥈 83,Lucas Torreira,Galatasaray,Trendyol Süper Lig,"Anticipate, Intercept, Jockey, Relentless, Slide Tackle, Tiki Taka"
🥈 83,Kieran Trippier,Newcastle Utd,Premier League,"Whipped Pass+, Dead Ball, Long Ball Pass, Long Throw"
🥈 83,Leandro Trossard,Arsenal,Premier League,"Flair, Rapid, Trivela"
🥈 83,Viktor Tsygankov,Girona FC,LALIGA EA SPOI,"Flair, Quick Step, Technical"
🥈 83,Mattia Zaccagni,Latium,Serie A Enilive,"Flair, Technical, Trivela"
🥈 83,Duván Zapata,Torino,Serie A Enilive,"Aerial, Power Header, Power Shot"
🥈 82,Isco,Real Betis,LALIGA EA SPOI,"Finesse Shot, Flair, Incisive Pass, Technical, Trivela"
🥈 82,Joelinton,Newcastle Utd,Premier League,"Bruiser, Intercept, Press Proven, Relentless"
🥈 82,Pepê,FC Porto,Liga Portugal,"First Touch, Quick Step, Technical, Trickster"
🥈 82,Pierre-Emerick Aubameyang,Al Qadisiyah,ROSHN Saudi League,"Chip Shot, Finesse Shot, Flair, Rapid, Trivela"
🥈 82,Leon Bailey,Aston Villa,Premier League,"Flair, Quick Step, Technical"
🥈 82,Oliver Baumann,TSG Hoffenheim,Bundesliga,"Deflector, Footwork"
🥈 82,Victor Boniface,Leverkusen,Bundesliga,"Power Shot+, Aerial"
🥈 82,Sven Botman,Newcastle Utd,Premier League,"Aerial, Bruiser, Jockey, Long Ball Pass"
🥈 82,Jarrod Bowen,West Ham,Premier League,Technical
🥈 82,Marcelo Brozović,Al Nassr,ROSHN Saudi League,"Long Ball Pass, Press Proven, Relentless"
🥈 82,Moisés Caicedo,Chelsea,Premier League,"Anticipate, Intercept, Pinged Pass, Press Proven, Relentless, Slide Tackle, Tiki Taka"
🥈 82,Emre Can,Borussia Dortmund,Bundesliga,"Bruiser, Long Ball Pass, Pinged Pass, Press Proven, Slide Tackle"
🥈 82,Marco Carnesecchi,Bergamo Calcio,Serie A Enilive,"1v1 Close Down"
🥈 82,Koen Casteels,Al Qadisiyah,ROSHN Saudi League,"1v1 Close Down"
🥈 82,Lucas Paquetá,West Ham,Premier League,"First Touch, Flair, Technical, Trivela"
🥈 82,Ángel Correa,Atlético de Madrid,LALIGA EA SPOI,"Flair, Technical, Trivela"
🥈 82,Marc Cucurella,Chelsea,Premier League,"Acrobatic, Block, Intercept, Jockey, Press Proven, Relentless"
🥈 82,Danilo,Juventus,Serie A Enilive,"Anticipate, Long Ball Pass"
🥈 82,Otávio,Al Nassr,ROSHN Saudi League,"First Touch, Flair, Incisive Pass, Pinged Pass, Relentless, Technical, Tiki Taka"
🥈 82,Diogo Dalot,Man Utd,Premier League,"Slide Tackle, Technical"
🥈 82,Sergi Darder,RCD Mallorca,LALIGA EA SPOI,"Flair, Incisive Pass, Long Ball Pass, Pinged Pass, Power Shot, Press Proven"
🥈 82,Alphonso Davies,FC Bayern München,Bundesliga,"Quick Step, Rapid"
🥈 82,Giovanni Di Lorenzo,SSC Napoli,Serie A Enilive,"First Touch, Rapid, Relentless, Whipped Pass"
🥈 82,Brahim,Real Madrid,LALIGA EA SPOI,"First Touch, Flair, Technical"
🥈 82,Denzel Dumfries,Lombardia FC,Serie A Enilive,"Quick Step, Relentless"
🥈 82,Edin Džeko,Fenerbahçe,Trendyol Süper Lig,"Finesse Shot, Incisive Pass, Technical"
🥈 82,Enzo Fernández,Chelsea,Premier League,"Long Ball Pass+, First Touch, Flair, Incisive Pass, Press Proven, Relentless"
🥈 82,Nacho Fernández,Al Qadisiyah,ROSHN Saudi League,"Aerial, Block, Intercept"
🥈 82,Gabriel Jesus,Arsenal,Premier League,"First Touch, Flair, Relentless, Technical"
🥈 82,Jorginho,Arsenal,Premier League,"Anticipate, First Touch, Incisive Pass, Pinged Pass, Press Proven"
🥈 82,Pau Torres,Aston Villa,Premier League,"Long Ball Pass"
🥈 82,Niclas Füllkrug,West Ham,Premier League,"Power Header"
🥈 82,Gayà,Valencia CF,LALIGA EA SPOI,"Anticipate, Technical"
🥈 82,Paulo Gazzaniga,Girona FC,LALIGA EA SPOI,"Cross Claimer, Footwork"
🥈 82,Matthias Ginter,SC Freiburg,Bundesliga,"Anticipate, Pinged Pass"
🥈 82,Serge Gnabry,FC Bayern München,Bundesliga,Technical
🥈 82,Anthony Gordon,Newcastle Utd,Premier League,"Finesse Shot, Quick Step, Rapid"
🥈 82,Raphaël Guerreiro,FC Bayern München,Bundesliga,"Tiki Taka+, First Touch, Flair, Intercept, Technical, Trivela"
🥈 82,Fabinho,Al Ittihad,ROSHN Saudi League,"Block, Bruiser, Long Ball Pass, Power Shot, Slide Tackle"
🥈 82,Yangel Herrera,Girona FC,LALIGA EA SPOI,"Flair, Incisive Pass"
🥈 82,Jonas Hofmann,Leverkusen,Bundesliga,"Incisive Pass, Relentless, Technical"
🥈 82,Ciro Immobile,Beşiktaş,Trendyol Süper Lig,"Power Shot, Press Proven"
🥈 82,Reece James,Chelsea,Premier League,"Bruiser, Jockey, Whipped Pass"
🥈 82,Boubacar Kamara,Aston Villa,Premier League,"Block, Intercept"
🥈 82,Franck Yannick Kessié,Al Ahli,ROSHN Saudi League,"Power Shot, Relentless"
🥈 82,Randal Kolo Muani,Paris SG,Ligue 1 McDonald's,"Finesse Shot, Flair, Quick Step, Technical"
🥈 82,Filip Kostić,Juventus,Serie A Enilive,"Rapid, Whipped Pass"
🥈 82,Mohammed Kudus,West Ham,Premier League,"First Touch, Flair, Technical"
🥈 82,Dejan Kulusevski,Spurs,Premier League,"Finesse Shot, Flair"
🥈 82,Alexandre Lacazette,OL,Ligue 1 McDonald's,"Finesse Shot, Technical"
🥈 82,Jeremías Conan Ledesma,River Plate,Libertadores,"Cross Claimer, Deflector, Far Throw"
🥈 82,Bernd Leno,Fulham,Premier League,"1v1 Close Down"
🥈 82,Stanislav Lobotka,SSC Napoli,Serie A Enilive,"Anticipate, First Touch, Relentless"
🥈 82,Ademola Lookman,Bergamo Calcio,Serie A Enilive,"First Touch, Technical"
🥈 82,Romelu Lukaku,SSC Napoli,Serie A Enilive,"Power Header, Power Shot, Press Proven"
🥈 82,Gianluca Mancini,AS Roma,Serie A Enilive,"Bruiser, Intercept, Long Ball Pass, Slide Tackle"
🥈 82,John McGinn,Aston Villa,Premier League,"Long Ball Pass, Press Proven, Relentless"
🥈 82,Aleksandar Mitrović,Al Hilal,ROSHN Saudi League,"Power Header+, Aerial"
🥈 82,Nahuel Molina,Atlético de Madrid,LALIGA EA SPOI,"Block, Whipped Pass"
🥈 82,Savinho,Manchester City,Premier League,Technical
🥈 82,Thomas Müller,FC Bayern München,Bundesliga,"Incisive Pass, Trivela"
🥈 82,Darwin Núñez,Liverpool,Premier League,"Quick Step, Rapid, Relentless"
🥈 82,Michael Olise,FC Bayern München,Bundesliga,"Dead Ball, Finesse Shot, Flair, Incisive Pass, Technical, Trivela, Whipped Pass"
🥈 82,Oyarzabal,Real Sociedad,LALIGA EA SPOI,"Technical, Trivela"
🥈 82,Thomas Partey,Arsenal,Premier League,"Long Ball Pass, Pinged Pass, Press Proven"
🥈 82,Tijjani Reijnders,Milano FC,Serie A Enilive,"Flair, Incisive Pass, Power Shot, Technical, Tiki Taka"
🥈 82,Fabián Ruiz,Paris SG,Ligue 1 McDonald's,"Finesse Shot, First Touch, Tiki Taka"
🥈 82,Brice Samba,RC Lens,Ligue 1 McDonald's,Footwork
🥈 82,Sancet,Athletic Club,LALIGA EA SPOI,"Finesse Shot, Technical, Trivela"
🥈 82,Jadon Sancho,Chelsea,Premier League,"Technical+, Finesse Shot, Flair, Trickster, Trivela"
🥈 82,Fabian Schär,Newcastle Utd,Premier League,"Long Ball Pass, Power Shot"
🥈 82,Patrik Schick,Leverkusen,Bundesliga,"Acrobatic, Flair, Power Header"
🥈 82,Luke Shaw,Man Utd,Premier League,Jockey
🥈 82,Malcom,Al Hilal,ROSHN Saudi League,"Flair, Incisive Pass, Rapid, Relentless"
🥈 82,Chris Smalling,Al Fayha,ROSHN Saudi League,"Aerial, Intercept, Jockey, Power Header"
🥈 82,Alexander Sørloth,Atlético de Madrid,LALIGA EA SPOI,"Flair, Rapid"
🥈 82,Anderson Talisca,Al Nassr,ROSHN Saudi League,"Acrobatic, Finesse Shot, Power Header, Trivela"
🥈 82,Luis Suárez,Inter Miami CF,MLS,Trivela
🥈 82,Niklas Süle,Borussia Dortmund,Bundesliga,"Bruiser, Intercept, Long Ball Pass, Pinged Pass, Slide Tackle"
🥈 82,Kevin Trapp,Frankfurt,Bundesliga,"Far Throw, Footwork"
🥈 82,Destiny Udogie,Spurs,Premier League,"Quick Step, Whipped Pass"
🥈 82,Dayot Upamecano,FC Bayern München,Bundesliga,"Bruiser, Pinged Pass"
🥈 82,Micky van de Ven,Spurs,Premier League,"Block, Slide Tackle"
🥈 82,Raphaël Varane,Como,Serie A Enilive,"Aerial, Anticipate"
🥈 82,Iñaki Williams,Athletic Club,LALIGA EA SPOI,"Chip Shot, Finesse Shot, Quick Step, Rapid, Trivela"
🥉 81,Luciano Acosta,FC Cincinnati,MLS,"Finesse Shot, First Touch, Flair, Incisive Pass, Technical, Trivela"
🥉 81,Edson Álvarez,West Ham,Premier League,"Block+, Anticipate, Bruiser, Power Header, Slide Tackle"
🥉 81,Yeray,Athletic Club,LALIGA EA SPOI,"Intercept, Slide Tackle"
🥉 81,Waldemar Anton,Borussia Dortmund,Bundesliga,"Aerial, Block, Pinged Pass"
🥉 81,Alphonse Areola,West Ham,Premier League,"Far Throw"
🥉 81,Marco Asensio,Paris SG,Ligue 1 McDonald's,"Finesse Shot, Incisive Pass, Whipped Pass"
🥉 81,Balde,FC Barcelona,LALIGA EA SPOI,"Anticipate, Jockey, Quick Step"
🥉 81,Rodrigo Bentancur,Spurs,Premier League,"First Touch, Relentless"
🥉 81,Álex Berenguer,Athletic Club,LALIGA EA SPOI,"Finesse Shot, Rapid, Trivela"
🥉 81,Sergio Busquets,Inter Miami CF,MLS,"Anticipate, Incisive Pass, Long Ball Pass, Press Proven"
🥉 81,Bryan Cristante,AS Roma,Serie A Enilive,"Anticipate, Incisive Pass, Long Ball Pass, Relentless"
🥉 81,Ricardo Horta,SC Braga,Liga Portugal,"Finesse Shot, First Touch, Pinged Pass, Power Shot, Tiki Taka"
🥉 81,Rui Silva,Real Betis,LALIGA EA SPOI,"Deflector, Footwork"
🥉 81,Matteo Darmian,Lombardia FC,Serie A Enilive,Relentless
🥉 81,Jonathan David,LOSC Lille,Ligue 1 McDonald's,"Quick Step, Relentless, Trivela"
🥉 81,Richarlison,Spurs,Premier League,"Acrobatic, Flair, Power Header, Technical, Trivela"
🥉 81,Luuk de Jong,PSV,Eredivisie,"Power Header+, Aerial"
🥉 81,Fred,Fenerbahçe,Trendyol Süper Lig,"Relentless+, Flair"
🥉 81,Eberechi Eze,Crystal Palace,Premier League,"Dead Ball, Finesse Shot, Flair, Power Shot, Technical"
🥉 81,Youssouf Fofana,Milano FC,Serie A Enilive,Intercept
🥉 81,Davide Frattesi,Lombardia FC,Serie A Enilive,Intercept
🥉 81,Remo Freuler,Bologna,Serie A Enilive,Intercept
🥉 81,Conor Gallagher,Atlético de Madrid,LALIGA EA SPOI,"Block, Intercept, Relentless"
🥉 81,Alexandr Golovin,AS Monaco,Ligue 1 McDonald's,"Finesse Shot, First Touch, Incisive Pass, Technical"
🥉 81,Pascal Groß,Borussia Dortmund,Bundesliga,"Dead Ball, Whipped Pass"
🥉 81,Marc Guéhi,Crystal Palace,Premier League,"Anticipate, Jockey, Long Ball Pass"
🥉 81,Dávid Hancko,Feyenoord,Eredivisie,"Anticipate, Jockey, Long Ball Pass, Power Header"
🥉 81,Benjamin Henrichs,RB Leipzig,Bundesliga,"Block, Bruiser, Incisive Pass, Jockey, Slide Tackle"
🥉 81,Piero Hincapié,Leverkusen,Bundesliga,"Block, Jockey"
🥉 81,Ferdi Kadıoğlu,Brighton,Premier League,"First Touch, Jockey, Quick Step, Rapid, Relentless, Whipped Pass"
🥉 81,Daichi Kamada,Crystal Palace,Premier League,"Flair, Incisive Pass, Technical"
🥉 81,Presnel Kimpembe,Paris SG,Ligue 1 McDonald's,"Aerial, Block, Bruiser, Slide Tackle"
🥉 81,Orkun Kökçü,SL Benfica,Liga Portugal,"Dead Ball, Finesse Shot, Incisive Pass, Power Shot, Trivela"
🥉 81,Ezri Konsa,Aston Villa,Premier League,"Anticipate, Jockey, Slide Tackle"
🥉 81,Odilon Kossounou,Bergamo Calcio,Serie A Enilive,Block
🥉 81,Andrej Kramarić,TSG Hoffenheim,Bundesliga,"Chip Shot, Finesse Shot, First Touch, Flair, Incisive Pass, Technical, Trivela"
🥉 81,Takefusa Kubo,Real Sociedad,LALIGA EA SPOI,"Finesse Shot, First Touch, Flair, Technical"
🥉 81,Ruben Loftus-Cheek,Milano FC,Serie A Enilive,"Press Proven"
🥉 81,Andriy Lunin,Real Madrid,LALIGA EA SPOI,Footwork
🥉 81,Iñigo Martínez,FC Barcelona,LALIGA EA SPOI,"Long Ball Pass, Slide Tackle"
🥉 81,Noussair Mazraoui,Man Utd,Premier League,"Anticipate, Flair, Intercept, Jockey, Technical"
🥉 81,Brais Méndez,Real Sociedad,LALIGA EA SPOI,"Dead Ball, Finesse Shot, Technical, Tiki Taka"
🥉 81,Arkadiusz Milik,Juventus,Serie A Enilive,"Power Shot"
🥉 81,Kaoru Mitoma,Brighton,Premier League,"Finesse Shot, Quick Step, Technical"
🥉 81,Fernando Muslera,Galatasaray,Trendyol Süper Lig,"1v1 Close Down, Cross Claimer, Far Throw, Long Ball Pass"
🥉 81,Riccardo Orsolini,Bologna,Serie A Enilive,"Dead Ball, Flair, Technical"
🥉 81,Stefan Ortega,Manchester City,Premier League,"Far Reach, Footwork"
🥉 81,Nicolás Otamendi,SL Benfica,Liga Portugal,"Aerial, Bruiser, Intercept, Jockey, Power Header, Slide Tackle"
🥉 81,Isi Palazón,Rayo Vallecano,LALIGA EA SPOI,"First Touch, Rapid"
🥉 81,Aaron Ramsdale,Southampton,Premier League,"Cross Claimer, Deflector"
🥉 81,Marcus Rashford,Man Utd,Premier League,"Power Shot+, Flair, Quick Step, Technical"
🥉 81,David Raum,RB Leipzig,Bundesliga,"Dead Ball, Rapid, Trivela, Whipped Pass"
🥉 81,Stefan Savić,Trabzonspor,Trendyol Süper Lig,"Aerial, Power Header"
🥉 81,Xaver Schlager,RB Leipzig,Bundesliga,"Bruiser, Incisive Pass, Jockey, Long Ball Pass, Relentless"
🥉 81,Jerdy Schouten,PSV,Eredivisie,"Anticipate, Intercept, Pinged Pass, Press Proven"
🥉 81,Ellyes Skhiri,Frankfurt,Bundesliga,"Intercept, Press Proven, Relentless"
🥉 81,Milan Škriniar,Paris SG,Ligue 1 McDonald's,"Bruiser, Jockey"
🥉 81,Dominic Solanke,Spurs,Premier League,"Acrobatic, Flair, Power Header"
🥉 81,David Soria,Getafe CF,LALIGA EA SPOI,Footwork
🥉 81,Raheem Sterling,Arsenal,Premier League,"Finesse Shot, Quick Step, Rapid"
🥉 81,Dominik Szoboszlai,Liverpool,Premier League,"Dead Ball, Flair, Power Shot, Technical, Trivela, Whipped Pass"
🥉 81,Youri Tielemans,Aston Villa,Premier League,"Incisive Pass, Long Ball Pass, Pinged Pass, Power Shot"
🥉 81,Manuel Ugarte,Man Utd,Premier League,"Bruiser, Intercept, Slide Tackle"
🥉 81,Deniz Undav,VfB Stuttgart,Bundesliga,"Chip Shot+, Finesse Shot, Incisive Pass"
🥉 81,Álvaro Valles,UD Las Palmas,LALIGA EA SPOI,"Cross Claimer, Deflector"
🥉 81,Lucas Vázquez,Real Madrid,LALIGA EA SPOI,"Block, Rapid, Whipped Pass"
🥉 81,Joey Veerman,PSV,Eredivisie,"Dead Ball, Finesse Shot, First Touch, Incisive Pass, Long Ball Pass, Technical, Trivela"
🥉 81,Vivian,Athletic Club,LALIGA EA SPOI,Intercept
🥉 81,Lamine Yamal,FC Barcelona,LALIGA EA SPOI,"Finesse Shot, Flair, Quick Step, Technical"
🥉 81,Wilfried Zaha,OL,Ligue 1 McDonald's,"Flair, Quick Step, Technical, Trickster"
🥉 81,Piotr Zieliński,Lombardia FC,Serie A Enilive,Technical
🥉 80,Salem Al Dawsari,Al Hilal,ROSHN Saudi League,"Chip Shot, Finesse Shot, First Touch, Flair, Technical"
🥉 80,Ali Al Musrati,Beşiktaş,Trendyol Süper Lig,"Bruiser, Intercept, Long Ball Pass, Pinged Pass, Relentless"
🥉 80,Jordi Alba,Inter Miami CF,MLS,"Anticipate, Jockey, Rapid"
🥉 80,Toby Alderweireld,Royal Antwerp FC,1A Pro League,"Anticipate, Long Ball Pass, Power Header"
🥉 80,Joachim Andersen,Fulham,Premier League,"Bruiser, Long Ball Pass"
🥉 80,Benjamin André,LOSC Lille,Ligue 1 McDonald's,"Aerial, Intercept, Long Ball Pass"
🥉 80,Marko Arnautovic,Lombardia FC,Serie A Enilive,"Flair, Technical, Tiki Taka"
🥉 80,Maximilian Arnold,VfL Wolfsburg,Bundesliga,"Dead Ball, Long Ball Pass, Power Shot, Trivela"
🥉 80,Fredrik Aursnes,SL Benfica,Liga Portugal,"Anticipate, Intercept, Press Proven, Relentless"
🥉 80,Simon Banza,SC Braga,Liga Portugal,"Acrobatic, Aerial, Press Proven"
🥉 80,Roberto Firmino,Al Ahli,ROSHN Saudi League,"First Touch, Flair, Incisive Pass, Technical"
🥉 80,Bradley Barcola,Paris SG,Ligue 1 McDonald's,"Finesse Shot, Flair, Rapid"
🥉 80,Harvey Barnes,Newcastle Utd,Premier League,"Finesse Shot"
🥉 80,Christoph Baumgartner,RB Leipzig,Bundesliga,"First Touch, Flair, Technical"
🥉 80,Walter Benítez,PSV,Eredivisie,"1v1 Close Down"
🥉 80,Gonçalo Inácio,Sporting CP,Liga Portugal,"Aerial, Intercept, Long Ball Pass, Pinged Pass"
🥉 80,Yves Bissouma,Spurs,Premier League,"Flair, Intercept"
🥉 80,Denis Bouanga,LAFC,MLS,"Finesse Shot, Flair, Power Shot, Quick Step, Technical, Trivela"
🥉 80,Yan Couto,Borussia Dortmund,Bundesliga,"Quick Step, Technical, Whipped Pass"
🥉 80,Alessandro Buongiorno,SSC Napoli,Serie A Enilive,"Aerial, Intercept"
🥉 80,Lucas Chevalier,LOSC Lille,Ligue 1 McDonald's,"1v1 Close Down"
🥉 80,Samuel Chukwueze,Milano FC,Serie A Enilive,"Flair, Quick Step, Rapid"
🥉 80,Jonathan Clauss,OGC Nice,Ligue 1 McDonald's,"Anticipate, Long Throw, Relentless, Whipped Pass"
🥉 80,Kevin Danso,RC Lens,Ligue 1 McDonald's,"Aerial, Bruiser, Long Ball Pass"
🥉 80,De Marcos,Athletic Club,LALIGA EA SPOI,"Whipped Pass"
🥉 80,Michele Di Gregorio,Juventus,Serie A Enilive,"1v1 Close Down, Footwork"
🥉 80,Eric Dier,FC Bayern München,Bundesliga,"Aerial, Bruiser, Power Header"
🥉 80,Jérémy Doku,Manchester City,Premier League,"Rapid+, Flair, Quick Step, Trickster"
🥉 80,Éderson,Bergamo Calcio,Serie A Enilive,"Anticipate, Block, Intercept"
🥉 80,Wataru Endo,Liverpool,Premier League,"Press Proven, Relentless"
🥉 80,Pervis Estupiñán,Brighton,Premier League,Rapid
🥉 80,Wladimiro Falcone,Lecce,Serie A Enilive,"1v1 Close Down, Footwork"
🥉 80,João Félix,Chelsea,Premier League,"First Touch, Flair, Technical"
🥉 80,Suso,Sevilla FC,LALIGA EA SPOI,"Finesse Shot, Incisive Pass, Technical"
🥉 80,Seko Fofana,Ettifaq FC,ROSHN Saudi League,"Incisive Pass, Power Shot, Relentless"
🥉 80,Juan Foyth,Villarreal CF,LALIGA EA SPOI,"Block, Bruiser, Slide Tackle"
🥉 80,Javi Galán,Atlético de Madrid,LALIGA EA SPOI,"Anticipate, Rapid"
🥉 80,Pepelu,Valencia CF,LALIGA EA SPOI,"Finesse Shot, Long Ball Pass"
🥉 80,Nuno Santos,Sporting CP,Liga Portugal,"Chip Shot, First Touch, Flair, Trivela"
🥉 80,Joe Gomez,Liverpool,Premier League,"Block, Long Throw"
🥉 80,Nicolás González,Juventus,Serie A Enilive,"First Touch, Technical, Trivela"
🥉 80,Mario Götze,Frankfurt,Bundesliga,"First Touch, Flair, Incisive Pass, Tiki Taka"
🥉 80,Vincenzo Grifo,SC Freiburg,Bundesliga,"Dead Ball+, Finesse Shot, Incisive Pass, Long Ball Pass, Trivela, Whipped Pass"
🥉 80,Nemanja Gudelj,Sevilla FC,LALIGA EA SPOI,"Power Shot"
🥉 80,Albert Guðmundsson,Fiorentina,Serie A Enilive,"Flair, Technical, Trivela"
🥉 80,Mattéo Guendouzi,Latium,Serie A Enilive,"First Touch, Incisive Pass, Tiki Taka"
🥉 80,Malo Gusto,Chelsea,Premier League,"Jockey, Rapid, Slide Tackle, Whipped Pass"
🥉 80,Amadou Haidara,RB Leipzig,Bundesliga,Anticipate
🥉 80,Danilo Pereira,Al Ittihad,ROSHN Saudi League,"Aerial, Intercept, Pinged Pass, Power Header"
🥉 80,Jordan Henderson,Ajax,Eredivisie,"Anticipate, Incisive Pass, Long Ball Pass"
🥉 80,Morten Hjulmand,Sporting CP,Liga Portugal,"Intercept, Relentless"
🥉 80,Pierre-Emile Højbjerg,OM,Ligue 1 McDonald's,"Intercept, Relentless"
🥉 80,Ibañez,Al Ahli,ROSHN Saudi League,"Slide Tackle+, Block, Intercept"
🥉 80,Bento,Al Nassr,ROSHN Saudi League,Deflector
🥉 80,Thomas Lemar,Atlético de Madrid,LALIGA EA SPOI,"Jockey, Technical, Trivela"
🥉 80,Dominik Livaković,Fenerbahçe,Trendyol Süper Lig,"Far Throw, Footwork"
🥉 80,Giovani Lo Celso,Real Betis,LALIGA EA SPOI,"Finesse Shot, Incisive Pass, Long Ball Pass, Technical"
🥉 80,David López,Girona FC,LALIGA EA SPOI,"Long Ball Pass, Slide Tackle"
🥉 80,Harry Maguire,Man Utd,Premier League,"Aerial, Block, Long Ball Pass, Power Header"
🥉 80,Reinildo,Atlético de Madrid,LALIGA EA SPOI,"Block, Bruiser, Intercept"
🥉 80,Iván Martín,Girona FC,LALIGA EA SPOI,Technical
🥉 80,Nemanja Matić,OL,Ligue 1 McDonald's,"Bruiser, Long Ball Pass, Press Proven"
🥉 80,Bryan Mbeumo,Brentford,Premier League,"Quick Step, Rapid"
🥉 80,Facundo Medina,RC Lens,Ligue 1 McDonald's,"Bruiser, Slide Tackle"
🥉 80,Édouard Mendy,Al Ahli,ROSHN Saudi League,"Cross Claimer"
🥉 80,Dries Mertens,Galatasaray,Trendyol Süper Lig,"Dead Ball, Finesse Shot, First Touch, Incisive Pass, Pinged Pass, Trivela"
🥉 80,Daniel Muñoz,Crystal Palace,Premier League,"Anticipate, Intercept, Long Ball Pass, Rapid, Relentless"
🥉 80,Vedat Muriqi,RCD Mallorca,LALIGA EA SPOI,"Aerial, Power Header, Power Shot, Trivela"
🥉 80,João Mário,SL Benfica,Liga Portugal,"First Touch, Incisive Pass, Technical"
🥉 80,Jesús Navas,Sevilla FC,LALIGA EA SPOI,"Rapid, Whipped Pass"
🥉 80,David Neres,SSC Napoli,Serie A Enilive,"Finesse Shot, Flair, Quick Step, Trickster, Trivela"
🥉 80,Alexander Nübel,VfB Stuttgart,Bundesliga,"Cross Claimer, Deflector"
🥉 80,Mario Pašalić,Bergamo Calcio,Serie A Enilive,Trivela
🥉 80,Vangelis Pavlidis,SL Benfica,Liga Portugal,"Chip Shot, Power Header, Relentless, Technical"
🥉 80,Matteo Politano,SSC Napoli,Serie A Enilive,"Technical, Trivela, Whipped Pass"
🥉 80,Ivan Rakitić,Hajduk Split,Liga Hrvatska,"Power Shot, Press Proven, Tiki Taka, Trivela"
🥉 80,Amir Rrahmani,SSC Napoli,Serie A Enilive,"Aerial, Long Ball Pass, Long Throw"
🥉 80,Allan Saint-Maximin,Fenerbahçe,Trendyol Süper Lig,"Technical+, Flair, Quick Step, Trickster"
🥉 80,Davinson Sánchez,Galatasaray,Trendyol Süper Lig,"Aerial, Bruiser, Slide Tackle"
🥉 80,Diego Carlos,Aston Villa,Premier League,"Anticipate, Long Ball Pass"
🥉 80,Téji Savanier,Montpellier,Ligue 1 McDonald's,"Dead Ball, Finesse Shot, First Touch, Incisive Pass, Long Ball Pass, Trivela"
🥉 80,Kasper Schmeichel,Celtic,Scottish Prem,Deflector
🥉 80,William Carvalho,Real Betis,LALIGA EA SPOI,"Long Ball Pass, Press Proven, Tiki Taka"
🥉 80,Mohamed Simakan,Al Nassr,ROSHN Saudi League,"Bruiser, Jockey"
🥉 80,Sebastian Szymański,Fenerbahçe,Trendyol Süper Lig,"Dead Ball, Finesse Shot, Incisive Pass, Technical"
🥉 80,Mehdi Taremi,Lombardia FC,Serie A Enilive,"First Touch, Flair, Press Proven"
🥉 80,James Tarkowski,Everton,Premier League,"Aerial, Block, Long Ball Pass, Power Header"
🥉 80,Jean-Clair Todibo,West Ham,Premier League,"Anticipate, Jockey, Long Ball Pass"
🥉 80,Ivan Toney,Brentford,Premier League,"Power Header"
🥉 80,Ferran Torres,FC Barcelona,LALIGA EA SPOI,"Finesse Shot, Technical"
🥉 80,Hamari Traoré,Real Sociedad,LALIGA EA SPOI,"Long Throw, Rapid"
🥉 80,Lars Unnerstall,FC Twente,Eredivisie,Footwork
🥉 80,André Silva,RB Leipzig,Bundesliga,"Chip Shot, Flair"
🥉 80,Hans Vanaken,Club Brugge,1A Pro League,"Aerial, Incisive Pass, Long Ball Pass, Power Header"
🥉 80,Jordan Veretout,OM,Ligue 1 McDonald's,"Long Ball Pass, Press Proven, Relentless"
🥉 80,Timo Werner,Spurs,Premier League,"Quick Step, Rapid"
🥉 80,Mats Wieffer,Brighton,Premier League,"Aerial, Block, Bruiser, Intercept, Press Proven"
🥉 80,Axel Witsel,Atlético de Madrid,LALIGA EA SPOI,Bruiser
🥉 80,Barış Alper Yılmaz,Galatasaray,Trendyol Süper Lig,"Bruiser, Quick Step, Rapid, Relentless"
🥉 80,Warren Zaïre-Emery,Paris SG,Ligue 1 McDonald's,"First Touch, Press Proven, Quick Step, Tiki Taka"
🥉 80,André-Franck Zambo Anguissa,SSC Napoli,Serie A Enilive,"Anticipate, Block, Intercept, Relentless"
🥉 80,Lucas Zelarayán,Al Fateh,ROSHN Saudi League,"Dead Ball, Flair, Incisive Pass, Technical, Trivela, Whipped Pass"
🥉 80,Hakim Ziyech,Galatasaray,Trendyol Süper Lig,"Finesse Shot, First Touch, Flair, Power Shot, Technical, Trivela"
🥉 80,Zubeldia,Real Sociedad,LALIGA EA SPOI,"Bruiser, Long Ball Pass"
🥉 79,Matheus Cunha,Wolves,Premier League,"Flair, Rapid"
🥉 79,Dante,OGC Nice,Ligue 1 McDonald's,"Aerial, Anticipate, Block, Bruiser"
🥉 79,Samuel Lino,Atlético de Madrid,LALIGA EA SPORTS,
🥉 79,Matheus,SC Braga,Liga Portugal,"Far Reach, Far Throw, Long Ball Pass"
🥉 79,Galeno,FC Porto,Liga Portugal,"First Touch, Flair, Quick Step, Rapid, Relentless"
🥉 79,Carlos Augusto,Lombardia FC,Serie A Enilive,Relentless
🥉 78,Murillo,Nott'm Forest,Premier League,"Bruiser, Long Ball Pass"
🥉 78,Oscar,Shanghai Port FC,CSL,"Dead Ball, Finesse Shot, First Touch, Incisive Pass, Long Ball Pass, Technical, Trivela"
🥉 78,Lucas Perri,OL,Ligue 1 McDonald's,"Far Throw"
🥉 78,João Gomes,Wolves,Premier League,"Slide Tackle"
🥉 78,Ismaily,LOSC Lille,Ligue 1 McDonald's,"Flair, Technical"
🥉 78,Andreas Pereira,Fulham,Premier League,"Dead Ball, Flair, Technical"
🥉 78,Arthur Cabral,SL Benfica,Liga Portugal,"Flair, Power Header"
🥉 78,Neto,Arsenal,Premier League,"Cross Claimer"
🥉 78,Rodrigo Becão,Fenerbahçe,Trendyol Süper Lig,"Bruiser, Jockey, Power Header"
🥉 78,Marcão,Sevilla FC,LALIGA EA SPOI,"Bruiser, Long Ball Pass, Relentless, Slide Tackle"
🥉 78,Caio Henrique,AS Monaco,Ligue 1 McDonald's,"Dead Ball, Long Ball Pass, Long Throw, Whipped Pass"
🥉 78,Matheus Reis,Sporting CP,Liga Portugal,"Block, Trivela, Whipped Pass"
🥉 77,Gabriel Paulista,Beşiktaş,Trendyol Süper Lig,"Acrobatic, Intercept, Power Header, Slide Tackle"
🥉 77,Igor Paixão,Feyenoord,Eredivisie,"Flair, Technical, Whipped Pass"
🥉 77,Dodô,Fiorentina,Serie A Enilive,Rapid
🥉 77,Evander,Portland Timbers,MLS,"Flair, Incisive Pass, Long Ball Pass, Technical, Trivela"
🥉 77,Rodinei,Olympiacos FC,Hellas Liga,"Long Throw, Rapid"
🥉 77,Vanderson,AS Monaco,Ligue 1 McDonald's,Technical
🥉 77,Igor,Brighton,Premier League,"Bruiser, Jockey"
🥉 77,Marcelo Grohe,Al Kholood,ROSHN Saudi League,"Far Reach"
🥉 77,João Pedro,Brighton,Premier League,Rapid
🥉 77,Renan Lodi,Al Hilal,ROSHN Saudi League,"Long Ball Pass"
🥉 77,Lucas Beraldo,Paris SG,Ligue 1 McDonald's,"Pinged Pass, Slide Tackle"
🥉 77,Antony,Man Utd,Premier League,"Finesse Shot, Flair, Technical, Trickster"
🥉 77,Endrick,Real Madrid,LALIGA EA SPOI,"Flair, Power Shot, Quick Step, Rapid"
🥉 77,Wendell,FC Porto,Liga Portugal,"Block, Jockey, Slide Tackle, Whipped Pass"
🥉 77,Arthur,Juventus,Serie A Enilive,"Press Proven, Trivela"
🥉 77,Marcos Leonardo,SL Benfica,Liga Portugal,"Chip Shot"
🥉 76,Hernani,Parma,Serie A Enilive,"Block, Power Shot, Technical"
🥉 76,Taison,PAOK FC,Hellas Liga,"Finesse Shot"
🥉 76,Davidson,Başakşehir,Trendyol Süper Lig,"Finesse Shot, Technical"
🥉 76,Alexsandro,LOSC Lille,Ligue 1 McDonald's,"Anticipate, Block"
🥉 76,Andrei Girotto,Al Taawoun,ROSHN Saudi League,"Block, Intercept, Power Shot"
🥉 76,Gabriel Sara,Galatasaray,Trendyol Süper Lig,"Dead Ball, Flair, Incisive Pass, Power Shot"
🥉 76,Guilherme Sityá,Konyaspor,Trendyol Süper Lig,"Bruiser, Dead Ball, Intercept, Whipped Pass"
🥉 76,Mauro Júnior,PSV,Eredivisie,Flair
🥉 76,Emerson Royal,Milano FC,Serie A Enilive,"Relentless, Slide Tackle"
🥉 76,João Paulo,Sounders FC,MLS,"Bruiser, Pinged Pass, Relentless"
🥉 76,Cryzan,Shandong Taishan,CSL,"Aerial, First Touch"
🥉 76,Luiz Júnior,Villarreal CF,LALIGA EA SPOI,"Cross Claimer, Deflector, Far Throw, Long Ball Pass"
🥉 76,Igor Thiago,Brentford,Premier League,
🥉 76,Morato,Nott'm Forest,Premier League,"Bruiser, Long Ball Pass"
🥉 76,Vitor Roque,Real Betis,LALIGA EA SPOI,"Flair, Quick Step, Rapid"
🥉 76,Danilo,Nott'm Forest,Premier League,"Flair, Long Ball Pass"
🥉 76,Tuta,Frankfurt,Bundesliga,"Block, Bruiser, Jockey"
🥉 76,Willian Arão,Panathinaikos,Hellas Liga,"Aerial, Anticipate, Intercept, Jockey"
🥉 76,Gabriel Strefezza,Como,Serie A Enilive,"Incisive Pass, Technical, Whipped Pass"
🥉 75,Oberdan,Pohang Steelers,K League 1,"Anticipate, Incisive Pass, Intercept, Press Proven, Relentless"
🥉 75,Otávio,FC Porto,Liga Portugal,
🥉 75,Andrew,Gil Vicente,Liga Portugal,"Deflector, Footwork, Pinged Pass"
🥉 75,Aderllan Santos,Rio Ave FC,Liga Portugal,"Aerial, Intercept"
🥉 75,Mateus,Al Taawoun,ROSHN Saudi League,"Dead Ball, Power Shot"
🥉 75,Léo Duarte,Başakşehir,Trendyol Süper Lig,"Block, Jockey, Slide Tackle"
🥉 75,Bernardo,VfL Bochum 1848,Bundesliga,"Block, Intercept, Jockey, Slide Tackle"
🥉 75,Leonardo,Zhejiang Pro,CSL,"Finesse Shot, First Touch"
🥉 75,Jhonatan,Rio Ave FC,Liga Portugal,"Cross Claimer, Far Throw, Long Ball Pass"
🥉 75,Junior Messias,Genoa,Serie A Enilive,Rapid
🥉 75,Rodrigo Muniz,Fulham,Premier League,"Acrobatic+, Flair"
🥉 75,Douglas Augusto,FC Nantes,Ligue 1 McDonald's,"Intercept, Jockey"
🥉 75,Tetê,Panathinaikos,Hellas Liga,Technical
🥉 74,Vinícius,Fulham,Premier League,
🥉 74,Léo Baptistão,UD Almería,LALIGA HYPERMOTION,
🥉 74,Vitor Carvalho,SC Braga,Liga Portugal,
🥉 74,Maracás,Moreirense FC,Liga Portugal,Aerial
🥉 74,Natan,Real Betis,LALIGA EA SPORTS,
🥉 74,Vinicius Souza,Sheffield Utd,EFL Championship,"Intercept, Long Ball Pass, Slide Tackle"
🥉 74,Pedrinho,Shakhtar Donetsk,Ukrayina Liha,"Flair, Technical"
🥉 74,Jean,Cerro Porteño,Libertadores,"Far Reach, Far Throw"
🥉 74,Gabriel Pec,LA Galaxy,MLS,Flair
`;
        
        const taticasDB = [
            { filosofia: "Gegenpressing", descricao: "Pressão implacável para recuperar a bola no campo de ataque.", formacao: "4-3-3", semBola: { profundidade: 70 }, comBola: { armacao: "Armação Rápida", criacao: "Corridas Ofensivas" }, instrucoes: { GK: "Sai nos Cruzamentos / Goleiro Líbero", ZC: "Interceptações Agressivas", LAT: "Participar do Ataque", MC: "Cobrir o Centro / Chegar na Área", VOL: "Ficar na Defesa", PD: "Voltar pra Defender / Entrar na Área", PE: "Voltar pra Defender / Entrar na Área", ATA: "Ficar no Ataque / Pivô" } }, 
            { filosofia: "Tiki-Taka Dominante", descricao: "Controle total através da posse de bola e passes curtos.", formacao: "4-3-3 Falso 9", semBola: { profundidade: 50 }, comBola: { armacao: "Posse de Bola", criacao: "Posse de Bola" }, instrucoes: { GK: "Goleiro Líbero", ZC: "Avançar a Linha", LAT: "Apoio Ofensivo", MC: "Ataque Equilibrado / Ficar na Entrada da Área", VOL: "Ficar na Defesa / Cobrir o Centro", SA: "Falso 9", PD: "Cortar pra Dentro / Apoio Defensivo Básico", PE: "Cortar pra Dentro / Apoio Defensivo Básico" } }, 
            { filosofia: "Bloco Baixo Reativo", descricao: "Defesa sólida e contra-ataques mortais.", formacao: "5-3-2", semBola: { profundidade: 30 }, comBola: { armacao: "Lançamentos", criacao: "Corridas Ofensivas" }, instrucoes: { GK: "Goleiro Tradicional", ZC: "Ficar na Defesa", LAD: "Voltar para Defender", LAE: "Voltar para Defender", MC: "Ficar na Defesa / Cobrir o Centro", ATA: "Chegar por Trás / Pivô" } },
            { filosofia: "Controle e Transição", descricao: "Domina o meio-campo com dois volantes e usa a velocidade dos pontas para transições rápidas.", formacao: "4-2-3-1", semBola: { profundidade: 45 }, comBola: { armacao: "Equilibrado", criacao: "Passes Direcionados" }, instrucoes: { GK: "Padrão", ZC: "Ficar na Defesa", LAT: "Ficar na Defesa", VOL: "Cortar Linhas de Passe / Cobrir o Centro", MD: "Voltar para Defender / Ficar na Ponta", ME: "Voltar para Defender / Ficar na Ponta", MEI: "Ficar na Entrada da Área", ATA: "Ficar no Centro" } },
            { filosofia: "Pressão Total na Saída", descricao: "Sufoca o adversário no campo de defesa com três atacantes e alas agressivos.", formacao: "3-4-3", semBola: { profundidade: 80 }, comBola: { armacao: "Armação Rápida", criacao: "Corridas Ofensivas" }, instrucoes: { GK: "Goleiro Líbero", ZC: "Participar do Ataque", MD: "Ficar na Ponta / Chegar por Trás", ME: "Ficar na Ponta / Chegar por Trás", MC: "Ataque Equilibrado", PE: "Ficar no Ataque / Cortar pra Dentro", PD: "Ficar no Ataque / Cortar pra Dentro", ATA: "Pivô" } },
            { filosofia: "Jogo Curto pelo Meio", descricao: "Foco no controle do centro do campo com um losango, usando passes curtos e triangulações.", formacao: "4-1-2-1-2", semBola: { profundidade: 55 }, comBola: { armacao: "Posse de Bola", criacao: "Posse de Bola" }, instrucoes: { GK: "Padrão", ZC: "Ficar na Defesa", LAT: "Apoio Ofensivo", VOL: "Ficar na Defesa / Cobrir o Centro", MC: "Ir para as Pontas / Chegar na Área", MEI: "Flutuar Livremente", ATA: "Entrar na Área para Cruzamento" } },
            { filosofia: "Muralha e Contra-Ataque", descricao: "Defesa ultra-sólida com três zagueiros e dois alas, buscando o MEI para lançar os dois atacantes em velocidade.", formacao: "5-2-1-2", semBola: { profundidade: 25 }, comBola: { armacao: "Lançamentos", criacao: "Passes Direcionados" }, instrucoes: { GK: "Goleiro Tradicional", ZC: "Interceptações Conservadoras", LAD: "Apoiar o Ataque", LAE: "Apoiar o Ataque", MC: "Ficar na Defesa / Cobrir o Centro", MEI: "Ficar no Ataque", ATA: "Chegar por Trás" } },
            { filosofia: "Quadrado Mágico", descricao: "Dois volantes dão suporte a dois meias ofensivos que flutuam por dentro, criando superioridade numérica para servir a dupla de ataque.", formacao: "4-2-2-2", semBola: { profundidade: 60 }, comBola: { armacao: "Equilibrado", criacao: "Posse de Bola" }, instrucoes: { GK: "Padrão", ZC: "Ficar na Defesa", LAT: "Ficar na Defesa", VOL: "Cobrir o Centro", MED: "Cortar pra Dentro / Apoio Defensivo Básico", MEE: "Cortar pra Dentro / Apoio Defensivo Básico", ATA: "Ataque Misto" } }
        ];
        
        const clubEmojis = { "Alianza Lima": "💙", "América-MG": "🐰", "Argentinos Juniors": "🐞", "Athletico-PR": "🌪️", "Atlético-MG": "🐓", "Atlético Nacional": "🏆", "Aucas": "🟡", "Audax Italiano": "🟢", "Barcelona SC": "🟡", "Blooming": "🎓", "Boca Juniors": "🍫", "Bolívar": "🌌", "Botafogo": "⭐", "Bragantino": "🐂", "Cerro Porteño": "🌀", "César Vallejo": "👨‍🏫", "Colo-Colo": "酋長", "Corinthians": "⚓️", "Danubio": "⚫️", "Defensa y Justicia": "🦅", "Deportivo Pereira": "🟠", "Emelec": "⚡️", "Estudiantes": "🦁", "Estudiantes de Mérida": "👨‍🎓", "Flamengo": "🔴⚫️", "Fluminense": "🇭🇺", "Fortaleza": "🦁🔴", "Gimnasia": "🐺", "Goiás": "🟢", "Guaraní": "🏹", "Huracán": "🎈", "Independiente del Valle": "⚫️🔵", "Independiente Medellín": "💪", "Internacional": "🇦🇹", "LDU Quito": "⚪️", "Libertad": "⚫️", "Liverpool-URU": "🐦", "Magallanes": "⛵️", "Melgar": "🔴⚫️", "Metropolitanos": "🟣", "Millonarios": "Ⓜ️", "Monagas": "🔵🔴", "Nacional": "🇺🇾", "Newell’s Old Boys": "🔴⚫️", "Ñublense": "👹🔴", "Olimpia": "⚫️", "Oriente Petrolero": "⛽️", "Palestino": "🇵🇸", "Palmeiras": "🐷", "Patronato": "😇", "Peñarol": "🟡⚫️", "Racing Club": "🎓", "River Plate": "🐔", "San Lorenzo": "🐦", "Santa Fe": "🦁🔴", "Santos": "🐟", "São Paulo": "🇾🇪", "Sporting Cristal": "🍺", "Tacuary": "⚫️", "The Strongest": "🐅", "Tigre": "🐅", "Tolima": "🏹", "Universitario": "🍦", "Atlético Tucumán": "👑", "Banfield": "🛠️", "Barracas Central": "🚚", "Belgrano": "🏴‍☠️", "Central Córdoba": "🚂", "Deportivo Riestra": "⚫️", "Godoy Cruz": "🍇", "Independiente": "👹", "Independiente Rivadavia": "🔵", "Instituto Córdoba": "🔴", "Lanús": "🇱🇻", "Platense": "🦑", "Rosario Central": "🇺🇦", "Sarmiento": "🟢", "Talleres": "🔵", "Unión": "⚪️", "Vélez Sarsfield": "🏰", "Atlanta United": "🚂", "Austin FC": "🌳", "CF Montreal": "⚜️", "Charlotte FC": "👑", "Chicago Fire": "🔥", "Colorado Rapids": "🏔️", "Columbus Crew": "👷‍♂️", "D.C. United": "🦅", "FC Cincinnati": "🦁⚔️", "FC Dallas": "🐂", "Houston Dynamo": "⚡️", "Inter Miami CF": "🦩", "LA Galaxy": "✨", "Los Angeles FC": "🪽", "Minnesota United": "🦆", "Nashville SC": "🎸", "New England Revolution": "🇺🇸", "New York City FC": "🗽", "New York Red Bulls": "🐂", "Orlando City SC": "🦁🟣", "Philadelphia Union": "🐍", "Portland Timbers": "🌲", "Real Salt Lake": "👑🔴", "San Jose Earthquakes": "🌎", "Seattle Sounders FC": "🔊", "Sporting Kansas City": "🔵", "St. Louis City SC": "⚜️", "Toronto FC": "🍁", "Vancouver Whitecaps FC": "🏔️", "Kansas City Current": "⚡️", "NJ/NY Gotham FC": "🦇", "North Carolina Courage": "🦁", "Orlando Pride": "🦁", "Portland Thorns FC": "🌹", "Racing Louisville FC": "🐎", "San Diego Wave FC": "🌊", "Seattle Reign FC": "👑", "Utah Royals": "👑", "Washington Spirit": "👻", "Arsenal": "🏹", "Aston Villa": "🦁🟣", "Bournemouth": "🍒", "Brentford": "🐝", "Brighton": "🕊️", "Chelsea": "🦁🔵", "Crystal Palace": "🦅🔴", "Everton": "🍬", "Fulham": "🏠", "Ipswich Town": "🚜", "Leicester": "🦊", "Liverpool": "🐦", "Man City": "🚢", "Man Utd": "👹", "Newcastle": "⚫️⚪️", "Nottingham Forest": "🌳", "Southampton": "😇", "Tottenham": "🐓", "West Ham": "⚒️", "Wolves": "🐺🟠", "Blackburn": "🌹", "Bristol City": "🐦", "Burnley": "🍷", "Cardiff": "🐦🔵", "Coventry": "🐘", "Derby": "🐏", "Hull": "🐅", "Leeds": "🦚", "Luton": "🎩", "Middlesbrough": "🦁🔴", "Millwall": "🦁⚪️", "Norwich": "🐤", "Oxford": "🐂", "Plymouth": "⛵️", "Portsmouth": "⚓️🌙", "Preston": "⚪️⚜️", "QPR": "👑", "Sheffield Utd": "⚔️", "Sheffield Wednesday": "🦉", "Stoke": "🏺", "Sunderland": "🐈⚫️", "Swansea": "🦢", "Watford": "🦌", "West Brom": "🐦🔵", "Barnsley": "🐶", "Birmingham": "🔵", "Blackpool": "🍊", "Bolton": "🐎", "Bristol Rovers": "🏴‍☠️", "Burton": "🍺", "Cambridge": "⚫️🟡", "Charlton": "⚔️", "Crawley": "👹", "Exeter": "🏛️", "Huddersfield": "🐶", "Leyton Orient": "🐉", "Lincoln": "👹", "Mansfield": "🦌", "Northampton": "👞", "Peterborough": "🔵", "Reading": "👑🔵", "Rotherham": "⚙️", "Shrewsbury": "🦁🔵", "Stevenage": "🔴", "Stockport": "🎩", "Wigan": "🔵⚪️", "Wrexham": "🐉🏴󠁧󠁢󠁷󠁬󠁳󠁿", "Wycombe": "🦢", "Alavés": "🦊🔵", "Athletic Bilbao": "🦁🔴", "Atlético de Madrid": "🐻🌳", "Barcelona": "❤️💙", "Celta Vigo": "⚪️🔵", "Getafe": "✈️", "Girona": "🦟", "Las Palmas": "🟡🔵", "Leganés": "🥒", "Mallorca": "🏝️", "Osasuna": "🐂", "Rayo Vallecano": "⚡️", "Real Betis": "🟢⚪️", "Real Madrid": "👑", "Real Sociedad": "🌊", "Sevilla": "🔥", "Valencia": "🦇", "Valladolid": "🟣⚪️", "Villarreal": "🟡", "Albacete": "🦇", "Almería": "🔴⚪️", "Burgos": "🏰", "Cádiz": "🟡", "Cartagena": "⚫️⚪️", "Castellón": "⚫️⚪️", "Deportivo La Coruña": "🐙", "Eibar": "🔴🔵", "Elche": "🌴", "Eldense": "🔴🔵", "Espanyol": "🐦", "Granada": "🔴⚪️", "Huesca": "🔴🔵", "Levante": "🐸", "Mirandés": "🔴⚫️", "Racing Ferrol": "🟢", "Racing Santander": "🟢⚪️", "Real Oviedo": "⛪️", "Sporting Gijón": "🔴⚪️", "Tenerife": "⚪️🔵", "Zaragoza": "🦁⚪️", "Hoffenheim": "🔵", "Bayer Leverkusen": "🏭", "Bayern Munich": "🍺", "Dortmund": "🧱", "Mönchengladbach": "🐎", "Frankfurt": "🦅", "Augsburg": "🌲🔴", "Heidenheim": "🔴", "Holstein Kiel": "🔵⚪️", "Mainz": "🔴", "RB Leipzig": "🐂", "Freiburg": "🌲⚫️", "St. Pauli": "☠️", "Union Berlin": "🐻", "Stuttgart": "🚗", "Bochum": "🔵⚪️", "Wolfsburg": "🐺🟢", "Werder Bremen": "🔑", "Darmstadt": "⚜️", "Braunschweig": "🦁🟡", "Elversberg": "⚫️⚪️", "Kaiserslautern": "👹🔴", "Köln": "🐐", "Nürnberg": "🔴⚫️", "Fortuna Düsseldorf": "🔴", "Greuther Fürth": "🍀", "Hamburger SV": "🦖", "Hannover 96": "9️⃣6️⃣", "Hertha BSC": "👵", "Jahn Regensburg": "🔴⚪️", "Karlsruher": "🔵⚪️", "Preußen Münster": "🦅⚫️", "Paderborn": "🔵⚫️", "Schalke 04": "⛏️", "SSV Ulm": "🐦⚫️", "AC Milan": "🔴⚫️", "AS Roma": "🐺", "Atalanta": "🏃‍♀️", "Bologna": "🍝", "Cagliari": "🏝️", "Como": "🏞️", "Empoli": "🖼️", "Fiorentina": "⚜️", "Genoa": "⚓️", "Hellas Verona": "🏛️", "Inter Milan": "🐍", "Juventus": "🦓", "Lazio": "🦅", "Lecce": "🐺🟡", "Monza": "🏎️", "Parma": "🧀", "Napoli": "🌋", "Torino": "🐂", "Udinese": "🦓⚫️", "Venezia": "🦁🪽", "Bari": "🐓", "Catanzaro": "🦅🟡", "Cesena": "🐴", "Cittadella": "🏰", "Cosenza": "🐺🔴", "Cremonese": "🎻", "Frosinone": "🦁🟡", "Juve Stabia": "🐝", "Mantova": "⚪️🔴", "Modena": "🐤", "Palermo": "🦅🩷", "Pisa": "🗼", "Reggina": "🟠⚫️", "Reggiana": "🔴", "Salernitana": "🐴", "Sampdoria": "⚓️🔵", "Sassuolo": "🟢⚫️", "Spezia": "🦅", "Südtirol": "⚪️🔴", "Angers": "⚫️⚪️", "Auxerre": "🔵⚪️", "Monaco": "🎰", "Le Havre": "🔵", "LOSC Lille": "🐶", "Montpellier": "🟠🔵", "Nice": "🦅⚫️", "Marseille": "🌟", "Nantes": "🐤", "Lyon": "🦁🔴", "PSG": "🗼", "Lens": "⛏️", "Strasbourg": "⚫️🔵", "Brest": "🏴‍☠️", "Reims": "🍾", "Rennes": "⚫️🔴", "Toulouse": "🟣", "Saint-Étienne": "💚", "Ajaccio": "🐻", "Amiens": "🦄", "Caen": "🛡️", "Clermont": "🔴🔵", "Dunkerque": "🔵⚪️", "Guingamp": "🔴⚫️", "Annecy": "🔴", "Lorient": "🐟", "Martigues": "🩸🟡", "Metz": "🔴", "Bordeaux": "🍷", "Grenoble": "🐬", "Laval": "🟠", "Paris FC": "🔵", "Pau": "🟡🔵", "Red Star": "⭐", "Rodez": "🔴🟡", "Bastia": "🗿", "Arouca": "🟡🔵", "AVS": "🔴", "Boavista": "🏁", "Casa Pia": "鵝", "CD Nacional": "⚫️⚪️", "Estrela Amadora": "⭐", "Estoril": "🐤", "Famalicão": "🔵⚪️", "Farense": "🦁⚫️", "FC Porto": "🐉", "Gil Vicente": "🐓", "Moreirense": "🟢⚪️", "Rio Ave": "🟢⚪️", "Santa Clara": "🔴", "SL Benfica": "🦅", "Sporting": "🦁🟢", "Braga": "⚔️", "Vitória SC": "👑", "Ajax": "❌", "Almere City": "⚫️🔴", "AZ": "🧀", "FC Utrecht": "🗼", "Feyenoord": "🏗️", "Fortuna Sittard": "🟡🟢", "Go Ahead Eagles": "🦅", "Groningen": "🟢⚪️", "Heracles Almelo": "⚫️⚪️", "NAC Breda": "🟡⚫️", "NEC Nijmegen": "🔴🟢", "PEC Zwolle": "🔵⚪️", "PSV": "💡", "RKC Waalwijk": "🟡🔵", "SC Heerenveen": "❤️", "Sparta Rotterdam": "🔴⚪️", "Twente": "🐎⚪️", "Willem II": "🔴⚪️🔵", "Beerschot": "🐻🟣", "Cercle Brugge": "🟢⚫️", "Charleroi": "🦓", "Club Brugge": "🔵⚫️", "Dender EH": "🔵⚫️", "Genk": "🔵", "Gent": "🐃", "Kortrijk": "🔴⚪️", "Leuven": "⚪️", "Mechelen": "🔴🟡", "Royal Antwerp FC": "🔴", "R.S.C Anderlecht": "🟣⚪️", "Sint-Truiden": "🐤", "Standard Liège": "🔴", "Union SG": "🟡🔵", "Westerlo": "🟡", "Aberdeen": "🔴", "Celtic": "🍀", "Dundee": "🔵", "Dundee United": "🟠", "Heart of Midlothian": "❤️", "Hibernian": "🟢⚪️", "Kilmarnock": "🔵⚪️", "Motherwell": "🟠", "Rangers": "🧸", "Ross County": "🦌", "St Johnstone": "😇", "St Mirren": "⚫️⚪️", "Bohemians": "🔴⚫️", "Derry City": "🍬", "Drogheda": "⭐", "Dundalk": "🛡️", "Galway United": "🤤", "Shamrock Rovers": "☘️", "Sligo Rovers": "🔴", "Shelbourne": "🔴", "St Patrick’s Athletic": "😇", "Waterford": "🔵", "Adana Demirspor": "⚡️", "Alanyaspor": "🟠🟢", "Antalyaspor": "🦂", "Beşiktaş": "⚫️🦅", "Bodrum": "🟢⚪️", "Eyüpspor": "🟣🟡", "Fenerbahçe": "🐤", "Galatasaray": "🦁⭐", "Gaziantep FK": "🔴⚫️", "Göztepe": "🔴🟡", "Hatayspor": "⚪️🔴", "Başakşehir": "🦉", "Kasımpaşa": "🔵⚪️", "Kayserispor": "🟡🔴", "Konyaspor": "🦅🟢", "Rizespor": "🍵", "Samsunspor": "🔴⚪️", "Sivasspor": "🔴⚪️", "Trabzonspor": "🌀", "Botoșani": "🔴⚪️", "CFR Cluj": "🚂", "Dinamo București": "🐕", "Farul Constanța": "🦈", "FCSB": "🔴🔵", "Gloria Buzău": "🔴🔵", "Hermannstadt": "🔴⚫️", "Oțelul Galați": "🔩", "Petrolul": "🐺🟡", "Politehnica Iași": "⚪️🔵", "Rapid București": "🦅", "Sepsi": "🛡️", "Unirea Slobozia": "🟡🔵", "Universitatea Cluj": "⚫️⚪️", "Universitatea Craiova": "🦁🔵", "UTA Arad": "👵", "Cracovia": "⚪️🔴", "GKS Katowice": "🟡🟢", "Górnik Zabrze": "⛏️", "Jagiellonia Białystok": "🐝🟡", "Korona Kielce": "👑", "Lechia Gdańsk": "🦁🟢", "Lech Poznań": "🚂", "Legia Warszawa": "L", "Motor Lublin": "🟡⚪️", "PGE Stal Mielec": "⚪️🔵", "Piast Gliwice": "🔵🔴", "Pogoń Szczecin": "🔴🔵", "Puszcza Niepołomice": "🌳", "Radomiak Radom": "🟢", "Raków Częstocho-wa": "🔴🔵", "Śląsk Wrocław": "🦅", "Widzew Łódź": "🔴", "Zagłębie Lubin": "🟠", "Aarhus GF": "⚪️", "Brøndby IF": "🟡🔵", "FC København": "🦁⚪️", "Kolding IF": "⚪️🔵", "AC Lyngby": "👑", "FC Midtjylland": "🐺", "FC Nordsjælland": "🐅", "Randers FC": "🐎", "Silkeborg IF": "🔴", "Soenderjyske Fodbold": "🔵⚪️", "Vejle Boldklub": "🔴", "Viborg FF": "🍀", "Bodø/Glimt": "🟡", "Brann": "🔴", "Fredrikstad": "🔴⚪️", "Hamarkameratene": "🟢⚪️", "Haugesund": "🔵⚪️", "KFUM Oslo": "⚪️", "Kristiansund": "🔵", "Lillestrøm": "🐤", "Molde": "🔵", "Odds BK": "⚫️⚪️", "Rosenborg": "⚫️⚪️", "Sandefjord": "🐋", "Sarpsborg 08": "🔵", "Strømsgodset": "🔵", "Tromsø": "🔴⚪️", "Viking": "🛡️", "AIK": "⚫️🟡", "BK Häcken": "🐝", "Djurgårdens IF": "🔵", "GAIS": "🟢⚫️", "Halmstads BK": "🔵", "Hammarby IF": "🟢⚪️", "IF Brommapojkarna": "🔴⚫️", "IF Elfsborg": "🟡⚫️", "IFK Göteborg": "🔵⚪️", "IFK Norrköping": "⚪️🔵", "IFK Värnamo": "⚪️🔵", "IK Sirius": "🔵⚫️", "Kalmar FF": "🔴", "Malmö FF": "🔵", "Mjällby AIF": "🟡⚫️", "Västerås SK": "🟢⚪️", "BSC Young Boys": "👦", "Basel": "🔴🔵", "Lausanne-Sport": "🔵⚪️", "Lugano": "⚫️", "Luzern": "🔵⚪️", "Sion": "🔴⚪️", "St. Gallen": "🟢⚪️", "Zürich": "🔵⚪️", "Grasshopper": "🦗", "Servette": "🍷", "Winterthur": "🔴", "Yverdon-Sport": "🟢", "Al Ahli": "🏰", "Al-Fateh": "🟢", "Al Fayha": "🟠", "Al Hilal": "🌙", "Al Ittihad": "🐅", "Al Khaleej": "🟡", "Al-Kholood": "🟢", "Al Nassr": "⚔️", "Al-Okhdood": "🔵", "Al-Orobah": "🟢", "Al-Qadsiah": "🔴", "Al Raed": "🔴", "Al-Riyadh": "🔴⚫️", "Al Shabab": "🦁⚪️", "Al Taawoun": "🐺", "Al Wehda": "🔴", "Damac": "🔴", "Ettifaq FC": "🟢", "Daegu FC": "🔵", "Daejeon Hana Citizen": "🟣", "FC Seoul": "⚫️🔴", "Gangwon FC": "🐻", "Gimcheon Sangmu": "🔴", "Gwangju FC": "🟡", "Incheon United": "✈️", "Jeonbuk Hyundai Motors": "🟢", "Jeju United": "🍊", "Pohang Steelers": "🔩", "Suwon FC": "🔵🔴", "Ulsan Hyundai": "🐅🔵", "Beijing Guoan": "🟢", "Cangzhou Lions": "🦁🔵", "Changchun Yatai": "🔴", "Chengdu Rongcheng": "🔴", "Henan": "🔴", "Meizhou Hakka": "🔴", "Nantong Zhiyun": "🔵", "Qingdao Hainiu": "🐂", "Qingdao West Coast": "🔵", "Shandong Taishan": "⛰️", "Shanghai Shenhua": "🔵", "Shanghai Port": "🔴", "Shenzhen Peng City": "🔴", "Tianjin Jinmen Tiger": "🐅", "Wuhan Three Towns": "🏙️", "Zhejiang": "🌳", "ATK Mohun Bagan": "🟢🔴", "Bengaluru": "🔵", "Chennaiyin": "🔵", "East Bengal": "🔴🟡", "Goa": "🐂", "Hyderabad": "🟡⚫️", "Jamshedpur": "🔴", "Kerala Blasters": "🐘", "Mohammedan": "⚫️⚪️", "Mumbai City": "🔵", "NorthEast United": "🔴", "Odisha": "⚫️", "RoundGlass Punjab": "🟠", "Adelaide United": "🔴", "Brisbane Roar": "🦁🟠", "Central Coast Mariners": "🌴", "Macarthur FC": "🐂", "Melbourne City": "🏙️", "Newcastle Jets": "✈️", "Perth Glory": "🟣", "Sydney FC": "🎭", "Wellington Phoenix": "🐦🟡", "Western Sydney Wanderers": "⚫️🔴", "Western United": "⚫️🟢", "default": "⚽️" };
        
        const eventsDB = {
            conflitoInterno: {
                Goleiro: [
                    { title: "🤬 Insatisfação do Goleiro", dialogue: "Treinador, essa história de 'sair jogando' com a bola no pé é pra time de futsal! Minha função é defender, não arriscar passe. Ou a gente para com essa palhaçada, ou eu vou começar a dar chutão pra arquibancada!" },
                    { title: "🤬 Insatisfação do Goleiro", dialogue: "Mister, eu sou o líder da defesa, o cara que organiza o time lá de trás. Eu quero ser o capitão da equipe! Se for pra ficar só no gol, é melhor eu ir pro banco." }
                ],
                Defensor: [
                    { title: "🤬 Insatisfação do Zagueiro", dialogue: "Treinador, essa linha alta tá me matando! A gente tá dando muito espaço nas costas! Não dá pra jogar com a defesa lá na frente contra atacantes rápidos. Ou a gente ajusta isso, ou vamos ser vazados a cada contra-ataque.", consequence: { type: 'CHANGE_FORMATION', formations: ['5-3-2', '5-2-1-2'] } },
                    { title: "🤬 Insatisfação do Zagueiro", dialogue: "Chefe, eu sou zagueiro, não volante! Essa insistência em me fazer subir e cobrir o meio-campo tá me exaurindo. Ou me deixam fazer o meu trabalho, ou a defesa vai virar uma peneira." }
                ],
                "Meio-campista": [
                    { title: "🤬 Insatisfação do Meio-Campo", dialogue: "Professor, eu não sou só um cão de guarda! Eu também sei atacar, tenho um bom chute. Mas essa tática de me prender lá atrás tá me limitando. Eu quero mais liberdade pra subir!", consequence: { type: 'CHANGE_FORMATION', formations: ['4-3-3', '4-2-3-1', '3-4-3'] } }
                ],
                Atacante: [
                    { title: "🤬 Insatisfação do Centroavante", dialogue: "Mister, eu não sou um exército de um homem só! Preciso de um companheiro de ataque, alguém pra dividir a marcação. Se for pra jogar sozinho lá na frente, é melhor eu ir pro banco e deixar outro tentar.", consequence: { type: 'CHANGE_FORMATION', formations: ['5-3-2', '4-1-2-1-2', '5-2-1-2', '4-2-2-2'] } },
                    { title: "🤬 Insatisfação do Ponta", dialogue: "Mister, eu sou o cara que decide jogo! Eu treino falta todo dia, mas quem bate é sempre o mesmo. Eu quero ser o cobrador oficial de faltas e pênaltis. É a minha chance de brilhar." },
                    { title: "🤬 Insatisfação do Ponta", dialogue: "Treinador, eu sou um jogador de meio-campo, não um ponta! Minha visão de jogo é desperdiçada na lateral. Eu quero jogar pelo meio, como um camisa 10. Eu quero ser o cérebro do time!", consequence: { type: 'CHANGE_FORMATION', formations: ['4-2-3-1', '4-1-2-1-2', '5-2-1-2'] } }
                ]
            },
            criseDeImprensa: [ { title: "📰 Crise de Imprensa", posGeral: "Atacante", description: "Seu atacante, {playerName}, está há alguns jogos sem marcar. O apelido dele no vestiário agora é 'chute de espoleta'." }, { title: "📰 Crise de Imprensa", posGeral: "Goleiro", description: "A torcida não perdoa o último frango do seu goleiro, {playerName}. Faixas de 'Mãos de Alface' foram vistas no estádio." }, { title: "📰 Crise de Imprensa", posGeral: "Defensor", description: "Seu zagueiro, {playerName}, foi driblado tantas vezes que a Amazon está oferecendo a ele um teste para o Prime." } ],
            clima: [ 
                { title: "☀️ Condições Climáticas", description: "Céu limpo e temperatura agradável. Condições perfeitas para o futebol!" }, 
                { title: "⛈️ Fúria da Natureza!", description: "Uma chuva de granizo inesperada danificou o gramado. A bola vai quicar de forma imprevisível." }, 
                { title: "❄️ Neve Intensa", description: "NEVASCA! O campo está coberto de neve, tornando a bola mais lenta e os passes mais difíceis de dominar." }, 
                { title: "💨 Ventania", description: "Um vento forte e inconstante atravessa o campo, afetando lançamentos, cruzamentos e a trajetória da bola." },
                { title: "🌱 Gramado Sintético", description: "O jogo será em gramado sintético. A bola correrá mais rápido que o normal." },
                { title: "🌿 Gramado Normal", description: "O gramado está em perfeitas condições. Um tapete para o espetáculo." }
            ],
            anomalias: [ { title: "‼️ Sorteio Duplo", description: "PACOTE EM DOBRO! A sua próxima escolha de jogador valerá por dois. Você receberá o jogador escolhido e mais um aleatório da mesma raridade.", consequence: { type: 'DOUBLE_DRAFT', targets: ['self'] } }, { title: "‼️ Sobrecarga de Servidor", description: "PICO de ENERGIA! O sistema concedeu um jogador aleatório extra para o time que está perdendo no placar da temporada como forma de estabilização.", consequence: { type: 'BONUS_PLAYER_LOSER', targets: ['loser'] } }],
            dilemas: [ { title: "⚖️ O Dilema do Manager", description: "A SABOTAGEM: Pague o preço: seu próximo sorteio será rebaixado em uma categoria de raridade. Em troca, o próximo sorteio do seu adversário também será.", choices: [{ text: "Sabotar", consequence: { type: 'SABOTAGE', targets: ['self', 'opponent'] } }, { text: "Jogar Limpo", consequence: { type: 'NONE' } }] }, { title: "⚖️ O Dilema do Manager", description: "O SACRIFÍCIO: Demita AGORA o seu jogador de menor OVR e, em troca, seu próximo pacote de sorteio terá a garantia de ser Ouro 🥇 ou superior.", choices: [{ text: "Sacrificar", consequence: { type: 'SACRIFICE_FOR_UPGRADE', targets: ['self'] } }, { text: "Manter Jogador", consequence: { type: 'NONE' } }] }, { title: "⚖️ O Dilema do Manager", description: "O PACTO: Você pode receber um jogador Diamante 💎 agora, mas em troca, seu adversário começará a próxima temporada com 2 vitórias de vantagem.", choices: [{ text: "Aceitar Pacto", consequence: { type: 'PACT_FOR_DIAMOND', targets: ['self'] } }, { text: "Recusar", consequence: { type: 'NONE' } }] }]
        };

        const frasesDeEfeito = ["Uma escolha sólida. O arroz com feijão que ganha campeonato.", "Ousado. O sistema não consegue calcular a probabilidade de isso dar certo.", "Este jogador é uma faca de dois gumes. Cuidado ao manuseá-lo.", "Uma peça que se encaixa perfeitamente na sua engrenagem tática.", "O sistema detecta um aumento de 7.3% na sua chance de vitória com esta adição."];
        const rarities = ["bronze", "prata", "ouro", "diamante"];
        const rarityEmojis = { bronze: '🥉', prata: '🥈', ouro: '🥇', diamante: '💎' };
        
        let gameState = { placarGeral: { caio: 0, ricardo: 0 }, temporadaAtual: { caio: 0, ricardo: 0 }, lossStreak: { caio: 0, ricardo: 0 }, elencos: { caio: [], ricardo: [] }, taticas: { caio: null, ricardo: null }, timesBase: { caio: null, ricardo: null }, turno: null, fase: 'INICIO', rodadaDraft: 1, draftPool: [], jogadoresUsados: [], historico: [], pendingDraft: null, effects: {}, usedDialogues: { conflitoInterno: [], criseDeImprensa: [], dilemmas: [] } };
        let jogoRapidoState = { placar: { caio: 0, ricardo: 0 }, taticas: { caio: null, ricardo: null } };

        // --- DECLARAÇÃO DE ELEMENTOS DOM ---
        const menuPrincipalEl = document.getElementById('menu-principal');
        const jogoContainerEl = document.getElementById('jogo-container');
        const historicoContainerEl = document.getElementById('historico-container');
        const btnJogar = document.getElementById('btn-jogar');
        const btnHistorico = document.getElementById('btn-historico');
        const btnRegras = document.getElementById('btn-regras');
        const btnModosJogo = document.getElementById('btn-modos-jogo');
        const btnVoltarMenu = document.getElementById('btn-voltar-menu');
        const btnVoltarMenuJogo = document.getElementById('btn-voltar-menu-jogo');
        const adminBtnMenu = document.getElementById('admin-btn-menu');
        const historicoContentEl = document.getElementById('historico-content');
        const jogoRapidoContainerEl = document.getElementById('jogo-rapido-container');
        const sorteioTimesContainerEl = document.getElementById('sorteio-times-container');

        const [placarGeralEl, placarTemporadaEl, listaCaioEl, listaRicardoEl, mensagensSistemaEl, areaDeEscolhaEl, areaDeDecisaoEl, areaDeComandosEl, modalEl, modalTitleEl, modalBodyEl, modalCloseBtn, modalBackdrop] = [ '#placar-geral', '#placar-temporada', '#lista-caio', '#lista-ricardo', '#mensagens-sistema', '#area-de-escolha', '#area-de-decisao', '#area-de-comandos', '#modal', '#modal-title', '#modal-body', '#modal-close-btn', '.modal-backdrop'].map(s => document.querySelector(s));

        // --- LÓGICA DO JOGO ---

        function getClubEmoji(clubName) {
            if (!clubName) return clubEmojis.default;
            const lowerClubName = clubName.toLowerCase();
            for (const key in clubEmojis) {
                if (key.toLowerCase() === lowerClubName) {
                    return clubEmojis[key];
                }
            }
            for (const key in clubEmojis) {
                if (lowerClubName.includes(key.toLowerCase())) {
                    return clubEmojis[key];
                }
            }
            return clubEmojis.default;
        }

        function typeMessage(text, slow = false) { 
            const p = document.createElement('p'); 
            mensagensSistemaEl.appendChild(p); 
            let i = 0; 
            function typing() { 
                if (i < text.length) { 
                    p.innerHTML += text.charAt(i); 
                    i++; 
                    setTimeout(typing, slow ? 25 : 5); 
                } 
            } 
            typing(); 
            mensagensSistemaEl.scrollTop = mensagensSistemaEl.scrollHeight; 
        }

        function gerarRaridadePonderada() {
            const rand = Math.random() * 100;
            if (rand < 15) return 'diamante';   // 15%
            if (rand < 45) return 'ouro';       // 30%
            if (rand < 85) return 'prata';      // 40%
            return 'bronze';                     // 15%
        }
        
        function updateUI() {
             placarGeralEl.textContent = `🏆 PLACAR GERAL: CAIO ${gameState.placarGeral.caio} x ${gameState.placarGeral.ricardo} 🏆`;
             placarTemporadaEl.textContent = `⚔️ TEMPORADA ATUAL: CAIO ${gameState.temporadaAtual.caio} x ${gameState.temporadaAtual.ricardo} ⚔️ (MD7)`;
             ['caio', 'ricardo'].forEach(manager => {
                 const listEl = document.getElementById(`lista-${manager}`);
                 const elencoBox = document.getElementById(`elenco-${manager}`);
                 const headerEl = document.getElementById(`header-${manager}`);
                listEl.innerHTML = '';
                 gameState.elencos[manager].sort((a,b) => b.ovr - a.ovr).forEach(p => {
                     const li = document.createElement('li');
                     li.className = "player-card-item";
                     li.classList.add(`card-glow-${p.rarity}`); 
                     let playerInfoHTML = `<div class="player-card-info">
                            <span class="text-2xl">${rarityEmojis[p.rarity]}</span>
                            <div>
                                <p class="font-bold rarity-${p.rarity}">${p.nome}</p>
                                <p class="text-xs text-gray-400">${p.posGeral || 'N/A'} • ${p.clube}</p>
                            </div>
                        </div>
                        <div class="player-card-ovr rarity-${p.rarity}">
                            ${p.ovr}
                        </div>`;
                     li.innerHTML = playerInfoHTML;

                     if (p.suspendedFor > 0) {
                        li.classList.add('opacity-50');
                        const suspensionTag = document.createElement('span');
                        suspensionTag.className = "text-xs text-red-400 font-bold ml-2";
                        suspensionTag.textContent = `(${p.suspendedFor} JOGOS)`;
                        li.querySelector('.font-bold').appendChild(suspensionTag);
                     }
                     if(p.forcedPosition) {
                        li.querySelector('.text-xs').textContent = `${p.forcedPosition} • ${p.clube}`;
                        li.querySelector('.text-xs').classList.add('text-yellow-400');
                     }
                    listEl.appendChild(li);
                 });

                let clubName = gameState.timesBase[manager];
                let emoji = clubName ? getClubEmoji(clubName) : '⚽️';
                const isDoubleEmoji = [...emoji].length > 1 && !/\d/.test(emoji);

                const emojiContainerClasses = isDoubleEmoji 
                    ? "w-28 h-20 rounded-3xl" // Forma oval
                    : "w-20 h-20 rounded-full"; // Forma de círculo

                const emojiTextSize = isDoubleEmoji ? "text-2xl" : "text-3xl";

                let headerHTML = `
                    <div class="flex flex-col items-center justify-center gap-2 text-center">
                         <div class="flex items-center justify-center bg-gray-800 border-2 border-gray-600 mb-2 ${emojiContainerClasses}">
                            <span class="whitespace-nowrap ${emojiTextSize}">${emoji}</span>
                        </div>
                        <div class="flex items-center justify-between w-full">
                           <h2 class="text-2xl font-bold">${manager.toUpperCase()}</h2>
                           <span class="text-sm font-semibold py-1 px-3 rounded-full bg-gray-900/50 border border-gray-700">${gameState.elencos[manager].length}/11</span>
                        </div>
                        `;

                if (clubName) {
                    headerHTML += `<p class="text-gray-400 text-sm -mt-1 w-full text-left">${clubName}</p>`;
                } else {
                    headerHTML += `<p class="text-gray-400 text-sm -mt-1 w-full text-left">Aguardando time-base</p>`;
                }

                headerHTML += `</div>`;
                const taticaContainer = document.getElementById(`tatica-${manager}`);
                 taticaContainer.innerHTML = '';
                 if (gameState.taticas[manager]) {
                     const tatica = gameState.taticas[manager];
                     taticaContainer.innerHTML = `<button class="diretrizes-btn" onclick="mostrarDossieCompleto('${manager}')">Ver Diretrizes</button>`;
                 } else {
                     taticaContainer.innerHTML = `(Aguardando Tática)`;
                 }
                headerEl.innerHTML = headerHTML;
            });
         }
        
        function mostrarDossieCompleto(manager, taticaObj = null) {
            const tatica = taticaObj || gameState.taticas[manager];
            if (!tatica) return;

            const instrucoesGrid = Object.entries(tatica.instrucoes).map(([pos, inst]) => `
                <div class="dossier-card">
                    <dt class="dossier-card-title">${pos}</dt>
                    <dd class="text-sm">${inst}</dd>
                </div>
            `).join('');

            const bodyHTML = `
                <div class="space-y-4 max-h-[70vh] overflow-y-auto pr-4">
                    <div class="dossier-section">
                        <h3 class="font-bold text-lg mb-2 text-green-400">FILOSOFIA: "${tatica.filosofia}"</h3>
                        <p class="text-sm text-gray-300">${tatica.descricao}</p>
                        <p class="mt-2"><strong>FORMAÇÃO BASE:</strong> ${tatica.formacao}</p>
                    </div>

                    <div class="dossier-section">
                        <h3 class="font-bold text-lg mb-2 text-green-400">PARÂMETROS TÁTICOS (EA FC 26)</h3>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div class="dossier-card">
                                 <p class="dossier-card-title">Sem a Bola</p>
                                 <p><strong>Profundidade:</strong> ${tatica.semBola.profundidade}</p>
                            </div>
                            <div class="dossier-card">
                                <p class="dossier-card-title">Com a Bola</p>
                                <p><strong>Armação:</strong> ${tatica.comBola.armacao}</p>
                                <p><strong>Criação:</strong> ${tatica.comBola.criacao}</p>
                            </div>
                        </div>
                    </div>

                    <div class="dossier-section">
                        <h3 class="font-bold text-lg mb-2 text-green-400">FUNÇÕES INDIVIDUAIS</h3>
                        <dl class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-2 text-xs">
                            ${instrucoesGrid}
                        </dl>
                    </div>
                </div>
            `;
            showModal(`--- DOSSIÊ TÁTICO: ${manager.toUpperCase()} ---`, bodyHTML, [{ text: 'Fechar' }]);
        }
        
        function sortear(array, num) { 
            const shuffled = [...array].sort(() => 0.5 - Math.random()); 
            return shuffled.slice(0, num); 
        }

        function createDraftPool() { 
            gameState.draftPool = []; 
            for (const rarity in playersDB) { 
                playersDB[rarity].forEach(player => { 
                    if (!gameState.jogadoresUsados.includes(player.nome)) { 
                        gameState.draftPool.push(player); 
                    } 
                }); 
            } 
        }
        
        function iniciarNovaTemporada() {
             gameState.temporadaAtual = { caio: 0, ricardo: 0 };
             if (gameState.nextSeasonBonus) {
                const { manager, wins } = gameState.nextSeasonBonus;
                gameState.temporadaAtual[manager] = wins;
                typeMessage(`EFEITO DE PACTO: ${manager.toUpperCase()} começa a temporada com ${wins} vitória(s) de vantagem!`, true);
                delete gameState.nextSeasonBonus;
            }
            gameState.lossStreak = { caio: 0, ricardo: 0 };
             gameState.elencos = { caio: [], ricardo: [] };
             gameState.taticas = { caio: null, ricardo: null };
             gameState.timesBase = { caio: null, ricardo: null };
             gameState.rodadaDraft = 1;
             gameState.fase = 'TIME_BASE';
             gameState.effects = {};
            gameState.usedDialogues = { conflitoInterno: [], criseDeImprensa: [], dilemmas: [] };
            createDraftPool();
             updateUI();
             areaDeComandosEl.innerHTML = '';
             typeMessage("...NOVA TEMPORADA INICIADA. A disputa pelo título recomeça.", true);
             setTimeout(faseTimeBase, 1500);
         }
        
        function faseTimeBase() { typeMessage("REGISTRO DE LEGADO: Insiram os times-base para esta temporada.", true); setTimeout(() => mostrarModalTimeBase('CAIO'), 500); }
        
        function mostrarModalTimeBase(manager) { const bodyHTML = `<p>Manager ${manager}, por favor, insira o nome do time real que servirá como base para sua equipe nesta temporada.</p><input type="text" id="time-base-input" class="w-full bg-gray-900 border border-gray-700 rounded p-2 mt-4 text-white" placeholder="Ex: Liverpool">`; const buttons = [{ text: 'Confirmar', className: 'py-2 px-4 rounded-lg font-bold action-button btn-primary', action: () => { const input = document.getElementById('time-base-input'); if (input.value.trim()) { gameState.timesBase[manager.toLowerCase()] = input.value.trim(); typeMessage(`Time-base de ${manager.toUpperCase()} registrado: ${input.value.trim()}`); updateUI(); if (manager === 'CAIO') { setTimeout(() => mostrarModalTimeBase('RICARDO'), 500); } else { setTimeout(faseTatica, 1000); } } } }]; showModal(`REGISTRO DE TIME-BASE: ${manager.toUpperCase()}`, bodyHTML, buttons); }
        
        function faseTatica() { gameState.fase = 'TATICA'; typeMessage("FASE 1: A TÁTICA INICIAL. Gerando dossiês táticos...", true); const [taticaCaio, taticaRicardo] = sortear(taticasDB, 2); gameState.taticas = { caio: taticaCaio, ricardo: taticaRicardo }; updateUI(); setTimeout(() => { typeMessage("Dossiês entregues. Preparem-se para a FASE 2: DRAFT.", true); gameState.fase = 'DRAFT'; gameState.turno = Math.random() < 0.5 ? 'caio' : 'ricardo'; setTimeout(proximoTurnoDraft, 2000); }, 1500); }
        
        function gerarOpcoesParaManager() {
             const { manager, raridade } = gameState.pendingDraft;
             let opcoesDisponiveis = gameState.draftPool.filter(p => p.rarity === raridade);
             
             if (opcoesDisponiveis.length < 3) {
                 typeMessage("ALERTA DE SISTEMA: Baixo número de atletas disponíveis. Sorteando de todos os jogadores restantes.");
                 opcoesDisponiveis = gameState.draftPool;
             }
             const opcoes = sortear(opcoesDisponiveis, 3);
             
             areaDeComandosEl.innerHTML = '';
             areaDeEscolhaEl.innerHTML = '';

             if (opcoes.length === 0) {
                 typeMessage("FALHA CRÍTICA: Nenhum jogador encontrado no banco de dados para esta rodada. Pulando turno...");
                 gameState.turno = gameState.turno === 'caio' ? 'ricardo' : 'caio';
                 setTimeout(continuarFluxoAposEvento, 2000);
                 return;
             }

             opcoes.forEach((p, i) => {
                 const btn = document.createElement('button');
                 btn.className = "player-choice-btn p-4 rounded-lg text-left w-full flex flex-col";
                 btn.innerHTML = `
                    <div class="flex justify-between items-start mb-2">
                        <span class="text-lg font-bold">${p.nome}</span>
                        <div class="flex items-center gap-2">
                             <span class="text-2xl">${rarityEmojis[p.rarity]}</span>
                        </div>
                    </div>
                    <p class="text-sm text-gray-400">${p.clube}</p>
                    <p class="text-xs text-gray-500 mt-2">PlayStyles: ${p.playstyles ? p.playstyles.join(', ') : 'N/A'}</p>
                 `;
                 btn.onclick = () => handleEscolha(manager, p);
                 areaDeEscolhaEl.appendChild(btn);
             });
         }
        
        function handleEscolha(manager, player) {
             gameState.elencos[manager].push(player);
             const playerIndex = gameState.draftPool.findIndex(p => p.nome === player.nome);
             if (playerIndex > -1) { gameState.draftPool.splice(playerIndex, 1); }
             const managerEffects = gameState.effects[manager] || {};
            if (managerEffects.doubleDraft > 0) {
                const bonusPlayerRarity = player.rarity;
                const bonusPool = gameState.draftPool.filter(p => p.rarity === bonusPlayerRarity);
                if (bonusPool.length > 0) {
                    const bonusPlayer = sortear(bonusPool, 1)[0];
                    gameState.elencos[manager].push(bonusPlayer);
                    const bonusPlayerIndex = gameState.draftPool.findIndex(p => p.nome === bonusPlayer.nome);
                    if (bonusPlayerIndex > -1) gameState.draftPool.splice(bonusPlayerIndex, 1);
                    typeMessage(`PACOTE EM DOBRO! 🎁 ${manager.toUpperCase()} também recebe ${bonusPlayer.nome}!`);
                }
                managerEffects.doubleDraft--;
            }
            areaDeEscolhaEl.innerHTML = '';
             areaDeComandosEl.innerHTML = '';
             updateUI();
             typeMessage(`Uma escolha audaciosa! 🎯 ${player.nome} se junta à equipe de ${manager.toUpperCase()}!`);
             typeMessage(`"${sortear(frasesDeEfeito, 1)[0]}"`, true);
             gameState.turno = manager === 'caio' ? 'ricardo' : 'caio';
             
             const proximoManager = gameState.turno;
             if (!triggerRandomEvent('post-draft', proximoManager)) {
                 setTimeout(continuarFluxoAposEvento, 2000);
             }
         }
        
        function handleResultadoPartida(vencedorComando) {
             if (gameState.fase !== 'PARTIDA') return;
             areaDeComandosEl.innerHTML = '';
             const vencedor = vencedorComando === 'vc' ? 'caio' : 'ricardo';
             const perdedor = vencedor === 'caio' ? 'ricardo' : 'caio';
             
            gameState.elencos.caio.forEach(p => { if (p.suspendedFor > 0) p.suspendedFor--; });
            gameState.elencos.ricardo.forEach(p => { if (p.suspendedFor > 0) p.suspendedFor--; });

            gameState.temporadaAtual[vencedor]++;
             gameState.lossStreak[vencedor] = 0;
             gameState.lossStreak[perdedor]++;
             updateUI();
             const totalGamesPlayed = gameState.temporadaAtual.caio + gameState.temporadaAtual.ricardo;

            if (gameState.temporadaAtual[vencedor] >= 7) {
                 gameState.fase = 'FIM_TEMPORADA';
                 gameState.placarGeral[vencedor]++;
                 gameState.historico.push({ campeao: vencedor, placar: `${gameState.temporadaAtual.caio}x${gameState.temporadaAtual.ricardo}`, elencoCampeao: [...gameState.elencos[vencedor]], timeBaseCampeao: gameState.timesBase[vencedor] });
                 
                 gameState.jogadoresUsados = [...new Set([...gameState.jogadoresUsados, ...gameState.elencos[vencedor].map(p => p.nome)])];
                 updateUI();
                 
                const championModalBody = `
                    <div class="text-center">
                        <p class="text-2xl mb-4">🏆 O CAMPEÃO DA TEMPORADA É... <strong>${vencedor.toUpperCase()}</strong>! 🏆</p>
                        <p class="text-4xl md:text-5xl font-bold text-yellow-300 my-6" style="text-shadow: 0 0 10px #ffd700;">
                            PARABÉNS, TU É FODA!<br>O REI DA COLINA!
                        </p>
                    </div>`;
                
                showModal(
                    '👑 TEMOS UM CAMPEÃO! 👑',
                    championModalBody,
                    [{ 
                        text: 'Ir para o Menu', 
                        action: () => {
                            setTimeout(() => {
                                jogoContainerEl.classList.add('hidden');
                                menuPrincipalEl.classList.remove('hidden');
                            }, 500);
                        }
                    }],
                    'gold'
                );

             } else {
                 gameState.fase = 'DRAFT';
                typeMessage(`Placar atualizado!`);
                 if (totalGamesPlayed >= 2 && gameState.lossStreak[perdedor] >= 3) {
                    triggerConflictEvent(perdedor);
                } else if (totalGamesPlayed >= 2 && gameState.lossStreak[perdedor] === 2) {
                    triggerPressCrisisEvent(perdedor);
                }
                else {
                    typeMessage(`Próxima rodada de reforços se inicia...`);
                    setTimeout(proximoTurnoDraft, 2000);
                }
            }
         }

        function handleRefusalConsequences(manager, player) {
            const rand = Math.random();
            const elenco = gameState.elencos[manager];
            const playerIndex = elenco.findIndex(p => p.nome === player.nome);
            if (playerIndex === -1) { 
                setTimeout(proximoTurnoDraft, 2000);
                return;
            }
            
            let consequenceTitle = `🔥 CONSEQUÊNCIA [${manager.toUpperCase()}] 🔥`;
            let consequenceMessage = "";

            if (rand < 0.40) {
                 const oldPosition = player.originalPosition || player.posGeral;
                let newPosition = 'Defensor';
                if(oldPosition === 'Defensor' || oldPosition === 'Goleiro') newPosition = 'Atacante';
                
                elenco[playerIndex].posGeral = newPosition;
                elenco[playerIndex].forcedPosition = true;
                elenco[playerIndex].originalPosition = oldPosition;
                consequenceMessage = `${player.nome} está furioso! "Ah é? Então vou mostrar como se joga em outra posição!". Ele foi movido para a ${newPosition} por tempo indeterminado!`;
                            
            } else if (rand < 0.70) {
                 const suspensionMatches = Math.floor(Math.random() * 2) + 4;
                 elenco[playerIndex].suspendedFor = suspensionMatches;
                                
                consequenceMessage = `${player.nome} se recusa a treinar! Ele está SUSPENSO por ${suspensionMatches} partidas por insubordinação!`;
            } else if (rand < 0.95) {
                 const removedPlayer = elenco.splice(playerIndex, 1)[0];
                consequenceMessage = `RUPTURA TOTAL! ${removedPlayer.nome} rescindiu o contrato e deixou o clube! A diretoria correu para achar um substituto...`;
                
                const lowerRarities = { 'diamante': 'ouro', 'ouro': 'prata', 'prata': 'bronze', 'bronze': 'bronze' };
                const targetRarity = lowerRarities[removedPlayer.rarity];
                const replacementPool = gameState.draftPool.filter(p => p.rarity === targetRarity);
                if (replacementPool.length > 0) {
                    const replacement = sortear(replacementPool, 1)[0];
                    elenco.push(replacement);
                    const replacementIndex = gameState.draftPool.findIndex(p => p.nome === replacement.nome);
                    if(replacementIndex > -1) gameState.draftPool.splice(replacementIndex, 1);
                    consequenceMessage += ` e contratou ${replacement.nome} ${rarityEmojis[replacement.rarity]} para a vaga. Um downgrade claro.`;
                } else {
                    consequenceMessage += ` mas não encontrou ninguém disponível no mercado! A vaga está aberta.`;
                }
            } else {
                 const removedPlayer = elenco.splice(playerIndex, 1)[0];
                consequenceMessage = `RUPTURA TOTAL! ${removedPlayer.nome} rescindiu o contrato e deixou o clube! A diretoria usou a oportunidade para uma jogada de mestre...`;
                const higherRarities = { 'diamante': 'diamante', 'ouro': 'diamante', 'prata': 'ouro', 'bronze': 'prata' };
                const targetRarity = higherRarities[removedPlayer.rarity];
                const replacementPool = gameState.draftPool.filter(p => p.rarity === targetRarity);
                
                if (replacementPool.length > 0) {
                    const replacement = sortear(replacementPool, 1)[0];
                    elenco.push(replacement);
                    const replacementIndex = gameState.draftPool.findIndex(p => p.nome === replacement.nome);
                    if(replacementIndex > -1) gameState.draftPool.splice(replacementIndex, 1);
                    consequenceMessage += ` e contratou ${replacement.nome} ${rarityEmojis[replacement.rarity]}! Um substituto de peso para a vaga!`;
                } else {
                    consequenceMessage += ` mas não conseguiu fechar o negócio dos sonhos. A vaga está aberta.`;
                }
            }
            
            showModal(consequenceTitle, `<p>${consequenceMessage}</p>`, [{ text: 'Continuar...', action: () => {
                updateUI();
                setTimeout(proximoTurnoDraft, 2000);
            }}], 'pact');
        }

        function triggerConflictEvent(manager) {
            const elenco = gameState.elencos[manager];
            const jogadoresElite = elenco.filter(p => p.rarity === 'diamante' || p.rarity === 'ouro');
            if (jogadoresElite.length === 0) {
                 typeMessage(`O vestiário de ${manager.toUpperCase()} está frustrado, mas silencioso. Próxima rodada de reforços se inicia...`);
                setTimeout(proximoTurnoDraft, 2000);
                return;
            }
            
            const jogadorRevoltado = sortear(jogadoresElite, 1)[0];
            const posicao = jogadorRevoltado.posGeral;
            let poolDeReclamacoes = eventsDB.conflitoInterno[posicao] || [...eventsDB.conflitoInterno.Atacante, ...eventsDB.conflitoInterno.Defensor];
            
            let availableDialogues = poolDeReclamacoes.filter(d => !gameState.usedDialogues.conflitoInterno.includes(d.dialogue));
            
            if (availableDialogues.length === 0) {
                gameState.usedDialogues.conflitoInterno = [];
                availableDialogues = poolDeReclamacoes;
                typeMessage("...Recalibrando matriz de eventos de conflito...", true);
            }

            const reclamacao = sortear(availableDialogues, 1)[0];
            gameState.usedDialogues.conflitoInterno.push(reclamacao.dialogue);

            const finalTitle = `${reclamacao.title} [${manager.toUpperCase()}]`;
            const finalDialogue = `<p class="mb-4">A sequência de derrotas pesou no vestiário. <strong>${jogadorRevoltado.nome} ${rarityEmojis[jogadorRevoltado.rarity]}</strong> te puxa para um canto e desabafa:</p><p class="text-red-400 italic">"${reclamacao.dialogue}"</p>`;
            
            const buttons = [
                {
                    text: 'Aceitar Exigência',
                    className: 'py-2 px-4 action-button btn-secondary',
                    action: () => {
                         if (reclamacao.consequence && reclamacao.consequence.type === 'CHANGE_FORMATION') {
                            const possibleTatics = taticasDB.filter(t => reclamacao.consequence.formations.includes(t.formacao));
                            if (possibleTatics.length > 0) {
                                const newTatica = sortear(possibleTatics, 1)[0];
                                const oldTatica = gameState.taticas[manager];
                                gameState.taticas[manager] = newTatica;
                                
                                const changeTitle = '📣 MUDANÇA TÁTICA! 📣';
                                const changeBody = `
                                    <p>Para atender a demanda de <strong>${jogadorRevoltado.nome}</strong>, você mudou a estratégia do time!</p>
                                    <div class="flex justify-center items-center text-3xl my-4 gap-4">
                                        <span class="opacity-50">${oldTatica.formacao}</span>
                                        <span class="text-green-400 font-bold">➡️</span>
                                        <span>${newTatica.formacao}</span>
                                    </div>
                                    <p class="text-sm text-center">A nova filosofia é: <strong>"${newTatica.filosofia}"</strong>.</p>
                                `;
                                showModal(changeTitle, changeBody, [{ text: 'Confirmado', action: () => setTimeout(proximoTurnoDraft, 2000) }]);
                            }
                        } else {
                            typeMessage(`Você cedeu às exigências de ${jogadorRevoltado.nome}. A crise foi contida... por enquanto.`);
                            setTimeout(proximoTurnoDraft, 3000);
                        }
                        updateUI();
                    }
                },
                {
                    text: 'Recusar Exigência',
                    className: 'py-2 px-4 action-button btn-danger',
                    action: () => {
                        typeMessage(`Você peitou sua estrela! ${jogadorRevoltado.nome} não aceitou bem a recusa...`, true);
                        handleRefusalConsequences(manager, jogadorRevoltado);
                    }
                }
            ];
            showModal(finalTitle, finalDialogue, buttons, 'pact');
        }
        
        function triggerPressCrisisEvent(manager) {
            const elenco = gameState.elencos[manager];
            if (elenco.length === 0) { 
                 setTimeout(proximoTurnoDraft, 2000); 
                 return;
            }
            
            let availableCrises = eventsDB.criseDeImprensa.filter(c => !gameState.usedDialogues.criseDeImprensa.includes(c.description));
            if(availableCrises.length === 0) {
                gameState.usedDialogues.criseDeImprensa = [];
                availableCrises = eventsDB.criseDeImprensa;
                typeMessage("...Recalibrando matriz de eventos de imprensa...", true);
            }
            const crise = sortear(availableCrises, 1)[0];
            gameState.usedDialogues.criseDeImprensa.push(crise.description);
            
            const jogadoresAlvo = elenco.filter(p => p.posGeral === crise.posGeral);
            const jogadorAlvo = jogadoresAlvo.length > 0 ? sortear(jogadoresAlvo, 1)[0] : sortear(elenco, 1)[0];
            
            const finalTitle = `${crise.title} [${manager.toUpperCase()}]`;
            const finalDescription = crise.description.replace('{playerName}', `<strong>${jogadorAlvo.nome}</strong>`);
            
             showModal(finalTitle, `<p>${finalDescription}</p>`, [{ text: 'Continuar...', action: () => {
                typeMessage(`A imprensa não perdoa a má fase. Próxima rodada de reforços se inicia...`);
                setTimeout(proximoTurnoDraft, 2000);
            }}], 'pact');
        }
        
        function showModal(title, bodyHTML, buttons = [], rarityOrStyle = null, customClass = '') {
             const modalContent = modalEl.querySelector('.modal-content');
            modalContent.className = 'modal-content relative w-full max-w-2xl p-6 rounded-lg overflow-y-auto'; // Reset
            
            if (rarityOrStyle) {
                modalContent.classList.add(`modal-rarity-${rarityOrStyle}`);
            }
            if (customClass) modalContent.classList.add(customClass);
            
            modalTitleEl.textContent = title;
             modalBodyEl.innerHTML = bodyHTML;

            const existingButtons = modalBodyEl.querySelector('.modal-buttons');
            if (existingButtons) existingButtons.remove();

            if (buttons.length > 0) {
                const buttonContainer = document.createElement('div');
                buttonContainer.className = 'modal-buttons mt-6 flex justify-center gap-4'; // Alterado para 'justify-center' e gap ajustado
                buttons.forEach(b => {
                    const btnEl = document.createElement('button');
                    btnEl.textContent = b.text;
                    btnEl.className = b.className || 'py-2 px-6 action-button btn-primary'; // CORREÇÃO: Aumentado o padding horizontal (px-6)
                    btnEl.onclick = () => { 
                        if (!b.keepOpen) hideModal(); 
                        if (b.action) b.action(); 
                    };
                    buttonContainer.appendChild(btnEl);
                });
                modalBodyEl.appendChild(buttonContainer);
            }
            modalEl.classList.remove('hidden');
            modalEl.classList.add('flex');
         }
        
        function hideModal() { modalEl.classList.add('hidden'); modalEl.classList.remove('flex'); }

        function applyConsequence(consequence, manager) {
            const opponent = manager === 'caio' ? 'ricardo' : 'caio';
            let continuationHandled = false; // Variável para controlar o fluxo

            const applyEffect = (targetManager, effect, value) => {
                if (!gameState.effects[targetManager]) gameState.effects[targetManager] = {};
                gameState.effects[targetManager][effect] = (gameState.effects[targetManager][effect] || 0) + value;
            };

            const targets = {
                self: manager,
                opponent: opponent,
                loser: gameState.temporadaAtual.caio > gameState.temporadaAtual.ricardo ? 'ricardo' : 'caio',
            };

            consequence.targets.forEach(targetKey => {
                const targetManager = targets[targetKey];
                if (!targetManager) return;

                switch (consequence.type) {
                    case 'DOUBLE_DRAFT':
                        applyEffect(targetManager, 'doubleDraft', 1);
                        break;
                    case 'SABOTAGE':
                        applyEffect(targetManager, 'downgradeRarity', 1);
                        break;
                    case 'SACRIFICE_FOR_UPGRADE':
                        const elenco = gameState.elencos[targetManager];
                        if (elenco.length > 0) {
                            elenco.sort((a,b) => a.ovr - b.ovr);
                            const sacrificedPlayer = elenco.shift();
                            typeMessage(`SACRIFÍCIO FEITO! ${sacrificedPlayer.nome} foi demitido para abrir espaço para a nova era.`);
                            if(!gameState.effects[targetManager]) gameState.effects[targetManager] = {};
                            gameState.effects[targetManager].guaranteedRarity = { rarities: ['ouro', 'diamante'], count: 1 };
                        }
                        updateUI();
                        break;
                    case 'PACT_FOR_DIAMOND':
                        continuationHandled = true; // Este evento tem seu próprio fluxo com um segundo modal
                        const jogadoresEmUsoNomes = [
                            ...gameState.elencos.caio.map(p => p.nome),
                            ...gameState.elencos.ricardo.map(p => p.nome)
                        ];
                        const diamondPool = playersDB.diamante.filter(p => !jogadoresEmUsoNomes.includes(p.nome));

                        if (diamondPool.length > 0) {
                            const diamondPlayer = sortear(diamondPool, 1)[0];
                            gameState.elencos[targetManager].push(diamondPlayer);
                            
                            const playerIndexInDraft = gameState.draftPool.findIndex(p => p.nome === diamondPlayer.nome);
                            if (playerIndexInDraft > -1) gameState.draftPool.splice(playerIndexInDraft, 1);
                            
                            const pactBody = `
                                <div class="text-center">
                                    <p class="text-6xl mb-4 animate-pulse">😈</p>
                                    <p>O pacto foi selado! Em troca de 2 vitórias para ${opponent.toUpperCase()} na próxima temporada, você recebe:</p>
                                     <div class="my-6 p-4 rounded-lg bg-black/20 border border-red-500/50">
                                        <p class="text-4xl font-bold rarity-diamond" style="text-shadow: 0 0 10px #b9f2ff;">${diamondPlayer.nome}</p>
                                    </div>
                                </div>
                            `;
                            showModal('PACTO REALIZADO!', pactBody, [{ text: 'Aceitar Consequências', action: () => {
                                updateUI();
                                setTimeout(continuarFluxoAposEvento, 1500); // Continua o fluxo do jogo após o modal.
                            } }], 'pact');

                            gameState.nextSeasonBonus = { manager: opponent, wins: 2 };
                        } else {
                            const fallbackBody = `
                                <div class="text-center">
                                     <p class="text-6xl mb-4">💨</p>
                                     <p>As entidades tentaram selar o pacto, mas não encontraram uma alma valiosa o suficiente (nenhum jogador diamante novo está disponível). O pacto falhou e nada acontece.</p>
                                </div>
                            `;
                            showModal('PACTO FALHOU!', fallbackBody, [{ text: 'Continuar', action: () => {
                                setTimeout(continuarFluxoAposEvento, 1500); // Continua o fluxo do jogo após o modal.
                            } }], 'pact');
                        }
                        break;
                    case 'BONUS_PLAYER_LOSER':
                        const loserElenco = gameState.elencos[targetManager];
                        if(loserElenco && loserElenco.length < 11) {
                            const bonusPlayer = sortear(gameState.draftPool, 1)[0];
                            if(bonusPlayer) {
                                loserElenco.push(bonusPlayer);
                                const playerIndex = gameState.draftPool.findIndex(p => p.nome === bonusPlayer.nome);
                                if (playerIndex > -1) gameState.draftPool.splice(playerIndex, 1);
                                typeMessage(`BÔNUS DE ESTABILIZAÇÃO! O time de ${targetManager.toUpperCase()} recebe ${bonusPlayer.nome} ${rarityEmojis[bonusPlayer.rarity]}!`);
                            }
                        }
                        updateUI();
                        break;
                }
            });
            return continuationHandled;
        }

        function triggerRandomEvent(eventPhase, manager) {
            // Chance de 60% de disparar um evento (40% de não fazer nada).
            if (Math.random() > 0.6) {
                return false;
            }
            
            let eventPool = [...eventsDB.anomalias, ...eventsDB.dilemas];
            let availableEvents = eventPool.filter(e => !gameState.usedDialogues.dilemmas.includes(e.description));

            if (availableEvents.length === 0) {
                gameState.usedDialogues.dilemmas = []; // Reset if all have been used
                availableEvents = eventPool;
            }
            
            if (availableEvents.length === 0) return false;

            const event = sortear(availableEvents, 1)[0];

            // Adicionado tratamento de erro para caso o sorteio não retorne um evento.
            if (!event) return false;
            
            if (event.choices) { // Only track dilemmas to prevent repetition
                 gameState.usedDialogues.dilemmas.push(event.description);
            }
            
            if (event.choices) {
                const buttons = event.choices.map(choice => {
                    // CORREÇÃO: Adicionado padding (py-2 px-6) e classes base para garantir a estética dos botões.
                    const baseClasses = 'py-2 px-6 action-button';
                    let specificClass = 'btn-secondary';

                    if (choice.text.toLowerCase().includes('sabotar') || choice.text.toLowerCase().includes('sacrificar')) {
                        specificClass = 'btn-danger';
                    } else if (choice.text.toLowerCase().includes('aceitar pacto')) {
                        specificClass = 'btn-pact';
                    }

                    return {
                        text: choice.text,
                        className: `${baseClasses} ${specificClass}`,
                        action: () => {
                            let continuationHandledByConsequence = false;
                            if (choice.consequence && choice.consequence.type !== 'NONE') {
                                continuationHandledByConsequence = applyConsequence(choice.consequence, manager);
                            }

                            // Se a consequência não gerou um novo fluxo (com um novo modal), continue o jogo normalmente.
                            if (!continuationHandledByConsequence) {
                                if (eventPhase === 'post-draft') {
                                    setTimeout(continuarFluxoAposEvento, 1500);
                                } else if (eventPhase === 'pre-partida') {
                                    typeMessage("Após a partida, informem o vencedor.");
                                    renderCommandButtons();
                                }
                            }
                        }
                    };
                });
                showModal(`${event.title} [${manager.toUpperCase()}]`, `<p>${event.description}</p>`, buttons, 'pact');
            } 
            else {
                if(event.consequence){
                    applyConsequence(event.consequence, manager);
                }
                showModal(`${event.title} [${manager.toUpperCase()}]`, `<p>${event.description}</p>`, [{
                    text: 'Entendido',
                    action: () => {
                        // CORREÇÃO: Lógica de fluxo do jogo simplificada para evitar travamentos.
                         if (eventPhase === 'post-draft') {
                            setTimeout(continuarFluxoAposEvento, 1500);
                        } else if (eventPhase === 'pre-partida') {
                            typeMessage("Após a partida, informem o vencedor.");
                            renderCommandButtons();
                        }
                    }
                }]);
            }

            return true;
        }
        
        function renderCommandButtons() { 
            areaDeComandosEl.innerHTML = ''; 
            areaDeEscolhaEl.innerHTML = ''; 
            areaDeDecisaoEl.innerHTML = ''; 
            let btn; 
            if (gameState.fase === 'DRAFT' && gameState.turno) { 
                btn = document.createElement('button'); 
                btn.textContent = `GERAR OPÇÕES PARA ${gameState.turno.toUpperCase()}`; 
                btn.className = 'w-full py-3 px-4 action-button btn-primary'; 
                btn.onclick = () => { 
                    btn.disabled = true; 
                    btn.textContent = 'PROCESSANDO...'; 
                    gerarOpcoesParaManager(); 
                }; 
                areaDeComandosEl.appendChild(btn); 
            } else if (gameState.fase === 'PARTIDA') { 
                const container = document.createElement('div'); 
                container.className = 'grid grid-cols-1 md:grid-cols-2 gap-4'; 
                const btnCaio = document.createElement('button'); 
                btnCaio.textContent = 'VITÓRIA DO CAIO'; 
                btnCaio.className = 'py-3 px-4 bg-blue-600 hover:bg-blue-700 font-bold action-button'; 
                btnCaio.onclick = () => handleResultadoPartida('vc'); 
                const btnRicardo = document.createElement('button'); 
                btnRicardo.textContent = 'VITÓRIA DO RICARDO'; 
                btnRicardo.className = 'py-3 px-4 bg-red-600 hover:bg-red-700 font-bold action-button'; 
                btnRicardo.onclick = () => handleResultadoPartida('vr'); 
                container.appendChild(btnCaio); 
                container.appendChild(btnRicardo); 
                areaDeComandosEl.appendChild(container); 
            } 
        }

        function proceedWithDraft(manager, raridade) {
            gameState.pendingDraft = { manager, raridade };
            typeMessage(`--- RODADA DE DRAFT ${Math.ceil(gameState.rodadaDraft / 2)} ⚽ ---`);
            typeMessage(`A vez é de... ${manager.toUpperCase()}! Seu pacote é... ${raridade.toUpperCase()} ${rarityEmojis[raridade]}!`);
            renderCommandButtons();
        }
        
        function proximoTurnoDraft() {
            const manager = gameState.turno;
            const managerEffects = gameState.effects[manager] || {};
            let originalRarity = gerarRaridadePonderada();
            let finalRarity = originalRarity;
            let effectTriggered = false;

            if (managerEffects.downgradeRarity > 0) {
                const currentIndex = rarities.indexOf(originalRarity);
                if (currentIndex > 0) {
                    finalRarity = rarities[currentIndex - 1];
                    showModal(
                        '💣 SABOTAGEM DETECTADA! 💣',
                        `<p class="text-center text-lg">O pacote de ${manager.toUpperCase()} foi corrompido!</p>
                         <div class="flex justify-center items-center text-5xl my-4 gap-4">
                            <span class="opacity-50">${rarityEmojis[originalRarity]}</span>
                            <span class="text-red-500 font-bold">➡️</span>
                            <span>${rarityEmojis[finalRarity]}</span>
                         </div>`,
                        [{ text: 'Continuar...', action: () => proceedWithDraft(manager, finalRarity) }],
                        'pact'
                    );
                    managerEffects.downgradeRarity--;
                    effectTriggered = true;
                }
            } else if (managerEffects.guaranteedRarity && managerEffects.guaranteedRarity.count > 0) {
                finalRarity = sortear(managerEffects.guaranteedRarity.rarities, 1)[0];
                showModal(
                    '✨ PACOTE DE ELITE! ✨',
                    `<p class="text-center text-lg">O sacrifício de ${manager.toUpperCase()} foi recompensado!</p>
                     <div class="flex justify-center items-center text-5xl my-4">
                        <span>${rarityEmojis[finalRarity]}</span>
                     </div>`,
                    [{ text: 'Receber Jogadores', action: () => proceedWithDraft(manager, finalRarity) }],
                    finalRarity
                );
                managerEffects.guaranteedRarity.count--;
                effectTriggered = true;
            }

            if (!effectTriggered) {
                proceedWithDraft(manager, finalRarity);
            }
         }
        
        function continuarFluxoAposEvento() { 
            if (gameState.rodadaDraft % 2 !== 0) { 
                gameState.rodadaDraft++; 
                setTimeout(proximoTurnoDraft, 2000); 
            } else {
                gameState.rodadaDraft++; 
                setTimeout(iniciarFasePartida, 2000); 
            } 
        }
        
        function iniciarFasePartida() {
             gameState.fase = 'PARTIDA';
             typeMessage("---------------------------------------------");
             typeMessage("Ambos os managers receberam reforços. É hora do confronto!");
             
            const weatherEvent = sortear(eventsDB.clima, 1)[0];
            const weatherButtons = [{ text: 'Avançar...', action: () => { 
                const targetManager = Math.random() < 0.5 ? 'caio' : 'ricardo'; 
                if (!triggerRandomEvent('pre-partida', targetManager)) { 
                    typeMessage("Nenhum evento adicional detectado."); 
                    typeMessage("Após a partida, informem o vencedor."); 
                    renderCommandButtons(); 
                } 
            }}];
            showModal(weatherEvent.title, `<p>${weatherEvent.description}</p>`, weatherButtons);
        }

        function renderizarHistorico() {
            historicoContentEl.innerHTML = '';
            if (gameState.historico.length === 0) {
                historicoContentEl.innerHTML = '<p class="text-center text-gray-400">Nenhuma temporada foi concluída ainda. O Hall dos Campeões aguarda seu primeiro herói!</p>';
                return;
            }

            gameState.historico.forEach((temporada, index) => {
                const elencoHTML = temporada.elencoCampeao.map(p => `<li>${p.nome} <span class="rarity-${p.rarity}">${rarityEmojis[p.rarity]}</span> (${p.ovr})</li>`).join('');
                
                const card = document.createElement('div');
                card.className = 'card-historico p-6 rounded-lg';
                card.innerHTML = `
                    <h2 class="text-2xl font-bold text-green-400 mb-2">Temporada ${index + 1} - Campeão: ${temporada.campeao.toUpperCase()}</h2>
                    <p class="text-lg mb-1"><strong>Placar Final:</strong> ${temporada.placar}</p>
                    <p class="text-md text-gray-300 mb-4"><strong>Time-Base:</strong> ${temporada.timeBaseCampeao || 'Não registrado'}</p>
                    <div class="border-t border-gray-700 pt-4">
                        <h3 class="font-bold text-xl mb-2">Elenco Campeão:</h3>
                        <ul class="list-disc list-inside columns-2 gap-x-8">${elencoHTML}</ul>
                    </div>
                `;
                historicoContentEl.appendChild(card);
            });
        }

        function openScoreEditor() {
            const bodyHTML = `
                <div class="space-y-4">
                    <div>
                        <h3 class="font-bold text-lg mb-2 text-green-400">Placar da Temporada</h3>
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label for="score-caio-temp" class="block mb-1">Placar Caio:</label>
                                <input type="number" id="score-caio-temp" value="${gameState.temporadaAtual.caio}" class="w-full bg-gray-900 border border-gray-700 rounded p-2 text-white">
                            </div>
                            <div>
                                <label for="score-ricardo-temp" class="block mb-1">Placar Ricardo:</label>
                                <input type="number" id="score-ricardo-temp" value="${gameState.temporadaAtual.ricardo}" class="w-full bg-gray-900 border border-gray-700 rounded p-2 text-white">
                            </div>
                        </div>
                    </div>
                    <div>
                        <h3 class="font-bold text-lg mb-2 text-green-400">Placar Geral</h3>
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label for="score-caio-geral" class="block mb-1">Placar Caio:</label>
                                <input type="number" id="score-caio-geral" value="${gameState.placarGeral.caio}" class="w-full bg-gray-900 border border-gray-700 rounded p-2 text-white">
                            </div>
                            <div>
                                <label for="score-ricardo-geral" class="block mb-1">Placar Ricardo:</label>
                                <input type="number" id="score-ricardo-geral" value="${gameState.placarGeral.ricardo}" class="w-full bg-gray-900 border border-gray-700 rounded p-2 text-white">
                            </div>
                        </div>
                    </div>
                </div>
            `;
            const buttons = [{
                text: 'Salvar Alterações',
                action: () => {
                    const newScoreCaioTemp = parseInt(document.getElementById('score-caio-temp').value, 10);
                    const newScoreRicardoTemp = parseInt(document.getElementById('score-ricardo-temp').value, 10);
                    const newScoreCaioGeral = parseInt(document.getElementById('score-caio-geral').value, 10);
                    const newScoreRicardoGeral = parseInt(document.getElementById('score-ricardo-geral').value, 10);

                    if (!isNaN(newScoreCaioTemp) && !isNaN(newScoreRicardoTemp)) {
                        gameState.temporadaAtual.caio = newScoreCaioTemp;
                        gameState.temporadaAtual.ricardo = newScoreRicardoTemp;
                    }
                     if (!isNaN(newScoreCaioGeral) && !isNaN(newScoreRicardoGeral)) {
                        gameState.placarGeral.caio = newScoreCaioGeral;
                        gameState.placarGeral.ricardo = newScoreRicardoGeral;
                    }

                    updateUI(); 
                    if(jogoContainerEl.classList.contains('hidden') === false){
                         typeMessage('Placares ajustados manualmente pelo administrador.');
                    }
                }
            }];
            showModal('Editar Placares', bodyHTML, buttons);
        }
        
        // --- MODO JOGO RÁPIDO ---
        let timesJogoRapido = { caio: [], ricardo: [] };

        function mostrarDossieCompletoJogoRapido(manager) {
            const tatica = jogoRapidoState.taticas[manager];
            if (!tatica) return;
            // Reutiliza a função principal de exibição do dossiê
            mostrarDossieCompleto(manager, tatica);
        }

        function resetJogoRapidoUI() {
            const placeholder = document.getElementById('central-animation-placeholder');
            const botoesVitoria = document.getElementById('botoes-vitoria-container');

            // Reseta o estado
            jogoRapidoState.placar = { caio: 0, ricardo: 0 };
            timesJogoRapido = { caio: [], ricardo: [] };
            jogoRapidoState.taticas = { caio: null, ricardo: null };

            // Reseta a UI
            if (botoesVitoria) {
                botoesVitoria.classList.add('hidden');
            }
            if (placeholder) {
                placeholder.classList.remove('hidden', 'opacity-0', 'scale-75');
            }

            renderizarTimesJogoRapido({ isInitial: true }); // Limpa as listas de jogadores
        }


        function renderizarTimesJogoRapido(options = { isInitial: false, animate: false }) {
             // Atualiza o placar do jogo rápido
            const placarJogoRapidoEl = document.getElementById('placar-jogo-rapido');
            if (placarJogoRapidoEl) {
                placarJogoRapidoEl.textContent = `CAIO ${jogoRapidoState.placar.caio} x ${jogoRapidoState.placar.ricardo} RICARDO`;
            }

            ['caio', 'ricardo'].forEach(manager => {
                const listEl = document.getElementById(`lista-${manager}-rapido`);
                const headerEl = document.getElementById(`header-${manager}-rapido`);

                if (!listEl || !headerEl) return;

                // Renderiza o cabeçalho com o botão de diretrizes
                headerEl.innerHTML = `
                    <div class="flex items-center justify-between w-full">
                        <h2 class="text-3xl font-bold">${manager.toUpperCase()}</h2>
                        ${!options.isInitial && jogoRapidoState.taticas[manager] ? `<button class="diretrizes-btn text-xs" onclick="mostrarDossieCompletoJogoRapido('${manager}')">Ver Diretrizes</button>` : ''}
                    </div>
                `;

                listEl.innerHTML = '';
                if(options.isInitial) return; 

                // Renderiza a lista de jogadores em duas colunas
                const sortedPlayers = timesJogoRapido[manager].sort((a, b) => b.ovr - a.ovr);
                for (let i = 0; i < sortedPlayers.length; i += 2) {
                    const player1 = sortedPlayers[i];
                    const player2 = sortedPlayers[i + 1];

                    const row = document.createElement('div');
                    row.className = "grid grid-cols-2 gap-2";
                    if (options.animate) {
                        row.classList.add('card-entry-animation');
                        row.style.animationDelay = `${i * 50}ms`;
                    }

                    // Card do Jogador 1
                    row.innerHTML += `
                        <div class="player-card-item card-glow-${player1.rarity}">
                            <div class="player-card-info">
                                <span class="text-2xl">${rarityEmojis[player1.rarity]}</span>
                                <div class="text-left">
                                    <p class="font-bold rarity-${player1.rarity} text-sm">${player1.nome}</p>
                                    <p class="text-xs text-gray-400">${player1.posGeral || 'N/A'} • ${player1.clube}</p>
                                </div>
                            </div>
                            <div class="player-card-ovr rarity-${player1.rarity}">${player1.ovr}</div>
                        </div>`;
                    
                    // Card do Jogador 2 (se existir)
                    if (player2) {
                        row.innerHTML += `
                         <div class="player-card-item card-glow-${player2.rarity}">
                            <div class="player-card-info">
                                <span class="text-2xl">${rarityEmojis[player2.rarity]}</span>
                                <div class="text-left">
                                    <p class="font-bold rarity-${player2.rarity} text-sm">${player2.nome}</p>
                                    <p class="text-xs text-gray-400">${player2.posGeral || 'N/A'} • ${player2.clube}</p>
                                </div>
                            </div>
                            <div class="player-card-ovr rarity-${player2.rarity}">${player2.ovr}</div>
                        </div>`;
                    }
                     listEl.appendChild(row);
                }
            });
        }

        function gerarTimesAleatoriosJogoRapido() {
            const placeholder = document.getElementById('central-animation-placeholder');
            const botoesVitoria = document.getElementById('botoes-vitoria-container');
            const btnGerar = document.getElementById('btn-gerar-times-rapido');

            if(btnGerar) btnGerar.disabled = true;

            if (placeholder) {
                placeholder.classList.add('opacity-0', 'scale-75');
                setTimeout(() => {
                    placeholder.classList.add('hidden');
                    if(botoesVitoria) {
                        botoesVitoria.classList.remove('hidden');
                        botoesVitoria.classList.add('animate-[fadeIn_0.5s_ease-out_forwards]');
                    }
                }, 500); 
            }

            // Reinicia o placar e sorteia novas táticas
            jogoRapidoState.placar = { caio: 0, ricardo: 0 };
            const [taticaCaio, taticaRicardo] = sortear(taticasDB, 2);
            jogoRapidoState.taticas = { caio: taticaCaio, ricardo: taticaRicardo };
            
            const todosJogadores = [].concat(...Object.values(playersDB));
            if (todosJogadores.length < 22) {
                showModal('Erro de Dados', '<p>Não há jogadores suficientes no banco de dados para formar dois times.</p>', [{text: 'Ok'}], 'pact');
                if(btnGerar) btnGerar.disabled = false;
                return;
            }
            const timeCompleto = sortear(todosJogadores, 22);
            
            timesJogoRapido.caio = timeCompleto.slice(0, 11);
            timesJogoRapido.ricardo = timeCompleto.slice(11, 22);

            setTimeout(() => {
                renderizarTimesJogoRapido({ animate: true });
                if(btnGerar) btnGerar.disabled = false; 
            }, 600);


            const weatherEvent = sortear(eventsDB.clima, 1)[0];
            setTimeout(() => {
                showModal(
                    weatherEvent.title,
                    `<p class="text-center">${weatherEvent.description}</p><p class="text-center mt-4 font-bold">Novos times foram gerados. Bom jogo!</p>`,
                    [{ text: 'Jogar!' }],
                    'purple'
                );
            }, 800);
        }

        function handleVitoriaJogoRapido(vencedor) {
            jogoRapidoState.placar[vencedor]++;
            renderizarTimesJogoRapido({ animate: false }); // Apenas atualiza o placar, sem animar jogadores

            if (jogoRapidoState.placar[vencedor] >= 7) {
                const vencedorNome = vencedor.toUpperCase();
                const bodyHTML = `
                    <div class="text-center">
                        <p class="text-2xl mb-4">🏆 O CAMPEÃO DA PARTIDA É... <strong>${vencedorNome}</strong>! 🏆</p>
                        <p class="text-3xl md:text-4xl font-bold text-purple-300 my-6" style="text-shadow: 0 0 10px var(--purple-glow);">
                            DOMINÂNCIA ABSOLUTA!
                        </p>
                    </div>
                `;
                showModal(
                    '👑 FIM DE JOGO! 👑',
                    bodyHTML,
                    [{ text: 'Começar de Novo', action: resetJogoRapidoUI }],
                    'purple'
                );
            }
        }

        function buildJogoRapidoUI() {
            jogoRapidoContainerEl.innerHTML = `
                <div class="relative min-h-screen flex flex-col p-4 md:p-8">
                    <button id="btn-voltar-menu-rapido" class="absolute top-6 left-6 py-1 px-3 text-sm action-button btn-secondary z-20">Voltar ao Menu</button>
                    <header class="text-center mb-6 pt-8">
                         <h1 class="text-5xl md:text-7xl font-bold text-white mb-2 flex items-center justify-center gap-4" style="text-shadow: 0 0 10px var(--purple-glow);">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-14 h-14"><path stroke-linecap="round" stroke-linejoin="round" d="M3.75 13.5l10.5-11.25L12 10.5h8.25L9.75 21.75 12 13.5H3.75z" /></svg>
                            JOGO RÁPIDO
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-14 h-14"><path stroke-linecap="round" stroke-linejoin="round" d="M3.75 13.5l10.5-11.25L12 10.5h8.25L9.75 21.75 12 13.5H3.75z" /></svg>
                        </h1>
                    </header>
                    <main class="grid grid-cols-1 lg:grid-cols-3 gap-6 flex-grow items-start">
                        <!-- Time Caio -->
                        <div class="elenco-box p-4 rounded-lg flex flex-col h-full" style="border-color: var(--purple-accent);">
                            <div id="header-caio-rapido" class="mb-4"></div>
                            <div id="lista-caio-rapido" class="space-y-2 mt-2 flex-grow overflow-y-auto min-h-0"></div>
                        </div>

                        <!-- Console Central -->
                        <div id="console-central-rapido" class="flex flex-col items-center justify-start gap-6 h-full">
                            <div id="placar-jogo-rapido" class="placar p-2 rounded-lg text-2xl font-bold text-center w-full max-w-sm border-purple-400"></div>
                            <div class="flex-grow w-full flex flex-col items-center justify-center">
                                 <div id="central-animation-placeholder" class="text-center transition-all duration-500 ease-in-out">
                                    <svg class="w-48 h-48 text-purple-400 scanner-animation" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                                        <defs>
                                            <linearGradient id="scanner-gradient" gradientTransform="rotate(90)">
                                                <stop offset="5%" stop-color="var(--purple-glow)" stop-opacity="0" />
                                                <stop offset="95%" stop-color="var(--purple-glow)" stop-opacity="1" />
                                            </linearGradient>
                                            <filter id="scanner-glow">
                                                <feGaussianBlur in="SourceGraphic" stdDeviation="2" result="blur" />
                                                <feMerge>
                                                    <feMergeNode in="blur" />
                                                    <feMergeNode in="SourceGraphic" />
                                                </feMerge>
                                            </filter>
                                        </defs>
                                        <g filter="url(#scanner-glow)">
                                            <!-- Static outer markers -->
                                            <path d="M 100 5 L 100 15 M 195 100 L 185 100 M 100 195 L 100 185 M 5 100 L 15 100" stroke="currentColor" stroke-width="2" stroke-opacity="0.5"/>
                                            <path d="M 35 35 L 45 45 M 165 35 L 155 45 M 165 165 L 155 155 M 35 165 L 45 155" stroke="currentColor" stroke-width="1.5" stroke-opacity="0.5"/>
                                            
                                            <!-- Outer rotating ring -->
                                            <g class="scanner-outer-ring">
                                                <circle cx="100" cy="100" r="95" stroke="currentColor" stroke-width="1" fill="none" stroke-opacity="0.2"/>
                                                <path d="M 100,5 A 95,95 0 0 1 195,100" stroke="url(#scanner-gradient)" stroke-width="2.5" fill="none"/>
                                            </g>

                                            <!-- Inner rotating ring -->
                                            <g class="scanner-inner-ring">
                                                <circle cx="100" cy="100" r="65" stroke="currentColor" stroke-width="1.5" fill="none" stroke-dasharray="2 10" stroke-opacity="0.4"/>
                                            </g>

                                            <!-- Pulsing core -->
                                            <g style="animation: pulse-glow 2.5s ease-in-out infinite;">
                                                <circle cx="100" cy="100" r="35" fill="currentColor" fill-opacity="0.1"/>
                                                <path d="M100 75 L125 100 L100 125 L75 100 Z" fill="none" stroke="currentColor" stroke-width="2.5"/>
                                                <circle cx="100" cy="100" r="8" fill="currentColor"/>
                                            </g>
                                        </g>
                                    </svg>
                                     <p class="mt-4 text-gray-400">Aguardando geração de times...</p>
                                </div>
                                <div id="botoes-vitoria-container" class="hidden w-full max-w-sm animate-[fadeIn_0.5s_ease-out_forwards]">
                                     <p class="text-gray-400 text-center mb-4">Após a partida, declare o vencedor:</p>
                                    <div class="grid grid-cols-1 gap-4">
                                        <button onclick="handleVitoriaJogoRapido('caio')" class="text-xl py-4 px-6 btn-jogo-rapido-win btn-win-caio">Vitória do Caio</button>
                                        <button onclick="handleVitoriaJogoRapido('ricardo')" class="text-xl py-4 px-6 btn-jogo-rapido-win btn-win-ricardo">Vitória do Ricardo</button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Time Ricardo -->
                        <div class="elenco-box p-4 rounded-lg flex flex-col h-full" style="border-color: var(--purple-accent);">
                             <div id="header-ricardo-rapido" class="mb-4"></div>
                            <div id="lista-ricardo-rapido" class="space-y-2 mt-2 flex-grow overflow-y-auto min-h-0"></div>
                        </div>
                    </main>
                     <footer class="text-center mt-6">
                        <button id="btn-gerar-times-rapido" onclick="gerarTimesAleatoriosJogoRapido()" class="py-3 px-8 text-lg action-button btn-purple">Gerar Novos Times</button>
                    </footer>
                </div>
            `;

            document.getElementById('btn-voltar-menu-rapido').addEventListener('click', () => {
                jogoRapidoContainerEl.classList.add('hidden');
                menuPrincipalEl.classList.remove('hidden');
            });
            renderizarTimesJogoRapido({ isInitial: true }); // Renderiza o estado inicial (sem jogadores)
        }

        function iniciarJogoRapido() {
            menuPrincipalEl.classList.add('hidden');
            jogoContainerEl.classList.add('hidden');
            historicoContainerEl.classList.add('hidden');
            sorteioTimesContainerEl.classList.add('hidden');
            jogoRapidoContainerEl.classList.remove('hidden');

            buildJogoRapidoUI();
        }

        // BANCO DE DADOS DE TIMES - Emoji : Nome
        const timesDB = {
            '💙': ['Alianza Lima'],
            '🐰': ['América-MG'],
            '🐞': ['Argentinos Juniors'],
            '🌪️': ['Athletico-PR'],
            '🐓': ['Atlético-MG', 'Bari', 'Gil Vicente'],
            '🏆': ['Atlético Nacional'],
            '🟡': ['Aucas', 'Barcelona SC', 'Villarreal', 'Luzern', 'Gwangju FC', 'Kolding IF'],
            '🟢': ['Audax Italiano', 'Gimnasia', 'Goiás', 'Sarmiento', 'Racing Ferrol'],
            '🎓': ['Blooming', 'Racing Club'],
            '🍫': ['Boca Juniors'],
            '🌌': ['Bolívar'],
            '⭐': ['Botafogo', 'Estrela Amadora', 'Red Star', 'Drogheda'],
            '🐂': ['Bragantino', 'FC Dallas', 'Oxford', 'Torino', 'Osasuna', 'New York Red Bulls', 'RB Leipzig'],
            '🌀': ['Cerro Porteño', 'Trabzonspor'],
            '👨‍🏫': ['César Vallejo'],
            '酋長': ['Colo-Colo'],
            '⚓️': ['Corinthians', 'Genoa', 'Sampdoria', 'Portsmouth'],
            '⚫️': ['Danubio', 'Deportivo Riestra', 'Libertad', 'Tacuary'],
            '🦅': ['Defensa y Justicia', 'D.C. United', 'Frankfurt', 'Lazio', 'GKS Katowice', 'Śląsk Wrocław', 'Go Ahead Eagles', 'Beşiktaş', 'Rapid București'],
            '🟠': ['Deportivo Pereira', 'Reggina', 'Motherwell', 'RoundGlass Punjab', 'Montpellier', 'Laval', 'Zagłębie Lubin'],
            '⚡️': ['Emelec', 'Houston Dynamo', 'Rayo Vallecano', 'Kansas City Current', 'Adana Demirspor'],
            '🦁': ['Estudiantes', 'Fortaleza', 'Santa Fe', 'Millwall', 'Shrewsbury', 'Braunschweig', 'Lechia Gdańsk'],
            '👨‍🎓': ['Estudiantes de Mérida'],
            '🔴⚫️': ['Flamengo', 'Melgar', "Newell's Old Boys", 'Mirandés', 'Hertha BSC', 'Nürnberg', 'AC Milan', 'Hermannstadt', 'Bohemians'],
            '🇭🇺': ['Fluminense'],
            '🐺': ['Gimnasia', 'Wolves', 'Wolfsburg', 'Petrolul', 'Lecce', 'FC Midtjylland', 'Al Taawoun'],
            '🏹': ['Guaraní', 'Tolima', 'Arsenal'],
            '🎈': ['Huracán'],
            '⚫️🔵': ['Independiente del Valle', 'LDU Quito', 'Inter Milan', 'Paderborn', 'Djurgårdens IF', 'IK Sirius', 'Club Brugge', 'Dender EH', 'St Mirren', 'FC Seoul'],
            '💪': ['Independiente Medellín'],
            '🇦🇹': ['Internacional'],
            '⚪️': ['LDU Quito', 'Unión', 'Leuven', 'KFUM Oslo'],
            '🐦': ['Liverpool-URU', 'San Lorenzo', 'Bristol City', 'West Brom', 'SSV Ulm', 'Wellington Phoenix'],
            '⛵️': ['Magallanes', 'Plymouth'],
            '⛽️': ['Oriente Petrolero'],
            '🇵🇸': ['Palestino'],
            '🐷': ['Palmeiras'],
            '😇': ['Patronato', 'Southampton', 'St Johnstone', "St Patrick's Athletic"],
            '🟡⚫️': ['Peñarol', 'AIK', 'NAC Breda', 'Hyderabad'],
            '🐔': ['River Plate'],
            '🐟': ['Santos', 'Lorient'],
            '🇾🇪': ['São Paulo'],
            '🍺': ['Sporting Cristal', 'Burton', 'Bayern Munich'],
            '🐅': ['The Strongest', 'Tigre', 'Hull', 'Tianjin Jinmen Tiger', 'Al Ittihad', 'Ulsan Hyundai', 'FC Nordsjælland'],
            '🍦': ['Universitario'],
            '👑': ['Atlético Tucumán', 'Charlotte FC', 'Real Salt Lake', 'Reading', 'Seattle Reign FC', 'Utah Royals', 'Real Madrid', 'Vitória SC', 'Korona Kielce', 'AC Lyngby'],
            '🛠️': ['Banfield'],
            '🚚': ['Barracas Central'],
            '🏴‍☠️': ['Belgrano', 'Bristol Rovers', 'Brest'],
            '🚂': ['Central Córdoba', 'Atlanta United', 'CFR Cluj', 'Lech Poznań'],
            '🍇': ['Godoy Cruz'],
            '👹': ['Independiente', 'Ñublense', 'Man Utd', 'Crawley', 'Kaiserslautern', 'Lincoln'],
            '🔵': ['Independiente Rivadavia', 'Birmingham'],
            '🔴': ['Instituto Córdoba', 'Stevenage', 'Reggiana', 'Mechelen', 'Standard Liège', 'Aberdeen', 'Brann', 'Silkeborg IF', 'Sligo Rovers', 'Shelbourne', 'AVS', 'Adelaide United', 'Heidenheim', 'Mainz'],
            '🇱🇻': ['Lanús'],
            '🦑': ['Platense'],
            '🇺🇦': ['Rosario Central'],
            '🏰': ['Vélez Sarsfield', 'Burgos', 'Cittadella', 'Al Ahli'],
            '🌳': ['Austin FC', 'Nottingham Forest', 'Zhejiang', 'Puszcza Niepołomice'],
            '⚜️': ['CF Montreal', 'St. Louis City SC', 'Darmstadt', 'Fiorentina'],
            '🔥': ['Chicago Fire', 'Sevilla'],
            '🏔️': ['Colorado Rapids', 'Vancouver Whitecaps FC'],
            '👷‍♂️': ['Columbus Crew'],
            '🦁⚔️': ['FC Cincinnati'],
            '🦩': ['Inter Miami CF'],
            '✨': ['LA Galaxy'],
            '🪽': ['Los Angeles FC'],
            '🦆': ['Minnesota United'],
            '🎸': ['Nashville SC'],
            '🇺🇸': ['New England Revolution'],
            '🗽': ['New York City FC'],
            '🦁🟣': ['Orlando City SC', 'Orlando Pride'],
            '🐍': ['Philadelphia Union'],
            '🌲': ['Portland Timbers'],
            '🌎': ['San Jose Earthquakes'],
            '🔊': ['Seattle Sounders FC'],
            '🦇': ['NJ/NY Gotham FC', 'Valencia', 'Albacete'],
            '🌹': ['Portland Thorns FC', 'Blackburn'],
            '🐎': ['Racing Louisville FC', 'Mönchengladbach', 'Bolton', 'Twente', 'Randers FC'],
            '🌊': ['San Diego Wave FC', 'Real Sociedad'],
            '👻': ['Washington Spirit'],
            '🍒': ['Bournemouth'],
            '🐝': ['Brentford', 'Juve Stabia', 'Jagiellonia Białystok', 'BK Häcken'],
            '🕊️': ['Brighton'],
            '🦁🔵': ['Chelsea', 'Shrewsbury'],
            '🦅🔴': ['Crystal Palace'],
            '🍬': ['Everton', 'Derry City'],
            '🏠': ['Fulham'],
            '🚜': ['Ipswich Town'],
            '🦊': ['Leicester', 'Alavés'],
            '🚢': ['Man City'],
            '⚫️⚪️': ['Newcastle', 'Royal Antwerp FC', 'Angers', 'Saint-Étienne', 'Cercle Brugge', 'Odds BK', 'Rosenborg', 'Hammarby IF', 'Lausanne-Sport', 'Luzern', 'St. Gallen', 'Sion', 'Zürich', 'Winterthur', 'Yverdon-Sport', 'Al Shabab', 'Mohammedan', 'St Mirren', 'Cartagena', 'Castellón', 'Elversberg', 'Kolding IF', 'Preußen Münster', 'Mantova', 'Dunkerke', 'Beerschot', 'Charleroi', 'Sint-Truiden', 'AIK', 'IK Sirius', 'Al-Qadsiah', 'Al-Riyadh', 'Western Sydney Wanderers'],
            '⚒️': ['West Ham'],
            '🍷': ['Burnley', 'Servette', 'Bordeaux'],
            '🐦🔵': ['Cardiff', 'West Brom'],
            '🐘': ['Coventry', 'Kerala Blasters'],
            '🐏': ['Derby'],
            '🦚': ['Leeds'],
            '🎩': ['Luton', 'Stockport'],
            '🦁🔴': ['Middlesbrough', 'Santa Fe', 'Athletic Bilbao'],
            '🐤': ['Norwich', 'Nantes', 'Sint-Truiden', 'Lillestrøm', 'Modena'],
            '⚓️🌙': ['Portsmouth'],
            '⚪️⚜️': ['Preston'],
            '⚔️': ['Sheffield Utd', 'Braga', 'Al Nassr'],
            '🦉': ['Sheffield Wednesday', 'Başakşehir'],
            '🏺': ['Stoke'],
            '🐈⚫️': ['Sunderland'],
            '🦢': ['Swansea', 'Wycombe'],
            '🦌': ['Watford', 'Mansfield', 'Ross County'],
            '🐶': ['Barnsley', 'Huddersfield', 'LOSC Lille'],
            '🐉': ['Leyton Orient', 'Wrexham', 'Sporting'],
            '🏛️': ['Exeter', 'Hellas Verona'],
            '👞': ['Northampton'],
            '🐻🌳': ['Atlético de Madrid'],
            '❤️💙': ['Barcelona'],
            '⚪️🔵': ['Celta Vigo', 'Huesca', 'Deportivo La Coruña', 'Eibar', 'Racing Santander', 'Tenerife', 'Elversberg', 'Holstein Kiel', 'Karlsruher', 'Bochum', 'Auxerre', 'Paris FC', 'Famalicão', 'FC Porto', 'Rio Ave', 'Moreirense', 'Soenderjyske Fodbold', 'FC København', 'Haugesund', 'IFK Göteborg', 'IFK Norrköping', 'IFK Värnamo', 'Malmö FF', 'Basel', 'Nantong Zhiyun', 'Qingdao West Coast', 'Shanghai Shenhua', 'Bengaluru', 'Mumbai City', 'Dundee'],
            '✈️': ['Getafe', 'Incheon United', 'Newcastle Jets'],
            '🦟': ['Girona'],
            '🟡🔵': ['Las Palmas', 'Levante', 'Union SG', 'Motor Lublin', 'PGE Stal Mielec', 'Brøndby IF', 'Unirea Slobozia'],
            '🥒': ['Leganés'],
            '🏝️': ['Mallorca', 'Cagliari'],
            '🟢⚪️': ['Real Betis', 'Sporting', 'Celtic', 'Hibernian', 'Hamarkameratene', 'Groningen', 'Sparta Rotterdam', 'Halmstads BK', 'Al-Fateh', 'Al-Kholood', 'Al-Orobah', 'Bodrum', 'ATK Mohun Bagan'],
            '🟣⚪️': ['Valladolid', 'R.S.C Anderlecht'],
            '🔴⚪️': ['Almería', 'Granada', 'Sporting Gijón', 'Jahn Regensburg', 'Südtirol', 'Annecy', 'Reims', 'Guingamp', 'Rodez', 'CD Nacional', 'Samsunpor', 'Botoșani', 'Cracovia', 'Widzew Łódź', 'Hatayspor', 'Fredrikstad', 'Tromsø', 'Västerås SK'],
            '⛪️': ['Real Oviedo'],
            '🏭': ['Bayer Leverkusen'],
            '🌲🔴': ['Augsburg'],
            '🌲⚫️': ['Freiburg'],
            '☠️': ['St. Pauli'],
            '🐻': ['Union Berlin', 'Ajaccio', 'Gangwon FC'],
            '🚗': ['Stuttgart'],
            '🔑': ['Werder Bremen'],
            '🦁🟡': ['Frosinone', 'Göztepe', 'Gloria Buzău'],
            '🐐': ['Köln'],
            '🍀': ['Greuther Fürth', 'Celtic', 'Viborg FF'],
            '🦖': ['Hamburger SV'],
            '9️⃣6️⃣': ['Hannover 96'],
            '👵': ['Hertha BSC', 'UTA Arad'],
            '🏃‍♀️': ['Atalanta'],
            '🍝': ['Bologna'],
            '🏞️': ['Como'],
            '🖼️': ['Empoli'],
            '🌋': ['Napoli'],
            '🦓': ['Juventus', 'Udinese'],
            '🧀': ['Parma', 'AZ'],
            '🦁🪽': ['Venezia'],
            '🎻': ['Cremonese'],
            '🐴': ['Cesena', 'Salernitana'],
            '🦅🩷': ['Palermo'],
            '🗼': ['Pisa', 'PSG', 'FC Utrecht'],
            '🎰': ['Monaco'],
            '🌟': ['Marseille'],
            '⛏️': ['Lens', 'Schalke 04', 'Górnik Zabrze'],
            '⚫️🔴': ['Rennes', 'Heracles Almelo', 'IF Brommapojkarna', 'Gaziantep FK', 'Kayserispor', 'Wuhan Three Towns'],
            '🟣': ['Toulouse', 'Metropolitanos', 'Perth Glory', 'Daejeon Hana Citizen'],
            '💚': ['Saint-Étienne'],
            '🦄': ['Amiens'],
            '🛡️': ['Caen', 'Sepsi', 'Dundalk', 'Viking'],
            '🩸🟡': ['Martigues'],
            '🐬': ['Grenoble'],
            '鵝': ['Casa Pia'],
            '❌': ['Ajax'],
            '🏗️': ['Feyenoord'],
            '🟡🟢': ['Fortuna Sittard'],
            '💡': ['PSV'],
            '❤️': ['SC Heerenveen', 'Heart of Midlothian'],
            '🔴⚪️🔵': ['Willem II'],
            '🐃': ['Gent'],
            '🔴🟡': ['East Bengal'],
            '🧸': ['Rangers'],
            '☘️': ['Shamrock Rovers'],
            '🦂': ['Antalyaspor'],
            '🍵': ['Rizespor'],
            '🐕': ['Dinamo București'],
            '🦈': ['Farul Constanța'],
            '🔩': ['Oțelul Galați', 'Pohang Steelers'],
            'L': ['Legia Warszawa'],
            '🌙': ['Al Hilal'],
            '⛰️': ['Shandong Taishan'],
            '🎭': ['Sydney FC'],
            '⚽️': ['Time Padrão']
        };

        // Função para obter todos os times como array
        function getAllTeams() {
            const teams = [];
            for (const emoji in timesDB) {
                timesDB[emoji].forEach(teamName => {
                    teams.push({ emoji, name: teamName });
                });
            }
            return teams;
        }

        // Função para sortear um time aleatório
        function getRandomTeam() {
            const allTeams = getAllTeams();
            return allTeams[Math.floor(Math.random() * allTeams.length)];
        }

        // Função para criar animação de caça-níquel
        function createSlotMachineAnimation(containerId, finalTeam, duration = 2000) {
            const container = document.getElementById(containerId);
            if (!container) return;

            const allEmojis = Object.keys(timesDB);
            let currentIndex = 0;
            const intervalTime = 50;
            const totalSteps = duration / intervalTime;
            let step = 0;

            container.innerHTML = `
                <div class="text-8xl mb-4 transition-all duration-75 slot-emoji" style="filter: blur(3px);">
                    ${allEmojis[0]}
                </div>
                <div class="text-2xl font-bold text-transparent slot-name" style="opacity: 0;">
                    Sorteando...
                </div>
            `;

            const emojiEl = container.querySelector('.slot-emoji');
            const nameEl = container.querySelector('.slot-name');

            const interval = setInterval(() => {
                step++;
                currentIndex = (currentIndex + 1) % allEmojis.length;
                emojiEl.textContent = allEmojis[currentIndex];

                if (step < totalSteps * 0.7) {
                    emojiEl.style.filter = 'blur(3px)';
                } else {
                    const blurAmount = 3 * (1 - (step - totalSteps * 0.7) / (totalSteps * 0.3));
                    emojiEl.style.filter = `blur(${blurAmount}px)`;
                }

                if (step >= totalSteps) {
                    clearInterval(interval);
                    emojiEl.textContent = finalTeam.emoji;
                    emojiEl.style.filter = 'blur(0px)';
                    emojiEl.style.transform = 'scale(1.1)';
                    
                    setTimeout(() => {
                        emojiEl.style.transform = 'scale(1)';
                        nameEl.textContent = finalTeam.name;
                        nameEl.style.opacity = '1';
                        nameEl.classList.remove('text-transparent');
                        nameEl.classList.add('text-white');
                    }, 200);
                }
            }, intervalTime);
        }

        // Função principal de sorteio
        function sortearTimes() {
            const btnSortear = document.getElementById('btn-sortear-times');
            const resultadoEl = document.getElementById('resultado-sorteio');
            const confrontoText = document.getElementById('confronto-text');

            btnSortear.disabled = true;
            btnSortear.style.opacity = '0.5';
            btnSortear.style.cursor = 'not-allowed';

            resultadoEl.style.opacity = '0';

            const teamCaio = getRandomTeam();
            const teamRicardo = getRandomTeam();

            createSlotMachineAnimation('team-slot-caio', teamCaio, 2000);
            createSlotMachineAnimation('team-slot-ricardo', teamRicardo, 2000);

            setTimeout(() => {
                confrontoText.textContent = `${teamCaio.emoji} ${teamCaio.name} VS ${teamRicardo.emoji} ${teamRicardo.name}`;
                resultadoEl.style.opacity = '1';

                btnSortear.disabled = false;
                btnSortear.style.opacity = '1';
                btnSortear.style.cursor = 'pointer';
            }, 2500);
        }

        // Inicializar o modo Sorteio de Times
        function initSorteioTimes() {
            const container = document.getElementById('sorteio-times-container');
            if (!container) return;

            container.innerHTML = `
                <div class="relative flex flex-col items-center justify-center min-h-screen p-4" style="background: linear-gradient(135deg, #001f3f 0%, #0a4d8c 50%, #1e5a9e 100%);">
                    <button id="btn-voltar-menu-sorteio" class="absolute top-6 left-6 py-2 px-4 text-sm rounded-lg font-semibold transition-all duration-300 border border-blue-400 text-blue-400 hover:bg-blue-400 hover:text-white z-20">
                        Voltar ao Menu
                    </button>

                    <div class="text-center w-full max-w-6xl">
                        <!-- Título -->
                        <div class="mb-12">
                            <h1 class="text-5xl md:text-6xl font-bold text-white uppercase tracking-widest mb-2" style="text-shadow: 0 0 20px rgba(59, 130, 246, 0.8);">
                                ⚔️ Sorteio de Times ⚔️
                            </h1>
                            <p class="text-lg text-blue-200">Deixe o destino escolher os adversários!</p>
                        </div>

                        <!-- Área de Sorteio -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
                            <!-- Time Caio -->
                            <div class="flex flex-col items-center">
                                <div class="text-3xl font-bold text-blue-300 mb-6 tracking-wider">CAIO</div>
                                <div id="team-slot-caio" class="w-64 h-64 rounded-2xl flex flex-col items-center justify-center transition-all duration-300" style="background: rgba(59, 130, 246, 0.2); border: 3px solid rgba(59, 130, 246, 0.5); backdrop-filter: blur(10px); box-shadow: 0 0 30px rgba(59, 130, 246, 0.3);">
                                    <div class="text-6xl">❓</div>
                                    <div class="text-xl text-blue-200 mt-4">Aguardando...</div>
                                </div>
                            </div>

                            <!-- Time Ricardo -->
                            <div class="flex flex-col items-center">
                                <div class="text-3xl font-bold text-blue-300 mb-6 tracking-wider">RICARDO</div>
                                <div id="team-slot-ricardo" class="w-64 h-64 rounded-2xl flex flex-col items-center justify-center transition-all duration-300" style="background: rgba(59, 130, 246, 0.2); border: 3px solid rgba(59, 130, 246, 0.5); backdrop-filter: blur(10px); box-shadow: 0 0 30px rgba(59, 130, 246, 0.3);">
                                    <div class="text-6xl">❓</div>
                                    <div class="text-xl text-blue-200 mt-4">Aguardando...</div>
                                </div>
                            </div>
                        </div>

                        <!-- Botão de Sortear -->
                        <button id="btn-sortear-times" class="py-4 px-12 text-2xl font-bold rounded-xl transition-all duration-300 uppercase tracking-wider" style="background: linear-gradient(45deg, #3b82f6, #60a5fa); color: white; box-shadow: 0 0 30px rgba(59, 130, 246, 0.6); border: 2px solid rgba(147, 197, 253, 0.5);">
                            🎲 Sortear Times
                        </button>

                        <!-- Resultado -->
                        <div id="resultado-sorteio" class="mt-12 opacity-0 transition-opacity duration-500">
                            <div class="p-6 rounded-xl" style="background: rgba(59, 130, 246, 0.1); border: 2px solid rgba(59, 130, 246, 0.3);">
                                <h2 class="text-3xl font-bold text-white mb-4">⚔️ CONFRONTO DEFINIDO! ⚔️</h2>
                                <p id="confronto-text" class="text-2xl text-blue-100"></p>
                            </div>
                        </div>
                    </div>
                </div>
            `;

            document.getElementById('btn-voltar-menu-sorteio').addEventListener('click', () => {
                container.classList.add('hidden');
                document.getElementById('menu-principal').classList.remove('hidden');
            });

            document.getElementById('btn-sortear-times').addEventListener('click', sortearTimes);
        }

        function iniciarSorteioTimes() {
            menuPrincipalEl.classList.add('hidden');
            jogoContainerEl.classList.add('hidden');
            historicoContainerEl.classList.add('hidden');
            jogoRapidoContainerEl.classList.add('hidden');
            sorteioTimesContainerEl.classList.remove('hidden');

            initSorteioTimes();
        }

        function setupMenu() {
            btnJogar.addEventListener('click', () => {
                menuPrincipalEl.classList.add('hidden');
                jogoContainerEl.classList.remove('hidden');
                
                mensagensSistemaEl.innerHTML = '';
                areaDeComandosEl.innerHTML = '';
                areaDeEscolhaEl.innerHTML = '';
                areaDeDecisaoEl.innerHTML = '';
                typeMessage("🟢 INICIALIZANDO SISTEMA METANOL 🟢");
                typeMessage("Carregando diretrizes... Validando competidores...");
                setTimeout(iniciarNovaTemporada, 1500);
            });

            btnHistorico.addEventListener('click', () => {
                menuPrincipalEl.classList.add('hidden');
                historicoContainerEl.classList.remove('hidden');
                renderizarHistorico();
            });

            btnModosJogo.addEventListener('click', () => {
                const modosHTML = `
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <button id="btn-modal-jogo-rapido" class="dossier-card text-left hover:border-purple-400 transition-colors">
                        <h3 class="font-bold text-xl mb-2 text-purple-400">⚡ Jogo Rápido</h3>
                        <p class="text-sm">Partidas diretas com times de 11 jogadores gerados aleatoriamente. Sem draft, sem placar geral.</p>
                    </button>
                    <button id="btn-modal-sorteio" class="dossier-card text-left hover:border-blue-400 transition-colors">
                        <h3 class="font-bold text-xl mb-2 text-blue-400">🎲 Sorteio de Times</h3>
                        <p class="text-sm">Sorteie dois times aleatórios do banco de dados para se enfrentarem.</p>
                    </button>
                </div>
                `;
                 showModal('🕹️ Modos de Jogo 🕹️', modosHTML, [], 'purple');
                 
                 document.getElementById('btn-modal-jogo-rapido').onclick = () => {
                     hideModal();
                     iniciarJogoRapido();
                 };
                 
                 document.getElementById('btn-modal-sorteio').onclick = () => {
                     hideModal();
                     iniciarSorteioTimes();
                 };
            });
            
            btnRegras.addEventListener('click', () => {
                const regrasHTML = `
                    <div class="space-y-6 max-h-[70vh] overflow-y-auto pr-4 text-left">
                        <div class="dossier-card">
                            <h3 class="font-bold text-xl mb-2 flex items-center gap-2"><span class="text-2xl">🎯</span> Objetivo</h3>
                            <p>Seja o primeiro a vencer <strong>7 partidas</strong> em uma temporada (MD7) para conquistar o título!</p>
                        </div>

                        <div class="dossier-card">
                            <h3 class="font-bold text-xl mb-2 flex items-center gap-2"><span class="text-2xl">⚙️</span> Como Jogar</h3>
                            <ul class="list-disc list-inside space-y-2">
                                <li>Cada jogador monta seu time através de sorteios de pacotes de jogadores.</li>
                                <li>Após montar os times, vocês jogam partidas no EA FC 25. O vencedor de cada partida ganha 1 ponto na temporada.</li>
                                <li>O primeiro a chegar em 7 vitórias vence a temporada.</li>
                            </ul>
                        </div>

                        <div class="dossier-card">
                            <h3 class="font-bold text-xl mb-3 flex items-center gap-2"><span class="text-2xl">💎</span> Raridades dos Jogadores</h3>
                             <p class="text-sm mb-4">A raridade é baseada no Overall (OVR) do jogador no EA FC:</p>
                            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-center">
                                <div class="p-3 rounded-lg bg-gray-900/50 border border-gray-700">
                                    <p class="text-2xl">${rarityEmojis.diamante}</p>
                                    <p class="font-bold rarity-diamond">Diamante</p>
                                    <p class="text-xs text-gray-400">OVR 89+</p>
                                </div>
                                <div class="p-3 rounded-lg bg-gray-900/50 border border-gray-700">
                                    <p class="text-2xl">${rarityEmojis.ouro}</p>
                                    <p class="font-bold rarity-gold">Ouro</p>
                                    <p class="text-xs text-gray-400">OVR 85-88</p>
                                </div>
                                <div class="p-3 rounded-lg bg-gray-900/50 border border-gray-700">
                                    <p class="text-2xl">${rarityEmojis.prata}</p>
                                    <p class="font-bold rarity-silver">Prata</p>
                                    <p class="text-xs text-gray-400">OVR 80-84</p>
                                </div>
                                <div class="p-3 rounded-lg bg-gray-900/50 border border-gray-700">
                                    <p class="text-2xl">${rarityEmojis.bronze}</p>
                                    <p class="font-bold rarity-bronze">Bronze</p>
                                    <p class="text-xs text-gray-400">OVR 70-79</p>
                                </div>
                            </div>
                        </div>
                         <div class="dossier-card">
                            <h3 class="font-bold text-xl mb-2 flex items-center gap-2"><span class="text-2xl">🏆</span> Sistema de Pontuação</h3>
                            <ul class="list-disc list-inside space-y-1">
                                <li><strong>Placar da Temporada:</strong> Vitórias na temporada atual (MD7).</li>
                                <li><strong>Placar Geral:</strong> Número de temporadas vencidas por cada jogador.</li>
                            </ul>
                        </div>
                         <div class="dossier-card">
                            <h3 class="font-bold text-xl mb-2 flex items-center gap-2"><span class="text-2xl">🎲</span> Eventos Aleatórios</h3>
                            <p>O sistema pode acionar eventos inesperados para apimentar a disputa:</p>
                            <ul class="list-disc list-inside space-y-1 mt-2">
                                <li><strong>Conflitos Internos:</strong> Sequências de derrotas podem gerar insatisfação no elenco. Gerencie as exigências de suas estrelas ou sofra as consequências.</li>
                                <li><strong>Dilemas do Manager:</strong> Escolhas difíceis que podem beneficiar você, prejudicar seu rival, ou ambos.</li>
                                <li><strong>Anomalias e Crises:</strong> Eventos como sorteios duplos, bônus de jogadores ou crises de imprensa podem ocorrer a qualquer momento.</li>
                            </ul>
                        </div>
                    </div>
                `;
                showModal('📖 Manual de Regras 📖', regrasHTML, [{ text: 'Fechar' }]);
            });

            btnVoltarMenu.addEventListener('click', () => {
                historicoContainerEl.classList.add('hidden');
                menuPrincipalEl.classList.remove('hidden');
            });

            btnVoltarMenuJogo.addEventListener('click', () => {
                jogoContainerEl.classList.add('hidden');
                menuPrincipalEl.classList.remove('hidden');
            });

            adminBtnMenu.addEventListener('click', () => {
                const bodyHTML = `
                    <p>Insira a senha de administrador para editar o placar.</p>
                    <input type="password" id="admin-password" class="w-full bg-gray-900 border border-gray-700 rounded p-2 mt-4 text-white">
                `;
                const buttons = [{
                    text: 'Acessar',
                    action: () => {
                        const password = document.getElementById('admin-password').value;
                        if (password === 'METANOL') {
                            openScoreEditor();
                        } else {
                            const errorBody = '<p class="text-red-400 font-bold">Senha incorreta. Acesso negado.</p>';
                            showModal('Acesso Negado', errorBody, [{ text: 'Fechar' }], 'pact');
                        }
                    }
                }];
                showModal('Painel do Administrador', bodyHTML, buttons);
            });
        }
        
        // CORREÇÃO APLICADA: Esta é a nova função para processar os dados do CSV, que estava ausente.
        // Ela lida com as particularidades do seu arquivo de dados.
        function parsePlayersFromCSV(csv) {
            const lines = csv.trim().split('\n');
            lines.slice(1).forEach(line => {
                const parts = line.split(',');
                if (parts.length < 5) return;
                
                const overall = parts[0].trim();
                const nome = parts[1].trim();
                const clube = parts[2].trim();
                const liga = parts[3].trim();
                const playstyles = parts[4] ? parts[4].trim().replace(/"/g, '').split(',').map(s => s.trim()) : [];
                
                let ovr = parseInt(overall.replace(/[^0-9]/g, ''));
                if (isNaN(ovr)) return;
                
                let rarity = 'bronze';
                if (ovr >= 89) rarity = 'diamante';
                else if (ovr >= 85) rarity = 'ouro';
                else if (ovr >= 80) rarity = 'prata';
                
                const emojiMatch = overall.match(/^(💎|🥇|🥈|🥉)/);
                if (emojiMatch) {
                    const emoji = emojiMatch[0];
                    if (emoji === '💎') rarity = 'diamante';
                    else if (emoji === '🥇') rarity = 'ouro';
                    else if (emoji === '🥈') rarity = 'prata';
                    else if (emoji === '🥉') rarity = 'bronze';
                }
                
                let posGeral = 'Meio-campista';
                if (nome.toLowerCase().includes('gk') || clube === 'Goleiro') posGeral = 'Goleiro';
                else if (ovr >= 85) posGeral = 'Atacante';
                else if (ovr <= 82) posGeral = 'Defensor';
                
                const player = {
                    nome,
                    clube,
                    liga,
                    ovr,
                    rarity,
                    posGeral,
                    playstyles,
                    suspendedFor: 0
                };
                
                if (!playersDB[rarity]) playersDB[rarity] = [];
                playersDB[rarity].push(player);
            });
            
            console.log('Jogadores carregados:', {
                diamante: playersDB.diamante.length,
                ouro: playersDB.ouro.length,
                prata: playersDB.prata.length,
                bronze: playersDB.bronze.length
            });
        }


        // --- INICIALIZAÇÃO ---
        modalCloseBtn.addEventListener('click', hideModal);
        
        window.onload = () => {
            parsePlayersFromCSV(csvData);
            setupMenu();
        };
    </script>
</body>
</html>
