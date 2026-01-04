# Neural-x1-ultra4<!DOCTYPE html>
<html class="dark" lang="it">
<head>
    <meta charset="utf-8"/>
    <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
    <title>AI Bet Generator - Neural X-1</title>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Noto+Sans:wght@400;500;700&display=swap" rel="stylesheet"/>
    <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet"/>
    <script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
    <script id="tailwind-config">
        tailwind.config = {
            darkMode: "class",
            theme: {
                extend: {
                    colors: {
                        "primary": "#135bec",
                        "background-light": "#f6f6f8",
                        "background-dark": "#101622",
                        "card-dark": "#1a2230",
                    },
                    fontFamily: {
                        "display": ["Space Grotesk", "sans-serif"],
                        "body": ["Noto Sans", "sans-serif"],
                    },
                    borderRadius: {"DEFAULT": "0.25rem", "md": "0.375rem", "lg": "0.5rem", "xl": "0.75rem", "2xl": "1rem", "full": "9999px"},
                },
            },
        }
    </script>
    <style>
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #101622; }
        ::-webkit-scrollbar-thumb { background: #232f48; border-radius: 4px; }
        .scanning-line {
            position: absolute; inset: 0;
            background: linear-gradient(to bottom, transparent, rgba(19,91,236,0.2), transparent);
            animation: scan 2s linear infinite; pointer-events: none;
        }
        @keyframes scan { 0% { transform: translateY(-100%); } 100% { transform: translateY(200%); } }
    </style>
</head>
<body class="bg-background-light dark:bg-background-dark text-slate-900 dark:text-white font-display antialiased min-h-screen flex flex-col overflow-x-hidden">

    <!-- Header -->
    <div class="sticky top-0 z-50 bg-background-light/95 dark:bg-background-dark/95 backdrop-blur-md border-b border-gray-200 dark:border-gray-800">
        <div class="flex items-center p-4 justify-between max-w-md mx-auto w-full">
            <div class="flex items-center gap-3">
                <div class="flex items-center justify-center size-10 rounded-full bg-primary/10 text-primary">
                    <span class="material-symbols-outlined text-[24px]">smart_toy</span>
                </div>
                <div>
                    <h2 class="text-lg font-bold leading-none tracking-tight uppercase italic">Neural<span class="text-primary">X1</span></h2>
                    <p id="system-status-sub" class="text-[10px] text-slate-500 font-medium uppercase mt-1">v2.5.0 • Pronto</p>
                </div>
            </div>
            <button onclick="location.reload()" class="flex items-center justify-center size-10 rounded-full hover:bg-slate-200 dark:hover:bg-slate-800 transition-colors">
                <span class="material-symbols-outlined text-slate-600 dark:text-slate-300">sync</span>
            </button>
        </div>
    </div>

    <!-- Main Content -->
    <main class="flex-1 flex flex-col max-w-md mx-auto w-full p-4 gap-6">
        
        <!-- Status Terminal -->
        <div class="w-full rounded-xl overflow-hidden relative group" id="status-terminal">
            <div class="absolute inset-0 bg-primary/5"></div>
            <div class="absolute inset-0 border border-primary/30 rounded-xl"></div>
            <div class="relative p-5 flex flex-col gap-3">
                <div class="flex justify-between items-center border-b border-primary/20 pb-2">
                    <div class="flex items-center gap-2">
                        <span id="status-dot" class="flex size-2 rounded-full bg-green-500"></span>
                        <span class="text-[10px] font-bold tracking-widest text-primary uppercase">Neural Terminal</span>
                    </div>
                </div>
                <div id="terminal-text" class="flex flex-col gap-1">
                    <p class="font-mono text-[11px] text-slate-400">&gt; Scansione ADM attiva...</p>
                    <p id="status-msg" class="font-mono text-[11px] text-primary font-semibold italic">&gt; Seleziona i campionati e genera schedina.</p>
                </div>
            </div>
        </div>

        <!-- AI Slip Result (Hidden initially) -->
        <div id="result-container" class="hidden animate-in fade-in slide-in-from-top-4 duration-500">
             <div id="result-content" class="bg-primary/5 border border-primary/20 rounded-2xl p-5 text-sm font-body leading-relaxed whitespace-pre-line text-slate-300"></div>
        </div>

        <!-- Bet Type Toggle -->
        <div>
            <h3 class="text-[10px] font-bold text-slate-500 uppercase tracking-[0.2em] mb-3 px-1">Bet Logic</h3>
            <div class="flex p-1 bg-slate-200 dark:bg-[#1a2230] rounded-xl relative">
                <label class="flex-1 relative cursor-pointer group text-center">
                    <input checked="" class="peer sr-only" name="bet_type" type="radio" value="double"/>
                    <div class="py-2.5 rounded-lg text-xs font-bold transition-all text-slate-500 peer-checked:bg-primary peer-checked:text-white">Doppia</div>
                </label>
                <label class="flex-1 relative cursor-pointer group text-center">
                    <input class="peer sr-only" name="bet_type" type="radio" value="triple"/>
                    <div class="py-2.5 rounded-lg text-xs font-bold transition-all text-slate-500 peer-checked:bg-primary peer-checked:text-white">Tripla</div>
                </label>
            </div>
        </div>

        <!-- League Selection Grid -->
        <div>
            <h3 class="text-[10px] font-bold text-slate-500 uppercase tracking-[0.2em] mb-3 px-1">Select Markets</h3>
            <div class="grid grid-cols-2 gap-3" id="leagues-grid">
                <!-- Serie A -->
                <label class="relative cursor-pointer group league-item" data-id="soccer_italy_serie_a">
                    <input checked="" class="peer sr-only" type="checkbox"/>
                    <div class="relative overflow-hidden rounded-xl border-2 border-transparent bg-slate-100 dark:bg-[#1a2230] transition-all peer-checked:border-primary">
                        <div class="h-20 w-full bg-cover bg-center" style='background-image: linear-gradient(0deg, rgba(0, 0, 0, 0.7) 0%, rgba(0, 0, 0, 0) 100%), url("https://lh3.googleusercontent.com/aida-public/AB6AXuDZomcCRnaqot_C_u-IwZyvUVBPbiCTXoswcrNTOKe88uUAGMMv_ev_xGSbVzNHIIwYqL6snVobjZg04Ti-ZFSefhIQH7Gj8HTZ1HQq6vVVQg-rZwG-hVBJCsqOiVPZXdt2wFdm9JM5uWwk1COWIhfGyrygcPZPEqbkKz9IKJG4x3ZB8Qt4Jg5MClHevK_s4CtvfFXTXENapgNUEj2icNkve4n6selj_uu3IQMmw53ja0W4-CZ56msej6GjmQQLLEP01Twfa_mMA7tN");'></div>
                        <div class="p-3"><p class="font-bold text-xs dark:text-white">Serie A</p></div>
                    </div>
                </label>
                <!-- Premier -->
                <label class="relative cursor-pointer group league-item" data-id="soccer_epl">
                    <input checked="" class="peer sr-only" type="checkbox"/>
                    <div class="relative overflow-hidden rounded-xl border-2 border-transparent bg-slate-100 dark:bg-[#1a2230] transition-all peer-checked:border-primary">
                        <div class="h-20 w-full bg-cover bg-center" style='background-image: linear-gradient(0deg, rgba(0, 0, 0, 0.7) 0%, rgba(0, 0, 0, 0) 100%), url("https://lh3.googleusercontent.com/aida-public/AB6AXuCaXDV5sHUrDVD38K5PurcNienmfBcx0TFm6-duXsVIPokJ96-jwUHHLyZHDpNOBP8yXsTcK9wtJ0U9eVFVJUskZTJrEy4vmdYKC-02vugGhkG5VZpqziJsiUmWlAxdXopldHPeEEad5nMD1W0cGH5LmMWE-OKZ-qzs1jGFEX3pBtD0RFPN3UADPQ0UEYsrB7Mv8MvQ823dDJQT6iBs0VoQ-SYIBnhDSzSnagv6wV9xtuC2Bn-D30HCpnpo5AZalGIV-4TXBHJPJIAU");'></div>
                        <div class="p-3"><p class="font-bold text-xs dark:text-white">Premier Lg</p></div>
                    </div>
                </label>
                <!-- La Liga -->
                <label class="relative cursor-pointer group league-item" data-id="soccer_spain_la_liga">
                    <input checked="" class="peer sr-only" type="checkbox"/>
                    <div class="relative overflow-hidden rounded-xl border-2 border-transparent bg-slate-100 dark:bg-[#1a2230] transition-all peer-checked:border-primary">
                        <div class="h-20 w-full bg-cover bg-center" style='background-image: linear-gradient(0deg, rgba(0, 0, 0, 0.7) 0%, rgba(0, 0, 0, 0) 100%), url("https://lh3.googleusercontent.com/aida-public/AB6AXuCGeocIrKDIzFNdoadhh9kUHdlYpnLDrIb1TV8_KDdMJAySIF8da1a_457Ak9aMmBF2PwlbXvldMnd8S3NahgYId_4eB2k9mkDkgwk8qi_qPgxcQYzo9rYrkHstIU2iN8oPY1-Qy_zj4FdIX5lW1vgcQ-XW7CW-pv2QWhIlC1bd0gRCt7romrNDrs1Zyzt7D2vPPcIjPPzmkissv-wXJaGgYRot8bKkuSbT4KcO2oan7oM0t6_BLzyIEOg-l7OsxlSo9nrQV6afk42b");'></div>
                        <div class="p-3"><p class="font-bold text-xs dark:text-white">La Liga</p></div>
                    </div>
                </label>
                <!-- Bundesliga -->
                <label class="relative cursor-pointer group league-item" data-id="soccer_germany_bundesliga">
                    <input checked="" class="peer sr-only" type="checkbox"/>
                    <div class="relative overflow-hidden rounded-xl border-2 border-transparent bg-slate-100 dark:bg-[#1a2230] transition-all peer-checked:border-primary">
                        <div class="h-20 w-full bg-cover bg-center" style='background-image: linear-gradient(0deg, rgba(0, 0, 0, 0.7) 0%, rgba(0, 0, 0, 0) 100%), url("https://lh3.googleusercontent.com/aida-public/AB6AXuC5ebRGjxy4vUgWTi3BZaaR-zolfrvi23BukOyg3Kd-vMcI86hWaYYWPpBlv0ew0i84nT2FaufDGszIP7Nc50pbmGcurpammsBx3SodeS3CSiQVPnuQwvZT8mgOu9B6Pe1wi3DTmv0bOVTOsi2Nf1EF3ObZCODmXDpsOGlXJhJ7gFcnoGk1au5xrNBEs7j0r6HjEx_GDVpq2co8XW3R7Sollr-tzdvEn32FvW45fh1KQQuc9JwP46OwUXVPc70H9mAm8HCeaFl5llt9");'></div>
                        <div class="p-3"><p class="font-bold text-xs dark:text-white">Bundesliga</p></div>
                    </div>
                </label>
            </div>
        </div>

        <div class="h-32"></div>
    </main>

    <!-- Bottom Action Bar -->
    <div class="fixed bottom-0 left-0 right-0 z-40 bg-gradient-to-t from-background-dark via-background-dark to-transparent pt-12 pb-8 px-4">
        <div class="max-w-md mx-auto w-full flex flex-col gap-3">
            <button id="generateBtn" onclick="generateAISlip()" class="relative w-full overflow-hidden rounded-2xl bg-primary hover:bg-blue-600 active:scale-[0.98] transition-all group shadow-lg shadow-primary/30">
                <div class="relative flex items-center justify-center py-4 px-6 gap-3">
                    <span class="material-symbols-outlined text-white animate-pulse">auto_awesome</span>
                    <span class="text-white text-lg font-bold tracking-wide uppercase">Generate AI Slip</span>
                </div>
            </button>
            <button onclick="resetUI()" class="text-[10px] font-bold text-slate-500 uppercase py-2 flex items-center justify-center gap-2">
                <span class="material-symbols-outlined text-[16px]">restart_alt</span> Reset Filters
            </button>
        </div>
    </div>

    <script>
        const apiKey = ""; 
        const ODDS_API_KEY = "f31093dd321254076707f7bcb1fd2234";

        async function generateAISlip() {
            const btn = document.getElementById('generateBtn');
            const statusMsg = document.getElementById('status-msg');
            const statusDot = document.getElementById('status-dot');
            const terminal = document.getElementById('status-terminal');
            const resultBox = document.getElementById('result-container');
            const resultContent = document.getElementById('result-content');

            // 1. UI Loading State
            btn.disabled = true;
            statusDot.classList.replace('bg-green-500', 'bg-amber-500');
            statusMsg.innerHTML = "&gt; Scansione cross-league in corso...";
            terminal.classList.add('scanning-active');
            terminal.insertAdjacentHTML('beforeend', '<div class="scanning-line"></div>');

            // 2. Rileva leghe selezionate
            const selectedLeagues = Array.from(document.querySelectorAll('.league-item')).filter(i => i.querySelector('input').checked).map(i => i.dataset.id);
            const betType = document.querySelector('input[name="bet_type"]:checked').value;

            try {
                // 3. Fetch dati
                const promises = selectedLeagues.map(l => fetch(`https://api.the-odds-api.com/v4/sports/${l}/odds/?apiKey=${ODDS_API_KEY}&regions=eu&markets=h2h`).then(r => r.json()));
                const results = await Promise.all(promises);
                const matches = results.flat().slice(0, 15);

                statusMsg.innerHTML = "&gt; Elaborazione Neural Network...";

                // 4. Analisi IA
                const systemPrompt = "Sei Neural X-1. Crea schedine ADM a basso rischio (1X, X2, Over 1.5, Goal Casa) incrociando i campionati. Indica sempre Bookmaker ADM italiani (SNAI, Sisal, Eurobet).";
                const userPrompt = `Dati: ${JSON.stringify(matches.map(m => ({league: m.sport_title, t: m.home_team + " vs " + m.away_team, q: m.bookmakers[0]?.markets[0].outcomes})))}. Genera una ${betType.toUpperCase()} schematica.`;

                const aiRes = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ 
                        contents: [{ parts: [{ text: userPrompt }] }],
                        systemInstruction: { parts: [{ text: systemPrompt }] }
                    })
                });

                const data = await aiRes.json();
                const text = data.candidates?.[0]?.content?.parts?.[0]?.text || "Errore elaborazione. Riprova.";

                // 5. Display Result
                statusMsg.innerHTML = "&gt; Schedina generata con successo.";
                statusDot.classList.replace('bg-amber-500', 'bg-green-500');
                
                resultBox.classList.remove('hidden');
                resultContent.innerHTML = `<div class="flex items-center gap-2 mb-3 text-primary"><span class="material-symbols-outlined text-sm">verified</span><span class="text-[10px] font-black uppercase tracking-widest">Analisi Completata</span></div>${text}`;
                
                window.scrollTo({ top: 0, behavior: 'smooth' });

            } catch (e) {
                statusMsg.innerHTML = "&gt; Errore critico nel collegamento API.";
                statusDot.classList.replace('bg-amber-500', 'bg-red-500');
            } finally {
                btn.disabled = false;
                document.querySelector('.scanning-line')?.remove();
            }
        }

        function resetUI() {
            document.getElementById('result-container').classList.add('hidden');
            document.getElementById('status-msg').innerHTML = "&gt; Seleziona i campionati e genera schedina.";
            document.querySelectorAll('.league-item input').forEach(i => i.checked = true);
        }
    </script>
</body>
</html>
