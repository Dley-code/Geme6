Ыыыыыыы:
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

Ыыыыыыы:
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

Ыыыыыыы:
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
