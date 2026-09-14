<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GAME HUB</title>
<style>
    :root {
        --bg-1: #0f0c1d;
        --bg-2: #1a1030;
        --card-bg: #1e1b2e;
        --card-bg-2: #252139;
        --text-color: #ffffff;
        --text-muted: #8a86a3;
        --accent-color: #ffb703;
        --p1-color: #ff4d6d;
        --p2-color: #00b4d8;
        --dev-color: #00ff66;
    }

    * { box-sizing: border-box; }

    body {
        margin: 0;
        padding: 0;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: radial-gradient(circle at 20% 0%, #2a1b4d 0%, var(--bg-1) 45%, #06040f 100%);
        background-attachment: fixed;
        color: var(--text-color);
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100vh;
        user-select: none;
    }

    header {
        width: 100%;
        max-width: 600px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 18px 16px 10px;
    }

    .logo {
        cursor: pointer;
        font-weight: 900;
        font-size: 1.5rem;
        letter-spacing: 1px;
        background: linear-gradient(90deg,#ff4d6d,#ffb703,#00ff66,#00b4d8,#a855f7);
        -webkit-background-clip: text;
        background-clip: text;
        -webkit-text-fill-color: transparent;
        position: relative;
        padding-bottom: 10px;
    }

    .dev-dots {
        position: absolute;
        bottom: 0; left: 0;
        display: flex; gap: 4px;
    }
    .dev-dots span {
        width: 6px; height: 6px; border-radius: 50%;
        background: rgba(255,255,255,0.15);
        transition: background 0.2s;
    }
    .dev-dots span.on { background: var(--dev-color); box-shadow: 0 0 6px var(--dev-color); }

    .balance {
        font-size: 1rem;
        font-weight: bold;
        display: flex;
        align-items: center;
        gap: 6px;
        background: rgba(255, 183, 3, 0.12);
        border: 1px solid rgba(255, 183, 3, 0.45);
        padding: 8px 16px;
        border-radius: 20px;
        color: var(--accent-color);
    }

    .container {
        width: 100%;
        max-width: 600px;
        padding: 0 16px 40px;
    }

    /* Реклама */
    .ad-card {
        display: flex;
        align-items: center;
        gap: 14px;
        background: linear-gradient(135deg, #6d28d9 0%, #a21caf 100%);
        border-radius: 18px;
        padding: 14px;
        margin-bottom: 18px;
        cursor: pointer;
        box-shadow: 0 8px 24px rgba(124, 58, 237, 0.35);
        transition: transform 0.15s;
    }
    .ad-card:active { transform: scale(0.98); }
    .ad-icon {
        font-size: 2rem;
        background: rgba(255,255,255,0.15);
        width: 50px; height: 50px;
        border-radius: 12px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
    }
    .ad-info { flex: 1; min-width: 0; }
    .ad-title { font-weight: 700; font-size: 0.95rem; margin-bottom: 2px; }
    .ad-sub { font-size: 0.75rem; color: rgba(255,255,255,0.75); }
    .ad-reward {
        background: var(--accent-color);
        color: #1a1030;
        font-weight: 800;
        font-size: 0.85rem;
        padding: 8px 14px;
        border-radius: 20px;
        flex-shrink: 0;
    }

    /* Табы */
    .tabs {
        display: flex;
        gap: 10px;
        background: rgba(255,255,255,0.04);
        border: 1px solid rgba(255,255,255,0.06);
        border-radius: 16px;
        padding: 6px;
        margin-bottom: 20px;
    }
    .tab {
        flex: 1;
        text-align: center;
        padding: 12px;
        border-radius: 12px;
        font-weight: 700;
        font-size: 0.95rem;
        cursor: pointer;
        color: var(--text-muted);
        transition: all 0.2s;
    }
    .tab.active {
        background: linear-gradient(135deg, #1f7a4d, #145a37);
        color: #fff;
    }

    .section-title {
        font-size: 0.78rem;
        font-weight: 700;
        letter-spacing: 1.5px;
        text-transform: uppercase;
        color: var(--text-muted);
        margin: 22px 0 12px;
        display: flex;
        align-items: center;
        gap: 12px;
    }
    .section-title::after {
        content: '';
        flex: 1;
        height: 1px;
        background: linear-gradient(90deg, rgba(255,255,255,0.12), transparent);
    }

    /* Карточки игр */
    .game-list { display: flex; flex-direction: column; gap: 12px; }

    .game-card {
        display: flex;
        align-items: center;
        gap: 14px;
        background: linear-gradient(135deg, var(--card-bg-2), var(--card-bg));
        border-radius: 16px;
        padding: 16px;
        cursor: pointer;
        position: relative;
        overflow: hidden;
        transition: transform 0.15s;
        border: 1px solid rgba(255,255,255,0.05);
    }
    .game-card:active { transform: scale(0.98); }

    .game-card::before {
        content: '';
        position: absolute;
        left: 0; top: 0; bottom: 0;
        width: 4px;
        border-radius: 0 4px 4px 0;
    }
    .game-card.c-green::before { background: #00ff66; box-shadow: 0 0 12px #00ff66; }
    .game-card.c-orange::before { background: #ff9500; box-shadow: 0 0 12px #ff9500; }
    .game-card.c-purple::before { background: #a855f7; box-shadow: 0 0 12px #a855f7; }
    .game-card.c-cyan::before { background: #00b4d8; box-shadow: 0 0 12px #00b4d8; }
    .game-card.c-red::before { background: #ff4d6d; box-shadow: 0 0 12px #ff4d6d; }
    .game-card.c-yellow::before { background: #ffb703; box-shadow: 0 0 12px #ffb703; }

    .game-info { flex: 1; min-width: 0; }
    .game-name { font-weight: 700; font-size: 1.05rem; margin-bottom: 4px; }
    .game-record { font-size: 0.82rem; color: var(--text-muted); }
    .game-icon {
        font-size: 2rem;
        flex-shrink: 0;
        filter: drop-shadow(0 2px 6px rgba(0,0,0,0.4));
    }
    .game-card.locked { opacity: 0.75; }
    .game-card .lock-price {
        position: absolute;
        top: 10px; right: 10px;
        background: var(--accent-color);
        color: #1a1030;
        font-size: 0.7rem;
        font-weight: 800;
        padding: 3px 8px;
        border-radius: 8px;
    }

    /* Экраны */
    .screen {
        display: none;
        width: 100%;
        max-width: 600px;
        min-height: 80vh;
        flex-direction: column;
        align-items: center;
        padding: 20px 16px;
    }
    .screen.active { display: flex; }

    .menu-btn {
        align-self: flex-start;
        background: rgba(255,255,255,0.1);
        color: #fff;
        border: none;
        padding: 10px 18px;
        border-radius: 10px;
        cursor: pointer;
        margin-bottom: 20px;
        font-weight: 600;
    }

    /* Модалка пароля */
    .modal-overlay {
        display: none;
        position: fixed;
        inset: 0;
        background: rgba(0,0,0,0.8);
        z-index: 200;
        justify-content: center;
        align-items: center;
        padding: 20px;
    }
    .modal-overlay.active { display: flex; }
    .modal {
        background: #0d0d0d;
        border: 2px dashed var(--dev-color);
        border-radius: 16px;
        padding: 24px;
        max-width: 340px;
        width: 100%;
        text-align: center;
        font-family: monospace;
    }
    .modal h3 { color: var(--dev-color); margin: 0 0 16px; }
    .modal input {
        width: 100%;
        padding: 12px;
        background: #1a1a1a;
        border: 1px solid var(--dev-color);
        color: var(--dev-color);
        border-radius: 8px;
        font-size: 1.2rem;
        text-align: center;
        letter-spacing: 4px;
        margin-bottom: 12px;
        font-family: monospace;
    }
    .modal input:focus { outline: none; box-shadow: 0 0 8px var(--dev-color); }
    .modal .row { display: flex; gap: 8px; }
    .modal button {
        flex: 1;
        padding: 10px;
        border-radius: 8px;
        border: 1px solid var(--dev-color);
        background: #222;
        color: var(--dev-color);
        cursor: pointer;
        font-weight: 700;
        font-family: monospace;
    }
    .modal button.cancel {
        border-color: #666;
        color: #aaa;
    }
    .modal .err { color: #ff4d6d; font-size: 0.8rem; height: 16px; margin-bottom: 8px; }

    /* Админ панель */
    #dev-panel {
        background: #0d0d0d;
        border: 2px dashed var(--dev-color);
        border-radius: 12px;
        padding: 15px;
        margin-bottom: 20px;
        display: none;
    }
    #dev-panel h3 {
        color: var(--dev-color);
        margin: 0 0 12px;
        font-family: monospace;
        display: flex;
        justify-content: space-between;
        font-size: 0.9rem;
    }
    .dev-grid { display: grid; grid-template-columns: repeat(2,1fr); gap: 8px; }
    .dev-btn {
        background: #222;
        color: var(--dev-color);
        border: 1px solid var(--dev-color);
        padding: 10px 8px;
        border-radius: 6px;
        cursor: pointer;
        font-family: monospace;
        font-weight: bold;
        font-size: 0.75rem;
    }

    /* Реакция */
    .reaction-zone {
        width: 100%; height: 300px;
        background-color: #444;
        border-radius: 16px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.3rem;
        font-weight: bold;
        cursor: pointer;
        text-align: center;
        padding: 20px;
        transition: background-color 0.1s;
    }

    /* Дуэль */
    .duel-container { width: 100%; height: 400px; display: flex; flex-direction: column; gap: 10px; }
    .duel-side {
        flex: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.4rem;
        font-weight: bold;
        cursor: pointer;
        border-radius: 12px;
    }
    #p1-side { background-color: var(--p1-color); }
    #p2-side { background-color: var(--p2-color); }

    /* Игровые поля */
    #game-canvas {
        background: #0a0a14;
        border-radius: 12px;
        display: block;
        margin: 0 auto;
        touch-action: none;
        max-width: 100%;
    }
    .game-header {
        display: flex;
        justify-content: space-between;
        width: 100%;
        max-width: 360px;
        margin-bottom: 12px;
        font-weight: 700;
    }
    .game-header span { color: var(--accent-color); }

    /* 2048 */
    #grid-2048 {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 8px;
        background: #1a1030;
        padding: 8px;
        border-radius: 12px;
        width: 100%;
        max-width: 360px;
        aspect-ratio: 1;
    }
    .tile-2048 {
        background: #2d2547;
        border-radius: 8px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-weight: 800;
        font-size: 1.4rem;
        color: #fff;
        transition: all 0.15s;
    }

    /* 3 в ряд */
    #grid-3row {
        display: grid;
        grid-template-columns: repeat(7, 1fr);
        gap: 4px;
        width: 100%;
        max-width: 360px;
        aspect-ratio: 7/8;
        background: #1a1030;
        padding: 6px;
        border-radius: 12px;
    }
    .cell-3row {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.5rem;
        border-radius: 6px;
        cursor: pointer;
        background: rgba(255,255,255,0.03);
    }
    .cell-3row.sel { outline: 3px solid var(--accent-color); }

    /* Пятнашки */
    #grid-15 {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 6px;
        width: 100%;
        max-width: 340px;
        aspect-ratio: 1;
    }
    .tile-15 {
        background: linear-gradient(135deg, #2d2547, #1e1b2e);
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-weight: 800;
        font-size: 1.5rem;
        cursor: pointer;
        border: 1px solid rgba(255,255,255,0.08);
    }
    .tile-15.empty { background: transparent; border: none; cursor: default; }

    /* Арканоид */
    #ad-screen {
        justify-content: center;
        background: #000;
        position: fixed;
        inset: 0;
        max-width: none;
        z-index: 100;
    }
</style>
</head>
<body>

<!-- ГЛАВНЫЙ ЭКРАН -->
<div id="hub-screen" class="screen active">
    <header>
        <div class="logo" onclick="devClick()">
            GAME HUB
            <div class="dev-dots" id="dev-dots">
                <span></span><span></span><span></span><span></span><span></span>
            </div>
        </div>
        <div class="balance">🪙 <span id="balance-val">0</span></div>
    </header>

    <div class="container">
        <!-- Реклама -->
        <div class="ad-card" onclick="showAd()">
            <div class="ad-icon">📺</div>
            <div class="ad-info">
                <div class="ad-title">Смотреть рекламу</div>
                <div class="ad-sub">Канал Dley перезаливы · VK Video</div>
            </div>
            <div class="ad-reward">+40 🪙</div>
        </div>

        <!-- Админ панель -->
        <div id="dev-panel">
            <h3>⚙️ REGM_DEV // АДМИНКА <span style="cursor:pointer;" onclick="toggleDevPanel()">[X]</span></h3>
            <div class="dev-grid">
                <button class="dev-btn" onclick="devAddCoins()">🪙 +1000</button>
                <button class="dev-btn" onclick="devUnlockAll()">🔓 ОТКРЫТЬ ВСЁ</button>
                <button class="dev-btn" onclick="devReset()">🔄 СБРОС</button>
                <button class="dev-btn" onclick="devMaxReaction()">⚡ РЕАКЦИЯ 1мс</button>
                <button class="dev-btn" onclick="devAddCoins10k()">💰 +10000</button>
                <button class="dev-btn" onclick="devFillRecords()">🏆 ТОП РЕКОРДЫ</button>
            </div>
        </div>

        <!-- Табы -->
        <div class="tabs">
            <div class="tab active" id="tab-solo" onclick="switchTab('solo')">🎮 Игры</div>
            <div class="tab" id="tab-duo" onclick="switchTab('duo')">👥 На двоих</div>
        </div>

        <!-- ОДИНОЧНЫЕ ИГРЫ -->
        <div id="content-solo">
            <div class="section-title">БЕСПЛАТНЫЕ ИГРЫ</div>
            <div class="game-list">
                <div class="game-card c-green" onclick="startSnake()">
                    <div class="game-info">
                        <div class="game-name">Змейка</div>
                        <div class="game-record">Рекорд: <span id="rec-snake">0</span></div>
                    </div>
                    <div class="game-icon">🐍</div>
                </div>

                <div class="game-card c-orange" onclick="start2048()">
                    <div class="game-info">
                        <div class="game-name">2048</div>
                        <div class="game-record">Рекорд: <span id="rec-2048">0</span></div>
                    </div>
                    <div class="game-icon">🔢</div>
                </div>

                <div class="game-card c-purple" onclick="start3Row()">
                    <div class="game-info">
                        <div class="game-name">3 в ряд</div>
                        <div class="game-record">Рекорд: <span id="rec-3row">0</span></div>
                    </div>
                    <div class="game-icon">💎</div>
                </div>

                <div class="game-card c-cyan" onclick="startReactionGame()">
                    <div class="game-info">
                        <div class="game-name">Реакция</div>
                        <div class="game-record">Лучшее: <span id="rec-reaction">---</span> мс</div>
                    </div>
                    <div class="game-icon">⚡</div>
                </div>

                <div class="game-card c-red" onclick="start15()">
                    <div class="game-info">
                        <div class="game-name">Пятнашки</div>
                        <div class="game-record">Рекорд: <span id="rec-15">---</span> ходов</div>
                    </div>
                    <div class="game-icon">🧩</div>
                </div>

                <div class="game-card c-yellow" onclick="startArkanoid()">
                    <div class="game-info">
                        <div class="game-name">Арканоид</div>
                        <div class="game-record">Рекорд: <span id="rec-arkanoid">0</span></div>
                    </div>
                    <div class="game-icon">🧱</div>
                </div>
            </div>

            <div class="section-title">ПРЕМИУМ ИГРЫ</div>
            <div class="game-list">
                <div class="game-card c-cyan" onclick="buyOrPlay('shooter', 200)">
                    <div class="game-info">
                        <div class="game-name">Космический Шутер</div>
                        <div class="game-record">Премиум</div>
                    </div>
                    <div class="game-icon">🚀</div>
                    <div class="lock-price" id="price-shooter">🪙 200</div>
                </div>
                <div class="game-card c-purple" onclick="buyOrPlay('tetris', 250)">
                    <div class="game-info">
                        <div class="game-name">Тетрис</div>
                        <div class="game-record">Премиум</div>
                    </div>
                    <div class="game-icon">🧊</div>
                    <div class="lock-price" id="price-tetris">🪙 250</div>
                </div>
            </div>
        </div>

        <!-- ИГРЫ НА ДВОИХ -->
        <div id="content-duo" style="display:none;">
            <div class="section-title">ИГРЫ НА ДВОИХ</div>
            <div class="game-list">
                <div class="game-card c-red" onclick="startDuelReaction()">
                    <div class="game-info">
                        <div class="game-name">Реакция-дуэль</div>
                        <div class="game-record">П1: <span id="duel-p1-wins">0</span> | П2: <span id="duel-p2-wins">0</span></div>
                    </div>
                    <div class="game-icon">⚔️</div>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- ЭКРАН РЕКЛАМЫ -->
<div id="ad-screen" class="screen">
    <h2>📺 Реклама</h2>
    <p>Канал: <b>Dley перезаливы</b> · VK Video</p>
    <p>Осталось: <span id="ad-timer">15</span> секунд...</p>
    <button id="ad-close-btn" class="menu-btn" style="display:none; align-self:center;" onclick="closeAd()">Забрать 40 🪙</button>
</div>

<!-- МОДАЛКА ПАРОЛЯ -->
<div id="pass-modal" class="modal-overlay">
    <div class="modal">
        <h3>🔐 ВВЕДИТЕ ПАРОЛЬ</h3>
        <input type="password" id="pass-input" maxlength="6" inputmode="numeric" placeholder="••••••">
        <div class="err" id="pass-err"></div>
        <div class="row">
            <button class="cancel" onclick="closePassModal()">Отмена</button>
            <button onclick="checkPass()">Войти</button>
        </div>
    </div>
</div>

<!-- ЭКРАН РЕАКЦИИ -->
<div id="reaction-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div style="margin-bottom: 15px; text-align: center;">Нажмите на панель ниже.</div>
    <div id="reaction-click-zone" class="reaction-zone" onclick="handleReactionTap()">НАЖМИТЕ ДЛЯ СТАРТА</div>
</div>

<!-- ЭКРАН ДУЭЛИ -->
<div id="duel-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div style="margin-bottom: 15px; text-align: center;">Когда появится цвет — жми! Кто раньше — победил.</div>
    <div class="duel-container">
        <div class="duel-side" id="p1-side" onclick="duelTap(1)">ИГРОК 1</div>
        <div class="duel-side" id="p2-side" onclick="duelTap(2)">ИГРОК 2</div>
    </div>
</div>

<!-- ЭКРАН ЗМЕЙКИ -->
<div id="snake-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div class="game-header">
        <div>Счёт: <span id="snake-score">0</span></div>
        <div>Рекорд: <span id="snake-best">0</span></div>
    </div>
    <canvas id="game-canvas" width="320" height="320"></canvas>
    <div style="margin-top:14px; color:#8a86a3; font-size:0.85rem; text-align:center;">Стрелки или свайпы</div>
    <div style="margin-top:10px; display:flex; gap:10px;">
        <button class="menu-btn" style="align-self:auto;" onclick="snakeDir(-1,0)">◀</button>
        <button class="menu-btn" style="align-self:auto;" onclick="snakeDir(0,-1)">▲</button>
        <button class="menu-btn" style="align-self:auto;" onclick="snakeDir(0,1)">▼</button>
        <button class="menu-btn" style="align-self:auto;" onclick="snakeDir(1,0)">▶</button>
    </div>
</div>

<!-- ЭКРАН 2048 -->
<div id="2048-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div class="game-header">
        <div>Счёт: <span id="score-2048">0</span></div>
        <div>Рекорд: <span id="best-2048">0</span></div>
    </div>
    <div id="grid-2048"></div>
    <div style="margin-top:14px; color:#8a86a3; font-size:0.85rem;">Стрелки или свайпы</div>
</div>

<!-- ЭКРАН 3 В РЯД -->
<div id="3row-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div class="game-header">
        <div>Счёт: <span id="score-3row">0</span></div>
        <div>Ходов: <span id="moves-3row">30</span></div>
    </div>
    <div id="grid-3row"></div>
    <div style="margin-top:14px; color:#8a86a3; font-size:0.85rem; text-align:center;">Нажмите 2 соседних элемента для обмена</div>
</div>

<!-- ЭКРАН ПЯТНАШЕК -->
<div id="15-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div class="game-header">
        <div>Ходов: <span id="moves-15">0</span></div>
        <div>Рекорд: <span id="best-15">---</span></div>
    </div>
    <div id="grid-15"></div>
</div>

<!-- ЭКРАН АРКАНОИДА -->
<div id="arkanoid-screen" class="screen">
    <button class="menu-btn" onclick="backToMenu()">◀ Меню</button>
    <div class="game-header">
        <div>Счёт: <span id="score-arkanoid">0</span></div>
        <div>Жизни: <span id="lives-arkanoid">3</span></div>
    </div>
    <canvas id="arkanoid-canvas" width="320" height="400"></canvas>
    <div style="margin-top:10px; color:#8a86a3; font-size:0.85rem;">Водите пальцем / мышью</div>
</div>

<script>
// ================== СОСТОЯНИЕ ==================
const state = {
    balance: 0,
    owned: {},
    records: { reaction: null, snake: 0, '2048': 0, '3row': 0, '15': null, arkanoid: 0 },
    duelWins: { p1: 0, p2: 0 },
    devClicks: 0,
    adminUnlocked: false
};

function save() { try { localStorage.setItem('gamehub_state', JSON.stringify(state)); } catch(e){} }
function load() {
    try {
        const raw = localStorage.getItem('gamehub_state');
        if (raw) {
            const p = JSON.parse(raw);
            Object.assign(state, p);
            state.records = Object.assign({ reaction: null, snake: 0, '2048': 0, '3row': 0, '15': null, arkanoid: 0 }, p.records || {});
            state.duelWins = Object.assign({ p1: 0, p2: 0 }, p.duelWins || {});
        }
    } catch(e) {}
}
load();

// ================== UI ==================
function updateUI() {
    document.getElementById('balance-val').textContent = state.balance;
    document.getElementById('rec-reaction').textContent = state.records.reaction || '---';
    document.getElementById('rec-snake').textContent = state.records.snake || 0;
    document.getElementById('rec-2048').textContent = state.records['2048'] || 0;
    document.getElementById('rec-3row').textContent = state.records['3row'] || 0;
    document.getElementById('rec-15').textContent = state.records['15'] || '---';
    document.getElementById('rec-arkanoid').textContent = state.records.arkanoid || 0;
    document.getElementById('duel-p1-wins').textContent = state.duelWins.p1;
    document.getElementById('duel-p2-wins').textContent = state.duelWins.p2;

    ['shooter','tetris'].forEach(id => {
        const el = document.getElementById('price-' + id);
        if (state.owned[id]) el.textContent = '✅';
        else el.textContent = id === 'shooter' ? '🪙 200' : '🪙 250';
    });
}

function showScreen(id) {
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
}

function backToMenu() {
    stopAllGames();
    updateUI();
    showScreen('hub-screen');
}

function switchTab(t) {
    document.getElementById('tab-solo').classList.toggle('active', t === 'solo');
    document.getElementById('tab-duo').classList.toggle('active', t === 'duo');
    document.getElementById('content-solo').style.display = t === 'solo' ? 'block' : 'none';
    document.getElementById('content-duo').style.display = t === 'duo' ? 'block' : 'none';
}

// ================== АДМИН ПАНЕЛЬ С ПАРОЛЕМ ==================
const ADMIN_PASSWORD = '123321';

function devClick() {
    if (state.adminUnlocked) { toggleDevPanel(); return; }
    state.devClicks++;
    updateDots();
    if (state.devClicks >= 5) {
        state.devClicks = 0;
        updateDots();
        openPassModal();
    }
}

function updateDots() {
    const dots = document.querySelectorAll('#dev-dots span');
    dots.forEach((d, i) => d.classList.toggle('on', i < state.devClicks));
}

function openPassModal() {
    document.getElementById('pass-modal').classList.add('active');
    document.getElementById('pass-input').value = '';
    document.getElementById('pass-err').textContent = '';
    setTimeout(() => document.getElementById('pass-input').focus(), 100);
}

function closePassModal() {
    document.getElementById('pass-modal').classList.remove('active');
    state.devClicks = 0;
    updateDots();
}

function checkPass() {
    const val = document.getElementById('pass-input').value;
    if (val === ADMIN_PASSWORD) {
        state.adminUnlocked = true;
        closePassModal();
        document.getElementById('dev-panel').style.display = 'block';
        alert('✅ Доступ разрешён! Админ-панель открыта.');
    } else {
        document.getElementById('pass-err').textContent = '❌ Неверный пароль';
        document.getElementById('pass-input').value = '';
    }
}

document.getElementById('pass-input').addEventListener('keydown', e => {
    if (e.key === 'Enter') checkPass();
});

function toggleDevPanel() {
    const p = document.getElementById('dev-panel');
    p.style.display = p.style.display === 'block' ? 'none' : 'block';
}

function devAddCoins()    { state.balance += 1000; save(); updateUI(); }
function devAddCoins10k() { state.balance += 10000; save(); updateUI(); }
function devUnlockAll()   { state.owned.shooter = true; state.owned.tetris = true; save(); updateUI(); }
function devReset()       {
    if (!confirm('Сбросить всё?')) return;
    state.balance = 0; state.owned = {};
    state.records = { reaction: null, snake: 0, '2048': 0, '3row': 0, '15': null, arkanoid: 0 };
    state.duelWins = { p1: 0, p2: 0 };
    save(); updateUI();
}
function devMaxReaction() { state.records.reaction = 1; save(); updateUI(); }
function devFillRecords() {
    state.records.reaction = 50;
    state.records.snake = 999;
    state.records['2048'] = 9999;
    state.records['3row'] = 9999;
    state.records['15'] = 10;
    state.records.arkanoid = 9999;
    state.balance = 99999;
    save(); updateUI();
}

// ================== РЕКЛАМА ==================
let adInterval = null, adSeconds = 15;
function showAd() {
    adSeconds = 15;
    document.getElementById('ad-timer').textContent = adSeconds;
    document.getElementById('ad-close-btn').style.display = 'none';
    showScreen('ad-screen');
    adInterval = setInterval(() => {
        adSeconds--;
        document.getElementById('ad-timer').textContent = adSeconds;
        if (adSeconds <= 0) {
            clearInterval(adInterval); adInterval = null;
            document.getElementById('ad-close-btn').style.display = 'inline-block';
        }
    }, 1000);
}
function closeAd() {
    if (adInterval) { clearInterval(adInterval); adInterval = null; }
    state.balance += 40; save(); updateUI();
    showScreen('hub-screen');
}

// ================== ПОКУПКИ ==================
function buyOrPlay(id, price) {
    if (state.owned[id]) { alert('Игра уже куплена! (в разработке)'); return; }
    if (state.balance < price) { alert('Недостаточно монет!'); return; }
    if (confirm('Купить за ' + price + ' 🪙?')) {
        state.balance -= price; state.owned[id] = true; save(); updateUI();
        alert('Куплено! Игра в разработке 🚧');
    }
}

// ================== РЕАКЦИЯ ==================
let reactionState = 'idle', reactionTimer = null, reactionStart = 0;
function startReactionGame() {
    reactionState = 'idle';
    const z = document.getElementById('reaction-click-zone');
    z.style.backgroundColor = '#444'; z.textContent = 'НАЖМИТЕ ДЛЯ СТАРТА';
    showScreen('reaction-screen');
}
function handleReactionTap() {
    const z = document.getElementById('reaction-click-zone');
    if (reactionState === 'idle') {
        reactionState = 'waiting';
        z.style.backgroundColor = '#8b0000'; z.textContent = 'ЖДИТЕ ЗЕЛЁНОГО...';
        const delay = 1000 + Math.random() * 3000;
        reactionTimer = setTimeout(() => {
            reactionState = 'ready'; reactionStart = performance.now();
            z.style.backgroundColor = '#00c853'; z.textContent = 'ЖМИ!!!';
        }, delay);
    } else if (reactionState === 'waiting') {
        clearTimeout(reactionTimer); reactionTimer = null;
        reactionState = 'idle';
        z.style.backgroundColor = '#444'; z.textContent = 'СЛИШКОМ РАНО! Нажмите снова.';
    } else if (reactionState === 'ready') {
        const t = Math.round(performance.now() - reactionStart);
        reactionState = 'result';
        z.style.backgroundColor = '#444';
        let msg = '⏱ ' + t + ' мс — нажмите ещё';
        if (!state.records.reaction || t < state.records.reaction) {
            state.records.reaction = t; save();
            msg = '🏆 НОВЫЙ РЕКОРД: ' + t + ' мс';
        }
        z.textContent = msg; updateUI();
    } else {
        reactionState = 'idle';
        z.style.backgroundColor = '#444'; z.textContent = 'НАЖМИТЕ ДЛЯ СТАРТА';
    }
}

// ================== ДУЭЛЬ ==================
let duelState = 'idle', duelTimer = null, duelStart = 0;
function startDuelReaction() {
    duelState = 'idle';
    resetDuelColors();
    setDuelText('ИГРОК 1', 'ИГРОК 2');
    showScreen('duel-screen');
}
function resetDuelColors() {
    document.getElementById('p1-side').style.backgroundColor = 'var(--p1-color)';
    document.getElementById('p2-side').style.backgroundColor = 'var(--p2-color)';
}
function setDuelText(a, b) {
    document.getElementById('p1-side').textContent = a;
    document.getElementById('p2-side').textContent = b;
}
function duelTap(p) {
    const p1 = document.getElementById('p1-side'), p2 = document.getElementById('p2-side');
    if (duelState === 'idle') {
        duelState = 'waiting';
        p1.style.backgroundColor = '#333'; p2.style.backgroundColor = '#333';
        setDuelText('ЖДИТЕ...', 'ЖДИТЕ...');
        const delay = 1500 + Math.random() * 3000;
        duelTimer = setTimeout(() => {
            duelState = 'ready'; duelStart = performance.now();
            resetDuelColors(); setDuelText('ЖМИ!', 'ЖМИ!');
        }, delay);
    } else if (duelState === 'waiting') {
        clearTimeout(duelTimer); duelTimer = null; duelState = 'idle';
        resetDuelColors();
        setDuelText('ФАЛЬСТАРТ Игрок ' + p, 'Нажмите снова');
        setTimeout(() => { if (duelState === 'idle') setDuelText('ИГРОК 1', 'ИГРОК 2'); }, 1200);
    } else if (duelState === 'ready') {
        const t = Math.round(performance.now() - duelStart);
        duelState = 'roundEnd';
        if (p === 1) { state.duelWins.p1++; setDuelText('🏆 ПОБЕДА (' + t + 'мс)', 'Проиграл'); p2.style.backgroundColor = '#333'; }
        else { state.duelWins.p2++; setDuelText('Проиграл', '🏆 ПОБЕДА (' + t + 'мс)'); p1.style.backgroundColor = '#333'; }
        save(); updateUI();
    } else {
        duelState = 'idle';
        resetDuelColors(); setDuelText('ИГРОК 1', 'ИГРОК 2');
    }
}

// ================== ИГРОВОЙ ЦИКЛ ==================
let activeGame = null;
function stopAllGames() {
    if (activeGame && activeGame.stop) activeGame.stop();
    activeGame = null;
    if (reactionTimer) { clearTimeout(reactionTimer); reactionTimer = null; }
    if (duelTimer) { clearTimeout(duelTimer); duelTimer = null; }
    reactionState = 'idle'; duelState = 'idle';
}

// ============ ЗМЕЙКА ============
function startSnake() {
    stopAllGames();
    showScreen('snake-screen');
    const canvas = document.getElementById('game-canvas');
    const ctx = canvas.getContext('2d');
    const CELL = 20, COLS = canvas.width / CELL, ROWS = canvas.height / CELL;

    let snake = [{x: 10, y: 10}];
    let dir = {x: 1, y: 0};
    let food = {x: 5, y: 5};
    let score = 0;
    let interval = null;
    let alive = true;

    document.getElementById('snake-best').textContent = state.records.snake || 0;

    function placeFood() {
        while (true) {
            food = { x: Math.floor(Math.random()*COLS), y: Math.floor(Math.random()*ROWS) };
            if (!snake.some(s => s.x === food.x && s.y === food.y)) break;
        }
    }
    placeFood();

    window.snakeDir = (dx, dy) => {
        if (!alive) return;
        if (dx === -dir.x && dy === -dir.y) return;
        if (dx === dir.x && dy === dir.y) return;
        dir = { x: dx, y: dy };
    };

    function draw() {
        ctx.fillStyle = '#0a0a14';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        // сетка
        ctx.strokeStyle = 'rgba(255,255,255,0.03)';
        for (let i = 0; i <= COLS; i++) {
            ctx.beginPath(); ctx.moveTo(i*CELL, 0); ctx.lineTo(i*CELL, canvas.height); ctx.stroke();
        }
        for (let j = 0; j <= ROWS; j++) {
            ctx.beginPath(); ctx.moveTo(0, j*CELL); ctx.lineTo(canvas.width, j*CELL); ctx.stroke();
        }
        // еда
        ctx.font = CELL + 'px serif';
        ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
        ctx.fillText('🍎', food.x*CELL + CELL/2, food.y*CELL + CELL/2 + 1);
        // змейка
        snake.forEach((s, i) => {
            ctx.fillStyle = i === 0 ? '#00ff66' : '#00b34a';
            ctx.fillRect(s.x*CELL + 1, s.y*CELL + 1, CELL - 2, CELL - 2);
            if (i === 0) {
                ctx.fillStyle = '#001a0d';
                ctx.beginPath();
                ctx.arc(s.x*CELL + CELL/2, s.y*CELL + CELL/2, 3, 0, Math.PI*2);
                ctx.fill();
            }
        });
    }

    function tick() {
        if (!alive) return;
        const head = { x: snake[0].x + dir.x, y: snake[0].y + dir.y };
        if (head.x < 0 || head.x >= COLS || head.y < 0 || head.y >= ROWS) return gameOver();
        if (snake.some(s => s.x === head.x && s.y === head.y)) return gameOver();
        snake.unshift(head);
        if (head.x === food.x && head.y === food.y) {
            score++;
            document.getElementById('snake-score').textContent = score;
            placeFood();
        } else snake.pop();
        draw();
    }

    function gameOver() {
        alive = false;
        clearInterval(interval); interval = null;
        if (score > (state.records.snake || 0)) {
            state.records.snake = score; save();
            document.getElementById('snake-best').textContent = score;
        }
        ctx.fillStyle = 'rgba(0,0,0,0.75)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#fff';
        ctx.font = 'bold 24px sans-serif';
        ctx.textAlign = 'center';
        ctx.fillText('ИГРА ОКОНЧЕНА', canvas.width/2, canvas.height/2 - 10);
        ctx.font = '16px sans-serif';
        ctx.fillStyle = '#ffb703';
        ctx.fillText('Счёт: ' + score, canvas.width/2, canvas.height/2 + 20);
        updateUI();
    }

    document.getElementById('snake-score').textContent = 0;
    draw();
    interval = setInterval(tick, 130);

    activeGame = { stop: () => { alive = false; if (interval) clearInterval(interval); } };
}

// ============ 2048 ============
function start2048() {
    stopAllGames();
    showScreen('2048-screen');
    const gridEl = document.getElementById('grid-2048');
    let board = Array(4).fill().map(() => Array(4).fill(0));
    let score = 0;
    let best = state.records['2048'] || 0;
    document.getElementById('best-2048').textContent = best;

    function addTile() {
        const empty = [];
        for (let i=0;i<4;i++) for (let j=0;j<4;j++) if (!board[i][j]) empty.push([i,j]);
        if (!empty.length) return;
        const [i,j] = empty[Math.floor(Math.random()*empty.length)];
        board[i][j] = Math.random() < 0.9 ? 2 : 4;
    }
    addTile(); addTile();

    function colors(v) {
        return {
            2:'#eee4da',4:'#ede0c8',8:'#f2b179',16:'#f59563',
            32:'#f67c5f',64:'#f65e3b',128:'#edcf72',256:'#edcc61',
            512:'#edc850',1024:'#edc53f',2048:'#edc22e'
        }[v] || '#3c3a32';
    }
    function textColor(v) { return v <= 4 ? '#776e65' : '#fff'; }

    function render() {
        gridEl.innerHTML = '';
        for (let i=0;i<4;i++) for (let j=0;j<4;j++) {
            const t = document.createElement('div');
            t.className = 'tile-2048';
            const v = board[i][j];
            t.textContent = v || '';
            if (v) {
                t.style.background = colors(v);
                t.style.color = textColor(v);
                t.style.fontSize = v >= 1024 ? '1rem' : v >= 128 ? '1.2rem' : '1.4rem';
            }
            gridEl.appendChild(t);
        }
        document.getElementById('score-2048').textContent = score;
    }

    function slide(row) {
        let r = row.filter(v => v);
        for (let i=0;i<r.length-1;i++) {
            if (r[i] === r[i+1]) { r[i] *= 2; score += r[i]; r.splice(i+1,1); }
        }
        while (r.length < 4) r.push(0);
        return r;
    }

    function move(dir) {
        const before = JSON.stringify(board);
        if (dir === 'left')  board = board.map(r => slide(r));
        if (dir === 'right') board = board.map(r => slide(r.slice().reverse()).reverse());
        if (dir === 'up') {
            for (let j=0;j<4;j++) {
                let col = [board[0][j],board[1][j],board[2][j],board[3][j]];
                col = slide(col);
                for (let i=0;i<4;i++) board[i][j] = col[i];
            }
        }
        if (dir === 'down') {
            for (let j=0;j<4;j++) {
                let col = [board[0][j],board[1][j],board[2][j],board[3][j]];
                col = slide(col.reverse()).reverse();
                for (let i=0;i<4;i++) board[i][j] = col[i];
            }
        }
        if (JSON.stringify(board) !== before) {
            addTile();
            render();
            if (score > best) { best = score; state.records['2048'] = score; save(); document.getElementById('best-2048').textContent = best; }
        }
    }

    window.handle2048Key = e => {
        if (!document.getElementById('2048-screen').classList.contains('active')) return;
        const map = { ArrowLeft:'left', ArrowRight:'right', ArrowUp:'up', ArrowDown:'down' };
        if (map[e.key]) { e.preventDefault(); move(map[e.key]); }
    };
    window.handle2048Swipe = (dx, dy) => {
        if (Math.abs(dx) > Math.abs(dy)) move(dx > 0 ? 'right' : 'left');
        else move(dy > 0 ? 'down' : 'up');
    };

    score = 0;
    render();
    activeGame = { stop: () => {} };
}

// ============ 3 В РЯД ============
function start3Row() {
    stopAllGames();
    showScreen('3row-screen');
    const gridEl = document.getElementById('grid-3row');
    const ROWS = 8, COLS = 7;
    const ICONS = ['💎','🍎','🍇','⭐','🔷','🍋'];
    let board = [];
    let score = 0, moves = 30;
    let selected = null;

    function rand() { return ICONS[Math.floor(Math.random()*ICONS.length)]; }

    function findMatches() {
        const matched = new Set();
        for (let i=0;i<ROWS;i++) {
            for (let j=0;j<COLS-2;j++) {
                if (board[i][j] && board[i][j] === board[i][j+1] && board[i][j] === board[i][j+2]) {
                    matched.add(i+','+j); matched.add(i+','+(j+1)); matched.add(i+','+(j+2));
                }
            }
        }
        for (let j=0;j<COLS;j++) {
            for (let i=0;i<ROWS-2;i++) {
                if (board[i][j] && board[i][j] === board[i+1][j] && board[i][j] === board[i+2][j]) {
                    matched.add(i+','+j); matched.add((i+1)+','+j); matched.add((i+2)+','+j);
                }
            }
        }
        return matched;
    }

    function clearMatches() {
        let any = false;
        while (true) {
            const m = findMatches();
            if (!m.size) break;
            any = true;
            score += m.size * 10;
            m.forEach(k => { const [i,j] = k.split(',').map(Number); board[i][j] = null; });
            // падение вниз
            for (let j=0;j<COLS;j++) {
                let col = [];
                for (let i=ROWS-1;i>=0;i--) if (board[i][j]) col.push(board[i][j]);
                for (let i=ROWS-1;i>=0;i--) board[i][j] = col[ROWS-1-i] || null;
            }
            // заполнение сверху
            for (let i=0;i<ROWS;i++) for (let j=0;j<COLS;j++) if (!board[i][j]) board[i][j] = rand();
        }
        return any;
    }

    function render() {
        gridEl.innerHTML = '';
        for (let i=0;i<ROWS;i++) for (let j=0;j<COLS;j++) {
            const c = document.createElement('div');
            c.className = 'cell-3row';
            c.textContent = board[i][j] || '';
            if (selected && selected.i === i && selected.j === j) c.classList.add('sel');
            c.onclick = () => click(i, j);
            gridEl.appendChild(c);
        }
        document.getElementById('score-3row').textContent = score;
        document.getElementById('moves-3row').textContent = moves;
    }

    function click(i, j) {
        if (moves <= 0) return;
        if (!selected) { selected = {i, j}; render(); return; }
        if (selected.i === i && selected.j === j) { selected = null; render(); return; }
        const dist = Math.abs(selected.i - i) + Math.abs(selected.j - j);
        if (dist === 1) {
            const a = selected, b = {i, j};
            [board[a.i][a.j], board[b.i][b.j]] = [board[b.i][b.j], board[a.i][a.j]];
            selected = null;
            if (clearMatches()) {
                moves--;
            } else {
                [board[a.i][a.j], board[b.i][b.j]] = [board[b.i][b.j], board[a.i][a.j]];
            }
        } else selected = {i, j};
        render();
        if (score > (state.records['3row'] || 0)) {
            state.records['3row'] = score; save(); updateUI();
        }
    }

    // стартовое поле без совпадений
    do {
        board = Array(ROWS).fill().map(() => Array(COLS).fill().map(rand));
    } while (findMatches().size);

    render();
    activeGame = { stop: () => {} };
}

// ============ ПЯТНАШКИ ============
function start15() {
    stopAllGames();
    showScreen('15-screen');
    const gridEl = document.getElementById('grid-15');
    let board = [];
    let moves = 0;
    document.getElementById('moves-15').textContent = 0;
    document.getElementById('best-15').textContent = state.records['15'] || '---';

    function reset() {
        board = [];
        for (let i=1;i<=15;i++) board.push(i);
        board.push(0);
        // перемешиваем корректно (много случайных ходов)
        let empty = 15;
        for (let k=0;k<500;k++) {
            const r = Math.floor(empty/4), c = empty%4;
            const dirs = [[1,0],[-1,0],[0,1],[0,-1]];
            const [di,dj] = dirs[Math.floor(Math.random()*4)];
            const nr = r+di, nc = c+dj;
            if (nr<0||nr>3||nc<0||nc>3) continue;
            const nIdx = nr*4+nc;
            [board[empty], board[nIdx]] = [board[nIdx], board[empty]];
            empty = nIdx;
        }
    }

    function solved() {
        for (let i=0;i<15;i++) if (board[i] !== i+1) return false;
        return board[15] === 0;
    }

    function render() {
        gridEl.innerHTML = '';
        board.forEach((v, idx) => {
            const t = document.createElement('div');
            t.className = 'tile-15' + (v === 0 ? ' empty' : '');
            t.textContent = v || '';
            if (v !== 0) t.onclick = () => move(idx);
            gridEl.appendChild(t);
        });
    }

    function move(idx) {
        const empty = board.indexOf(0);
        const r1 = Math.floor(idx/4), c1 = idx%4;
        const r2 = Math.floor(empty/4), c2 = empty%4;
        if (Math.abs(r1-r2) + Math.abs(c1-c2) !== 1) return;
        [board[idx], board[empty]] = [board[empty], board[idx]];
        moves++;
        document.getElementById('moves-15').textContent = moves;
        render();
        if (solved()) {
            if (!state.records['15'] || moves < state.records['15']) {
                state.records['15'] = moves; save(); updateUI();
                document.getElementById('best-15').textContent = moves;
                setTimeout(() => alert('🏆 Победа! Ходов: ' + moves), 100);
            }
        }
    }

    reset(); render();
    activeGame = { stop: () => {} };
}

// ============ АРКАНОИД ============
function startArkanoid() {
    stopAllGames();
    showScreen('arkanoid-screen');
    const canvas = document.getElementById('arkanoid-canvas');
    const ctx = canvas.getContext('2d');
    const W = canvas.width, H = canvas.height;

    const paddle = { w: 70, h: 10, x: W/2 - 35, y: H - 25, speed: 7 };
    const ball = { x: W/2, y: H/2, r: 6, dx: 3, dy: -3 };
    let bricks = [];
    let score = 0, lives = 3;
    let running = true;
    let rafId = null;

    function initBricks() {
        bricks = [];
        const rows = 5, cols = 8;
        const bw = (W - 20) / cols;
        const bh = 18;
        const colors = ['#ff4d6d','#ff9500','#ffb703','#00ff66','#00b4d8'];
        for (let r=0;r<rows;r++) for (let c=0;c<cols;c++) {
            bricks.push({
                x: 10 + c*bw, y: 40 + r*(bh+4),
                w: bw - 3, h: bh,
                color: colors[r], alive: true
            });
        }
    }
    initBricks();

    function updateHUD() {
        document.getElementById('score-arkanoid').textContent = score;
        document.getElementById('lives-arkanoid').textContent = lives;
    }

    function draw() {
        ctx.fillStyle = '#0a0a14';
        ctx.fillRect(0, 0, W, H);

        // кирпичи
        bricks.forEach(b => {
            if (!b.alive) return;
            ctx.fillStyle = b.color;
            ctx.fillRect(b.x, b.y, b.w, b.h);
            ctx.fillStyle = 'rgba(255,255,255,0.15)';
            ctx.fillRect(b.x, b.y, b.w, 3);
        });

        // платформа
        ctx.fillStyle = '#ffb703';
        ctx.fillRect(paddle.x, paddle.y, paddle.w, paddle.h);

        // мяч
        ctx.beginPath();
        ctx.arc(ball.x, ball.y, ball.r, 0, Math.PI*2);
        ctx.fillStyle = '#fff';
        ctx.fill();
    }

    function step() {
        if (!running) return;
        ball.x += ball.dx;
        ball.y += ball.dy;

        if (ball.x - ball.r < 0 || ball.x + ball.r > W) ball.dx = -ball.dx;
        if (ball.y - ball.r < 0) ball.dy = -ball.dy;

        // платформа
        if (ball.y + ball.r >= paddle.y && ball.y - ball.r <= paddle.y + paddle.h &&
            ball.x >= paddle.x && ball.x <= paddle.x + paddle.w && ball.dy > 0) {
            ball.dy = -ball.dy;
            const hit = (ball.x - (paddle.x + paddle.w/2)) / (paddle.w/2);
            ball.dx = hit * 5;
        }

        // кирпичи
        bricks.forEach(b => {
            if (!b.alive) return;
            if (ball.x + ball.r > b.x && ball.x - ball.r < b.x + b.w &&
                ball.y + ball.r > b.y && ball.y - ball.r < b.y + b.h) {
                b.alive = false;
                score += 10;
                updateHUD();
                ball.dy = -ball.dy;
            }
        });

        // проигрыш жизни
        if (ball.y - ball.r > H) {
            lives--;
            updateHUD();
            if (lives <= 0) {
                running = false;
                if (score > (state.records.arkanoid || 0)) {
                    state.records.arkanoid = score; save(); updateUI();
                }
                ctx.fillStyle = 'rgba(0,0,0,0.8)';
                ctx.fillRect(0, 0, W, H);
                ctx.fillStyle = '#ff4d6d';
                ctx.font = 'bold 22px sans-serif';
                ctx.textAlign = 'center';
                ctx.fillText('GAME OVER', W/2, H/2 - 10);
                ctx.fillStyle = '#ffb703';
                ctx.font = '16px sans-serif';
                ctx.fillText('Счёт: ' + score, W/2, H/2 + 20);
                return;
            }
            ball.x = W/2; ball.y = H/2;
            ball.dx = 3 * (Math.random() < 0.5 ? 1 : -1);
            ball.dy = -3;
        }

        // победа
        if (bricks.every(b => !b.alive)) {
            running = false;
            if (score > (state.records.arkanoid || 0)) {
                state.records.arkanoid = score; save(); updateUI();
            }
            ctx.fillStyle = 'rgba(0,0,0,0.8)';
            ctx.fillRect(0, 0, W, H);
            ctx.fillStyle = '#00ff66';
            ctx.font = 'bold 22px sans-serif';
            ctx.textAlign = 'center';
            ctx.fillText('ПОБЕДА!', W/2, H/2);
            return;
        }

        draw();
        rafId = requestAnimationFrame(step);
    }

    function movePaddle(clientX) {
        const rect = canvas.getBoundingClientRect();
        const x = (clientX - rect.left) * (W / rect.width);
        paddle.x = Math.max(0, Math.min(W - paddle.w, x - paddle.w/2));
    }

    const onMove = e => {
        e.preventDefault();
        const t = e.touches ? e.touches[0] : e;
        movePaddle(t.clientX);
    };

    canvas.addEventListener('mousemove', onMove);
    canvas.addEventListener('touchmove', onMove, { passive: false });

    updateHUD();
    draw();
    rafId = requestAnimationFrame(step);

    activeGame = { stop: () => { running = false; if (rafId) cancelAnimationFrame(rafId); } };
}

// ================== УПРАВЛЕНИЕ ==================
document.addEventListener('keydown', e => {
    if (window.handle2048Key) window.handle2048Key(e);
    if (document.getElementById('snake-screen').classList.contains('active')) {
        const map = { ArrowLeft:[-1,0], ArrowRight:[1,0], ArrowUp:[0,-1], ArrowDown:[0,1] };
        if (map[e.key]) { e.preventDefault(); window.snakeDir(...map[e.key]); }
    }
});

// Свайпы
let touchStart = null;
document.addEventListener('touchstart', e => {
    touchStart = { x: e.touches[0].clientX, y: e.touches[0].clientY };
}, { passive: true });
document.addEventListener('touchend', e => {
    if (!touchStart) return;
    const dx = e.changedTouches[0].clientX - touchStart.x;
    const dy = e.changedTouches[0].clientY - touchStart.y;
    if (Math.abs(dx) < 30 && Math.abs(dy) < 30) return;
    if (document.getElementById('2048-screen').classList.contains('active')) {
        window.handle2048Swipe(dx, dy);
    } else if (document.getElementById('snake-screen').classList.contains('active')) {
        if (Math.abs(dx) > Math.abs(dy)) window.snakeDir(dx > 0 ? 1 : -1, 0);
        else window.snakeDir(0, dy > 0 ? 1 : -1);
    }
    touchStart = null;
});

// Инициализация
updateUI();
</script>
</body>
</html>            align-items: center;
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
