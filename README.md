<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#3390ec">
    <title>Test Platformasi</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        /* Telegram-like reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: var(--tg-theme-bg-color, #ffffff);
            color: var(--tg-theme-text-color, #000000);
            width: 100%;
            min-height: 100vh;
            overflow-x: hidden;
            padding: 0;
            margin: 0;
            line-height: 1.4;
        }

        /* Telegram-like variables */
        :root {
            --telegram-blue: #3390ec;
            --telegram-blue-hover: #2481e0;
            --telegram-green: #34c759;
            --telegram-red: #ff3b30;
            --telegram-gray: #8e8e93;
            --telegram-light-gray: #f2f2f7;
            --telegram-border: #e5e5ea;
            --telegram-card: #ffffff;
            --telegram-shadow: rgba(0, 0, 0, 0.08);
        }

        /* APP CONTAINER - Telegram style */
        .app {
            width: 100%;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            background: var(--telegram-light-gray);
        }

        /* HEADER - Telegram style */
        .header {
            padding: 56px 16px 16px;
            background: var(--telegram-blue);
            color: white;
            position: relative;
            border-radius: 0 0 20px 20px;
            box-shadow: 0 2px 10px rgba(51, 144, 236, 0.2);
        }

        .header-content {
            max-width: 600px;
            margin: 0 auto;
        }

        h1 {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 6px;
            letter-spacing: -0.2px;
        }

        .subtitle {
            font-size: 15px;
            opacity: 0.9;
            font-weight: 400;
        }

        /* MENU CARDS - Telegram style */
        .menu {
            flex: 1;
            padding: 20px 16px 20px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-width: 600px;
            margin: 0 auto;
            width: 100%;
        }

        .card {
            background: var(--telegram-card);
            border-radius: 14px;
            padding: 18px 16px;
            cursor: pointer;
            transition: all 0.2s ease;
            user-select: none;
            border: 1px solid var(--telegram-border);
            box-shadow: 0 2px 8px var(--telegram-shadow);
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .card:hover {
            background: #fafafa;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
        }

        .card:active {
            transform: scale(0.995);
            background: #f6f6f6;
        }

        .card-icon {
            width: 44px;
            height: 44px;
            border-radius: 12px;
            background: var(--telegram-blue);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 22px;
            font-weight: 600;
            flex-shrink: 0;
        }

        .card-content {
            flex: 1;
        }

        .card .title {
            font-size: 17px;
            font-weight: 600;
            margin-bottom: 4px;
            color: var(--telegram-text, #000000);
        }

        .card .desc {
            font-size: 14px;
            color: var(--telegram-gray);
            line-height: 1.35;
        }

        .card-arrow {
            color: var(--telegram-gray);
            font-size: 18px;
            opacity: 0.6;
            transition: transform 0.2s;
        }

        .card:hover .card-arrow {
            transform: translateX(3px);
            opacity: 1;
        }

        /* AUTH SCREEN - Telegram style */
        .auth-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--telegram-blue);
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            z-index: 1000;
            transition: opacity 0.3s ease;
        }

        .auth-box {
            background: white;
            border-radius: 20px;
            padding: 32px 24px;
            text-align: center;
            max-width: 320px;
            width: 100%;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
            animation: slideUp 0.4s ease;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .auth-icon {
            width: 80px;
            height: 80px;
            background: var(--telegram-blue);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 24px;
            color: white;
            font-size: 36px;
        }

        .auth-text {
            font-size: 17px;
            margin-bottom: 24px;
            font-weight: 500;
            line-height: 1.4;
            color: #000000;
        }

        .auth-btn {
            background: var(--telegram-blue);
            border: none;
            color: white;
            padding: 14px 24px;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: all 0.2s ease;
            position: relative;
            overflow: hidden;
        }

        .auth-btn:hover {
            background: var(--telegram-blue-hover);
        }

        .auth-btn:active {
            transform: scale(0.98);
        }

        .auth-btn::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 5px;
            height: 5px;
            background: rgba(255, 255, 255, 0.5);
            opacity: 0;
            border-radius: 100%;
            transform: scale(1, 1) translate(-50%);
            transform-origin: 50% 50%;
        }

        .auth-btn:focus:not(:active)::after {
            animation: ripple 1s ease-out;
        }

        @keyframes ripple {
            0% {
                transform: scale(0, 0);
                opacity: 0.5;
            }
            100% {
                transform: scale(30, 30);
                opacity: 0;
            }
        }

        /* FOOTER - Telegram style */
        .footer {
            text-align: center;
            padding: 20px 16px;
            font-size: 13px;
            color: var(--telegram-gray);
            margin-top: auto;
            border-top: 1px solid var(--telegram-border);
            background: white;
        }

        /* BOTTOM NAVIGATION - Telegram style */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: white;
            border-top: 1px solid var(--telegram-border);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            z-index: 100;
            box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.05);
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: var(--telegram-gray);
            font-size: 12px;
            gap: 4px;
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 10px;
            transition: all 0.2s;
        }

        .nav-item:hover {
            background: var(--telegram-light-gray);
        }

        .nav-icon {
            font-size: 20px;
            opacity: 0.7;
        }

        .nav-item.active {
            color: var(--telegram-blue);
        }

        .nav-item.active .nav-icon {
            opacity: 1;
        }

        /* LOADER - Telegram style */
        .loader {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 0.8s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* STATUS BAR */
        .status-bar {
            height: 44px;
            background: transparent;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            z-index: 1000;
        }

        /* RESPONSIVE */
        @media (max-width: 480px) {
            .header {
                padding: 48px 16px 16px;
            }
            
            h1 {
                font-size: 20px;
            }
            
            .card {
                padding: 16px;
            }
            
            .card-icon {
                width: 40px;
                height: 40px;
                font-size: 20px;
            }
        }

        @media (min-width: 768px) {
            .menu {
                padding: 24px 20px;
                gap: 16px;
            }
            
            .card {
                padding: 20px;
                border-radius: 16px;
            }
        }

        /* DARK MODE SUPPORT */
        @media (prefers-color-scheme: dark) {
            :root {
                --telegram-card: #1c1c1e;
                --telegram-light-gray: #000000;
                --telegram-border: #38383a;
                --telegram-gray: #8e8e93;
                --telegram-shadow: rgba(0, 0, 0, 0.3);
            }
            
            body {
                background: #000000;
            }
            
            .auth-box {
                background: #1c1c1e;
                color: white;
            }
            
            .auth-text {
                color: white;
            }
            
            .bottom-nav {
                background: #1c1c1e;
            }
        }

        /* UTILITY CLASSES */
        .fade-in {
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .slide-up {
            animation: slideUp 0.4s ease;
        }

        /* ACCESSIBILITY */
        button:focus-visible,
        .card:focus-visible {
            outline: 2px solid var(--telegram-blue);
            outline-offset: 2px;
        }
    </style>
</head>
<body>
    <!-- STATUS BAR (Telegram uchun) -->
    <div class="status-bar"></div>

    <!-- AUTH SCREEN -->
    <div class="auth-screen" id="authScreen">
        <div class="auth-box">
            <div class="auth-icon">🔐</div>
            <div class="auth-text">Telegram hisobingiz bilan test platformasiga kiring</div>
            <button class="auth-btn" onclick="handleAuth()" id="authButton">
                <span id="authButtonText">Telegram orqali kirish</span>
                <span id="authLoader" style="display: none;" class="loader"></span>
            </button>
        </div>
    </div>

    <!-- MAIN APP -->
    <div class="app" id="mainApp" style="display: none;">
        <div class="header">
            <div class="header-content">
                <h1>Test Platformasi</h1>
                <div class="subtitle">Zamonaviy test yechish platformasi</div>
            </div>
        </div>
        
        <div class="menu">
            <div class="card" onclick="openFeature('test')" tabindex="0">
                <div class="card-icon">1</div>
                <div class="card-content">
                    <div class="title">Test Ishlash</div>
                    <div class="desc">Turli mavzulardagi testlarni yeching va bilimingizni sinab ko'ring</div>
                </div>
                <div class="card-arrow">›</div>
            </div>
            
            <div class="card" onclick="openFeature('converter')" tabindex="0">
                <div class="card-icon" style="background: var(--telegram-green);">2</div>
                <div class="card-content">
                    <div class="title">Fayl Konvertori</div>
                    <div class="desc">PDF va DOCX fayllarni AI yordamida XLSX formatiga o'tkazing</div>
                </div>
                <div class="card-arrow">›</div>
            </div>
            
            <div class="card" onclick="openFeature('auto')" tabindex="0">
                <div class="card-icon" style="background: #ff9500;">3</div>
                <div class="card-content">
                    <div class="title">Avto Test</div>
                    <div class="desc">Avtomatik test tuzish va natijalarni tahlil qilish</div>
                </div>
                <div class="card-arrow">›</div>
            </div>
            
            <div class="card" onclick="openFeature('tariff')" tabindex="0">
                <div class="card-icon" style="background: #af52de;">4</div>
                <div class="card-content">
                    <div class="title">Tariflar</div>
                    <div class="desc">Mos tarifni tanlang va to'liq imkoniyatlardan foydalaning</div>
                </div>
                <div class="card-arrow">›</div>
            </div>
        </div>
        
        <div class="footer">
            © 2024 Test Platformasi | Telegram Web App
        </div>
        
        <!-- BOTTOM NAVIGATION -->
        <div class="bottom-nav">
            <div class="nav-item active" onclick="switchTab('home')">
                <div class="nav-icon">🏠</div>
                <div>Bosh sahifa</div>
            </div>
            <div class="nav-item" onclick="switchTab('tests')">
                <div class="nav-icon">📝</div>
                <div>Testlar</div>
            </div>
            <div class="nav-item" onclick="switchTab('profile')">
                <div class="nav-icon">👤</div>
                <div>Profil</div>
            </div>
        </div>
    </div>

    <script>
        // ============================================
        // ASOSIY KOD - TELEGRAM STYLE
        // ============================================
        
        console.log("✅ Dastur ishga tushmoqda...");
        
        // DOM elementlari
        const authScreen = document.getElementById('authScreen');
        const mainApp = document.getElementById('mainApp');
        const authButton = document.getElementById('authButton');
        const authButtonText = document.getElementById('authButtonText');
        const authLoader = document.getElementById('authLoader');
        
        // Telegram WebApp obyekti
        let tg = window.Telegram?.WebApp;
        
        // Telegram WebApp mavjudligini tekshirish
        function checkTelegram() {
            if (window.Telegram && window.Telegram.WebApp) {
                console.log("✅ Telegram WebApp mavjud");
                return true;
            } else {
                console.log("🌐 Telegram WebApp mavjud emas (brauzerda test)");
                return false;
            }
        }
        
        // Dasturni ishga tushirish
        function initApp() {
            console.log("🚀 Dastur ishga tushyapti...");
            
            // Telefonda scrollni optimallashtirish
            document.body.style.overscrollBehavior = 'none';
            
            if (checkTelegram()) {
                // Telegram WebApp sozlamalari
                tg = window.Telegram.WebApp;
                
                try {
                    // Telegram WebApp'ni to'liq ekranga kengaytirish
                    tg.expand();
                    
                    // Telegram rang mavzusiga moslashish
                    applyTelegramTheme();
                    
                    // Back button'ni sozlash
                    setupBackButton();
                    
                    // Tayyor holatga o'tish
                    tg.ready();
                    
                    console.log("✅ Telegram WebApp muvaffaqiyatli sozlandi");
                    
                    // Foydalanuvchi autentifikatsiyasini tekshirish
                    setTimeout(checkAuth, 300);
                    
                } catch (error) {
                    console.error("❌ Telegram sozlashda xato:", error);
                    // Xato bo'lsa ham dasturni ko'rsatish
                    showMainApp();
                }
            } else {
                // Telegram WebApp yo'q (brauzerda test)
                console.log("🔧 Brauzer rejimida ishlayapman");
                simulateTelegramMode();
            }
        }
        
        // Telegram mavzusiga moslashish
        function applyTelegramTheme() {
            if (!tg) return;
            
            // Header rangini Telegram rangiga moslash
            document.querySelector('.header').style.backgroundColor = tg.themeParams.bg_color || '#3390ec';
            
            // Orqa fon rangini moslash
            document.body.style.backgroundColor = tg.themeParams.bg_color || '#ffffff';
            document.body.style.color = tg.themeParams.text_color || '#000000';
            
            // Status bar rangini moslash
            document.querySelector('.status-bar').style.backgroundColor = tg.themeParams.bg_color || '#3390ec';
        }
        
        // Back button'ni sozlash
        function setupBackButton() {
            if (!tg || !tg.BackButton) return;
            
            tg.BackButton.show();
            tg.BackButton.onClick(function() {
                if (tg.showConfirm) {
                    tg.showConfirm('Dasturdan chiqmoqchimisiz?', function(ok) {
                        if (ok) {
                            tg.close();
                        }
                    });
                } else {
                    tg.close();
                }
            });
        }
        
        // Brauzerda Telegram rejimini simulyatsiya qilish
        function simulateTelegramMode() {
            // Brauzerda test qilish uchun UI elementlarni sozlash
            document.querySelector('.status-bar').style.backgroundColor = '#3390ec';
            document.querySelector('.header').style.backgroundColor = '#3390ec';
            
            // 2 soniyadan keyin autentifikatsiyani tekshirish
            setTimeout(checkAuth, 2000);
        }
        
        // Autentifikatsiyani tekshirish
        function checkAuth() {
            if (tg && tg.initDataUnsafe) {
                const user = tg.initDataUnsafe?.user;
                
                if (user && user.id) {
                    // Foydalanuvchi mavjud - autentifikatsiyadan o'tgan
                    console.log(`✅ Foydalanuvchi: ${user.first_name} (ID: ${user.id})`);
                    
                    // Ma'lumotlarni saqlash
                    localStorage.setItem('tg_user_id', user.id);
                    localStorage.setItem('tg_user_name', user.first_name || 'Foydalanuvchi');
                    localStorage.setItem('tg_user_username', user.username || '');
                    
                    // Asosiy app'ni ko'rsatish
                    showMainApp();
                    return;
                }
            }
            
            // Foydalanuvchi autentifikatsiyadan o'tmagan yoki Telegram mavjud emas
            console.log("🔐 Autentifikatsiya talab qilinadi");
            showAuthScreen();
        }
        
        // Asosiy app'ni ko'rsatish
        function showMainApp() {
            console.log("📱 Asosiy app ko'rsatilmoqda...");
            
            // Auth screen'ni yashirish
            authScreen.style.opacity = '0';
            
            setTimeout(() => {
                authScreen.style.display = 'none';
                mainApp.style.display = 'flex';
                
                // Animatsiya effekti
                mainApp.classList.add('fade-in');
                
                // Scrollni yuqoriga olib chiqish
                window.scrollTo({ top: 0, behavior: 'smooth' });
                
                console.log("✅ Asosiy app ko'rsatildi");
            }, 300);
        }
        
        // Auth screen'ni ko'rsatish
        function showAuthScreen() {
            console.log("🔐 Auth screen ko'rsatilmoqda...");
            
            mainApp.style.display = 'none';
            authScreen.style.display = 'flex';
            
            setTimeout(() => {
                authScreen.style.opacity = '1';
            }, 10);
        }
        
        // Kirish tugmasi bosilganda
        function handleAuth() {
            // Yuklanish animatsiyasini ko'rsatish
            authButtonText.style.display = 'none';
            authLoader.style.display = 'inline-block';
            authButton.disabled = true;
            
            if (tg && tg.showAlert) {
                // Telegram WebApp mavjud
                setTimeout(() => {
                    tg.showAlert('Bot orqali kirish uchun /start buyrug\'ini yuboring.', () => {
                        // Botga qaytish
                        if (tg.close) {
                            tg.close();
                        }
                    });
                }, 500);
            } else {
                // Brauzerda test rejimi
                setTimeout(() => {
                    // Yuklanish animatsiyasini to'xtatish
                    authButtonText.style.display = 'inline';
                    authLoader.style.display = 'none';
                    authButton.disabled = false;
                    
                    // Test rejimida avtomatik kirish
                    console.log("🔧 Test rejimi: Avtomatik kirish");
                    localStorage.setItem('tg_user_id', '123456789');
                    localStorage.setItem('tg_user_name', 'Test Foydalanuvchi');
                    localStorage.setItem('tg_user_username', 'test_user');
                    
                    showMainApp();
                }, 1500);
            }
        }
        
        // Tab'larni almashtirish
        function switchTab(tabName) {
            console.log(`🔄 Tab o'zgartirildi: ${tabName}`);
            
            // Barcha tab'lardan faol klassini olib tashlash
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
            });
            
            // Faol tab'ga klass qo'shish
            event.currentTarget.classList.add('active');
            
            // Tab bo'yicha harakat
            switch(tabName) {
                case 'home':
                    window.scrollTo({ top: 0, behavior: 'smooth' });
                    break;
                case 'tests':
                    tg?.showAlert('Testlar bo\'limi tez orada ochiladi!');
                    break;
                case 'profile':
                    openFeature('profile');
                    break;
            }
        }
        
        // Feature'lar
        function openFeature(feature) {
            console.log(`🎯 Feature ochilmoqda: ${feature}`);
            
            // Foydalanuvchi ma'lumotlari
            const userId = localStorage.getItem('tg_user_id') || 'Noma\'lum';
            const userName = localStorage.getItem('tg_user_name') || 'Mehmon';
            const userUsername = localStorage.getItem('tg_user_username');
            
            let message = '';
            let featureName = '';
            
            switch(feature) {
                case 'test':
                    featureName = "🧪 Test Ishlash";
                    message = `${featureName}\n\nSalom, ${userName}!\nTest ishlash bo'limi tez orada ochiladi.\nBu yerda turli mavzulardagi testlarni yechishingiz mumkin bo'ladi.`;
                    break;
                    
                case 'converter':
                    featureName = "🔄 Fayl Konvertori";
                    message = `${featureName}\n\nPDF va DOCX fayllarni XLSX formatiga o'tkazish tizimi ishlab chiqilmoqda.\nTez orada foydalanishingiz mumkin bo'ladi.`;
                    break;
                    
                case 'auto':
                    featureName = "🤖 Avto Test";
                    message = `${featureName}\n\nAvtomatik test tuzish va natijalarni tahlil qilish tizimi yaqin orada ishga tushadi.`;
                    break;
                    
                case 'tariff':
                    featureName = "💰 Tariflar";
                    message = `${featureName}\n\nFoydalanuvchi ID: ${userId}${userUsername ? `\nUsername: @${userUsername}` : ''}\n\nTarif tanlash bo'limi tez orada ochiladi.`;
                    break;
                    
                case 'profile':
                    featureName = "👤 Profil";
                    message = `${featureName}\n\nIsm: ${userName}${userUsername ? `\nUsername: @${userUsername}` : ''}\nID: ${userId}\n\nProfil sozlamalari tez orada ochiladi.`;
                    break;
                    
                default:
                    featureName = "❌ Xatolik";
                    message = 'Bu funksiya hozircha mavjud emas!';
            }
            
            // Xabarni ko'rsatish
            if (tg && tg.showAlert) {
                tg.showAlert(message);
            } else {
                alert(message);
            }
            
            // Haptik feedback (agar mavjud bo'lsa)
            vibrate(50);
        }
        
        // ============================================
        // EVENT LISTENERS
        // ============================================
        
        // DOM yuklanganda
        document.addEventListener('DOMContentLoaded', function() {
            console.log("📄 DOM yuklandi");
            
            // Ekran o'lchamini sozlash
            document.documentElement.style.height = '100%';
            document.body.style.height = '100%';
            
            // 0.5 soniyadan keyin dasturni ishga tushirish
            setTimeout(initApp, 500);
        });
        
        // Resize event
        window.addEventListener('resize', function() {
            // Mobil qurilmalar uchun ekran o'lchamini sozlash
            document.documentElement.style.height = window.innerHeight + 'px';
        });
        
        // Load event
        window.addEventListener('load', function() {
            console.log("🖼️ Sahifa to'liq yuklandi");
        });
        
        // ============================================
        // QO'SHIMCHA FUNKSIYALAR
        // ============================================
        
        // Vibrate effect (mobil uchun)
        function vibrate(duration = 50) {
            if (navigator.vibrate) {
                navigator.vibrate(duration);
            }
        }
        
        // Card'larga click effekt
        document.querySelectorAll('.card').forEach(card => {
            card.addEventListener('click', function() {
                vibrate(30);
                
                // Click effekti
                this.style.transform = 'scale(0.98)';
                setTimeout(() => {
                    this.style.transform = '';
                }, 150);
            });
            
            // Klaviatura bilan foydalanish imkoniyati
            card.addEventListener('keydown', function(e) {
                if (e.key === 'Enter' || e.key === ' ') {
                    e.preventDefault();
                    this.click();
                }
            });
        });
        
        // Tab'larga click effekt
        document.querySelectorAll('.nav-item').forEach(tab => {
            tab.addEventListener('click', function() {
                vibrate(20);
            });
        });
        
        // ============================================
        // BRAUZERDA TEST QILISH UCHUN (faqat rivojlanish uchun)
        // ============================================
        
        // Agar Telegram yo'q bo'lsa, test rejimida ishlash
        if (!checkTelegram()) {
            console.log("🔧 Test rejimi yoqildi");
            
            // URL parametrlari orqali test rejimini boshqarish
            const urlParams = new URLSearchParams(window.location.search);
            if (urlParams.has('autologin')) {
                console.log("🔧 Auto-login parametri mavjud");
                setTimeout(() => {
                    localStorage.setItem('tg_user_id', '123456789');
                    localStorage.setItem('tg_user_name', 'Test Foydalanuvchi');
                    localStorage.setItem('tg_user_username', 'test_user');
                    showMainApp();
                }, 1000);
            }
        }
        
        // ============================================
        // TELEGRAM EVENT HANDLERS
        // ============================================
        
        // Telegram tema o'zgarishi
        if (tg && tg.onEvent) {
            tg.onEvent('themeChanged', applyTelegramTheme);
            tg.onEvent('viewportChanged', function() {
                tg.expand();
            });
        }
        
    </script>
</body>
</html>
