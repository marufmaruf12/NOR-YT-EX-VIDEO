<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="app-title">NOR YT EX</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #ff4d4d;
            --bg-color: #0d0d0d;
            --surface-color: #212121;
            --text-color: #ffffff;
            --secondary-text-color: #aaaaaa;
            --border-color: #383838;
        }

        body[data-theme="light"] {
            --primary-color: #ff4d4d;
            --bg-color: #f9f9f9;
            --surface-color: #ffffff;
            --text-color: #0f0f0f;
            --secondary-text-color: #606060;
            --border-color: #e0e0e0;
        }

        *, *::before, *::after {
            box-sizing: border-box;
        }

        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            background-color: var(--bg-color);
            color: var(--text-color);
        }

        .hidden {
            display: none !important;
        }

        .container {
            padding: 70px 0 80px;
        }

        .section {
            display: none;
            animation: fadeIn 0.4s;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, rgba(255, 77, 77, 0.1), rgba(13, 13, 13, 0.1));
            animation: moveGradient 20s infinite alternate;
            z-index: -2;
        }

        @keyframes moveGradient {
            from {
                background-position: 0% 0%;
            }
            to {
                background-position: 100% 100%;
            }
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.8rem 1rem;
            background-color: rgba(33, 33, 33, 0.7);
            backdrop-filter: blur(10px);
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            border-bottom: 1px solid var(--border-color);
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-color);
        }

        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background-color: rgba(33, 33, 33, 0.7);
            backdrop-filter: blur(10px);
            display: flex;
            border-top: 1px solid var(--border-color);
            z-index: 1000;
        }

        .nav-item {
            flex-grow: 1;
            padding: 10px 0;
            cursor: pointer;
            text-align: center;
            color: var(--secondary-text-color);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            transition: color 0.3s ease;
        }

        .nav-item svg {
            width: 24px;
            height: 24px;
            fill: currentColor;
            transition: transform 0.3s ease;
        }

        .nav-item.active {
            color: var(--primary-color);
            text-shadow: 0 0 5px rgba(255, 77, 77, 0.5);
        }

        .content-row {
            margin-bottom: 2rem;
        }

        .row-title {
            font-size: 1.2rem;
            font-weight: 700;
            margin: 0 0 1rem 1rem;
        }

        .video-carousel {
            display: flex;
            overflow-x: auto;
            padding: 0 1rem 1rem;
            scrollbar-width: none;
            -ms-overflow-style: none;
            gap: 1rem;
        }

        .video-carousel::-webkit-scrollbar {
            display: none;
        }

        .video-card-carousel {
            flex: 0 0 250px;
        }

        .video-grid {
            padding: 1rem;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }
        
        /* Banner Ad Container Styling */
        .banner-ad-container {
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1rem 0;
            margin: 1rem 0;
            background-color: var(--surface-color);
            border-radius: 8px;
            border: 1px solid var(--border-color);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .video-card {
            cursor: pointer;
            background-color: transparent;
            position: relative;
            overflow: hidden;
            border-radius: 12px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .video-card:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2), 0 0 30px var(--primary-color);
        }
        
        .video-card .thumbnail {
            width: 100%;
            aspect-ratio: 16/9;
            object-fit: cover;
            background-color: #333;
            border-radius: 12px;
            margin-bottom: 0.8rem;
            transition: transform 0.3s ease;
        }
        
        .video-card:hover .thumbnail {
            transform: scale(1.05);
        }

        .video-details {
            display: flex;
            gap: 0.8rem;
            align-items: flex-start;
        }

        .uploader-pic {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-size: cover;
            background-position: center;
            flex-shrink: 0;
            border: 2px solid var(--border-color);
            cursor: pointer;
        }

        .video-info h3 {
            margin: 0 0 4px;
            font-size: 1rem;
            font-weight: 500;
        }

        .video-info p {
            margin: 0;
            font-size: 0.85rem;
            color: var(--secondary-text-color);
        }

        .live-badge {
            position: absolute;
            top: 10px;
            left: 10px;
            background-color: #ff0000;
            color: white;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 0.7rem;
            font-weight: 700;
            z-index: 5;
            animation: livePulse 1s infinite alternate;
        }

        @keyframes livePulse {
            from { box-shadow: 0 0 0 0 rgba(255, 0, 0, 0.7); }
            to { box-shadow: 0 0 0 10px rgba(255, 0, 0, 0); }
        }

        .player-page {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--bg-color);
            z-index: 2000;
            overflow-y: auto;
        }

        .player-wrapper {
            width: 100%;
            background-color: #000;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .player-container {
            width: 100%;
            aspect-ratio: 16/9;
            position: relative;
        }

        .player-container iframe, .player-container video {
            width: 100%;
            height: 100%;
            border: none;
        }

        .back-btn, .fullscreen-btn {
            background: rgba(0, 0, 0, 0.5);
            border: none;
            color: white;
            font-size: 1.5rem;
            position: absolute;
            top: 1rem;
            z-index: 11;
            cursor: pointer;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .back-btn {
            left: 1rem;
        }

        .fullscreen-btn {
            right: 1rem;
        }

        .search-bar {
            display: flex;
            gap: 10px;
            padding: 1rem;
            max-width: 600px;
            margin: 0 auto;
        }

        .search-bar input {
            flex-grow: 1;
            padding: 0.8rem;
            background-color: var(--surface-color);
            border: 1px solid var(--border-color);
            color: var(--text-color);
            border-radius: 25px;
            transition: box-shadow 0.3s ease, border-color 0.3s ease;
        }

        .search-bar input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 10px rgba(255, 77, 77, 0.5);
        }

        #loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #0d0d0d;
            z-index: 9999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            transition: opacity 1s ease-out, transform 1s ease-out;
            pointer-events: none;
        }

        #loading-screen.hidden {
            opacity: 0;
            transform: scale(0.8);
            visibility: hidden;
        }

        .logo-container {
            perspective: 800px;
            width: 200px;
            height: 200px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .logo-3d {
            font-size: 3rem;
            font-weight: 700;
            color: var(--primary-color);
            position: relative;
            transform-style: preserve-3d;
            animation: rotateLogo 5s infinite ease-in-out;
            text-shadow: 0 0 20px rgba(255, 77, 77, 0.5);
            -webkit-box-reflect: below 1px linear-gradient(transparent, rgba(0, 0, 0, 0.4));
        }

        @keyframes rotateLogo {
            0% { transform: rotateY(0deg) rotateZ(0deg); }
            25% { transform: rotateY(30deg) rotateZ(10deg); }
            50% { transform: rotateY(0deg) rotateZ(0deg); }
            75% { transform: rotateY(-30deg) rotateZ(-10deg); }
            100% { transform: rotateY(0deg) rotateZ(0deg); }
        }

        .logo-3d span {
            display: inline-block;
            transform-origin: 50% 50% -50px;
            animation: bounceIn 2s infinite ease-out;
            opacity: 0;
        }

        .logo-3d span:nth-child(1) { animation-delay: 0.1s; }
        .logo-3d span:nth-child(2) { animation-delay: 0.2s; }
        .logo-3d span:nth-child(3) { animation-delay: 0.3s; }
        .logo-3d span:nth-child(4) { animation-delay: 0.4s; }
        .logo-3d span:nth-child(5) { animation-delay: 0.5s; }
        .logo-3d span:nth-child(6) { animation-delay: 0.6s; }
        .logo-3d span:nth-child(7) { animation-delay: 0.7s; }
        .logo-3d span:nth-child(8) { animation-delay: 0.8s; }
        .logo-3d span:nth-child(9) { animation-delay: 0.9s; }
        .logo-3d span:nth-child(10) { animation-delay: 1.0s; }
        .logo-3d span:nth-child(11) { animation-delay: 1.1s; }
        .logo-3d span:nth-child(12) { animation-delay: 1.2s; }

        @keyframes bounceIn {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); opacity: 1; }
            40% { transform: translateY(-30px); }
            60% { transform: translateY(-15px); }
        }

        .loading-text {
            color: var(--secondary-text-color);
            font-size: 1rem;
            margin-top: 20px;
            animation: fadeIn 2s infinite;
        }

        @keyframes fadeIn {
            0%, 100% { opacity: 0; }
            50% { opacity: 1; }
        }

        .cosmic-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #0d0d0d;
            opacity: 1;
            z-index: -1;
        }

        .cosmic-bg::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100"><circle cx="10" cy="10" r="1" fill="white" /><circle cx="30" cy="50" r="0.5" fill="white" /><circle cx="70" cy="20" r="0.8" fill="white" /><circle cx="90" cy="80" r="1.2" fill="white" /><circle cx="5" cy="90" r="0.6" fill="white" /><circle cx="40" cy="10" r="1" fill="white" /><circle cx="80" cy="40" r="0.7" fill="white" /></svg>') repeat;
            animation: starfield 100s linear infinite;
        }

        @keyframes starfield {
            from { background-position: 0 0; }
            to { background-position: -10000px 10000px; }
        }

        /* --- PC/Desktop Specific Styles --- */
        @media screen and (min-width: 768px) {
            .container {
                max-width: 1200px;
                margin: 0 auto;
                padding-top: 80px;
            }

            .video-grid {
                display: grid;
                grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
                gap: 1.5rem;
            }
            
            .player-page .banner-ad-container {
                max-width: 800px;
                margin: 2rem auto;
            }

            .bottom-nav {
                display: none; /* Hide mobile bottom nav on desktop */
            }

            header { /* Add navigation to header for desktop */
                justify-content: flex-start;
                gap: 2rem;
            }

            .header-nav {
                display: flex;
                gap: 1.5rem;
            }

            .header-nav-item {
                cursor: pointer;
                color: var(--secondary-text-color);
                transition: color 0.3s;
                font-weight: 500;
            }

            .header-nav-item.active {
                color: var(--primary-color);
            }

            .header-nav-item:hover {
                color: var(--text-color);
            }
        }

    </style>
</head>
<body data-theme="dark">

    <div id="loading-screen">
        <div class="cosmic-bg"></div>
        <div class="logo-container">
            <h1 class="logo-3d">
                <span>N</span><span>O</span><span>R</span><span> </span><span>Y</span><span>T</span><span> </span><span>E</span><span>X</span>
            </h1>
        </div>
        <div class="loading-text">Loading...</div>
    </div>

    <div id="app-wrapper" class="hidden">
        <header>
            <div id="app-name-logo" class="logo">AppName</div>
            <div class="header-nav">
                 <div class="header-nav-item active" data-section="home-section">Home</div>
                 <div class="header-nav-item" data-section="search-section">Search</div>
            </div>
        </header>

        <div class="container">
            <section id="home-section" class="section active">
                <div id="featured-carousel-container" class="content-row"></div>
                
                <div class="banner-ad-container">
                    <script type='text/javascript' src='//pl27461905.profitableratecpm.com/60/6a/6c/606a6c3100d9a23e598000191be7784e.js'></script>
                </div>

                <div id="latest-videos-container">
                    <h2 class="row-title">Latest Videos</h2>
                    <div id="video-grid" class="video-grid"></div>
                </div>

                <div class="banner-ad-container">
                    <script type='text/javascript' src='//pl27461905.profitableratecpm.com/60/6a/6c/606a6c3100d9a23e598000191be7784e.js'></script>
                </div>
            </section>
            <section id="search-section" class="section">
                <div class="search-bar">
                    <input type="text" id="search-input" placeholder="Search for videos...">
                </div>

                <div class="banner-ad-container">
                    <script type='text/javascript' src='//pl27461905.profitableratecpm.com/60/6a/6c/606a6c3100d9a23e598000191be7784e.js'></script>
                </div>
                <div id="search-results-container" class="video-grid"></div>
            </section>
        </div>

        <nav class="bottom-nav">
            <div class="nav-item active" data-section="home-section">
                <svg viewBox="0 0 24 24"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"></path></svg>
                <span>Home</span>
            </div>
            <div class="nav-item" data-section="search-section">
                <svg viewBox="0 0 24 24"><path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"></path></svg>
                <span>Search</span>
            </div>
        </nav>
    </div>

    <div id="player-page" class="player-page hidden"></div>

    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

    <script>
        const firebaseConfig = {
            apiKey: "AIzaSyAQ8NPsSeG2w2IQ7R_zAvNdBbhG_nN1jmo",
            authDomain: "uyukiyu-870aa.firebaseapp.com",
            databaseURL: "https://uyukiyu-870aa-default-rtdb.firebaseio.com",
            projectId: "uyukiyu-870aa",
            storageBucket: "uyukiyu-870aa.firebasestorage.app",
            messagingSenderId: "370165725248",
            appId: "1:370165725248:web:d82b7fe13719846e7087a5",
        };
        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();

        let allVideos = [];

        document.addEventListener('DOMContentLoaded', initializeApp);

        function initializeApp() {
            setTimeout(() => {
                const loadingScreen = document.getElementById('loading-screen');
                const appWrapper = document.getElementById('app-wrapper');
                loadingScreen.classList.add('hidden');
                appWrapper.classList.remove('hidden');
            }, 3000);

            setupEventListeners();
            fetchVideos();
            watchAppSettings();
        }

        function watchAppSettings() {
            database.ref('app_settings/general/appName').on('value', snapshot => {
                const appName = snapshot.val() || 'NOR YT EX';
                document.getElementById('app-name-logo').textContent = appName;
                document.getElementById('app-title').textContent = appName;
            });

            database.ref('app_settings/theme').on('value', snapshot => {
                if (!snapshot.exists()) return;
                const themes = snapshot.val();
                const currentTheme = themes.dark;
                if (currentTheme) {
                    document.documentElement.style.setProperty('--primary-color', currentTheme.primaryColor);
                    document.documentElement.style.setProperty('--bg-color', currentTheme.bgColor);
                    document.documentElement.style.setProperty('--surface-color', currentTheme.surfaceColor);
                    document.documentElement.style.setProperty('--text-color', currentTheme.textColor);
                }
            });
        }

        function handleNavigation(sectionId) {
            document.querySelectorAll('.nav-item.active, .header-nav-item.active').forEach(i => i.classList.remove('active'));
            document.querySelectorAll(`.nav-item[data-section="${sectionId}"], .header-nav-item[data-section="${sectionId}"]`).forEach(i => i.classList.add('active'));
            
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.getElementById(sectionId).classList.add('active');
        }

        function setupEventListeners() {
            document.querySelectorAll('.nav-item, .header-nav-item').forEach(item => {
                item.addEventListener('click', () => handleNavigation(item.dataset.section));
            });

            document.getElementById('search-input').addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase().trim();
                const resultsContainer = document.getElementById('search-results-container');
                resultsContainer.innerHTML = '';
                if (query.length < 2) return;

                const filteredVideos = allVideos.filter(video => 
                    video.title.toLowerCase().includes(query)
                );

                if (filteredVideos.length > 0) {
                    filteredVideos.forEach(video => {
                        resultsContainer.appendChild(createVideoCard(video.id, video));
                    });
                } else {
                    resultsContainer.innerHTML = '<p style="text-align:center;">No results found.</p>';
                }
            });
        }

        function fetchVideos() {
            const grid = document.getElementById('video-grid');
            database.ref('videos').on('value', snapshot => {
                grid.innerHTML = '';
                allVideos = [];
                if (snapshot.exists()) {
                    snapshot.forEach(child => {
                        const videoData = { id: child.key, ...child.val() };
                        allVideos.push(videoData);
                        grid.prepend(createVideoCard(child.key, child.val()));
                    });
                } else {
                    grid.innerHTML = '<p style="text-align:center;">No videos found.</p>';
                }
            });
        }

        function createVideoCard(key, videoData) {
            const card = document.createElement('div');
            card.className = 'video-card';
            card.addEventListener('click', () => showInterstitialAd(() => openPlayer(videoData)));

            card.innerHTML = `
                <img src="${videoData.thumbnailUrl}" class="thumbnail" alt="${videoData.title}" loading="lazy">
                <div class="video-details">
                    <div class="video-info">
                        <h3>${videoData.title}</h3>
                        <p>${(videoData.views || 0).toLocaleString()} views</p>
                    </div>
                </div>
            `;
            if (videoData.isLive) {
                const liveBadge = document.createElement('span');
                liveBadge.className = 'live-badge';
                liveBadge.textContent = 'LIVE';
                card.prepend(liveBadge);
            }
            return card;
        }

        function showInterstitialAd(callback) {
            const adContainer = document.createElement('div');
            adContainer.id = 'interstitial-ad';
            adContainer.style.cssText = 'position:fixed; top:0; left:0; width:100%; height:100%; background-color:rgba(0,0,0,0.9); z-index:9999; display:flex; flex-direction:column; justify-content:center; align-items:center;';

            adContainer.innerHTML = `
                <div id="interstitial-ad-content" style="position:relative; width:100%; height:100%; display:flex; justify-content:center; align-items:center;"></div>
                <button id="skip-ad-btn" style="position:absolute; top:20px; right:20px; background-color:#ff4d4d; color:white; border:none; padding:10px 20px; font-size:1rem; font-weight:bold; border-radius:25px; cursor:pointer; box-shadow: 0 4px 6px rgba(0,0,0,0.2); transition: all 0.3s;">Skip Ad</button>
            `;
            document.body.appendChild(adContainer);

            // আপনার দেওয়া নতুন বিজ্ঞাপন কোডটি এখানে যুক্ত করা হলো
            const adScript = document.createElement('script');
            adScript.type = 'text/javascript';
            adScript.src = '//pl27461905.profitableratecpm.com/60/6a/6c/606a6c3100d9a23e598000191be7784e.js';
            document.getElementById('interstitial-ad-content').appendChild(adScript);
            
            const closeAd = () => {
                if (adContainer.parentNode) {
                    adContainer.remove();
                }
                if (callback) callback();
            };

            document.getElementById('skip-ad-btn').addEventListener('click', closeAd);
            setTimeout(closeAd, 8000); // ৮ সেকেন্ড পর অটোমেটিক চলে যাবে
        }

        function openPlayer(videoData) {
            const playerPage = document.getElementById('player-page');
            let playerHTML = '';

            if (videoData.type === 'gdrive') {
                playerHTML = `<iframe src="${videoData.videoUrl.replace('/view', '/preview')}" allow="fullscreen" allowfullscreen></iframe>`;
            } else if (videoData.type === 'youtube') {
                const videoId = getYouTubeID(videoData.videoUrl);
                playerHTML = `<iframe src="https://www.youtube.com/embed/${videoId}?autoplay=1" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>`;
            } else {
                playerHTML = `<video src="${videoData.videoUrl}" controls autoplay></video>`;
            }

            playerPage.innerHTML = `
                <div class="player-wrapper">
                     <button class="back-btn" onclick="closePlayer()">←</button>
                     <button class="fullscreen-btn" onclick="toggleFullScreen()">⛶</button>
                    <div class="player-container" id="main-player-container">${playerHTML}</div>
                </div>
                <div class="banner-ad-container">
                    <script type='text/javascript' src='//pl27461905.profitableratecpm.com/60/6a/6c/606a6c3100d9a23e598000191be7784e.js'><\/script>
                </div>`;
            playerPage.classList.remove('hidden');
        }

        function toggleFullScreen() {
            const playerContainer = document.getElementById('main-player-container');
            if (!playerContainer) return;
            
            if (!document.fullscreenElement) {
                playerContainer.requestFullscreen().catch(err => console.error(`Error attempting to enable full-screen mode: ${err.message} (${err.name})`));
            } else {
                document.exitFullscreen();
            }
        }

        function closePlayer() {
            const playerPage = document.getElementById('player-page');
            playerPage.classList.add('hidden');
            playerPage.innerHTML = ''; // video বন্ধ করার জন্য কন্টেন্ট খালি করা হলো
            if (document.fullscreenElement) {
                document.exitFullscreen();
            }
        }

        function getYouTubeID(url) {
            const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
            const match = url.match(regExp);
            return (match && match[2].length === 11) ? match[2] : null;
        }
    </script>
</body>
</html>
