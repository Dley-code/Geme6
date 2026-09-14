<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GAME HUB - Стабильная Версия</title>
    <style>
        :root {
            --bg-color: #1a1a1a;
            --card-bg: #2d2d2d;
            --text-color: #ffffff;
            --accent-color: #ffb703;
            --p1-color: #ff4d6d;
            --p2-color: #00b4d8;
            --dev-color: #00ff66;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        header {
            width: 100%;
            max-width: 600px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            box-sizing: border-box;
            border-bottom: 2px solid var(--card-bg);
        }

        .logo {
            cursor: pointer;
            user-select: none;
            font-weight: bold;
        }

        .balance {
            font-size: 1.2rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .ad-btn {
            background: #4caf50;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
        }

        .container {
            width: 100%;
            max-width: 600px;
            padding: 15px;
            box-sizing: border-box;
        }

        h2 {
            border-left: 4px solid var(--accent-color);
            padding-left: 10px;
            margin-top: 25px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .card:active {
            transform: scale(0.95);
        }

        .card .icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .card .title {
            font-weight: bold;
            font-size: 1.1rem;
        }

        .card .record {
            font-size: 0.85rem;
            color: #aaa;
            margin-top: 5px;
        }

        .price-tag {
            background: var(--accent-color);
            color: #000;
            padding: 2px 8px;
            border-radius: 10px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-top: 5px;
            display: inline-block;
        }

        .price-tag.owned {
            background: #4caf50;
            color: #fff;
        }

        /* Экраны */
        .screen {
            display: none;
            width: 100%;
            max-width: 600px;
            min-height: 80vh;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            box-sizing: border-box;
        }

        .screen.active {
            display: flex;
        }

        .menu-btn {
            align-self: flex-start;
            background: #555;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            margin-bottom: 20px;
        }

        /* Панель админа */
        #dev-panel {
            background: #0d0d0d;
            border: 2px dashed var(--dev-color);
            border-radius: 12px;
            padding: 15px;
            margin-top: 10px;
            margin-bottom: 20px;
            width: 100%;
            box-sizing: border-box;
            display: none;
        }
        #dev-panel h3 {
            color: var(--dev-color);
            margin-top: 0;
            font-family: monospace;
            display: flex;
            justify-content: space-between;
        }
        .dev-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
        }
        .dev-btn {
            background: #222;
            color: var(--dev-color);
            border: 1px solid var(--dev-color);
            padding: 10px;
            border-radius: 6px;
            cursor: pointer;
            font-family: monospace;
            font-weight: bold;
        }

        #ad-screen {
            justify-content: center;
            background: #000;
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            max-width: none;
            z-index: 100;
        }

        /* Интерактивная зона для теста одиночной реакции */
        .reaction-zone {
            width: 100%;
            height: 300px;
            background-color: #444;
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
            user-select: none;
            text-align: center;
            padding: 20px;
            box-sizing: border-box;
            transition: background-color 0.1s;
        }

        /* Окно дуэли */
        .duel-container {
            width: 100%;
            height: 400px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .duel-side {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
            border-radius: 10px;
            user-select: none;
        }
        #p1-side { background-color: var(--p1-color); }
        #p2-side { background-color: var(--p2-color); }
    </style>
</head>
<body>

    <!-- Экран меню -->
    <div id="hub-screen" class="screen active">
        <header>
            <div class="logo" onclick="devClickCount()">🚀 GAME HUB <span style="font-size: 0.6rem; color: #777;">v1.0.dev</span></div>
            <div style="display: flex; align-items: center; gap: 15px;">
                <button class="ad-btn" onclick="showAd()">📺 +40 🪙</button>
                <div class="balance">🪙 <span id="balance-val">0</span></div>
            </div>
        </header>

        <div class="container">
            <!-- Панель админа -->
            <div id="dev-panel">
                <h3>⚙️ REGM_DEV // АДМИНКА <span style="cursor:pointer;" onclick="toggleDevPanel()">[X]</span></h3>
                <div class="dev-grid">
                    <button class="dev-btn" onclick="devAddCoins()">🪙 +1000 МОНЕТ</button>
                    <button class="dev-btn" onclick="devUnlockAll()">🔓 ОТКРЫТЬ ВСЕ ИГРЫ</button>
                    <button class="dev-btn" onclick="devResetRecords()">🔄 СБРОСИТЬ ВСЁ</button>
                    <button class="dev-btn" onclick="devMaxReaction()">⚡ ЧИТ РЕАКЦИИ (1мс)</button>
                </div>
            </div>

            <h2>🎮 Бесплатные игры</h2>
            <div class="grid">
                <div class="card" onclick="startReactionGame()">
                    <div class="icon">⚡</div>
                    <div class="title">Реакция</div>
                    <div class="record">Лучшее: <span id="rec-reaction">---</span> мс</div>
                </div>
                <div class="card" onclick="alert('Игра в разработке!')">
                    <div class="icon">💎</div>
                    <div class="title">3 в ряд</div>
                    <div class="record">Рекорд: 0</div>
                </div>
            </div>

            <h2>💎 Премиум игры</h2>
            <div class="grid">
                <div class="card" onclick="buyOrPlay('shooter', 200)">
                    <div class="icon">🚀</div>
                    <div class="title">Космический Шутер</div>
                    <div class="price-tag" id="price-shooter">🪙 200</div>
                </div>
                <div class="card" onclick="buyOrPlay('tetris', 250)">
                    <div class="icon">🧊</div>
                    <div class="title">Тетрис</div>
                    <div class="price-tag" id="price-tetris">🪙 250</div>
                </div>
            </div>

            <h2>👥 Игры на двоих</h2>
            <div class="grid">
                <div class="card" onclick="startDuelReaction()">
                    <div class="icon">⚔️</div>
                    <div class="title">Реакция-дуэль</div>
                    <div class="record">П1: <span id="duel-p1-wins">0</span> | П2: <span id="duel-p2-wins">0</span></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Экран рекламы -->
    <div id="ad-screen" class="screen">
        <h2>📺 Реклама</h2>
        <p>Канал: <b>Dley перезаливы</b> · VK Video</p>
        <p>Осталось: <span id="ad-timer">15</span> секунд...</p>
        <button id="ad-close-btn" class="menu-btn" style="display:none; align-self:center;" onclick="closeAd()">Забрать 40 🪙</button>
    </div>

    <!-- Экран игры: Одиночная Реакция -->
    <div id="reaction-screen" class="screen">
        <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
        <div style="margin-bottom: 15px; font-size: 1.1rem; text-align: center;">Нажмите на панель ниже, чтобы начать тест.</div>
        
        <div id="reaction-click-zone" class="reaction-zone" onclick="handleReactionTap()">
            НАЖМИТЕ ДЛЯ СТАРТА
        </div>
    </div>

    <!-- Экран игры: Реакция-Дуэль -->
    <div id="duel-screen" class="screen">
        <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
        <div style="margin-bottom: 15px; text-align: center;">
            Когда появится цвет — жми! Кто раньше — тот победил.
        </div>
        <div class="duel-container">
            <div class="duel-side" id="p1-side" onclick="duelTap(1)">ИГРОК 1</div>
            <div class="duel-side" id="p2-side" onclick="duelTap(2)">ИГРОК 2</div>
        </div>
    </div>

    <script>
        // ===== СОСТОЯНИЕ =====
        const state = {
            balance: 0,
            owned: {},          // { shooter: true, tetris: false }
            records: {
                reaction: null
            },
            duelWins: { p1: 0, p2: 0 },
            devClicks: 0
        };

        // ===== LOCALSTORAGE =====
        function save() {
            localStorage.setItem('gamehub_state', JSON.stringify(state));
        }
        function load() {
            try {
                const raw = localStorage.getItem('gamehub_state');
                if (raw) {
                    const parsed = JSON.parse(raw);
                    Object.assign(state, parsed);
                }
            } catch (e) { console.warn('Save load error', e); }
        }
        load();

        // ===== UI =====
        function updateUI() {
            document.getElementById('balance-val').textContent = state.balance;

            // Рекорд реакции
            const recEl = document.getElementById('rec-reaction');
            recEl.textContent = state.records.reaction ? state.records.reaction : '---';

            // Дуэль
            document.getElementById('duel-p1-wins').textContent = state.duelWins.p1;
            document.getElementById('duel-p2-wins').textContent = state.duelWins.p2;

            // Цены / статус покупки
            ['shooter', 'tetris'].forEach(id => {
                const el = document.getElementById('price-' + id);
                if (!el) return;
                if (state.owned[id]) {
                    el.textContent = '✅ Куплено';
                    el.classList.add('owned');
                } else {
                    el.textContent = id === 'shooter' ? '🪙 200' : '🪙 250';
                    el.classList.remove('owned');
                }
            });
        }

        function showScreen(id) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function backToMenu() {
            // Сброс игровых таймеров
            if (reactionTimer) { clearTimeout(reactionTimer); reactionTimer = null; }
            if (duelTimer) { clearTimeout(duelTimer); duelTimer = null; }
            reactionState = 'idle';
            duelState = 'idle';
            updateUI();
            showScreen('hub-screen');
        }

        // ===== РЕКЛАМА =====
        let adInterval = null;
        let adSeconds = 15;

        function showAd() {
            adSeconds = 15;
            document.getElementById('ad-timer').textContent = adSeconds;
            document.getElementById('ad-close-btn').style.display = 'none';
            showScreen('ad-screen');

            adInterval = setInterval(() => {
                adSeconds--;
                document.getElementById('ad-timer').textContent = adSeconds;
                if (adSeconds <= 0) {
                    clearInterval(adInterval);
                    adInterval = null;
                    document.getElementById('ad-close-btn').style.display = 'inline-block';
                }
            }, 1000);
        }

        function closeAd() {
            if (adInterval) { clearInterval(adInterval); adInterval = null; }
            state.balance += 40;
            save();
            updateUI();
            showScreen('hub-screen');
        }

        // ===== ДЕВ-ПАНЕЛЬ =====
        function devClickCount() {
            state.devClicks++;
            if (state.devClicks >= 5) {
                state.devClicks = 0;
                toggleDevPanel();
            }
        }

        function toggleDevPanel() {
            const p = document.getElementById('dev-panel');
            p.style.display = (p.style.display === 'block') ? 'none' : 'block';
        }

        function devAddCoins() {
            state.balance += 1000;
            save(); updateUI();
        }

        function devUnlockAll() {
            state.owned.shooter = true;
            state.owned.tetris = true;
            save(); updateUI();
        }

        function devResetRecords() {
            state.balance = 0;
            state.owned = {};
            state.records = { reaction: null };
            state.duelWins = { p1: 0, p2: 0 };
            save(); updateUI();
            alert('Всё сброшено!');
        }

        function devMaxReaction() {
            state.records.reaction = 1;
            save(); updateUI();
            alert('Чит активирован: рекорд 1 мс');
        }

        // ===== ПОКУПКА / ИГРА =====
        function buyOrPlay(id, price) {
            if (state.owned[id]) {
                alert('Игра "' + id + '" уже куплена! (в разработке)');
                return;
            }
            if (state.balance < price) {
                alert('Недостаточно монет! Нужно ' + price + ', у вас ' + state.balance);
                return;
            }
            if (confirm('Купить игру за ' + price + ' 🪙?')) {
                state.balance -= price;
                state.owned[id] = true;
                save(); updateUI();
                alert('Покупка успешна! Игра в разработке 🚧');
            }
        }

        // ===== ИГРА: ОДИНОЧНАЯ РЕАКЦИЯ =====
        let reactionState = 'idle'; // idle | waiting | ready | result
        let reactionTimer = null;
        let reactionStart = 0;

        function startReactionGame() {
            reactionState = 'idle';
            const zone = document.getElementById('reaction-click-zone');
            zone.style.backgroundColor = '#444';
            zone.textContent = 'НАЖМИТЕ ДЛЯ СТАРТА';
            showScreen('reaction-screen');
        }

        function handleReactionTap() {
            const zone = document.getElementById('reaction-click-zone');

            if (reactionState === 'idle') {
                // Старт: ждём случайное время
                reactionState = 'waiting';
                zone.style.backgroundColor = '#8b0000';
                zone.textContent = 'ЖДИТЕ ЗЕЛЁНОГО...';

                const delay = 1000 + Math.random() * 3000;
                reactionTimer = setTimeout(() => {
                    reactionState = 'ready';
                    reactionStart = performance.now();
                    zone.style.backgroundColor = '#00c853';
                    zone.textContent = 'ЖМИ!!!';
                }, delay);

            } else if (reactionState === 'waiting') {
                // Слишком рано
                clearTimeout(reactionTimer);
                reactionTimer = null;
                reactionState = 'idle';
                zone.style.backgroundColor = '#444';
                zone.textContent = 'СЛИШКОМ РАНО! Нажмите, чтобы попробовать снова.';

            } else if (reactionState === 'ready') {
                const time = Math.round(performance.now() - reactionStart);
                reactionState = 'result';
                zone.style.backgroundColor = '#444';
                zone.textContent = '⏱ ' + time + ' мс — нажмите для следующей попытки';

                if (!state.records.reaction || time < state.records.reaction) {
                    state.records.reaction = time;
                    save();
                    zone.textContent = '🏆 НОВЫЙ РЕКОРД: ' + time + ' мс — нажмите ещё';
                }
                updateUI();

            } else if (reactionState === 'result') {
                // Новая попытка
                reactionState = 'idle';
                zone.style.backgroundColor = '#444';
                zone.textContent = 'НАЖМИТЕ ДЛЯ СТАРТА';
            }
        }

        // ===== ИГРА: ДУЭЛЬ РЕАКЦИИ =====
        let duelState = 'idle'; // idle | waiting | ready | roundEnd
        let duelTimer = null;
        let duelStart = 0;
        let duelWinner = null;

        function startDuelReaction() {
            duelState = 'idle';
            duelWinner = null;
            resetDuelColors();
            setDuelText('ИГРОК 1', 'ИГРОК 2');
            showScreen('duel-screen');
        }

        function resetDuelColors() {
            document.getElementById('p1-side').style.backgroundColor = 'var(--p1-color)';
            document.getElementById('p2-side').style.backgroundColor = 'var(--p2-color)';
        }

        function setDuelText(t1, t2) {
            document.getElementById('p1-side').textContent = t1;
            document.getElementById('p2-side').textContent = t2;
        }

        function duelTap(player) {
            const p1 = document.getElementById('p1-side');
            const p2 = document.getElementById('p2-side');

            if (duelState === 'idle') {
                // Старт раунда
                duelState = 'waiting';
                duelWinner = null;
                p1.style.backgroundColor = '#333';
                p2.style.backgroundColor = '#333';
                setDuelText('ЖДИТЕ...', 'ЖДИТЕ...');

                const delay = 1500 + Math.random() * 3000;
                duelTimer = setTimeout(() => {
                    duelState = 'ready';
                    duelStart = performance.now();
                    resetDuelColors();
                    setDuelText('ЖМИ!', 'ЖМИ!');
                }, delay);

            } else if (duelState === 'waiting') {
                // Фальстарт
                clearTimeout(duelTimer);
                duelTimer = null;
                duelState = 'idle';
                resetDuelColors();
                setDuelText('ФАЛЬСТАРТ! Игрок ' + player, 'Жмите, чтобы заново');
                setTimeout(() => {
                    if (duelState === 'idle') {
                        setDuelText('ИГРОК 1', 'ИГРОК 2');
                    }
                }, 1200);

            } else if (duelState === 'ready') {
                const time = Math.round(performance.now() - duelStart);
                duelState = 'roundEnd';
                duelWinner = player;

                if (player === 1) {
                    state.duelWins.p1++;
                    setDuelText('🏆 ПОБЕДА! (' + time + 'мс)', 'Проиграл');
                    p2.style.backgroundColor = '#333';
                } else {
                    state.duelWins.p2++;
                    setDuelText('Проиграл', '🏆 ПОБЕДА! (' + time + 'мс)');
                    p1.style.backgroundColor = '#333';
                }
                save();
                updateUI();

            } else if (duelState === 'roundEnd') {
                // Следующий раунд
                duelState = 'idle';
                duelWinner = null;
                resetDuelColors();
                setDuelText('ИГРОК 1', 'ИГРОК 2');
            }
        }

        // ===== ИНИЦИАЛИЗАЦИЯ =====
        updateUI();
    </script>
</body>
</html>
