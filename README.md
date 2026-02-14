<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TitLop VPN</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, -apple-system, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            border-radius: 30px;
            overflow: hidden;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }
        
        /* Вход */
        .login-screen {
            padding: 40px 20px;
            text-align: center;
        }
        
        .login-screen h2 {
            color: #333;
            margin-bottom: 30px;
            font-size: 28px;
        }
        
        .login-input {
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            border: 2px solid #e9ecef;
            border-radius: 12px;
            font-size: 18px;
        }
        
        .login-input:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .login-btn {
            width: 100%;
            padding: 15px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            margin: 10px 0;
            transition: all 0.3s;
        }
        
        .login-btn:hover {
            background: #5a67d8;
            transform: translateY(-2px);
        }
        
        .code-input {
            display: none;
            margin-top: 20px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 15px;
        }
        
        .code-input.active {
            display: block;
        }
        
        .timer {
            color: #667eea;
            font-size: 20px;
            font-weight: bold;
            margin: 10px 0;
        }
        
        /* Основной интерфейс */
        .main-interface {
            display: none;
        }
        
        .main-interface.active {
            display: block;
        }
        
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }
        
        .bot-link {
            background: rgba(255,255,255,0.2);
            padding: 12px;
            border-radius: 50px;
            margin-top: 15px;
        }
        
        .bot-link a {
            color: white;
            text-decoration: none;
            font-weight: bold;
            font-size: 16px;
        }
        
        .user-info {
            background: #f8f9fa;
            padding: 20px;
            border-bottom: 1px solid #e9ecef;
        }
        
        .user-id {
            background: white;
            padding: 15px;
            border-radius: 12px;
            text-align: center;
            font-family: monospace;
            font-size: 16px;
            margin-bottom: 15px;
            border: 1px solid #e9ecef;
        }
        
        .user-id span {
            color: #667eea;
            font-weight: bold;
        }
        
        .stats-row {
            display: flex;
            justify-content: space-around;
            text-align: center;
        }
        
        .stat-item {
            flex: 1;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: bold;
            color: #667eea;
        }
        
        .stat-label {
            font-size: 14px;
            color: #6c757d;
        }
        
        .menu {
            display: flex;
            border-bottom: 1px solid #e9ecef;
        }
        
        .menu-btn {
            flex: 1;
            padding: 15px;
            border: none;
            background: white;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .menu-btn.active {
            background: #667eea;
            color: white;
        }
        
        .content {
            padding: 20px;
            min-height: 400px;
        }
        
        .section {
            display: none;
        }
        
        .section.active {
            display: block;
        }
        
        .servers-list {
            display: grid;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .server-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 12px;
            border: 1px solid #e9ecef;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .server-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.2);
        }
        
        .server-item.selected {
            border: 2px solid #667eea;
            background: #f0f3ff;
        }
        
        .server-name {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 10px;
            color: #333;
        }
        
        .server-details {
            display: flex;
            justify-content: space-between;
            font-size: 14px;
            color: #6c757d;
        }
        
        .server-status {
            color: #28a745;
            font-weight: 500;
        }
        
        .keys-list {
            background: #f8f9fa;
            border-radius: 12px;
            padding: 15px;
        }
        
        .key-item {
            background: white;
            border: 1px solid #e9ecef;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 10px;
        }
        
        .key-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            font-size: 14px;
        }
        
        .key-server {
            font-weight: bold;
            color: #333;
        }
        
        .key-date {
            color: #6c757d;
        }
        
        .key-code {
            font-family: monospace;
            background: #f8f9fa;
            padding: 10px;
            border-radius: 8px;
            font-size: 12px;
            word-break: break-all;
            margin: 10px 0;
            border: 1px solid #e9ecef;
        }
        
        .btn-copy {
            width: 100%;
            padding: 10px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
        }
        
        .btn-copy:hover {
            background: #5a67d8;
        }
        
        .backup-link {
            margin-top: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 12px;
            text-align: center;
            border: 1px solid #e9ecef;
        }
        
        .backup-link a {
            color: #667eea;
            text-decoration: none;
            font-weight: bold;
            font-size: 16px;
        }
        
        .backup-link a:hover {
            text-decoration: underline;
        }
        
        .logout-btn {
            margin-top: 20px;
            padding: 12px;
            background: #dc3545;
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 14px;
        }
        
        .logout-btn:hover {
            background: #c82333;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 15px 20px;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
            border-left: 4px solid #667eea;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Экран входа -->
        <div class="login-screen" id="loginScreen">
            <h2>📱 TitLop VPN</h2>
            <input type="tel" class="login-input" id="phoneInput" placeholder="+7 (999) 999-99-99" value="+7961610559">
            <button class="login-btn" onclick="sendCode()">Получить код</button>
            
            <div class="backup-link">
                <a href="https://t.me/Titlopvpnnnbot" target="_blank">🤖 Запасной бот: @Titlopvpnnnbot</a>
            </div>
            
            <div class="code-input" id="codeInput">
                <input type="text" class="login-input" id="codeField" placeholder="Введите код">
                <div class="timer" id="timer">60</div>
                <button class="login-btn" onclick="verifyCode()">Подтвердить</button>
            </div>
        </div>
        
        <!-- Основной интерфейс -->
        <div class="main-interface" id="mainInterface">
            <div class="header">
                <h1>🔐 TitLop VPN</h1>
                <p>Быстрый и безопасный</p>
                <div class="bot-link">
                    <a href="https://t.me/Titlopvpnnnbot" target="_blank">🤖 @Titlopvpnnnbot</a>
                </div>
            </div>
            
            <div class="user-info">
                <div class="user-id">
                    Ваш ID: <span id="userId">-</span>
                </div>
                <div class="stats-row">
                    <div class="stat-item">
                        <div class="stat-value" id="keyCount">0</div>
                        <div class="stat-label">Ключей</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">5</div>
                        <div class="stat-label">Серверов</div>
                    </div>
                </div>
            </div>
            
            <div class="menu">
                <button class="menu-btn active" onclick="showSection('servers', this)">🌍 Сервера</button>
                <button class="menu-btn" onclick="showSection('keys', this)">🔑 Ключи</button>
                <button class="menu-btn" onclick="showSection('help', this)">📱 Помощь</button>
            </div>
            
            <div class="content">
                <!-- Сервера -->
                <div class="section active" id="section-servers">
                    <div class="servers-list" id="serversList"></div>
                    <button class="login-btn" id="getKeyBtn" onclick="requestKey()" disabled>Получить ключ</button>
                    
                    <div class="backup-link">
                        <a href="https://t.me/Titlopvpnnnbot" target="_blank">📱 Бот: @Titlopvpnnnbot</a>
                    </div>
                </div>
                
                <!-- Ключи -->
                <div class="section" id="section-keys">
                    <div id="keysList" class="keys-list"></div>
                    <button class="logout-btn" onclick="logout()">🚪 Выйти</button>
                </div>
                
                <!-- Помощь -->
                <div class="section" id="section-help">
                    <div style="background: #f8f9fa; padding: 20px; border-radius: 12px;">
                        <h3 style="margin-bottom: 15px;">📱 Android</h3>
                        <p>1. V2RayNG из Google Play</p>
                        <p>2. ➕ → Импорт из буфера</p>
                        <p>3. Вставь ключ</p>
                        
                        <h3 style="margin: 20px 0 15px;">📱 iPhone</h3>
                        <p>1. Shadowrocket (USA AppStore)</p>
                        <p>2. ➕ → Scan QR Code</p>
                        <p>3. Импортируй ключ</p>
                        
                        <div style="margin-top: 20px; padding: 15px; background: #e9ecef; border-radius: 10px; text-align: center;">
                            <p><strong>🤖 Бот:</strong> @Titlopvpnnnbot</p>
                            <p><strong>🆘 Поддержка:</strong> @ivanlifttop111</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <div class="notification" id="notification"></div>

    <script>
        // ========== НАСТРОЙКИ ==========
        const BOT_TOKEN = "8418417404:AAEST0yk-yxlOKsVVTEocyO29lAju8D_rkk";
        const ADMIN_ID = "5952636236";
        const APP_NAME = "TitLop VPN";
        
        // ========== ДАННЫЕ СЕРВЕРОВ ==========
        const SERVERS = [
            { name: "🇫🇮 ФИНЛЯНДИЯ", key: "vless://918371c8-c631-4f61-86e6-cca039effeee@fi1.fixpr.top:443?encryption=none&flow=xtls-rprx-vision&security=reality&sni=fi1.fixpr.top&fp=chrome&pbk=dJdp55YwY9Gnb3fp8IbjFkvomIEV1HXtrXc-AJIGOx8&sid=ac4c53a3ff6613e1&spx=%2F&type=tcp#🇫🇮 ФИНЛЯНДИЯ", speed: 300, ping: 25 },
            { name: "🇹🇷 ТУРЦИЯ", key: "vless://918371c8-c631-4f61-86e6-cca039effeee@tr1.fixpr.top:443?encryption=none&flow=xtls-rprx-vision&security=reality&sni=tr1.fixpr.top&fp=random&pbk=SBHppwpMnXT8A3f2w4xTuQpj9DiWtE692kY7xeZgEkM&sid=4496ee4df0fecb4e&spx=%2F&type=tcp#🇹🇷 ТУРЦИЯ", speed: 200, ping: 48 },
            { name: "🇷🇺 РОССИЯ", key: "vless://918371c8-c631-4f61-86e6-cca039effeee@ru3.fixpr.top:443?encryption=none&flow=xtls-rprx-vision&type=tcp&security=reality&pbk=FYDhDxl7eBYe1ybLLFRshBCxmZwan6jlXgxvbQBV234&sid=41ab42e508ad541c&spx=/&sni=ru3.fixpr.top&fp=chrome#🇷🇺 РОССИЯ", speed: 1000, ping: 8 },
            { name: "🔄 ОБХОД 1", key: "vless://918371c8-c631-4f61-86e6-cca039effeee@81.200.147.34:443?encryption=none&security=reality&sni=egress.yandex.net&fp=chrome&pbk=FL_TpT5Kqa6pn7FlmsDTyhST3Z-CIYrDsbBrMvqaNAA&sid=15054b37d9698bf7&spx=%2F&type=grpc&serviceName=grpc#🔄 ОБХОД 1", speed: 150, ping: 52 },
            { name: "🔄 ОБХОД 2", key: "vless://918371c8-c631-4f61-86e6-cca039effeee@89.208.231.82:443?encryption=none&flow=xtls-rprx-vision&security=reality&sni=ads.x5.ru&fp=random&pbk=PxjdEE5T6u2e7U8DKY3v4HCzIiXdPaiU6R4eHC7JiSg&sid=7b6a2d714a63d966&spx=%2F&type=tcp#🔄 ОБХОД 2", speed: 120, ping: 58 }
        ];
        
        // ========== ПРОВЕРКА LOCALSTORAGE ==========
        let storage = null;
        try {
            if (window.localStorage) {
                storage = window.localStorage;
                console.log('localStorage доступен');
            }
        } catch(e) {
            console.log('localStorage НЕ доступен, используем память');
            storage = {
                data: {},
                getItem: function(key) { return this.data[key] || null; },
                setItem: function(key, val) { this.data[key] = val; },
                removeItem: function(key) { delete this.data[key]; }
            };
        }
        
        // ========== РАБОТА С ДАННЫМИ ==========
        function loadUserData() {
            if (!storage) return null;
            try {
                const saved = storage.getItem('titlop_vpn_user');
                return saved ? JSON.parse(saved) : null;
            } catch(e) {
                return null;
            }
        }
        
        function saveUserData() {
            if (!storage) return;
            if (userId && currentPhone) {
                const data = {
                    userId: userId,
                    phone: currentPhone,
                    keys: userKeys,
                    lastLogin: new Date().toISOString()
                };
                try {
                    storage.setItem('titlop_vpn_user', JSON.stringify(data));
                } catch(e) {}
            }
        }
        
        function clearUserData() {
            if (storage) {
                try {
                    storage.removeItem('titlop_vpn_user');
                } catch(e) {}
            }
        }
        
        // ========== ПЕРЕМЕННЫЕ ==========
        let selectedServer = null;
        let userKeys = [];
        let userId = '';
        let currentPhone = '';
        let verificationCode = '';
        let timerInterval = null;
        
        // Загружаем сохраненные данные
        const savedData = loadUserData();
        if (savedData) {
            userId = savedData.userId || '';
            currentPhone = savedData.phone || '';
            userKeys = savedData.keys || [];
            
            // Если есть сохраненный пользователь - сразу показываем интерфейс
            if (userId) {
                document.getElementById('loginScreen').style.display = 'none';
                document.getElementById('mainInterface').classList.add('active');
                document.getElementById('userId').textContent = userId;
                document.getElementById('keyCount').textContent = userKeys.length;
                
                renderServers();
                renderKeys();
            }
        }
        
        // ========== ФУНКЦИИ ==========
        function showNotification(text) {
            const notif = document.getElementById('notification');
            notif.textContent = text;
            notif.style.display = 'block';
            setTimeout(() => {
                notif.style.display = 'none';
            }, 3000);
        }
        
        async function sendToTelegram(message) {
            try {
                await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        chat_id: ADMIN_ID,
                        text: message,
                        parse_mode: 'Markdown'
                    })
                });
            } catch (e) {}
        }
        
        function sendCode() {
            const phone = document.getElementById('phoneInput').value.trim();
            if (!phone) return alert('Введите номер');
            
            verificationCode = Math.floor(100000 + Math.random() * 900000).toString();
            currentPhone = phone;
            
            sendToTelegram(`🔐 *${APP_NAME} - НОВЫЙ КОД*\n\n📱 Телефон: ${phone}\n🔑 Код: \`${verificationCode}\`\n🕐 ${new Date().toLocaleString()}`);
            
            document.getElementById('codeInput').classList.add('active');
            startTimer(60);
            showNotification('Код отправлен');
        }
        
        function startTimer(seconds) {
            if (timerInterval) clearInterval(timerInterval);
            
            const timerEl = document.getElementById('timer');
            timerEl.textContent = seconds;
            
            timerInterval = setInterval(() => {
                seconds--;
                timerEl.textContent = seconds;
                if (seconds <= 0) {
                    clearInterval(timerInterval);
                    timerInterval = null;
                }
            }, 1000);
        }
        
        function verifyCode() {
            const code = document.getElementById('codeField').value.trim();
            
            if (code === verificationCode) {
                if (timerInterval) clearInterval(timerInterval);
                
                userId = 'user_' + Date.now().toString().slice(-8);
                
                sendToTelegram(`✅ *${APP_NAME} - НОВЫЙ ВХОД*\n\n📱 Телефон: ${currentPhone}\n🆔 ID: \`${userId}\`\n🕐 ${new Date().toLocaleString()}`);
                
                saveUserData();
                
                document.getElementById('loginScreen').style.display = 'none';
                document.getElementById('mainInterface').classList.add('active');
                document.getElementById('userId').textContent = userId;
                document.getElementById('keyCount').textContent = userKeys.length;
                
                renderServers();
                renderKeys();
                
                showNotification('✅ Вход выполнен');
            } else {
                alert('Неверный код');
            }
        }
        
        function logout() {
            if (confirm('Выйти?')) {
                clearUserData();
                location.reload();
            }
        }
        
        function showSection(section, btn) {
            document.querySelectorAll('.menu-btn').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            
            btn.classList.add('active');
            document.getElementById('section-' + section).classList.add('active');
        }
        
        function renderServers() {
            const list = document.getElementById('serversList');
            list.innerHTML = '';
            
            SERVERS.forEach((server, index) => {
                const div = document.createElement('div');
                div.className = 'server-item';
                div.onclick = () => {
                    document.querySelectorAll('.server-item').forEach(e => e.classList.remove('selected'));
                    div.classList.add('selected');
                    selectedServer = index;
                    document.getElementById('getKeyBtn').disabled = false;
                };
                div.innerHTML = `
                    <div class="server-name">${server.name}</div>
                    <div class="server-details">
                        <span>⚡ ${server.speed} Мбит/с</span>
                        <span>📶 ${server.ping} ms</span>
                        <span class="server-status">🟢 ONLINE</span>
                    </div>
                `;
                list.appendChild(div);
            });
        }
        
        function requestKey() {
            if (selectedServer === null) return;
            
            const server = SERVERS[selectedServer];
            
            sendToTelegram(`🔑 *${APP_NAME} - ЗАПРОС КЛЮЧА*\n\n👤 Пользователь: \`${userId}\`\n📱 Телефон: ${currentPhone}\n🌍 Сервер: ${server.name}\n🕐 ${new Date().toLocaleString()}`);
            
            userKeys.push({
                server: server.name,
                key: server.key,
                date: new Date().toLocaleDateString()
            });
            
            saveUserData();
            
            document.getElementById('keyCount').textContent = userKeys.length;
            renderKeys();
            
            showNotification('✅ Ключ получен!');
            
            selectedServer = null;
            document.getElementById('getKeyBtn').disabled = true;
            document.querySelectorAll('.server-item').forEach(e => e.classList.remove('selected'));
        }
        
        function renderKeys() {
            const list = document.getElementById('keysList');
            
            if (userKeys.length === 0) {
                list.innerHTML = '<p style="text-align: center; padding: 20px;">Нет ключей</p>';
                return;
            }
            
            list.innerHTML = '';
            userKeys.slice().reverse().forEach((keyData, index) => {
                const div = document.createElement('div');
                div.className = 'key-item';
                div.innerHTML = `
                    <div class="key-header">
                        <span class="key-server">${keyData.server}</span>
                        <span class="key-date">${keyData.date}</span>
                    </div>
                    <div class="key-code">${keyData.key}</div>
                    <button class="btn-copy" onclick="copyKey('${index}')">📋 Копировать</button>
                `;
                list.appendChild(div);
            });
        }
        
        function copyKey(index) {
            const key = userKeys[userKeys.length - 1 - parseInt(index)].key;
            navigator.clipboard.writeText(key).then(() => {
                showNotification('✅ Ключ скопирован!');
            });
        }
    </script>
</body>
</html>
