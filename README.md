<!DOCTYPE html>
<html lang="it" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Neural X-1 Ultra 4</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&display=swap');
        
        :root {
            --primary: #135bec;
            --accent: #10b981;
            --bg-dark: #0a0c14;
            --card-dark: #161b2a;
        }

        body { 
            font-family: 'Outfit', sans-serif; 
            background-color: var(--bg-dark); 
            color: #e2e8f0; 
            margin: 0;
            overflow: hidden;
        }
        
        .page { display: none; height: 100vh; overflow-y: auto; padding-bottom: 100px; animation: fadeIn 0.3s ease-in-out; }
        .page.active { display: block; }
        
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .neo-card { background: var(--card-dark); border-radius: 20px; border: 1px solid rgba(255,255,255,0.05); margin-bottom: 15px; }
        .glass-nav { background: rgba(10, 12, 20, 0.8); backdrop-filter: blur(15px); border-top: 1px solid rgba(255,255,255,0.08); }
        
        /* Nasconde la scrollbar */
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <!-- Schermata di Caricamento -->
    <div id="loader" class="fixed inset-0 z-[100] bg-black flex flex-col items-center justify-center transition-opacity duration-500">
        <i class="fas fa-brain text-primary text-5xl animate-pulse mb-4"></i>
        <h1 class="text-xl font-black italic uppercase tracking-tighter">Neural<span class="text-primary">X1</span></h1>
        <p class="text-[10px] text-zinc-500 mt-2 uppercase tracking-widest">Inizializzazione Sistema...</p>
    </div>

    <!-- Header Fisso -->
    <header id="main-header" class="hidden fixed top-0 w-full z-40 p-4 flex justify-between items-center bg-black/60 backdrop-blur-md">
        <div class="flex items-center gap-2">
            <div class="size-2 rounded-full bg-emerald-500 animate-pulse"></div>
            <h2 class="text-xs font-black uppercase italic tracking-tighter">Neural<span class="text-primary">X1</span> <span class="text-zinc-500">ULTRA 4</span></h2>
        </div>
        <i class="fas fa-signal text-zinc-400 text-xs"></i>
    </header>

    <!-- Contenuto Principale -->
    <main>
        
        <!-- Pagina Iniziale -->
        <section id="welcome" class="page active flex flex-col items-center justify-center px-8 text-center">
            <div class="relative mb-8">
                <div class="absolute inset-0 bg-primary blur-3xl opacity-30 animate-pulse"></div>
                <i class="fas fa-microchip text-6xl text-primary relative"></i>
            </div>
            <h1 class="text-3xl font-extrabold mb-4">Potenza Neurale al tuo servizio</h1>
            <p class="text-zinc-500 text-sm mb-10">Analisi predittiva in tempo reale per scommesse ad alta precisione.</p>
            <button onclick="startApp()" class="w-full bg-primary py-4 rounded-2xl font-bold text-white shadow-lg shadow-primary/30 active:scale-95 transition-transform">AVVIA OS</button>
        </section>

        <!-- Dashboard / Generatore -->
        <section id="home" class="page px-4 pt-20">
            <div class="mb-6 px-1">
                <h3 class="text-lg font-bold">Generatore IA</h3>
                <p class="text-[10px] text-zinc-500 font-bold uppercase tracking-widest">Seleziona la tua strategia</p>
            </div>
            
            <div class="neo-card p-5">
                <div class="grid grid-cols-2 gap-3 mb-5">
                    <button class="bg-white/5 p-4 rounded-xl text-left border-l-4 border-primary">
                        <i class="fas fa-bolt text-primary mb-2"></i>
                        <h4 class="text-xs font-bold">Multi Mix</h4>
                        <p class="text-[8px] text-zinc-500">Quota ~3.50</p>
                    </button>
                    <button onclick="navigateTo('surebet')" class="bg-white/5 p-4 rounded-xl text-left border-l-4 border-emerald-500">
                        <i class="fas fa-bullseye text-emerald-500 mb-2"></i>
                        <h4 class="text-xs font-bold">Surebet</h4>
                        <p class="text-[8px] text-zinc-500">Rischio Zero</p>
                    </button>
                </div>
                <button onclick="simulateGeneration()" id="gen-btn" class="w-full bg-primary py-4 rounded-xl font-bold text-xs uppercase tracking-widest flex items-center justify-center gap-2">
                    <i class="fas fa-wand-magic-sparkles"></i> Analizza Mercati
                </button>
            </div>

            <div class="space-y-3">
                <h4 class="text-[10px] font-black uppercase text-zinc-500 tracking-widest px-1">Top Pick del momento</h4>
                <div class="neo-card p-4 flex justify-between items-center border-r-4 border-emerald-500/30">
                    <div>
                        <p class="text-[10px] font-bold">Serie A • Lazio vs Milan</p>
                        <p class="text-[9px] text-emerald-500 font-bold uppercase">Consiglio: Goal @ 1.75</p>
                    </div>
                    <div class="text-right">
                        <p class="text-[8px] text-zinc-500 font-bold">AFFIDABILITÀ</p>
                        <p class="text-[10px] font-black text-primary">88%</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Pagina Surebet -->
        <section id="surebet" class="page px-4 pt-20">
            <div class="flex items-center gap-3 mb-6">
                <button onclick="navigateTo('home')" class="size-8 rounded-full bg-white/5 flex items-center justify-center text-xs"><i class="fas fa-arrow-left"></i></button>
                <h3 class="text-lg font-bold">Analisi Surebet</h3>
            </div>
            
            <div class="neo-card p-4 border-l-4 border-emerald-500">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-[10px] font-black bg-emerald-500/20 text-emerald-500 px-2 py-1 rounded">PROFITTO: 4.2%</span>
                    <i class="fas fa-check-circle text-emerald-500 text-sm"></i>
                </div>
                <div class="space-y-3">
                    <div class="bg-white/5 p-3 rounded-lg flex justify-between items-center">
                        <span class="text-[10px] font-bold">Bookmaker A (Esito 1)</span>
                        <span class="text-xs font-black text-primary">2.15</span>
                    </div>
                    <div class="bg-white/5 p-3 rounded-lg flex justify-between items-center">
                        <span class="text-[10px] font-bold">Bookmaker B (Esito X2)</span>
                        <span class="text-xs font-black text-primary">2.08</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Pagina Bot -->
        <section id="bot" class="page px-4 pt-20">
            <h3 class="text-lg font-bold mb-6">Neural Bot Auto-Trade</h3>
            <div class="neo-card p-8 text-center">
                <div id="bot-circle" class="size-24 rounded-full bg-zinc-900 flex items-center justify-center mx-auto mb-6 border-4 border-zinc-800 shadow-2xl relative">
                    <i id="bot-icon" class="fas fa-robot text-4xl text-zinc-700"></i>
                    <div id="bot-pulse" class="absolute inset-0 rounded-full bg-emerald-500/20 scale-0"></div>
                </div>
                <h4 id="bot-status" class="text-sm font-bold mb-1">Bot Stand-by</h4>
                <p class="text-[10px] text-zinc-500 mb-8 uppercase tracking-widest">In attesa di istruzioni</p>
                
                <div class="grid grid-cols-2 gap-3 mb-6">
                    <div class="bg-white/5 p-3 rounded-xl">
                        <p class="text-[8px] text-zinc-500 uppercase font-bold">Profitto Oggi</p>
                        <p class="text-xs font-bold text-emerald-500">€0.00</p>
                    </div>
                    <div class="bg-white/5 p-3 rounded-xl">
                        <p class="text-[8px] text-zinc-500 uppercase font-bold">Operazioni</p>
                        <p class="text-xs font-bold text-primary">0</p>
                    </div>
                </div>

                <button onclick="toggleBot()" id="bot-toggle-btn" class="w-full bg-white/10 py-4 rounded-2xl font-black text-xs uppercase tracking-tighter">ATTIVA AUTOMAZIONE</button>
            </div>
        </section>

    </main>

    <!-- Navigazione Inferiore -->
    <nav id="app-nav" class="hidden glass-nav fixed bottom-0 w-full h-20 flex items-center justify-around z-50 px-4">
        <button onclick="navigateTo('home')" class="nav-btn flex flex-col items-center gap-1 text-primary">
            <i class="fas fa-brain text-xl"></i>
            <span class="text-[9px] font-bold uppercase">Gen IA</span>
        </button>
        <button onclick="navigateTo('bot')" class="nav-btn flex flex-col items-center gap-1 text-zinc-500">
            <i class="fas fa-robot text-xl"></i>
            <span class="text-[9px] font-bold uppercase">Bot</span>
        </button>
        <button class="nav-btn flex flex-col items-center gap-1 text-zinc-500">
            <i class="fas fa-chart-simple text-xl"></i>
            <span class="text-[9px] font-bold uppercase">Dati</span>
        </button>
        <button class="nav-btn flex flex-col items-center gap-1 text-zinc-500">
            <i class="fas fa-user-shield text-xl"></i>
            <span class="text-[9px] font-bold uppercase">Profilo</span>
        </button>
    </nav>

    <script>
        // Funzione Navigazione
        function navigateTo(pageId) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            
            // Aggiorna icone navigazione
            document.querySelectorAll('.nav-btn').forEach(btn => {
                const label = btn.querySelector('span').innerText.toLowerCase();
                if (pageId.includes(label) || (pageId === 'home' && label === 'gen ia')) {
                    btn.classList.add('text-primary');
                    btn.classList.remove('text-zinc-500');
                } else {
                    btn.classList.add('text-zinc-500');
                    btn.classList.remove('text-primary');
                }
            });
            
            // Scroll in alto
            document.getElementById(pageId).scrollTop = 0;
        }

        // Avvio App
        function startApp() {
            document.getElementById('welcome').classList.remove('active');
            document.getElementById('main-header').classList.remove('hidden');
            document.getElementById('app-nav').classList.remove('hidden');
            navigateTo('home');
        }

        // Simulazione Generazione
        function simulateGeneration() {
            const btn = document.getElementById('gen-btn');
            const original = btn.innerHTML;
            btn.disabled = true;
            btn.innerHTML = '<i class="fas fa-spinner animate-spin"></i> Scansione in corso...';
            
            setTimeout(() => {
                btn.innerHTML = '<i class="fas fa-check"></i> Analisi Completata';
                btn.classList.replace('bg-primary', 'bg-emerald-500');
                setTimeout(() => {
                    btn.innerHTML = original;
                    btn.classList.replace('bg-emerald-500', 'bg-primary');
                    btn.disabled = false;
                }, 2000);
            }, 1500);
        }

        // Logica Bot
        let botActive = false;
        function toggleBot() {
            botActive = !botActive;
            const btn = document.getElementById('bot-toggle-btn');
            const icon = document.getElementById('bot-icon');
            const status = document.getElementById('bot-status');
            const pulse = document.getElementById('bot-pulse');

            if(botActive) {
                btn.classList.replace('bg-white/10', 'bg-emerald-500');
                btn.classList.add('text-white');
                btn.innerText = "Spegni Bot";
                icon.classList.replace('text-zinc-700', 'text-emerald-500');
                status.innerText = "Bot in Esecuzione";
                pulse.classList.add('animate-ping');
                pulse.classList.replace('scale-0', 'scale-100');
            } else {
                btn.classList.replace('bg-emerald-500', 'bg-white/10');
                btn.classList.remove('text-white');
                btn.innerText = "Attiva Automazione";
                icon.classList.replace('text-emerald-500', 'text-zinc-700');
                status.innerText = "Bot Stand-by";
                pulse.classList.remove('animate-ping');
                pulse.classList.replace('scale-100', 'scale-0');
            }
        }

        // Loader Iniziale
        window.addEventListener('load', () => {
            setTimeout(() => {
                const loader = document.getElementById('loader');
                loader.classList.add('opacity-0');
                setTimeout(() => loader.style.display = 'none', 500);
            }, 1500);
        });
    </script>
</body>
</html>
