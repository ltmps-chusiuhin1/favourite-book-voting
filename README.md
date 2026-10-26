<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我最喜愛隨身書投票</title>
    
    
    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;700;900&family=Noto+Sans+TC:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff7eb3;
            --secondary: #ff758c;
            --text-color: #555;
            --glass-bg: rgba(255, 255, 255, 0.75);
            --glass-border: rgba(255, 255, 255, 0.5);
        }
        
        body {
            font-family: 'Nunito', 'Noto Sans TC', sans-serif;
            margin: 0;
            padding: 20px;
            color: var(--text-color);
            text-align: center;
            overflow-x: hidden;
            background: linear-gradient(-45deg, #ff9a9e, #fecfef, #a1c4fd, #c2e9fb);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .light-layers {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
            pointer-events: none; z-index: -1;
            background: 
                radial-gradient(circle at 20% 30%, rgba(255, 255, 255, 0.6) 0%, transparent 40%),
                radial-gradient(circle at 80% 70%, rgba(255, 240, 200, 0.5) 0%, transparent 50%),
                radial-gradient(circle at 50% 50%, rgba(255, 200, 255, 0.4) 0%, transparent 60%);
            filter: blur(30px);
            animation: pulseLight 8s alternate infinite ease-in-out;
        }

        @keyframes pulseLight {
            0% { transform: scale(1); opacity: 0.7; }
            100% { transform: scale(1.1) translate(20px, -20px); opacity: 1; }
        }

        .floating-elements {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: -2; overflow: hidden;
        }
        .floating-elements span {
            position: absolute; bottom: -10%;
            animation: floatUp linear infinite;
            opacity: 0.6; filter: drop-shadow(0 4px 6px rgba(0,0,0,0.1));
        }
        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg) scale(0.8); opacity: 0; }
            10% { opacity: 0.7; }
            90% { opacity: 0.7; }
            100% { transform: translateY(-120vh) rotate(20deg) scale(1.2); opacity: 0; }
        }

        /* 標題與漸層文字 */
        h1, h2 {
            font-weight: 900;
            letter-spacing: 2px;
            filter: drop-shadow(2px 2px 0px #fff) drop-shadow(0px 4px 10px rgba(255, 94, 126, 0.4));
            margin-bottom: 10px;
        }
        h1 { font-size: 2.8em; }
        
        .gradient-text {
            background: linear-gradient(90deg, #ff5e7e, #ff9a9e, #ff5e7e);
            background-size: 200% auto;
            color: transparent;
            -webkit-background-clip: text;
            background-clip: text;
            animation: shineText 3s linear infinite;
            display: inline-block;
        }
        @keyframes shineText { to { background-position: 200% center; } }
        
        .emoji {
            display: inline-block;
            -webkit-text-fill-color: initial;
            color: initial;
        }
        
        .view { 
            display: none; animation: fadeIn 0.6s cubic-bezier(0.25, 0.8, 0.25, 1);
            background: var(--glass-bg); backdrop-filter: blur(15px); -webkit-backdrop-filter: blur(15px);
            border: 2px solid var(--glass-border); border-radius: 30px;
            padding: 30px; max-width: 1000px; margin: 0 auto;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            position: relative; 
        }
        .view.active { display: block; }
        
        @keyframes fadeIn { 
            from { opacity: 0; transform: translateY(20px) scale(0.98); } 
            to { opacity: 1; transform: translateY(0) scale(1); } 
        }

        /* 管理員登入按鈕 */
        .admin-login-btn {
            position: absolute;
            top: 20px; left: 20px;
            background: rgba(255,255,255,0.8); border: 1px solid rgba(0,0,0,0.1);
            color: #666; padding: 8px 15px; border-radius: 20px;
            font-size: 0.9em; font-weight: bold; cursor: pointer;
            transition: all 0.3s ease; box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            z-index: 10;
        }
        .admin-login-btn:hover { background: rgba(255,255,255,1); transform: scale(1.05); }

        .btn {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white; border: none; padding: 15px 35px; font-size: 1.2em;
            font-weight: bold; border-radius: 50px; cursor: pointer;
            box-shadow: 0 5px 15px rgba(255,117,140,0.4), inset 0 -3px 0 rgba(0,0,0,0.1);
            transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1); margin: 10px;
            text-transform: uppercase; position: relative; overflow: hidden;
        }
        .btn::after {
            content: ""; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
            background: rgba(255,255,255,0.2); transform: rotate(45deg); transition: 0.5s; opacity: 0;
        }
        .btn:hover { 
            transform: translateY(-5px) scale(1.05); 
            box-shadow: 0 10px 25px rgba(255,117,140,0.6), 0 0 15px rgba(255,117,140,0.5), inset 0 -3px 0 rgba(0,0,0,0.1); 
        }
        .btn:hover::after { left: 100%; opacity: 1; }
        .btn-secondary { background: linear-gradient(45deg, #4facfe, #00f2fe); box-shadow: 0 5px 15px rgba(79,172,254,0.4), inset 0 -3px 0 rgba(0,0,0,0.1); }
        .btn-secondary:hover { box-shadow: 0 10px 25px rgba(79,172,254,0.6), 0 0 15px rgba(79,172,254,0.5), inset 0 -3px 0 rgba(0,0,0,0.1); }

        .grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
            gap: 25px; margin: 30px auto; padding: 10px;
        }
        .grid-3 {
            display: grid; grid-template-columns: repeat(3, 1fr);
            gap: 20px; margin: 20px auto; padding: 10px;
        }

        .card {
            background: rgba(255, 255, 255, 0.9); border-radius: 25px; cursor: pointer; position: relative;
            overflow: hidden; box-shadow: 0 8px 20px rgba(0,0,0,0.06); transition: all 0.3s ease;
            border: 2px solid white;
        }
        
        /* 年級方格基礎設定 */
        .grade-card {
            aspect-ratio: 1; display: flex; align-items: center; justify-content: center;
            font-size: 1.8em; font-weight: 900; color: white; text-align: center; line-height: 1.3;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
        }
        .grade-card:hover { transform: translateY(-10px) scale(1.05); box-shadow: 0 20px 30px rgba(0,0,0,0.15); border-color: rgba(255,255,255,0.8); }

        /* 六種不同漸變色 (一至六年級) */
        .grid-3 .grade-card:nth-child(1) { background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%); }
        .grid-3 .grade-card:nth-child(2) { background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%); }
        .grid-3 .grade-card:nth-child(3) { background: linear-gradient(135deg, #d4fc79 0%, #96e6a1 100%); }
        .grid-3 .grade-card:nth-child(4) { background: linear-gradient(135deg, #84fab0 0%, #8fd3f4 100%); }
        .grid-3 .grade-card:nth-child(5) { background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%); }
        .grid-3 .grade-card:nth-child(6) { background: linear-gradient(135deg, #a18cd1 0%, #fbc2eb 100%); }

        @media (max-width: 500px) {
            .grade-card { font-size: 1.3em; } .grid-3 { gap: 10px; } .view { padding: 15px; }
            .admin-login-btn { top: 10px; left: 10px; padding: 5px 10px; font-size: 0.8em; }
        }

        /* 書本外層容器 */
        .book-wrapper {
            position: relative;
            display: flex; justify-content: center;
            cursor: pointer;
            -webkit-tap-highlight-color: transparent; 
        }
        .book-wrapper:hover { z-index: 100; } 
        .book-wrapper.touch-active { z-index: 100; }

        .book-card {
            width: 100%; aspect-ratio: 3/4; display: flex; flex-direction: column;
            align-items: center; justify-content: center; font-size: 1.1em; color: #888;
            border: 5px solid transparent; padding: 0; text-align: center; font-weight: bold;
            background-color: #fff;
            transition: all 0.3s ease;
        }
        .book-card img {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; z-index: 1;
            transition: transform 0.5s ease;
        }
        
        .recommender-tag-floating {
            position: absolute; top: 10px; left: -2px; z-index: 3;
            background: linear-gradient(90deg, var(--primary), var(--secondary)); color: white;
            padding: 4px 10px; border-radius: 0 15px 15px 0; font-size: 0.8em; font-weight: bold;
            box-shadow: 2px 2px 8px rgba(0,0,0,0.2); text-shadow: 1px 1px 2px rgba(0,0,0,0.2);
        }

        /* 書本卡片的已選狀態 */
        .book-card.selected { 
            border: 6px solid #00f2fe; 
            transform: scale(0.95); 
            background-color: #f0faff; 
            animation: selectedPulse 2s infinite alternate;
        }
        
        @keyframes selectedPulse {
            0% { box-shadow: 0 0 15px rgba(0, 242, 254, 0.5), inset 0 0 15px rgba(0, 242, 254, 0.3); border-color: #00f2fe; }
            100% { box-shadow: 0 0 30px rgba(0, 242, 254, 0.9), inset 0 0 25px rgba(0, 242, 254, 0.6); border-color: #4facfe; }
        }

        .book-card.selected::after {
            content: '✨已選✨';
            position: absolute; bottom: 10px; right: 10px; font-size: 0.9em; z-index: 5;
            background: linear-gradient(45deg, #4facfe, #00f2fe); color: white; 
            border-radius: 15px; padding: 5px 10px; 
            box-shadow: 0 4px 10px rgba(0, 242, 254, 0.5); border: 2px solid white;
            font-weight: 900;
            animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        /* 🌟 升級版魔法放大懸浮框：加寬並允許自動延展高度以顯示所有文字 */
        .book-detail-popup {
            position: absolute;
            top: 50%; left: 50%;
            transform: translate(-50%, -40%) scale(0.8);
            width: 320px; /* 加寬視窗以容納更多文字 */
            max-width: 85vw; /* 確保在手機小螢幕上不會超出畫面 */
            max-height: 85vh; /* 防止在極小螢幕上超出上下邊界 */
            overflow-y: auto; /* 萬一螢幕極小，允許整個框滑動 */
            background: rgba(255, 255, 255, 0.98);
            backdrop-filter: blur(15px); -webkit-backdrop-filter: blur(15px);
            border: 3px solid #ff9a9e; border-radius: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3), 0 0 30px rgba(255, 126, 179, 0.5);
            padding: 20px;
            z-index: 101;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            pointer-events: none; /* 未顯示時不阻擋滑鼠 */
            display: flex; flex-direction: column; align-items: center;
        }

        /* 懸浮框展開時解鎖滑鼠與觸控互動 (pointer-events: auto)，讓滑鼠移出底框時懸浮框不會消失 */
        @media (hover: hover) {
            .book-wrapper:hover .book-detail-popup {
                opacity: 1; visibility: visible;
                transform: translate(-50%, -50%) scale(1);
                pointer-events: auto; 
            }
        }
        
        .book-wrapper.touch-active .book-detail-popup {
            opacity: 1; visibility: visible;
            transform: translate(-50%, -50%) scale(1);
            pointer-events: auto;
        }

        .book-card.selected + .book-detail-popup {
            border: 4px solid #00f2fe;
            background: rgba(240, 250, 255, 0.98); 
            box-shadow: 0 20px 40px rgba(0,0,0,0.3), 0 0 45px rgba(0, 242, 254, 0.6);
        }
        
        .book-card.selected + .book-detail-popup::after {
            content: '✨ 已選';
            position: absolute;
            top: 10px; right: 10px; 
            background: linear-gradient(45deg, #4facfe, #00f2fe); color: white;
            padding: 5px 12px; border-radius: 20px;
            font-size: 0.9em; font-weight: 900;
            box-shadow: 0 5px 15px rgba(0, 242, 254, 0.6); border: 2px solid white;
            animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .popup-img { width: 110px; height: 145px; object-fit: cover; border-radius: 12px; margin-bottom: 10px; box-shadow: 0 5px 15px rgba(0,0,0,0.15); border: 2px solid #fff; flex-shrink: 0; }
        .popup-title { margin: 0 0 6px 0; font-size: 1.25em; color: var(--secondary); font-weight: 900; line-height: 1.3; text-shadow: none; background: none; }
        .popup-recommender { background: linear-gradient(90deg, #a18cd1, #fbc2eb); color: white; padding: 4px 12px; border-radius: 20px; font-size: 0.85em; font-weight: bold; margin-bottom: 10px; box-shadow: 0 3px 8px rgba(0,0,0,0.1); flex-shrink: 0; }
        
        /* 🌟 移除高度限制與拉杆，一次過完整顯示所有簡介文字 */
        .popup-desc { 
            font-size: 0.95em; color: #444; line-height: 1.6; font-weight: normal; 
            text-align: justify; padding: 10px 12px; 
            background: rgba(255, 240, 245, 0.7); border-radius: 15px; width: 100%; box-sizing: border-box;
        }
        
        .popup-vote-btn {
            margin-top: 14px;
            background: linear-gradient(45deg, #ff7eb3, #ff758c);
            color: white; font-weight: bold; font-size: 1.05em;
            padding: 8px 25px; border-radius: 25px;
            box-shadow: 0 4px 10px rgba(255,117,140,0.4);
            animation: pulseBtnPink 1.5s infinite;
            transition: all 0.3s ease;
            flex-shrink: 0;
        }

        @keyframes pulseBtnPink {
            0% { transform: scale(1); box-shadow: 0 4px 10px rgba(255,117,140,0.4); }
            50% { transform: scale(1.05); box-shadow: 0 6px 15px rgba(255,117,140,0.6); }
            100% { transform: scale(1); box-shadow: 0 4px 10px rgba(255,117,140,0.4); }
        }
        @keyframes pulseBtnBlue {
            0% { transform: scale(1); box-shadow: 0 4px 10px rgba(0, 242, 254, 0.4); }
            50% { transform: scale(1.05); box-shadow: 0 6px 15px rgba(0, 242, 254, 0.6); }
            100% { transform: scale(1); box-shadow: 0 4px 10px rgba(0, 242, 254, 0.4); }
        }

        @keyframes popIn { 0% { transform: scale(0.5); opacity: 0; } 100% { transform: scale(1); opacity: 1; } }

        /* 龍虎榜樣式 */
        .leaderboard-item {
            background: rgba(255, 255, 255, 0.85); margin: 12px auto; max-width: 650px; padding: 15px 25px;
            border-radius: 20px; display: flex; justify-content: space-between;
            align-items: center; font-size: 1.2em; font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05); text-align: left;
            border: 1px solid rgba(255,255,255,1); transition: transform 0.3s ease;
        }
        .leaderboard-item:hover { transform: scale(1.02); box-shadow: 0 8px 25px rgba(255,117,140,0.2); }
        .leaderboard-img {
            width: 50px; height: 70px; object-fit: cover; border-radius: 8px; 
            margin: 0 15px; background-color: #f0f0f0; border: 2px solid #fff; box-shadow: 0 3px 6px rgba(0,0,0,0.1);
        }
        .leaderboard-item span.votes {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white; padding: 8px 20px; border-radius: 20px; white-space: nowrap; margin-left: 10px; box-shadow: 0 3px 8px rgba(255,117,140,0.4);
        }
        
        #user-info { margin-bottom: 20px; font-weight: bold; color: #666; background: rgba(255,255,255,0.6); display: inline-block; padding: 5px 20px; border-radius: 20px;}
        
        #google-btn-container { 
            display: flex; justify-content: center; margin-top: 30px; 
            position: relative; z-index: 5; 
        }
    </style>
</head>
<body>

    <div class="light-layers"></div>

    <div class="floating-elements">
        <span style="left: 10%; animation-duration: 12s; font-size: 2.5em; animation-delay: 0s;">📖</span>
        <span style="left: 85%; animation-duration: 15s; font-size: 3em; animation-delay: 2s;">☁️</span>
        <span style="left: 45%; animation-duration: 10s; font-size: 2em; animation-delay: 5s;">📚</span>
        <span style="left: 25%; animation-duration: 8s; font-size: 1.5em; animation-delay: 1s;">✨</span>
        <span style="left: 70%; animation-duration: 14s; font-size: 1.8em; animation-delay: 3s;">🎈</span>
        <span style="left: 90%; animation-duration: 9s; font-size: 1.2em; animation-delay: 6s;">✨</span>
        <span style="left: 5%; animation-duration: 16s; font-size: 4em; animation-delay: 7s; opacity: 0.4;">☁️</span>
    </div>

    <!-- 1. 登入畫面 -->
    <div id="login-view" class="view active">
        <!-- 管理員登入按鈕 -->
        <button class="admin-login-btn" onclick="adminLogin()">⚙️ 管理員登入</button>
        
        <br><br>
        <h1><span class="emoji">📖</span> <span class="gradient-text">我最喜愛隨身書投票</span> <span class="emoji">🌟</span></h1>
        <p style="font-size: 1.2em; font-weight: bold; color: #666;">進入夢幻繪本世界，請使用學校 Google 帳戶登入</p>
        <div id="google-btn-container"></div>
    </div>

    <!-- 2. 主選單畫面 -->
    <div id="main-menu-view" class="view">
        <h1><span class="emoji">📖</span> <span class="gradient-text">我最喜愛隨身書投票</span> <span class="emoji">✨</span></h1>
        <div id="user-info"></div><br>
        <button class="btn btn-secondary" onclick="showLeaderboardMenu()">🏆 查看龍虎榜</button>
        <button class="btn" style="background: rgba(200,200,200,0.8); box-shadow: none; color: #555;" onclick="logout()">登出</button>
        
        <div class="grid-3" id="grade-grid"></div>
    </div>

    <!-- 3. 投票畫面 -->
    <div id="voting-view" class="view">
        <h2 id="voting-title" style="font-size: 2.5em;"><span class="gradient-text">年級投票</span></h2>
        <p style="font-weight: bold;">點擊選擇多本喜愛的隨身書，完成後點擊最下方的「提交投票」</p>
        <button class="btn btn-secondary" onclick="showMainMenu()">⬅️ 返回主選單</button>
        
        <div class="grid" id="book-grid"></div>

        <button class="btn" style="font-size: 1.5em; width: 80%; max-width: 400px; margin-top: 30px; padding: 20px;" onclick="submitVote()">🚀 提交投票</button>
    </div>

    <!-- 4. 龍虎榜 獨立選單 -->
    <div id="leaderboard-menu-view" class="view">
        <h1><span class="emoji">🏆</span> <span class="gradient-text">我最喜愛隨身書龍虎榜</span> <span class="emoji">🏆</span></h1>
        <button class="btn btn-secondary" onclick="showMainMenu()">⬅️ 返回主選單</button>
        
        <div style="max-width: 900px; margin: 30px auto 10px; padding: 0 10px;">
            <div class="card grade-card" style="background: linear-gradient(135deg, #f6d365 0%, #fda085 100%); aspect-ratio: auto; padding: 25px; flex-direction: row; gap: 15px; font-size: 2em; box-shadow: 0 10px 20px rgba(253,160,133,0.3);" onclick="openLeaderboardDetail('top')">
                👑 各級首名
            </div>
        </div>

        <div class="grid-3" id="leaderboard-grid"></div>
    </div>

    <!-- 5. 龍虎榜 詳細內頁 -->
    <div id="leaderboard-detail-view" class="view">
        <h1 id="leaderboard-detail-title" style="font-size: 2.5em;"><span class="emoji">🏆</span> <span class="gradient-text">龍虎榜內頁</span> <span class="emoji">🏆</span></h1>
        <button class="btn btn-secondary" onclick="showLeaderboardMenu()">⬅️ 返回龍虎榜選單</button>
        <div id="leaderboard-list" style="margin-top: 20px;"></div>
    </div>

    <!-- Firebase SDK (Firestore) -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.1/firebase-app.js";
        import { getFirestore, doc, setDoc, getDocs, collection } from "https://www.gstatic.com/firebasejs/10.8.1/firebase-firestore.js";

        // ==========================================
        // 觸控設備精準偵測與隱藏系統
        // ==========================================
        let isUsingTouch = false;
        
        window.addEventListener('touchstart', () => { 
            isUsingTouch = true; 
        }, { passive: true });

        const hidePopups = (e) => {
            if (!e.target.closest('.book-wrapper')) {
                document.querySelectorAll('.book-wrapper').forEach(w => w.classList.remove('touch-active'));
            }
        };
        document.addEventListener('click', hidePopups);
        document.addEventListener('touchstart', hidePopups, { passive: true }); 

        // 圖書資料
        const booksConfig = {
            '一年級': [
                { id: 'P1_1', img: 'P1_1.jpg', title: "繪本西遊記", desc: "繪本西遊記有豐富的圖片，內容吸引，有很多妙想天開、生動有趣的故事，我特別喜歡三打白骨精這個情節呢！你們也來一起看吧！", recommender: "1A 曾約舜" },
                { id: 'P1_2', img: 'P1_2.jpg', title: "黃金便便大出來", desc: "我們要多吃膳食纖维的食物。", recommender: "1A 余潤霖" },
                { id: 'P1_3', img: 'P1_3.png', title: "猜猜謎多識字 (2)：漫畫版猜字謎大挑戰", desc: "我推薦的是《猜猜迷，多識字》，首先這本書體積比較小，只比我的手大一點，方便小朋友平時放在書包裡，隨時隨地可以立刻拿出來看，也不會阻礙到其他人。其次這本書用漫畫畫出謎語好有趣，在謎語的下面還有提示，令小朋友並不覺得難度太大而放棄繼續看。最後這本書還可以當作小朋友之間的遊戲，互相猜謎語。這本書讓我們在猜謎語的樂趣裡不知不覺學到了很多新詞語。", recommender: "1A 馮楚萱" },
                { id: 'P1_4', img: 'P1_4.jpg', title: "5分鐘專注力訓練 迷宮100：神秘恐龍", desc: "書本裏包含了100迷宮冒險遊戲，可以培養我們專注力和提高智力，而且每一頁都有不同的場景和任務 ， 要不斷嘗試才能找出正確的出口。", recommender: "1B 馮朗僖" },
                { id: 'P1_5', img: 'P1_5.jpg', title: "屁屁偵探: 噗噗! 有兩個屁屁偵探?!", desc: "這本書講述屁屁偵探在慶典中解開「分身之謎」的故事。情節幽默、畫面可愛，還可以玩找找看遊戲，值得推薦！", recommender: "1B 招樂謙" },
                { id: 'P1_6', img: 'P1_6.jpg', title: "The Digits: Double the Fun", desc: "It’s Digits 3’s birthday, and numbers 1 to 10 are invited to the party! When things start going wrong, the helpful digits step in to save the day. It’s a super fun and playful book that makes learning numbers joyful to us.", recommender: "1B 戴以軒" },
                { id: 'P1_7', img: 'P1_7.jpg', title: "明天的我", desc: "今天做不到？明天一定做到！幽默畫風滿載正能量，鼓勵小朋友勇敢嘗試，明天會變得更強！", recommender: "1C 劉栩妤" },
                { id: 'P1_8', img: 'P1_8.jpg', title: "哇！這是餐車！", desc: "這是一本有趣把各種熟悉既交通工具改裝成不同餐廳的餐車圖書，裡面餐廳都是不同類型，書上圖畫都一一細膩畫出餐廳內食物種類，特色。而我是非常喜歡食物題材圖書，看完非常開心。", recommender: "1C 全若瑜" },
                { id: 'P1_9', img: 'P1_9.png', title: "ZOE ZELLER and the terrible thieves ", desc: "可以學英文，故事內容有魔法，有教人煮食，刺激，驚嚇。", recommender: "1D 郭豐燁" },
                { id: 'P1_10', img: 'P1_10.jpg', title: "When l'm feeling Sad", desc: "這本書是《When I'm Feeling SAD》,透過小兔子掉眼淚的情景,讓小朋友認識「傷心」的情緒，學習理解並接納自己的難過，尋找陪伴與安慰的方法。", recommender: "1E 陳姸稀" }
            ],
            '二年級': [
                { id: 'P2_1', img: 'P2_1.jpg', title: "X尋寶探險隊 36: 夜光斷風劍", desc: "我推薦這本圖書是因為這本圖書的主角們有一個十分值得我學習的品格強項：「團隊精神」。他們通過團隊合作和勇敢的精神，最終戰勝了怪獸。我從這個故事中學習到通過團隊合作，能夠更容易更迅速地解決問題。", recommender: "2A 梁浩宸" },
                { id: 'P2_2', img: 'P2_2.jpg', title: "貓奴的浪漫", desc: "書裡的女孩和兩隻小貓一起生活，記錄了她們的日常，從吃飯、洗澡、玩耍到睡覺，畫面可愛又溫馨，我也喜歡貓咪，讀起來有共鳴，能令我學會愛護動物。", recommender: "2A 高之瑤" },
                { id: 'P2_3', img: 'P2_3.jpg', title: "Oxford Story Tree New Edition 5-Pink: The Bully", desc: "A new girl named Rosie comes to school. She acts unfriendly and starts bullying the children. The magic key takes  her  on an adventure and turn into terrible things.", recommender: "2A 陳凱儒" },
                { id: 'P2_4', img: 'P2_4.png', title: "爭吵有用嗎？", desc: "尼克、莊尼、阿德因為爭奪合歡樹而爭吵，幸好在麗莎的勸喻下，大家學會了以和平的方式溝通。以上情節相信大家也似曾相識，本書透過生活化的故事，讓我們認識甚麼是「非暴力溝通」。", recommender: "2A 曾昭然" },
                { id: 'P2_5', img: 'P2_5.png', title: "Is This a Plum?", desc: "很有趣的圖書，從前頁的小洞透視後頁圖畫的部份內容，引發讀者的好奇心和思考力，猜想後頁長得像棗的是甚麼呢？", recommender: "2B 梁譯文" },
                { id: 'P2_6', img: 'P2_6.jpg', title: "Arthur's Reading Race", desc: "這本書透過兩兄妹的有趣互動，非常適合鼓勵剛開始學習英文的小朋友，會發現原來生活周遭處處都是可以學習的英文字母與標誌！", recommender: "2B 招樂宜" },
                { id: 'P2_7', img: 'P2_7.jpg', title: "英國權威科學家解答世界孩子科學100問", desc: "你知道小狗會哭嗎？你又知不知鼻屎是怎樣進入我們的鼻子？你知道一盞燈怎麼會發亮？而星星為何又會一閃一亮？這本書介紹人體、生物、自然科學及物理知識，可謂上知天文，下曉地理。", recommender: "2D 王智皜" },
                { id: 'P2_8', img: 'P2_8.jpg', title: "Micky's Magic Pencil", desc: "故事說：「Micky有了，有一個同學不信Micky支魔法筆會有魔法，然後好多同學都用了Micky的魔法筆，然後同學不見了Micky的魔法筆Micky很不開心，同學們在找Micky的魔法筆，最後找到了。", recommender: "2D 何 冰" },
                { id: 'P2_9', img: 'P2_9.jpg', title: "只有我們能夠拯救地球", desc: "以12個孩子面對氣候危機解難的故事，激發小小年紀的孩子們對地球盡一份心力，強調拯救世界不是大人才能做得到。", recommender: "2D 李敬華" },
                { id: 'P2_10', img: 'P2_10.jpg', title: "黑寶生氣了", desc: "這本書有隻可愛小貓叫黑寶，牠發脾氣時會嚇跑朋友。跟牠一起看書，就能學會冷靜，不再被生氣怪獸控制！", recommender: "2E 吳芊語" }
            ],
            '三年級': [
                { id: 'P3_1', img: 'P3_1.jpg', title: "InvestiGators: Take the Plunge", desc: "it’s attractive and Creative and funny And some songs.", recommender: "3A 陳子樂" },
                { id: 'P3_2', img: 'P3_2.jpg', title: "水中最強王圖鑑：NO.1爭奪淘汰賽", desc: "這本書超棒！古代海怪跟巨鯊在水中大對決，要搶奪海洋最強霸主寶座！戰鬥圖片真實又刺激，快跟我一起看誰能贏！", recommender: "3A 蘇飛" },
                { id: 'P3_3', img: 'P3_3.jpg', title: "Dog Man 13: Big Jim Begins", desc: "圖書以幽默的手法去講述Dog Man、Big Jim及Grampa的冒險故事，書本圖文並茂、字句簡單，同時傳遞想像力、友誼等的正向思考價值。", recommender: "3A 李懿洋" },
                { id: 'P3_4', img: 'P3_4.jpg', title: "小妖怪系列04: 校園裡的小妖怪 1", desc: "故事是講述一所校園裡住了許多各色各樣的小妖怪，他們大多很善良，只是比較愛捉弄同學們，他們會在學校裡的每一個角落出現，故事既驚險又有趣！", recommender: "3A 梁正熙" },
                { id: 'P3_5', img: 'P3_5.png', title: "繽紛中華：中國節日 清明節", desc: "清明節是中國傳統及重要的節日。從這本書中，我認識了清明節的起源及習俗。我明白到我們可透過拜祭祖先，表達對他們的思念與敬意。", recommender: "3B 陳芷微" },
                { id: 'P3_6', img: 'P3_6.jpg', title: "十萬個為什麼 : 探秘藍色星球", desc: "我推介這本書原因是內容有趣，如月亮上有小白兔嗎？這是神話傳說，月亮上沒有水和空氣是不適合居住的，加深了對藍色星球的認識。", recommender: "3C 趙詠嵐" },
                { id: 'P3_7', img: 'P3_7.png', title: "無聊爛GAG怪 3", desc: "這本書內容輕鬆愉快，既能讓我們思考，又能讓我們哈哈大笑。", recommender: "3C 湯凡祺" },
                { id: 'P3_8', img: 'P3_8.jpeg', title: "永遠的好朋友", desc: "松鼠皮諾救助受傷的燕子萊拉，兩人結為好友。離別後，皮諾在思念中度過寒冬。春天來臨，萊拉信守承諾歸來，這是一個關於友情與守信的美好故事。", recommender: "3D 蔡子喬" },
                { id: 'P3_9', img: 'P3_9.jpg', title: "穿越古今8000年", desc: "具有歷史知識，穿梭不同朝代的平行時空，認識中華文化，強化文物教育。", recommender: "3E 黃莉婷" },
                { id: 'P3_10', img: 'P3_10.jpg', title: "Dog Man 11: Twenty Thousand Fleas Under the Sea", desc: "這本書刺激又搞笑！Dog Man和朋友這次要在水底迎戰壞蛋，同心協力保護城市。漫畫生動有趣，適合想輕鬆時笑一笑！", recommender: "3E鄭伊焯" }
            ],
            '四年級': [
                { id: 'P4_1', img: 'P4_1.jpg', title: "我有意見", desc: "你是不是也覺得大人規矩很多？這本書把我們的「意見」用搞笑的方式講出來，插圖幽默又有趣，保證你看完也開懷大笑！", recommender: "4A 蘇怡" },
                { id: 'P4_2', img: 'P4_2.jpg', title: "廁所幫少年偵探: 7-11偷竊風波", desc: "《廁所幫少年偵探》輕鬆幽默，貼近校園生活，引發閱讀興趣，適合小學生閱讀。", recommender: "4A 黎樂晴" },
                { id: 'P4_3', img: 'P4_3.jpg', title: "看漫畫學理財: 我會聰明管理零用錢", desc: "理財並非只屬於大人，這本書內容生動有趣，教我管理零用錢，學習儲蓄同理性消費，建立良好的金錢觀，使我獲益良多。", recommender: "4A 馬晞恩" },
                { id: 'P4_4', img: 'P4_4.jpeg', title: "吳有用唐朝上學記1：長安城裡開超市", desc: "吳有用意外獲得會穿越的奇書，來到唐朝長安。他結識李白等詩人，體驗古代生活，在爆笑冒險中學習唐詩與唐朝歷史知識。", recommender: "4B 何燁籽" },
                { id: 'P4_5', img: 'P4_5.jpg', title: "哈小浪上學記 15: 神奇的變身餅乾", desc: "我推薦的書是《哈小浪上學記14地下王國歷險記》。我最喜歡的人物是哈小浪，因為他不但很勇敢和有好奇心，而且會解決難題。", recommender: "4B 莫雅晴" },
                { id: 'P4_6', img: 'P4_6.jpg', title: "烏龍貓 1: 拯救麵店大作戰", desc: "故事主角烏龍貓是麵團變出來的貓，他和朋友在麵店裏烏龍百出，故事情節幽默又驚喜，主角烏龍貓活潑可愛，書中插圖生動有趣。", recommender: "4C 黎一諾" },
                { id: 'P4_7', img: 'P4_7.jpg', title: "ADAM & EVE", desc: "它的內容很有趣，可以讓我學會上帝如何創造世界，可以認識書天上的動物，海上的動物和陸地的動物。", recommender: "4C 章允芝" },
                { id: 'P4_8', img: 'P4_8.jpeg', title: "Princess Celestia and the Royal Rescue", desc: "這本圖書主要是Princess Celestia 收到好友 Diamond Waves 的求助後，立即前往拯救一間快要倒閉的魔法學院。故事十分感人，令我明白到友誼的重要性。", recommender: "4C 李芯言" },
                { id: 'P4_9', img: 'P4_9.jpeg', title: "IQ鬥一番(1)(鬥智擂台)", desc: "因為這本書有很多有趣的IQ題，小小的一本書方便攜帶，很適合在小息時用來放鬆腦袋。", recommender: "4D 葉允言" },
                { id: 'P4_10', img: 'P4_10.jpg', title: "完美小孩", desc: "你想要一個「完美弟妹」嗎？我們常要求別人完美，但自己做到了嗎？這本書會給你反思與共鳴，快來看看吧！", recommender: "4E 黎浠彤" }
            ],
            '五年級': [
                { id: 'P5_1', img: 'P5_1.jpg', title: "查理九世 16 不死國的生命樹", desc: "《查理九世》是一部適合兒童看的冒險小說，它可以讓讀者像也跟着冒險一樣， 很好看也很緊張。", recommender: "5B 黄超盈" },
                { id: 'P5_2', img: 'P5_2.jpg', title: "布瓜總動員", desc: "因為他可以解答人生中的一些問題,還很搞笑（圖片也是)", recommender: "5B 盧俊天" },
                { id: 'P5_3', img: 'P5_3.jpeg', title: "Dog man", desc: "This is a book about dogs and cats fighting villains and it’s pretty cool and funny ", recommender: "5B 羅禮駿" },
                { id: 'P5_4', img: 'P5_4.jpg', title: "我…有夢", desc: "這本圖書很簡單，主要要說動物的，一年級也看得明白，動畫很色彩鮮艷，親身經歷很獨特！", recommender: "5B 邱雅" },
                { id: 'P5_5', img: 'P5_5.jpg', title: "未知生物大百科: 探索世界102種神祕生物", desc: "這本書因為可以帶來很多未知生物的知識讓我們知道很多世界上不知道的生物的樣貌和在哪裏出現。", recommender: "5B 魏子韜" },
                { id: 'P5_6', img: 'P5_6.jpg', title: "鬥嘴一班 1 插班新同學", desc: "故事內容十分吸引，新來的插班生文樂心和同學高立民相處中的鬥氣和衝突。同學閱讀後，更能學會和他人相處之道。", recommender: "5D 黃志堯" },
                { id: 'P5_7', img: 'P5_7.jpg', title: "昆蟲大決鬥-日本腦力遊戲書[思維遊戲大挑戰]", desc: "「昆蟲王者大決戰」開始了，別小看蟲蟲們細小的身軀，牠們的力量會嚇你一跳！到底哪一隻昆蟲能奪得最強的稱號？誰有最堅厚的護甲？誰能跳得最高？我們去見證牠們的激鬥吧！但是你必須具備良好的觀察力和豐富的昆蟲知識，才能破解各種謎題啊！", recommender: "5D 周峻熙" },
                { id: 'P5_8', img: 'P5_8.png', title: "Rosie Easy English 露思兔子漫畫學Grammar（Common Errors 常見錯誤）", desc: "這本書以漫畫形式解說文法錯誤，輕鬆有趣又實用，幫助讀者避免常見陷阱，提升英文表達能力。", recommender: "5E 施昭言" },
                { id: 'P5_9', img: 'P5_9.jpg', title: "Harry Potter and the Goblet of Fire", desc: "Hi everyone! Try this book together. Harry joins a magic tournament. He battles a fire dragon and faces dark magic. Super thrilling!", recommender: "5E 朱泓翰" },
                { id: 'P5_10', img: 'P5_10.jpg', title: "世界史偵探柯南 4: 馬可波羅的足跡", desc: "它裏面是説柯南（裏面的其中一個人物）跟他的好朋友要去意大利威尼斯拿「智慧果實」，來治好柯南媽媽的病。途中，他們與到了毒蛇！幸好，柯南的腦袋裏裝滿了知識，立馬想出了辦法：他立刻把水倒在每個人身上，然後張樹枝上點燃了一些火，扔去草叢裏，引毒蛇過去。他們飛奔到王宮，請求國王賜給他們「智慧果實」⋯⋯最後，你覺得他們會成功拿到「智慧果實」嗎？", recommender: "5E 談可曈" }
            ],
            '六年級': [
                { id: 'P6_1', img: 'P6_1.jpg', title: "爆笑校園59", desc: "這本書十分有趣和好笑🤣，這本書的主角“男豬腳”—呆頭，三番四次地弄出笑話。", recommender: "6A 陳峻樂" },
                { id: 'P6_2', img: 'P6_2.jpg', title: "CLASSROOM Primary Good Writing Guide (Book 3) P5-P6", desc: "這本書的設計是在同一主題下會有兩篇不同程度的文章，幫助我們學習寫作技巧及詞語。還提供詞語參考，並配合精美的圖畫，幫助理解。", recommender: "6A 林愷盈" },
                { id: 'P6_3', img: 'P6_3.jpg', title: "給生活多一顆糖 3: 金魚街的小金魚", desc: "《金魚街的小金魚》是一個關於回憶的故事。但對我來說，這本書不只是一個故事，而是一份心意，希望可完這個故事後，大家都會更加珍惜自己身邊所擁有的。因為我們好容易忽略了身邊最重要的人，甚至自己。所以無論這些回憶是好還是壞，都是非常珍貴的！最後願這個故事能夠陪你們渡過一些不容易的時光。", recommender: "6B 卓宛蓉" },
                { id: 'P6_4', img: 'P6_4.jpg', title: "TIME for Kids: 2027 Almanac", desc: "這本書是說 2026 發生的事和 2027 有幾會發生的事，還有世界各地的知識，而最有趣的是會介紹不同國家的語言， 例如Israel 的語言 Hebrew、Guinea-Bissau的語言是 Portuguese 等。", recommender: "6B 黃逸楠" },
                { id: 'P6_5', img: 'P6_5.jpg', title: "如果歷史是一群喵 12: 元末明初篇", desc: "讀《如果歷史是一羣喵》，我發現枯燥的歷史變得生動有趣。可愛的貓咪演繹歷代故事，讓我輕鬆讀懂朝代更替、歷史興衰。既學到了歷史知識，也懂得了許多做人與處事的道理。", recommender: "6D 羅珞烯" },
                { id: 'P6_6', img: 'P6_6.jpg', title: "疑難雜症旅行社 1: 沙漠果實採摘之旅", desc: "噓！你發現了嗎？安靜商店街裡唯有它大門敞開，一旦走進去，一趟神奇的旅程就此展開...「好喝！」大悟順手抓起冰箱裡的果汁大口豪飲，陶醉在這小小的幸福中，突然瞥見桌上有一張紙條—不准偷喝果汁唷！要等全家人一起享用。糟了！要是被姊姊知道，肯定會變身成大怪獸。大悟馬上往街上衝，卻怎麼樣都找不到相同的果汁，只見到一隻不該在都市裡出現的貓頭鷹！這番驚喜令大悟瞬間忘了面臨的危機。貓頭鷹好似領著大悟一般，來到一家貼滿海報的商店前，附近只有這家店尚在營業，究竟是家什麽樣的店？大悟看向掛在上方的招牌，上頭寫著「疑難雜症旅行社」...", recommender: "6D 岳佩林" },
                { id: 'P6_7', img: 'P6_7.jpg', title: "神奇柑仔店 1: 帶來幸福的錢天堂", desc: "故事開頭就已經吸引了我，不禁繼續看下去。每個章節都記述有幸運的客人光顧柑仔店，至於會發生什麼事，就待你去看吧！", recommender: "6E 廖凱琳" },
                { id: 'P6_8', img: 'P6_8.jpg', title: "魔法公主書院16:怪奇小鎮", desc: "魔法少女們進入怪奇小鎮，意外碰見失憶少女，攜手找回記憶和施展魔法，打破小鎮謊言與秘密！開啟聰明思維與智慧邏輯！", recommender: "6E 鄭子欣" },
                { id: 'P6_9', img: 'P6_9.jpg', title: "聆聽虎鯨之聲: 鯨豚研究奠基者的追鯨紀實", desc: "《聆聽虎鯨之聲》是由鯨豚學者艾利希‧霍伊特撰寫，詳實記錄他首創以水下麥克風解讀野生虎鯨專屬「方言」與母系社會行為的冒險歷程，同時深刻揭露圈養產業的殘酷與背鰭塌陷等身心創傷，是一部結合科學發現與長達半世紀守護海洋的經典保育紀實。", recommender: "6E 吳家惠" },
                { id: 'P6_10', img: 'P6_10.jpg', title: "大偵探福爾摩斯 7: 六個拿破崙", desc: "這本書主要是說關於福爾摩斯和華生正在處理一單關於病態的人總是別人的商店找拿破崙的雕像，這本書10分刺激、精彩和有趣，十分推介你看這本書。", recommender: "6E 黃昊" }
            ]
        };

        const firebaseConfig = {
            apiKey: "AIzaSyBHL8yscpNGsXDUAFa7dBNywztX3-mDuuM",
            authDomain: "lunch-announcement-9f0d5.firebaseapp.com",
            projectId: "lunch-announcement-9f0d5",
            storageBucket: "lunch-announcement-9f0d5.firebasestorage.app",
            messagingSenderId: "370563000744",
            appId: "1:370563000744:web:409da50d8edb040223d59d"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const GOOGLE_CLIENT_ID = "573911894747-0c28hfr0bmkjnn8pkm2msg6sjal1thqe.apps.googleusercontent.com";

        let currentUser = null;
        let isAdminMode = false;
        let currentGrade = '';
        let selectedBooks = [];
        const grades = ['一年級', '二年級', '三年級', '四年級', '五年級', '六年級'];

        // 管理員登入邏輯
        window.adminLogin = () => {
            const pwd = prompt("請輸入管理員密碼：");
            if (pwd === "123567") {
                isAdminMode = true;
                refreshAdminUser();
                initMainMenu();
                switchView('main-menu-view');
            } else if (pwd !== null) {
                alert("密碼錯誤！");
            }
        };

        function refreshAdminUser() {
            currentUser = {
                uid: "admin_" + Date.now() + "_" + Math.floor(Math.random() * 1000),
                name: "管理員代投",
                email: "admin@school.edu.hk"
            };
            document.getElementById('user-info').innerHTML = `👨‍💼 <span style="color:var(--secondary);">管理員代投模式 (無限制)</span><br><small style="font-weight:normal;">目前ID: ${currentUser.uid}</small>`;
        }

        function decodeJwtResponse(token) {
            let base64Url = token.split('.')[1];
            let base64 = base64Url.replace(/-/g, '+').replace(/_/g, '/');
            let jsonPayload = decodeURIComponent(atob(base64).split('').map(function(c) {
                return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
            }).join(''));
            return JSON.parse(jsonPayload);
        }
        
        window.handleGoogleResponse = (response) => {
            const responsePayload = decodeJwtResponse(response.credential);
            isAdminMode = false;
            currentUser = {
                uid: responsePayload.sub,
                name: responsePayload.name,
                email: responsePayload.email
            };
            document.getElementById('user-info').innerText = `你好，${currentUser.name} (${currentUser.email})`;
            initMainMenu();
            switchView('main-menu-view');
        };

        window.onload = () => {
            google.accounts.id.initialize({
                client_id: GOOGLE_CLIENT_ID,
                callback: handleGoogleResponse
            });
            google.accounts.id.renderButton(
                document.getElementById("google-btn-container"),
                { theme: "outline", size: "large", shape: "pill", text: "signin_with" }
            );
        };

        window.logout = () => { 
            currentUser = null;
            isAdminMode = false;
            google.accounts.id.disableAutoSelect();
            switchView('login-view');
        };

        window.switchView = (viewId) => {
            document.querySelectorAll('.view').forEach(el => el.classList.remove('active'));
            document.getElementById(viewId).classList.add('active');
        };
        
        window.showMainMenu = () => switchView('main-menu-view');

        function initMainMenu() {
            const gradeGrid = document.getElementById('grade-grid');
            gradeGrid.innerHTML = '';
            grades.forEach(grade => {
                const div = document.createElement('div');
                div.className = 'card grade-card';
                div.innerText = grade;
                div.onclick = () => openGradeVoting(grade);
                gradeGrid.appendChild(div);
            });
        }

        window.openGradeVoting = (grade) => {
            currentGrade = grade;
            selectedBooks = [];
            document.getElementById('voting-title').innerHTML = `<span class="gradient-text">${grade} 投票</span>`;
            
            const bookGrid = document.getElementById('book-grid');
            bookGrid.innerHTML = '';

            const gradeBooks = booksConfig[grade];

            gradeBooks.forEach((book, index) => {
                const bookNum = index + 1;
                const displayTitle = book.title !== "" ? book.title : `書本 ${bookNum}`;
                const displayDesc = book.desc !== "" ? book.desc : "精彩簡介稍後補上...";
                const displayRecommender = book.recommender !== "" ? book.recommender : "稍後公佈";

                const wrapper = document.createElement('div');
                wrapper.className = 'book-wrapper';
                
                wrapper.innerHTML = `
                    <div class="card book-card" id="card-${book.id}">
                        <div class="recommender-tag-floating">👤 ${displayRecommender}</div>
                        <img src="${book.img}" alt="${displayTitle}" onerror="this.style.display='none'">
                        <span class="no-img-text" style="z-index:0; padding:10px;">${displayTitle}</span>
                    </div>

                    <div class="book-detail-popup">
                        <img class="popup-img" src="${book.img}" onerror="this.style.display='none'">
                        <h4 class="popup-title">${displayTitle}</h4>
                        <div class="popup-recommender">👤 推介人：${displayRecommender}</div>
                        <div class="popup-desc">${displayDesc}</div>
                        
                        <div class="popup-vote-btn">👆 點擊書本投票</div>
                    </div>
                `;

                wrapper.onclick = (e) => {
                    if (isUsingTouch) {
                        if (!wrapper.classList.contains('touch-active')) {
                            document.querySelectorAll('.book-wrapper').forEach(w => w.classList.remove('touch-active'));
                            wrapper.classList.add('touch-active');
                            return; 
                        }
                    }

                    const cardEl = document.getElementById(`card-${book.id}`);
                    const popupVoteBtn = wrapper.querySelector('.popup-vote-btn');
                    
                    if (selectedBooks.includes(book.id)) {
                        selectedBooks = selectedBooks.filter(id => id !== book.id);
                        cardEl.classList.remove('selected');
                        
                        popupVoteBtn.innerHTML = '👆 點擊書本投票';
                        popupVoteBtn.style.background = 'linear-gradient(45deg, #ff7eb3, #ff758c)';
                        popupVoteBtn.style.animation = 'pulseBtnPink 1.5s infinite';
                    } else {
                        selectedBooks.push(book.id);
                        cardEl.classList.add('selected');
                        
                        popupVoteBtn.innerHTML = '✔️ 點擊取消選擇';
                        popupVoteBtn.style.background = 'linear-gradient(45deg, #4facfe, #00f2fe)';
                        popupVoteBtn.style.animation = 'pulseBtnBlue 1.5s infinite';
                    }
                };
                bookGrid.appendChild(wrapper);
            });
            switchView('voting-view');
        };

        window.submitVote = async () => {
            if (selectedBooks.length === 0) {
                alert("請至少選擇一本書！");
                return;
            }
            try {
                const voteRef = doc(db, "votes", currentUser.uid);
                
                await setDoc(voteRef, {
                    studentEmail: currentUser.email,
                    studentName: currentUser.name,
                    [currentGrade]: selectedBooks,
                    lastUpdated: new Date(),
                    isAdminVote: isAdminMode 
                });
                
                alert(`太棒了！你已成功提交 ${currentGrade} 的投票！🎉`);
                
                if (isAdminMode) {
                    refreshAdminUser();
                }
                
                showMainMenu();
            } catch (error) {
                alert("投票提交失敗，請檢查網路狀態及 Firebase 安全性規則。錯誤：" + error.message);
            }
        };

        window.showLeaderboardMenu = () => {
            switchView('leaderboard-menu-view');
            const grid = document.getElementById('leaderboard-grid');
            grid.innerHTML = '';
            
            grades.forEach((grade) => {
                const div = document.createElement('div');
                div.className = 'card grade-card';
                div.innerText = grade;
                div.onclick = () => openLeaderboardDetail(grade);
                grid.appendChild(div);
            });
        };

        const getBookInfo = (bookId, grade) => {
            const foundBook = booksConfig[grade].find(b => b.id === bookId);
            if (foundBook) {
                const num = bookId.split('_')[1];
                const title = foundBook.title !== "" ? foundBook.title : `書本 ${num}`;
                const recommender = foundBook.recommender !== "" ? foundBook.recommender : "稍後公佈";
                return { title: title, img: foundBook.img, recommender: recommender };
            }
            return { title: bookId, img: '', recommender: '未知' };
        };

        window.openLeaderboardDetail = async (category) => {
            switchView('leaderboard-detail-view');
            document.getElementById('leaderboard-detail-title').innerHTML = `<span class="emoji">🏆</span> <span class="gradient-text">${category === 'top' ? '各級首名' : category + '榜單'}</span> <span class="emoji">🏆</span>`;
            const listDiv = document.getElementById('leaderboard-list');
            listDiv.innerHTML = '<p style="font-size: 1.5em;">載入中，請稍候...⏳</p>';

            try {
                const querySnapshot = await getDocs(collection(db, "votes"));
                
                let votersCount = {}; 
                let votesCount = {};  
                
                grades.forEach(g => {
                    votersCount[g] = 0;
                    votesCount[g] = {};
                    booksConfig[g].forEach(b => {
                        votesCount[g][b.id] = 0; 
                    });
                });

                querySnapshot.forEach((doc) => {
                    const data = doc.data();
                    grades.forEach(g => {
                        if (data[g] && Array.isArray(data[g])) {
                            votersCount[g]++;
                            data[g].forEach(bookId => {
                                if(votesCount[g][bookId] !== undefined) {
                                    votesCount[g][bookId]++;
                                }
                            });
                        }
                    });
                });

                let html = '';

                if (category === 'top') {
                    grades.forEach(grade => {
                        const sortedBooks = Object.entries(votesCount[grade]).sort((a, b) => b[1] - a[1]);
                        if (sortedBooks.length > 0 && sortedBooks[0][1] > 0) { 
                            const topBookId = sortedBooks[0][0];
                            const topBookCount = sortedBooks[0][1];
                            const bookInfo = getBookInfo(topBookId, grade);
                            
                            html += `
                                <div class="leaderboard-item">
                                    <div style="display: flex; align-items: center;">
                                        <span style="font-size: 1.8em; margin-right: 15px; text-shadow: 0 2px 5px rgba(0,0,0,0.2);">🏆</span>
                                        <img src="${bookInfo.img}" class="leaderboard-img" onerror="this.style.display='none'">
                                        <div style="display: flex; flex-direction: column;">
                                            <span style="font-size: 0.8em; color: #888; font-weight: normal;">${grade}</span>
                                            <span style="font-size: 1.1em;">${bookInfo.title}</span>
                                            <span style="font-size: 0.85em; color: var(--primary); margin-top: 3px;">👤 推介人：${bookInfo.recommender}</span>
                                        </div>
                                    </div>
                                    <span class="votes">${topBookCount} 票</span>
                                </div>
                            `;
                        }
                    });
                    if (html === '') html = '<p style="font-size: 1.2em;">目前還沒有人投票喔！</p>';
                } 
                else {
                    const grade = category;
                    html += `<div style="background: rgba(255,255,255,0.7); border-radius: 15px; padding: 10px; display: inline-block; margin-bottom: 25px; border: 1px solid #fff; box-shadow: 0 5px 10px rgba(0,0,0,0.05);"><p style="font-size: 1.1em; color: #555; margin: 0;">👤 本級投票總人數：<span style="font-weight: 900; color: var(--primary); font-size: 1.3em;">${votersCount[grade]}</span> 人</p></div>`;
                    
                    const sortedBooks = Object.entries(votesCount[grade]).sort((a, b) => b[1] - a[1]);
                    
                    sortedBooks.forEach(([bookId, count], index) => {
                        const bookInfo = getBookInfo(bookId, grade);
                        
                        let rankIcon = `<span style="width: 40px; display: inline-block; text-align: center; color: #999;">${index + 1}.</span>`;
                        if (index === 0 && count > 0) rankIcon = `<span style="font-size: 1.8em; width: 40px; display: inline-block; text-align: center;">🥇</span>`;
                        else if (index === 1 && count > 0) rankIcon = `<span style="font-size: 1.8em; width: 40px; display: inline-block; text-align: center;">🥈</span>`;
                        else if (index === 2 && count > 0) rankIcon = `<span style="font-size: 1.8em; width: 40px; display: inline-block; text-align: center;">🥉</span>`;

                        html += `
                            <div class="leaderboard-item">
                                <div style="display: flex; align-items: center;">
                                    ${rankIcon}
                                    <img src="${bookInfo.img}" class="leaderboard-img" onerror="this.style.display='none'">
                                    <div style="display: flex; flex-direction: column; justify-content: center;">
                                        <span style="font-size: 1.1em;">${bookInfo.title}</span>
                                        <span style="font-size: 0.85em; color: var(--primary); margin-top: 3px;">👤 推介人：${bookInfo.recommender}</span>
                                    </div>
                                </div>
                                <span class="votes">${count} 票</span>
                            </div>
                        `;
                    });
                }

                listDiv.innerHTML = html;

            } catch (error) {
                listDiv.innerHTML = '<p>讀取排行榜失敗，請檢查 Firebase 權限設定。</p>';
                console.error(error);
            }
        };
    </script>
</body>
</html>
