[bekas.html](https://github.com/user-attachments/files/23877499/bekas.html)
<!DOCTYPE html>
<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>AI & Құқық: Саналы Ұрпақ</title>
    <style id="app-styles">
        /* НЕГІЗГІ ТҮСТЕР ЖӘНЕ ҚАҒИДАЛАР */
        :root {
            --primary-color: #4F46E5; /* Көк-Күлгін (Негізгі) */
            --secondary-color: #0EA5E9; /* Ашық Көк (Акцент) */
            --bg-light: #F8FAFC; /* Өте ашық фон */
            --card-bg: #FFFFFF; /* Ақ фон */
            --text-main: #1F2937; /* Қара мәтін */
            --text-secondary: #6B7280;
            /* ЖАҢА КҮШТІ КӨЛЕҢКЕ */
            --shadow-strong: 0 20px 40px -10px rgba(0, 0, 0, 0.15), 0 10px 15px -3px rgba(0, 0, 0, 0.05);
            --shadow-light: 0 5px 15px rgba(0, 0, 0, 0.08);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
        }

        /* 3D-КӨРІНІС ҮШІН BODY */
        body {
            font-family: 'Segoe UI', Roboto,Arial, Helvetica, sans-serif;
            background: linear-gradient(135deg, var(--bg-light) 0%, #E0E7FF 100%); /* Жұмсақ градиент */
            color: var(--text-main);
            overflow: hidden;
            height: 100vh;
            width: 100vw;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* 3D ФОН (CANVAS) */
        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.8;
            /* CANVAS-ТЫҢ ҮСТІНЕН ӨТЕТІН ЖҰМСАҚ ГРАДИЕНТ */
            background: radial-gradient(circle at top left, rgba(79, 70, 229, 0.05) 0%, transparent 40%);
        }

        /* НЕГІЗГІ КОНТЕЙНЕР (МОБИЛЬДІ КӨРІНІС ҮШІН ШЕКТЕУ) */
        #app-container {
            position: relative;
            width: 100%;
            max-width: 500px; /* Телефон экранына ұқсас ету */
            height: 100%;
            max-height: 900px;
            overflow-y: auto;
            scroll-behavior: smooth;
            padding: 30px 20px 100px 20px;
            /* ЖҰМСАҚ ПЕРСПЕКТИВАЛЫ АНИМАЦИЯ */
            transition: transform 0.3s ease-out;
        }
        
        /* BET LOGIC */
        .page { display: none; padding-bottom: 20px; }
        .page.active { display: block; }
        
        /* КАРТОЧКАЛАР (СУРЕТТЕГІДЕЙ ОРТАДА, ЖҰМСАҚ КӨЛЕҢКЕ) */
        .card {
            background: var(--card-bg);
            border-radius: 30px; /* Көбірек дөңгеленген жиектер */
            padding: 30px;
            margin-bottom: 25px;
            box-shadow: var(--shadow-strong);
            transition: all 0.3s ease-out;
            border: 1px solid rgba(255, 255, 255, 0.5); /* Ақ жиек */
        }

        .home-card {
            text-align: center;
            padding: 40px 30px;
            background: linear-gradient(145deg, #ffffff 0%, #f0f7ff 100%);
            animation: fadeInDown 0.6s ease-out;
        }
        
        /* ТИПОГРАФИКА */
        h1 { color: var(--primary-color); font-weight: 800; font-size: 26px; line-height: 1.3; margin-bottom: 10px; }
        h2 { color: var(--text-main); font-weight: 700; font-size: 22px; margin-bottom: 15px; }
        h3 { color: var(--primary-color); font-weight: 600; font-size: 18px; margin-bottom: 10px; }
        p { line-height: 1.7; color: var(--text-secondary); margin-bottom: 12px; font-size: 15px; }

        .subtitle { font-size: 15px; color: var(--text-secondary); font-weight: 500; margin-bottom: 20px; }
        .section-title { color: var(--primary-color); text-align: center; margin-bottom: 25px; font-size: 24px; }
        .section-subtitle { color: var(--text-main); margin-top: 25px; margin-bottom: 10px; font-weight: 700; border-left: 4px solid var(--secondary-color); padding-left: 10px; }


        /* HOME & AUTHOR INFO */
        .icon-header { font-size: 40px; margin-bottom: 15px; display: flex; justify-content: center; gap: 10px;}
        .author-info {
            background: #F3F4F6;
            padding: 15px;
            border-radius: 15px;
            margin: 25px 0;
            border: 1px solid #E5E7EB;
        }
        .author-info p { margin-bottom: 5px; font-size: 13px; line-height: 1.5; color: #4B5563; }
        .author-info .role { color: var(--primary-color); font-weight: 600; }
        .school-full, .goal-text { font-style: italic; color: #4B5563; }
        .admin-list { padding-left: 20px; line-height: 2; font-size: 14px; }


        /* МОДУЛЬДЕР ТОРЫ (GRID) */
        .module-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .module-item {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 20px;
            text-align: center;
            box-shadow: var(--shadow-light);
            transition: transform 0.2s, box-shadow 0.3s;
            cursor: pointer;
            border: 1px solid #E0E7FF;
        }

        .module-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 25px rgba(79, 70, 229, 0.2);
        }

        .module-item .emoji { font-size: 32px; display: block; margin-bottom: 5px; }
        .module-item h3 { margin-bottom: 0; font-size: 15px; color: var(--text-main); }
        .module-item p { font-size: 12px; color: var(--text-secondary); margin: 0; }
        
        .module-item.full-width {
            grid-column: span 2; /* 2 бағанды толық алу */
            display: flex;
            align-items: center;
            text-align: left;
            gap: 15px;
        }
        .module-item.full-width h3 { font-size: 16px; }
        .module-item.full-width .emoji { margin-bottom: 0; }


        /* САБАҚТАР ТІЗІМІ */
        .lesson-list-container {
            display: grid;
            gap: 12px;
        }
        .lesson-item {
            background: var(--card-bg);
            padding: 15px 20px;
            border-radius: 18px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: 0.2s;
            border: 1px solid #E0E7FF;
        }
        .lesson-item:hover {
            background: #EEF2FF;
            transform: translateX(5px);
            box-shadow: 0 8px 15px rgba(79, 70, 229, 0.1);
        }
        .lesson-icon {
            font-size: 24px;
            margin-right: 15px;
            line-height: 1;
        }
        .lesson-title {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-main);
        }


        /* ТҮЙМЕЛЕР (BUTTONS) */
        .btn {
            border: none;
            padding: 15px 25px;
            border-radius: 18px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            width: 100%;
            margin-top: 15px;
            transition: 0.3s;
            text-decoration: none;
            display: inline-flex;
            justify-content: center;
            align-items: center;
        }

        .btn-primary {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            box-shadow: 0 8px 15px rgba(79, 70, 229, 0.4);
        }
        .btn-primary:active { transform: scale(0.98); opacity: 0.9; }

        .btn-secondary {
            background: #F3F4F6;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
            box-shadow: none;
            width: auto;
        }
        .btn-back {
             padding: 10px 18px;
             font-size: 14px;
             margin-bottom: 20px;
        }
        
        /* НАВИГАЦИЯ (МЕНЮ) */
        .nav-bar {
            position: fixed;
            bottom: 20px;
            width: 100%;
            max-width: 500px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 25px;
            padding: 12px 0;
            display: flex;
            justify-content: space-around;
            box-shadow: var(--shadow-strong);
            z-index: 100;
            border: 1px solid rgba(255,255,255,0.7);
            left: 50%;
            transform: translateX(-50%);
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: var(--text-secondary);
            font-size: 10px;
            font-weight: 600;
            padding: 5px;
            border-radius: 15px;
            transition: 0.3s;
            cursor: pointer;
            width: 80px;
        }

        .nav-item span { font-size: 24px; margin-bottom: 2px; }
        .nav-item.active { color: var(--primary-color); background: #EEF2FF; transform: translateY(-3px); box-shadow: 0 4px 8px rgba(79, 70, 229, 0.1); }
        
        
        /* САБАҚ ДЕТАЛДАРЫ (TABS) */
        .tab-container {
            display: flex;
            background: #F3F4F6;
            padding: 8px;
            border-radius: 18px;
            margin-bottom: 25px;
        }
        .tab-btn {
            flex: 1;
            padding: 12px;
            text-align: center;
            border-radius: 14px;
            font-size: 14px;
            font-weight: 600;
            color: var(--text-secondary);
            cursor: pointer;
            transition: 0.3s;
            border: none;
            background: transparent;
        }
        .tab-btn.active { 
            background: var(--primary-color); 
            color: white; 
            box-shadow: 0 4px 10px rgba(79, 70, 229, 0.3);
        }
        
        .lecture-text { color: #374151; font-size: 16px; }
        .source-link { font-size: 12px; text-align: center; margin-top: 20px; }

        /* Глоссарий стилі */
        .glossary-box {
            background: #EEF2FF;
            padding: 20px;
            border-radius: 15px;
            margin-top: 25px;
            border-left: 5px solid var(--primary-color);
        }
        .box-title { color: var(--primary-color); margin-bottom: 10px; font-weight: 700; }
        .glossary-box ul { padding-left: 20px; }
        .glossary-box li { 
            font-size: 14px; 
            color: #374151; 
            line-height: 1.8;
            margin-bottom: 2px;
        }


        /* ACCORDION (ТАПСЫРМАЛАР) */
        .accordion {
            background: #F8FAFC; 
            color: var(--text-main); font-weight: 600;
            padding: 15px; width: 100%; text-align: left;
            border: 1px solid #E5E7EB;
            border-radius: 15px; cursor: pointer; margin-top: 10px;
            display: flex; justify-content: space-between; align-items: center;
            transition: background 0.2s;
        }
        .accordion:hover { background: #F3F4F6; }
        .accordion:after { content: '➕'; font-size: 16px; color: var(--secondary-color); transition: transform 0.3s; }
        .active-acc { background: #EEF2FF; border-color: var(--primary-color); }
        .active-acc:after { content: '➖'; transform: rotate(0deg); color: var(--primary-color); }
        .panel { padding: 0 15px; background: #EEF2FF; max-height: 0; overflow: hidden; transition: max-height 0.3s ease-in-out; border-radius: 0 0 15px 15px; margin-bottom: 10px; }
        .panel p { padding: 8px 0; margin: 0; border-bottom: 1px dashed #D1D5DB; }
        .panel p:last-child { border-bottom: none; }
        
        
        /* QUIZ */
        .quiz-option-label {
            display: block;
            background: #F3F4F6;
            border: 2px solid #E5E7EB;
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: 0.2s;
        }
        .quiz-option-label:hover { border-color: var(--secondary-color); background: #E0E7FF; }
        .quiz-option-label input { margin-right: 10px; }

        .quiz-result {
            margin-top: 20px; font-weight: 800; text-align: center; font-size: 20px; padding: 10px; border-radius: 15px;
        }
        
        /* SETTINGS */
        .color-picker-grid {
            display: flex;
            gap: 15px;
            margin-top: 10px;
        }
        .color-dot {
            width: 40px; height: 40px; border-radius: 50%; cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            border: 2px solid white;
            box-shadow: var(--shadow-light);
        }
        .color-dot:hover { transform: scale(1.1); box-shadow: 0 0 0 4px var(--secondary-color); }
        
        /* АНИМАЦИЯЛАР */
        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .home-card { animation: fadeInDown 0.6s ease-out; }
        
    </style>
</head>
<body>

    <canvas id="bg-canvas"></canvas>

    <div class="nav-bar">
        <div class="nav-item active" onclick="showPage('home')">
            <span>🏠</span>Басты
        </div>
        <div class="nav-item" onclick="showPage('modules')">
            <span>📚</span>Курс
        </div>
        <div class="nav-item" onclick="showPage('admin')">
            <span>🏛️</span>Құжаттама
        </div>
        <div class="nav-item" onclick="showPage('settings')">
            <span>⚙️</span>Баптау
        </div>
    </div>

    <div id="app-container">
        
        <div id="home" class="page active">
            <div class="card home-card">
                <div class="icon-header">
                    <span class="emoji">🤖</span>
                    <span class="emoji">⚖️</span>
                </div>
                <h1>ЖАСАНДЫ ИНТЕЛЛЕКТ ЖҮЙЕЛЕРІНДЕГІ<br>ҚҰҚЫҚТЫҚ ҚАУІПСІЗДІК МӘДЕНИЕТІ</h1>
                <p class="subtitle">9-сыныпқа арналған авторлық курс</p>

            <div class="author-info">
    <div class="icon">
        👤
    </div>

    <p class="title">Авторы: <strong>Арыстанбекова Улпан Аманбековна</strong></p>
    <p class="role">Құқық пәнінің мұғалімі</p>
    <p class="school">«Түлкібас ауданының үш тілде оқытатын мамандандырылған мектеп-интернаты»</p>
</div>

<style>
.author-info {
    width: fit-content;
    margin: 30px auto;
    padding: 25px 40px;
    border-radius: 20px;

    /* Жылтыр көк аним фон */
    background: linear-gradient(135deg, #e8f2ff, #cde3ff, #dcedff);
    background-size: 300% 300%;
    animation: moveBG 8s ease infinite;

    /* Жұмсақ контур */
    border: 2px solid rgba(255, 255, 255, 0.7);

    /* Көлеңке */
    box-shadow: 0 8px 18px rgba(0, 0, 0, 0.12);

    text-align: center;

    /* Жайлап шығатын анимация */
    opacity: 0;
    animation: fadeIn 1.5s ease forwards, moveBG 8s ease infinite;
}

/* Иконка */
.author-info .icon {
    font-size: 40px;
    margin-bottom: 10px;
    animation: floatIcon 3s ease-in-out infinite;
}

/* Бірдей шрифт стилі */
.author-info p {
    margin: 6px 0;
    font-size: 17px;
    font-weight: 600;
    color: #103458; /* анық көрінетін қою көк */
}

.author-info strong {
    color: #0a2038;
    font-weight: 800;
}

/* Фон қозғалысы */
@keyframes moveBG {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

/* Жайлап шығу */
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

/* Иконкаға қозғалыс (жоғары-төмен) */
@keyframes floatIcon {
    0% { transform: translateY(0); }
    50% { transform: translateY(-6px); }
    100% { transform: translateY(0); }
}
</style>




                <button class="btn btn-primary" onclick="showPage('modules')">БАСТАУ 🚀</button>
            </div>
        </div>

        <div id="modules" class="page">
         <div style="
    text-align:center; 
    margin:20px 0; 
    padding:30px;
    border-radius:18px;
    background:linear-gradient(120deg, #6bb6ff, #4a90e2, #8ac3ff);
    background-size:300% 300%;
    animation:moveBg 6s ease infinite;
    box-shadow:0 6px 14px rgba(0,0,0,0.15);
">

  <h2 style="
      font-size:28px;
      color:white;
      margin-bottom:5px;
      font-weight:700;
      text-shadow:0 2px 6px rgba(0,0,0,0.25);
  ">
    Курс мазмұны
  </h2>

  <p style="
      font-size:17px;
      color:#eaf4ff;
      opacity:0.95;
  ">
    Бөлімді таңдаңыз
  </p>

  <div style="
      width:70px;
      height:3px;
      background:white;
      margin:12px auto;
      border-radius:10px;
      opacity:0.9;
  "></div>

</div>

<style>
@keyframes moveBg {
    0% { background-position:0% 50%; }
    50% { background-position:100% 50%; }
    100% { background-position:0% 50%; }
}
</style>



            
            <div class="module-grid">
                <div class="module-item" onclick="openModule(1)">
                    <span class="emoji">🧠</span>
                    <h3>І Бөлім</h3>
                    <p>ЖИ негіздері</p>
                </div>
                <div class="module-item" onclick="openModule(2)">
                    <span class="emoji">⚖️</span>
                    <h3>ІІ Бөлім</h3>
                    <p>Құқық және этика</p>
                </div>
                <div class="module-item" onclick="openModule(3)">
                    <span class="emoji">⚠️</span>
                    <h3>III Бөлім</h3>
                    <p>Қауіптер мен тәуекелдер</p>
                </div>
                <div class="module-item" onclick="openModule(4)">
                    <span class="emoji">🛡️</span>
                    <h3>IV Бөлім</h3>
                    <p>Қауіпсіздік мәдениеті</p>
                </div>
             <!-- --------------------------
  Батырма (оригинал) — өзгерген жоқ,
  бірақ енді ол чат модалын ашады + showPage('lesson-list') шақырады
--------------------------- -->
<!-- AI CHAT FULL READY BLOCK -->

<!-- AI CHAT BUTTON -->
<div class="module-item full-width ai-open-btn" onclick="openAiChat()"
     style="cursor:pointer; border:2px solid #0077ff; padding:18px; border-radius:16px; text-align:center; background:#eaf3ff;">
    <span class="emoji" style="font-size:32px;">🤖</span>
    <h3 style="margin:8px 0 4px;">Жасанды интеллект чаты</h3>
    <p style="margin:0; color:#004c99;">Кез келген сұраққа жауап алады</p>
</div>


<!-- AI CHAT MODAL -->
<div id="aiChatModal" class="ai-modal">
    <div class="ai-modal-content">

        <!-- CLOSE BUTTON -->
        <span class="ai-close">&times;</span>

        <h2 class="ai-title">🤖 AI чат</h2>

        <!-- CHAT WINDOW -->
        <div id="aiMessages" class="ai-messages"></div>

        <!-- INPUT FORM -->
        <form id="aiForm" class="ai-form">
            <input id="aiInput" type="text" placeholder="Сұрағыңызды жазыңыз..." required />
            <button type="submit">Жіберу</button>
        </form>

    </div>
</div>


<style>
/* MODAL BACKGROUND */
.ai-modal {
    display: none;
    position: fixed;
    z-index: 2000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.55);
    backdrop-filter: blur(4px);
}

/* MODAL WINDOW */
.ai-modal-content {
    background: #ffffff;
    width: 90%;
    max-width: 420px;
    margin: 80px auto;
    padding: 20px;
    border-radius: 18px;
    position: relative;
    box-shadow: 0 8px 30px rgba(0,0,0,0.2);
    animation: fadeIn 0.3s ease;
}

/* CLOSE BUTTON */
.ai-close {
    position: absolute;
    right: 14px;
    top: 10px;
    font-size: 28px;
    cursor: pointer;
    color: #444;
}

/* TITLE */
.ai-title {
    text-align: center;
    margin-bottom: 12px;
    color: #0077ff;
}

/* CHAT MESSAGE WINDOW */
.ai-messages {
    height: 260px;
    overflow-y: auto;
    padding: 10px;
    border: 1px solid #e2e2e2;
    border-radius: 12px;
    background: #f9f9f9;
    margin-bottom: 12px;
    font-size: 15px;
}

/* INPUT AREA */
.ai-form {
    display: flex;
    gap: 10px;
}

.ai-form input {
    flex: 1;
    padding: 10px;
    border-radius: 10px;
    border: 1px solid #bbb;
    font-size: 15px;
}

.ai-form button {
    background: #0077ff;
    color: #fff;
    padding: 10px 18px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
}

.ai-form button:hover {
    background: #005fcc;
}

/* OPEN ANIMATION */
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
}
</style>



<script>
/* -------------------------------
   AI CHAT — ДҰРЫС АЙНЫМАЛЫЛАР
--------------------------------*/
const modal6 = document.getElementById('aiChatModal');
const aiMessages = document.getElementById('aiMessages');
const aiInput = document.getElementById('aiInput');
const aiForm = document.getElementById('aiForm');
const closeBtn6 = document.querySelector('.ai-close');

/* ----- OPEN CHAT ----- */
function openAiChat() {
    modal6.style.display = "block";
}

/* ----- CLOSE CHAT BUTTON ----- */
closeBtn6.addEventListener('click', () => {
    modal6.style.display = "none";
});

/* ----- CLICK OUTSIDE TO CLOSE ----- */
window.addEventListener('click', (e) => {
    if (e.target === modal6) modal6.style.display = "none";
});

/* ----- SEND MESSAGE ----- */
aiForm.addEventListener('submit', function(e) {
    e.preventDefault();

    const text = aiInput.value.trim();
    if (!text) return;

    addMessage("🧑‍💻 Сіз:", text);
    aiInput.value = "";

    setTimeout(() => {
        addMessage("🤖 AI:", "Жазылуда...");
    }, 600);
});

/* ----- ADD MESSAGE ----- */
function addMessage(author, text) {
    const div = document.createElement("div");
    div.innerHTML = `<strong>${author}</strong> ${text}`;
    aiMessages.appendChild(div);
    aiMessages.scrollTop = aiMessages.scrollHeight;
}
</script>



<!-- --- SafeNet кнопкасы --- -->
<!-- ============================= -->
<!--   ONE BUTTON – TWO PROJECTS   -->
<!-- ============================= -->

<!-- OPEN BUTTON -->
<div onclick="openProjectsModal()" 
     style="padding:20px; background:#007bff; color:white; 
            text-align:center; border-radius:14px; 
            cursor:pointer; font-size:20px; 
            max-width:300px; margin:25px auto;
            transition:0.3s; box-shadow:0 6px 18px rgba(0,0,0,0.2);">
    📘 SafeNet & GovConnect
</div>

<!-- MODAL FULLSCREEN WINDOW -->
<div id="projectsModal" class="proj-modal">
    <div class="proj-content">

        <span class="proj-close">&times;</span>

        <h1 class="proj-title">📘 SafeNet және GovConnect жобалары</h1>

        <div class="proj-section">
            <h2>1 — Оқушылардың жасаған жұмыстары</h2>
            <p>
                Осы курстың нәтижесінде оқушылар жасөспірімдердің 
                киберкеңістіктегі құқықтарын қорғауға арналған 
                шағын онлайн платформа (сайт) жасады.
            </p>
            <p>
                Платформаның мақсаты:
                <br>• Жасөспірімдерді интернеттегі құқықтарымен таныстыру
                <br>• Кибербуллингтен, фейк аккаунттардан қорғану
                <br>• Қиындық туғанда қайда хабарласу керегін көрсету
            </p>

            <a href="https://safenet-safe-space.lovable.app/" 
               target="_blank" class="proj-link">
               🔗 SafeNet платформасын ашу
            </a>
        </div>

        <hr>

        <div class="proj-section">
            <h2>2 — GovConnect платформасы</h2>
            <p>
                GovConnect платформасы азаматтар мен үкімет арасындағы 
                ашық және тиімді коммуникация орнатады. 
            </p>
            <p>
                Онлайн қызметтерді жылдам, түсінікті және қауіпсіз түрде 
                пайдалануға мүмкіндік береді.
            </p>
        </div>

    </div>
</div>

<!-- ============================= -->
<!--          STYLES               -->
<!-- ============================= -->

<style>
/* FULLSCREEN MODAL */
.proj-modal {
    display: none;
    position: fixed;
    left:0; top:0;
    width:100%; height:100%;
    background: rgba(0,0,0,0.55);
    backdrop-filter: blur(8px);
    z-index:3000;
}

/* MODAL BOX */
.proj-content {
    background:white;
    width:90%;
    max-width:750px;
    max-height:85%;
    overflow-y:auto;
    margin:60px auto;
    padding:30px;
    border-radius:20px;
    animation: slideUp 0.35s ease;
    box-shadow:0 10px 35px rgba(0,0,0,0.25);
}

/* CLOSE BUTTON */
.proj-close {
    float:right;
    font-size:36px;
    cursor:pointer;
    color:#007bff;
    transition:0.2s;
}
.proj-close:hover {
    color:#0046ba;
}

/* TITLES */
.proj-title {
    text-align:center;
    margin-bottom:25px;
    color:#005ad6;
}

.proj-section h2 {
    margin-bottom:8px;
    color:#007bff;
}

.proj-section p {
    line-height:1.55;
    margin-bottom:10px;
}

/* LINK BUTTON */
.proj-link {
    display:inline-block;
    margin-top:10px;
    padding:10px 18px;
    background:#007bff;
    color:white;
    border-radius:10px;
    text-decoration:none;
    transition:0.3s;
}
.proj-link:hover {
    background:#005fcc;
}

/* ANIMATION */
@keyframes slideUp {
    from { transform: translateY(40px); opacity:0; }
    to   { transform: translateY(0); opacity:1; }
}
</style>

<!-- ============================= -->
<!--          SCRIPT               -->
<!-- ============================= -->

<script>
const projModal = document.getElementById("projectsModal");
const projClose = document.querySelector(".proj-close");

function openProjectsModal() {
    projModal.style.display = "block";
}

projClose.onclick = () => {
    projModal.style.display = "none";
};

window.onclick = (e) => {
    if (e.target === projModal) projModal.style.display = "none";
};
</script>




            </div>
        </div>

        <div id="lesson-list" class="page">
            <button class="btn btn-secondary btn-back" onclick="showPage('modules')">⬅ Бөлімдерге оралу</button>
            <h2 id="module-title" class="section-title"></h2>
            <div id="lessons-container" class="lesson-list-container"></div>
        </div>
        
        <div id="lesson-view" class="page lesson-detail-page">
            <button class="btn btn-secondary btn-back" onclick="showPage('lesson-list')">⬅ Сабақтар тізіміне</button>
            <div class="card">
                <h2 id="lesson-header-title"></h2>
                
                <div class="tab-container">
                    <button class="tab-btn active" onclick="switchTab('lecture')">📖 Лекция</button>
                    <button class="tab-btn" onclick="switchTab('tasks')">✍️ Тапсырма</button>
                    <button class="tab-btn" onclick="switchTab('quiz')">✅ Тест</button>
                </div>

                <div id="tab-lecture" class="tab-content">
                    <div id="lecture-text" class="lecture-text"></div>
                    <div class="glossary-box">
                        <h4 class="box-title">📖 Глоссарий</h4>
                        <ul id="glossary-list"></ul>
                    </div>
                    <p class="source-link">Толық ақпарат: <div style="text-align:center; margin-top:20px;">
  <a href="https://chat.openai.com" target="_blank" rel="noopener"
     style="
        display:inline-block;
        padding:6px 14px;
        font-size:14px;
        border-radius:10px;
        background:#4a90e2;
        color:white;
        text-decoration:none;
        margin:5px;
        box-shadow:0 3px 6px rgba(0,0,0,0.15);
        transition:0.2s;
     "
     onmouseover="this.style.background='#3b7ccd'"
     onmouseout="this.style.background='#4a90e2'">
    ChatGPT
  </a>

  <a href="https://adilet.zan.kz" target="_blank" rel="noopener"
     style="
        display:inline-block;
        padding:6px 14px;
        font-size:14px;
        border-radius:10px;
        background:#27ae60;
        color:white;
        text-decoration:none;
        margin:5px;
        box-shadow:0 3px 6px rgba(0,0,0,0.15);
        transition:0.2s;
     "
     onmouseover="this.style.background='#1f8f4f'"
     onmouseout="this.style.background='#27ae60'">
    Adilet ZAN KZ
  </a>
</div>


                </div>

                <div id="tab-tasks" class="tab-content" style="display: none;">
                    <h3 class="section-subtitle">Деңгейлік тапсырмалар</h3>
                    <div id="tasks-accordion"></div>
                </div>

                <div id="tab-quiz" class="tab-content" style="display: none;">
                    <h3 class="section-subtitle">Білімді тексеру (10 сұрақ)</h3>
                    <form id="quiz-form"></form>
                    <button class="btn btn-primary" onclick="checkQuiz()">Нәтижені тексеру</button>
                    <div id="quiz-result" class="quiz-result"></div>
                </div>

            </div>
        </div>
        
        <div id="admin" class="page">
            <div class="card">
                <h2 class="section-title">🏛️ Құжаттама </h2>
                <p><strong>Жобаның негіздемесін берген мекеме:</strong></p>
                <p class="school-full">«Түлкібас ауданының үш тілде оқытатын мамандандырылған мектеп-интернаты» КММ</p>

                <h3 class="section-subtitle">Автор туралы</h3>
                <div class="author-details">
                    <p><strong>Арыстанбекова Улпан Аманбековна</strong></p>
                    <p class="role">Құқық пәнінің мұғалімі</p>
                </div>
                
                <h3 class="section-subtitle">Бағдарлама мақсаты</h3>
                <p class="goal-text">Оқушыларды Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті туралы жан-жақты біліммен қамтамасыз ету.</p>
                
                <h3 class="section-subtitle">✨ Жоба көмекшілері </h3>
                <ul class="admin-list">
                    <li>Оқушылар: Абдысадық М.А және Иса Е.А</li>
                    </ul>
            </div>
            <!-- ----------------------------------------- -->
<!--   Қосымша Құжат: Пікір (Дизайн + Анимация) -->
<!-- ----------------------------------------- -->

<style>
    .doc-card {
        background: #ffffff;
        padding: 25px;
        margin-top: 25px;
        border-radius: 20px;
        box-shadow: 0 8px 25px rgba(0,0,0,0.12);
        border: 1px solid rgba(0,0,0,0.08);
        animation: fadeUpDoc 0.7s ease forwards;
        opacity: 0;
        transform: translateY(20px);
    }

    @keyframes fadeUpDoc {
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .doc-title {
        font-size: 24px;
        font-weight: 700;
        color: #005ce6;
        margin-bottom: 15px;
        text-align: center;
    }

    .doc-text {
        color: #333;
        line-height: 1.7;
        font-size: 16px;
        white-space: pre-line;
    }

    .doc-author {
        margin-top: 25px;
        background: #f3f7ff;
        padding: 15px;
        border-left: 4px solid #0077ff;
        border-radius: 10px;
        font-size: 15px;
    }
</style>

<div class="doc-card">
    <div class="doc-title">📄 Пікір құжаты</div>

    <div class="doc-text">
Түлкібас ауданының үш тілде оқытатын мамандандырылған мектеп-интернатының 
тарих және география пәнінің мұғалімі Арыстанбекова Улпан Аманбековнаның 
«Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» авторлық 
бағдарламасына

Пікір

Арыстанбекова Улпанның «Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» 
авторлық бағдарламасы сабақтарды практикалық және интерактивті түрде ұйымдастыру арқылы 
оқушылардың қызығушылығын арттырады. Сабақтарда ЖИ құралдарын қолдану тәжірибесі, 
мысалы, ChatGPT, Midjourney, нақты өмірлік кейстермен үйлестірілген, бұл оқушыларға 
теория мен практиканы байланыстыруға мүмкіндік береді. Құқықтық және этикалық бөлімдер 
оқушылардың цифрлық мәдениеті мен қауіпсіздік дағдыларын дамытуға бағытталған.

І бөлімінде ЖИ эволюциясы, Тьюринг тесті, алғашқы нейрондық желілер сияқты тарихи 
аспектілер қамтылған. SWOT талдау арқылы оқушылар ЖИ-дің қоғамға әсерін бағалауды үйренеді.

ІІ бөлімінде халықаралық және ҚР заңнамаларын таныстыру, авторлық құқық және этика 
қағидалары енгізілген. Дебаттар мен кейс-талдаулар арқылы этикалық шешім қабылдау 
дағдылары қалыптасады.

III бөлімінде Deepfake, кибербуллинг, интернет алаяқтық, алгоритмдік әділетсіздік мәселелері 
қарастырылған. Құқықтық кейстерді шешу практикалық дағдыларды дамытады.

IV бөлімінде АІ мәдениеті, құқықтық симуляция, мини-жобалар мен презентацияларды 
қорғау. Жеке жауапкершілік пен этикалық ойлауды дамытады.

Бағдарлама оқушыларға ЖИ саласында жан-жақты білім береді: теориялық түсінік, құқықтық 
нормаларды білу, практикалық тәжірибе және этикалық ойлау қабілеті қалыптастырады. 
Заманауи технологияларды қолдануға үйретеді және жауапкершілікті саналы азамат ретінде қалыптастырады.
    </div>

    <div class="doc-author">
        М.Әуезов атындағы ОҚУ  
        «Жалпы тарих және музей ісі» кафедрасының доценті,  
        тарих ғылымдарының кандидаты:  
        <strong>Г. К. Отарбаева</strong>
    </div>
</div>
<!-- ----------------------------------------- -->
<!--   Қосымша Құжат: Пікір 2 (Дизайн + Анимация) -->
<!-- ----------------------------------------- -->

<div class="doc-card">
    <div class="doc-title">📄 Пікір құжаты</div>

    <div class="doc-text">
Түлкібас ауданының үш тілде оқытатын мамандандырылған мектеп-интернатының 
тарих және география пәнінің мұғалімі Арыстанбекова Улпан Аманбековнаның 
«Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» авторлық бағдарламасына

Пікір

Арыстанбекова Улпанның «Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» 
авторлық бағдарламасы қазіргі заманғы білім беру талаптарына толық жауап береді және 
оқушылардың теориялық білімін практикалық дағдылармен тиімді үйлестірген. Сабақтар  
интерактивті, қызықты тәсілдер арқылы құралып, оқушылардың белсенділігін арттырады.  
Әр бөлімде теория мен практика қатар дамиды, бұл ЖИ саласына кешенді көзқарас қалыптастырады.

ЖИ тарихы, алғашқы нейрондық желілер, Тьюринг тесті және Дартмут конференциясы тақырыптары 
логикалық түрде берілген. Практикалық сабақтар (ChatGPT, Midjourney) арқылы оқушылар 
ЖИ-ді өз тәжірибесінде қолдана алады. SWOT талдау сабақтары қоғамға әсерін терең түсінуге мүмкіндік береді. 
Халықаралық және Қазақстандық заңнамаларды қамту оқушыларға құқықтық ойлау қабілетін қалыптастырады. 
Дебат, кейс-талдау және цифрлық келісім-шарттарды талдау практикалық шешім қабылдауға үйретеді. 
Deepfake, кибербуллинг, интернет алаяқтық және алгоритмдік әділетсіздік мәселелері жан-жақты қарастырылған. 
Құқықтық кейстерді шешу сабақтары оқушылардың сыни ойлау және практикалық дағдыларын дамытады. 
АІ мәдениеті, нұсқаулық жасау, құқықтық симуляция, мини-жобалар және презентациялық қорғау сабақтары 
оқушылардың жеке жауапкершілігін, сыни ойлауын және коммуникация дағдыларын дамытады.

Бағдарлама оқушыларға ЖИ саласында жан-жақты білім береді: теориялық түсінік, құқықтық нормаларды 
білу, практикалық тәжірибе және этикалық ойлау қабілеті қалыптасады. Сабақтар технологиялық дағдыларды 
дамытып, саналы азамат ретінде қалыптасуға үлес қосады.
    </div>

    <div class="doc-author">
        Мектеп-интернат директоры<br>
        тарих пәнінің мұғалімі:<br>
        <strong>Талдахметов С.Ш.</strong>
    </div>
</div>
<!-- ----------------------------------------- -->
<!--   Қосымша Құжат: Түсіндірме жазба (Дизайн + Анимация) -->
<!-- ----------------------------------------- -->

<div class="doc-card">
    <div class="doc-title">📄 Түсіндірме жазба</div>

    <div class="doc-text">
«Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» авторлық бағдарлама
Түсіндірме жазба
Бағыты: Құқық негіздері

Бағдарламаның өзектілігі: Қазіргі цифрлық дәуірде жасанды интеллект жүйелері қоғамның барлық
саласында құқықтық қатынастардың жаңа формаларын қалыптастырды. Бұл технологияларды жауапкершілікпен
қолдану үшін құқықтық қауіпсіздік мәдениетін қалыптастыруды талап етіп отыр. 9-сынып оқушылары үшін
бұл курс құқықтық сауаттылықты арттырып жасанды интеллекттің тәуекелдерін түсінуге бағытталған.

Бағдарламаның жаңашылдығы: Бағдарлама жасанды интеллект пен құқықтық реттеу ұғымдарын біріктіріп,
оқушылардың цифрлық этика мен құқықтық жауапкершілік дағдыларын қалыптастырады.

Практикалық мақсаттылығы: Оқушылардың құқықтық мәдениетін цифрлық ортаға бейімдейді және сандық
қауіпсіздікке қатысты саналы көзқарасын дамытады.

Бағдарламаның мақсаты: Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті туралы түсінік
қалыптастыру және оқушыларды цифрлық ортадағы құқықтық жауапкершілік дағдыларына үйрету.

Бағдарламаның міндеттері:
- ЖИ жүйелерінің құқықтық негіздерін түсіндіру;
- Оқушылардың цифрлік құқықтық сауаттылығын арттыру;
- ЖИ қауіпсіздігін анықтау және қауіпті болса алдын алу жолдарын үйрету;
- Практикалық тапсырмалар арқылы құқықтық ойлау қабілетін дамыту.

Бағдарламаның ерекшелігі: Практикалық мысалдарға негізделген, ҚР заңнамасымен үйлестірілген және нақты
цифрлық жағдайларды талдауға арналған.

Күтілетін нәтижелер:
- ЖИ жүйелеріндегі құқықтық қауіпсіздік меңгереді;
- Құқықтық тәуекелдердің алдын алу;
- Цифрлық ортада өзін-өзі қорғау мәдениетін қалыптастырады.

Тексеру әдістері:
- деңгейлік тапсырмалар
- тест тапсырмалары
- практикалық жұмыстар
- жобалар
    </div>

    <div class="doc-author">
        «Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» бағдарламасының авторы
    </div>
</div>
<!-- ----------------------------------------- -->
<!--   Қосымша Құжат: Бағдарлама құрылымы (Дизайн + Анимация) -->
<!-- ----------------------------------------- -->

<div class="doc-card">
    <div class="doc-title">📄 Бағдарлама құрылымы</div>

    <div class="doc-text">
«Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәдениеті» бағдарламасының құрылымы:

I бөлім. Жасанды интеллекттің негіздері  
Жасанды интеллект негіздері және оның қоғамдағы рөлі. Жасанды интеллект ұғымы және даму тарихы.  
ЖИ түрлері және қолданылу салалары. ЖИ алгоритмдері және деректердің рөлі.  
Қазақстанда ЖИ енгізу саясаты. ЖИ құралдарын тәжірибе жүзінде қолдану.  
ЖИ-дің қоғамға әсері. ЖИ-дің ұлттық қауіпсіздікке ықпалы. Қорытынды сабақ.

II бөлім. Құқықтық негіздер және цифрлық этика  
ЖИ саласындағы халықаралық заңдар. Қазақстан Республикасының цифрлық заңнамасы.  
Авторлық құқық және ЖИ. ЖИ этикасы және адам құқықтары.  
Цифрлық келісім-шарттар. ЖИ платформаларын заңды қолдану.  
Этика кодексін әзірлеу. Қорытынды тест.

III бөлім. Жасанды интеллект жүйелеріндегі қауіптер мен құқықтық тәуекелдер  
Жалған ақпарат және Deepfake. Кибербуллинг пен ЖИ. Интернет алаяқтық.  
Алгоритмдік әділетсіздік. ЖИ-дің психологиялық әсері.  
Құқықтық жауапкершілік. Қауіпсіздік стратегиялары.  
Құқықтық кейс шешу. Бөлімдік жоба.

IV бөлім. Құқықтық қауіпсіздік мәдениетін қалыптастыру және практикалық жобалар  
Қауіпсіз AI мәдениетінің қағидалары. Жасанды интеллектті дұрыс қолдану практикасы.  
Құқықтық симуляция. Мини жоба: «ЖИ және құқық».  
Жобаны рәсімдеу. Презентациялық дайындық.  
Қорытынды жоба қорғау. Рефлексия. Қорытынды бағалау.
    </div>

    <div class="doc-author">
        Бағдарлама құрылымы.
    </div>
</div>



        </div>

        <div id="settings" class="page">
            <div class="card">
                <h2 class="section-title">⚙️ Баптаулар</h2>
                <h3 class="section-subtitle">Тақырып Түсі</h3>
                <p>Қосымшаның негізгі түсін өзгерту:</p>
                <div class="color-picker-grid">
                    <div class="color-dot" style="background: #4F46E5;" onclick="setTheme('#4F46E5')"></div>
                    <div class="color-dot" style="background: #E54646;" onclick="setTheme('#E54646')"></div>
                    <div class="color-dot" style="background: #059669;" onclick="setTheme('#059669')"></div>
                    <div class="color-dot" style="background: #F59E0B;" onclick="setTheme('#F59E0B')"></div>
                </div>
                
               <h3 class="section-subtitle"> Қолдау және байланыс</h3>
<p><strong>Telegram:</strong> @koldaubailanyskz</p>
<p><strong>Email:</strong> @ji-koldau.kz</p>
<p><strong>Қолдау қызметі:</strong> Жасанды интеллект жүйелеріндегі құқықтық қауіпсіздік мәселелері бойынша сұрақтарыңызды осы байланыс арналары арқылы жолдай аласыз.</p>
<p><em>Нұсқа:</em> 1.0 (алғашқы ресми шығарылым)</p>

            </div>
        </div>

    </div>
    
    <script>
        // Барлық 34 сабақтың атаулары
        const lessons = [
            // I БӨЛІМ. ЖИ Негіздері
            { id: 1, mod: 1, title: "1. Жасанды интеллект ұғымы және тарихы" },
            { id: 2, mod: 1, title: "2. ЖИ түрлері және қолданылу салалары" },
            { id: 3, mod: 1, title: "3. ЖИ алгоритмдері және деректердің рөлі" },
            { id: 4, mod: 1, title: "4. Қазақстанда ЖИ енгізу саясаты" },
            { id: 5, mod: 1, title: "5. ЖИ құралдарын тәжірибе жүзінде қолдану" },
            { id: 6, mod: 1, title: "6. ЖИ-дің қоғамға әсері (SWOT талдау)" },
            { id: 7, mod: 1, title: "7. ЖИ-дің ұлттық қауіпсіздікке ықпалы" },
            { id: 8, mod: 1, title: "8. Қорытынды сабақ (Талдау жұмысы)" },
            // II БӨЛІМ. Құқық және Этика
            { id: 9, mod: 2, title: "9. ЖИ саласындағы халықаралық заңдар" },
            { id: 10, mod: 2, title: "10. ҚР цифрлық заңнамасы" },
            { id: 11, mod: 2, title: "11. Авторлық құқық және ЖИ" },
            { id: 12, mod: 2, title: "12. ЖИ этикасы және адам құқықтары" },
            { id: 13, mod: 2, title: "13. Цифрлық келісім-шарттар" },
            { id: 14, mod: 2, title: "14. ЖИ платформаларын заңды қолдану" },
            { id: 15, mod: 2, title: "15. Цифрлық этика кодексін әзірлеу" },
            { id: 16, mod: 2, title: "16. Қорытынды тест (Бөлімдік бағалау)" },
            // III БӨЛІМ. Қауіптер мен Тәуекелдер
            { id: 17, mod: 3, title: "17. Жалған ақпарат және Deepfake" },
            { id: 18, mod: 3, title: "18. Кибербуллинг пен ЖИ" },
            { id: 19, mod: 3, title: "19. Интернет алаяқтық" },
            { id: 20, mod: 3, title: "20. Алгоритмдік әділетсіздік" },
            { id: 21, mod: 3, title: "21. ЖИ-дің психологиялық әсері" },
            { id: 22, mod: 3, title: "22. Құқықтық жауапкершілік" },
            { id: 23, mod: 3, title: "23. Қауіпсіздік стратегиялары" },
            { id: 24, mod: 3, title: "24. Құқықтық кейс шешу" },
            { id: 25, mod: 3, title: "25. Бөлімдік жоба: Қорғаныс" },
            { id: 26, mod: 3, title: "26. Бөлімдік қорытынды" },
            // IV БӨЛІМ. Қауіпсіздік Мәдениеті
            { id: 27, mod: 4, title: "27. Қауіпсіз ЖИ мәдениетінің қағидалары" },
            { id: 28, mod: 4, title: "28. ЖИ дұрыс қолдану практикасы" },
            { id: 29, mod: 4, title: "29. Құқықтық симуляция (Сот)" },
            { id: 30, mod: 4, title: "30. Мини жоба: «ЖИ және құқық»" },
            { id: 31, mod: 4, title: "31. Жобаны рәсімдеу" },
            { id: 32, mod: 4, title: "32. Презентациялық дайындық" },
            { id: 33, mod: 4, title: "33. Қорытынды жоба қорғау" },
            { id: 34, mod: 4, title: "34. Рефлексия және бағалау" }
        ];

        // Әр сабаққа арналған бірегей мазмұнды сақтайтын объект
        const LESSON_DATA = {};

        // --- САБАҚ 1 ---
        LESSON_DATA[1] = {
            lecture: `
                <p><strong>Жасанды Интеллект (ЖИ)</strong> — бұл адамның ми қызметіне ұқсас міндеттерді орындай алатын компьютерлік жүйелердің қабілеті. Оған оқыту, проблемаларды шешу және шешім қабылдау сияқты процестер кіреді.</p>
                <p>ЖИ тарихы XX ғасырдың ортасында, "ЖИ" термині алғаш рет Джон Маккартимен 1956 жылы қолданылғаннан бастау алады. Алғашқы кезеңдердегі үлкен үміттер "ЖИ қысы" деп аталатын дағдарыс кезеңдерімен алмасты. Алайда, 2000 жылдардан бастап, деректер көлемінің өсуі және есептеу қуатының артуы арқасында, ЖИ қазіргі "алтын ғасырына" жетті. Қазақстанда ЖИ дамыту - мемлекеттік бағдарламалардың басты басымдығы.</p>
            `,
            glossary: ["Жасанды Интеллект (ЖИ)", "Джон Маккарти", "ЖИ қысы", "Машиналық оқыту", "Нейрондық желі"],
            tasks: {
                l1: [
                    "«Жасанды интеллект» ұғымына өз сөзіңізбен анықтама беріңіз.", 
                    "ЖИ тарихындағы ең маңызды 3 оқиғаны атаңыз."
                ],
                l2: [
                    "Адам миы мен ЖИ-дің жұмыс істеу принциптерін Венн диаграммасы арқылы салыстырыңыз.", 
                    "Егер сіз ЖИ-ді алғаш ашқан ғалым болсаңыз, оны қалай атаған болар едіңіз? Ұсынысыңызды негіздеңіз."
                ],
                l3: [
                    "ЖИ-дің даму кезеңдерінің бірі – «ЖИ қысы» неліктен орын алды? Сол кездегі ғалымдардың көзқарасы қандай болды? Шағын талдау жасаңыз (50-70 сөз)."
                ]
            },
            questions: [
                { q: "«Жасанды интеллект» терминін кім енгізді?", opts: ["Алан Тьюринг", "Джон Маккарти", "Билл Гейтс", "Стив Джобс"], a: 1 },
                { q: "ЖИ тарихының дағдарыс кезеңі қалай аталады?", opts: ["Ақпараттық жарылыс", "ЖИ көктемі", "ЖИ қысы", "Сандық дәуір"], a: 2 },
                { q: "Машиналық оқыту ЖИ-дің қандай саласына жатады?", opts: ["Тарих", "Негізгі бағыт", "Құқық", "Этика"], a: 1 },
                { q: "ЖИ-дің қазіргі қарқынды дамуына не себеп болды?", opts: ["Адамдардың қызығушылығы", "Деректер көлемінің артуы", "Тек бағдарламалау тілдері", "Саясат"], a: 1 },
                { q: "Алғашқы ЖИ конференциясы қай жылы өтті?", opts: ["1980", "1956", "2005", "1991"], a: 1 },
                { type: 'tf', q: "ЖИ бұрыннан бар мәселелерді шешуге ғана қабілетті.", a: false },
                { type: 'tf', q: "Қазақстанда ЖИ дамытуға мемлекеттік қолдау көрсетіледі.", a: true },
                { type: 'tf', q: "ЖИ адамның эмоцияларын толықтай сезіне алады.", a: false },
                { type: 'text', q: "ЖИ-дің негізгі міндеті не?", a: "Шешім қабылдау" },
                { type: 'text', q: "ЖИ-дің ең көп қолданылатын әдісі (екі сөз)?", a: "Машиналық оқыту" }
            ]
        };

        // --- САБАҚ 2 ---
        LESSON_DATA[2] = {
            lecture: `
                <p>Жасанды интеллект жүйелері негізінен үш үлкен түрге бөлінеді: <strong>Әлсіз ЖИ (ANI)</strong>, <strong>Күшті ЖИ (AGI)</strong> және <strong>Супер ЖИ (ASI)</strong>.</p>
                <p>Әлсіз ЖИ белгілі бір тар міндеттерді (мысалы, Siri, дауысты тану) орындауға арналған. Қазіргі қолданыстағы ЖИ-дің басым көпшілігі осы түрге жатады. Күшті ЖИ - бұл адам сияқты кез келген зияткерлік міндетті орындай алатын теориялық жүйе. Супер ЖИ – адамзаттың ең ақылды адамынан да асып түсетін гипотетикалық интеллект. ЖИ-дің қолданылу салалары өте кең: медицина, қаржы, білім беру, өнер және қауіпсіздік салаларында ЖИ күнделікті өмірдің ажырамас бөлігіне айналуда.</p>
            `,
            glossary: ["Әлсіз ЖИ (ANI)", "Күшті ЖИ (AGI)", "Супер ЖИ (ASI)", "Тар міндет", "Гипотетикалық интеллект"],
            tasks: {
                l1: [
                    "Әлсіз, Күшті және Супер ЖИ арасындағы басты айырмашылықтарды атаңыз.", 
                    "Сіз күнделікті өмірде қолданатын 3 Әлсіз ЖИ құралын атаңыз."
                ],
                l2: [
                    "AGI қазіргі қоғамға енгізілсе, адамдардың жұмыс орындарына әсерін талдаңыз.", 
                    "Медицинадағы ЖИ қолданысы туралы шағын инфографика эскизін сызыңыз (диагноз қою)."
                ],
                l3: [
                    "Егер ASI (Супер ЖИ) жасалса, оның адамзат үшін әлеуетті қауіптері мен пайдасын болжаңыз. Қауіпсіздік тұрғысынан 2-3 дәлел келтіріңіз."
                ]
            },
            questions: [
                { q: "Қазіргі қолданыстағы ЖИ-дің көпшілігі қай түрге жатады?", opts: ["Күшті ЖИ", "Супер ЖИ", "Әлсіз ЖИ", "Механикалық ЖИ"], a: 2 },
                { q: "Адамнан да асып түсетін ЖИ қалай аталады?", opts: ["AGI", "ANI", "ASI", "NVIDIA"], a: 2 },
                { q: "Тар міндеттерді орындайтын жүйе?", opts: ["Күшті ЖИ", "Әлсіз ЖИ", "Супер ЖИ"], a: 1 },
                { q: "ЖИ қай салада қолданылмайды?", opts: ["Қаржы", "Мәдениет", "Жер ауырлығын өлшеу", "Білім беру"], a: 2 },
                { q: "AGI дегеніміз не?", opts: ["Тар міндетті шешу", "Кез келген зияткерлік міндетті шешу", "Ең қарапайым бағдарлама"], a: 1 },
                { type: 'tf', q: "Siri және Alexa - Күшті ЖИ (AGI) мысалдары.", a: false },
                { type: 'tf', q: "ЖИ-ді өнер саласында қолдануға болады.", a: true },
                { type: 'tf', q: "Супер ЖИ қазіргі таңда кеңінен қолданылады.", a: false },
                { type: 'text', q: "Күшті ЖИ-дің ағылшынша аббревиатурасы (үш әріп)?", a: "AGI" },
                { type: 'text', q: "ЖИ қолданылатын екі маңызды сала (бір сөйлеммен)?", a: "Медицина, қаржы" }
            ]
        };

        // --- САБАҚ 1 ---
LESSON_DATA[1] = {
    lecture: `
        <p><strong>Жасанды интеллект (ЖИ)</strong> - бұл адамның ақыл-ой әрекеттерін (үйрену, мәселе шешу, тану) имитациялай алатын компьютерлік жүйелер. ЖИ-ді заңды реттеу қажеттілігі оның қоғамға әсерінің артуымен байланысты. ЖИ-дің этикалық және құқықтық негіздері – бұл оның әділ, ашық және қауіпсіз жұмыс істеуін қамтамасыз ететін қағидалар жиынтығы.</p>
        <p>Құқықтық реттеу ЖИ-дің адам құқықтарын бұзу, кемсітушілікке жол беру және жауапкершілік мәселелері сияқты қауіптерін азайтуға бағытталған. Қазақстан Республикасының (ҚР) заңнамасында ЖИ-ге қатысты арнайы ережелерді енгізу өзекті мәселе болып отыр.</p>
    `,
    glossary: ["Жасанды интеллект (ЖИ)", "Имитациялау", "Құқықтық реттеу", "Этикалық негіздер", "Қағидалар"],
    tasks: {
        l1: [
            "Жасанды интеллектке (ЖИ) анықтама беріңіз.", 
            "ЖИ-ді құқықтық реттеу неліктен қажет? (2 себеп)."
        ],
        l2: [
            "ЖИ қолданылуы кезінде туындайтын 3 негізгі этикалық мәселені атаңыз.", 
            "ҚР заңнамасына ЖИ-ге қатысты арнайы ережелерді енгізу қаншалықты өзекті? (2 дәлел)."
        ],
        l3: [
            "Сіздің ойыңызша, ЖИ үшін ең маңызды 2 этикалық қағида қандай? Неліктен? (Түсіндіріңіз)."
        ]
    },
    questions: [
        { q: "Жасанды интеллект нені имитациялайды?", opts: ["Табиғатты", "Адамның ақыл-ой әрекеттерін", "Қозғалысты"], a: 1 },
        { q: "ЖИ-дің этикалық негіздері нені қамтамасыз етеді?", opts: ["Жылдамдықты", "Әділ, ашық және қауіпсіз жұмысты", "Арзандықты"], a: 1 },
        { q: "ҚР заңнамасына ЖИ-ге қатысты ережелерді енгізу - бұл:", opts: ["Өзекті мәселе", "Маңызды емес мәселе", "Шешілген мәселе"], a: 0 },
        { q: "Құқықтық реттеу неге бағытталған?", opts: ["ЖИ-дің дамуын тежеуге", "ЖИ-дің қауіптерін азайтуға", "Тек техникалық мәселелерді шешуге"], a: 1 },
        { q: "Қағидалар жиынтығы нені білдіреді?", opts: ["Техникалық сипаттаманы", "Этикалық және құқықтық негіздерді", "Тек бағдарлама кодын"], a: 1 },
        { type: 'tf', q: "ЖИ-ді реттеу адам құқықтарын қорғауға қатысты емес.", a: false },
        { type: 'tf', q: "ЖИ-дің әсері артқан сайын оны заңды реттеу қажеттілігі артады.", a: true },
        { type: 'tf', q: "ҚР заңнамасында ЖИ туралы арнайы ережелер толығымен бар.", a: false },
        { type: 'text', q: "ЖИ-дің адамның ақыл-ой әрекеттерін көшіруі (бір сөз)?", a: "Имитациялау" },
        { type: 'text', q: "ЖИ-дің әділ жұмыс істеуін қамтамасыз ететін негіздер (екі сөз)?", a: "Этикалық негіздер" }
    ]
};

// --- САБАҚ 2 ---
LESSON_DATA[2] = {
    lecture: `
        <p><strong>Құқықтық нормалар</strong> – бұл мемлекет белгілеген, орындалуы міндетті жалпыға ортақ жүріс-тұрыс ережелері. ЖИ-дің жұмысын реттеудегі құқықтық нормалар, әсіресе Қазақстан Республикасының Конституциясы, азаматтық және қылмыстық кодекстер сияқты негізгі заңдарға сүйенеді.</p>
        <p>ЖИ жүйелерінің әрекеттері (мысалы, қате шешім, деректерді өңдеу) барлық осы нормаларға қайшы келмеуі керек. Қазіргі таңда көптеген мемлекеттер ЖИ-ге арналған арнайы заңдарды әзірлеуде. ҚР-да да «Цифрлық Қазақстан» бағдарламасы аясында ЖИ-ді құқықтық реттеу мәселесі талқылануда.</p>
    `,
    glossary: ["Құқықтық нормалар", "Конституция", "Азаматтық кодекс", "Қылмыстық кодекс", "Цифрлық Қазақстан"],
    tasks: {
        l1: [
            "Құқықтық нормаларға анықтама беріңіз.", 
            "ЖИ-дің әрекеттері ҚР-дағы қандай 2 негізгі құқықтық құжатқа қайшы келмеуі керек?"
        ],
        l2: [
            "Азаматтық кодекс тұрғысынан ЖИ қатысқан қандай 2 мәселе туындауы мүмкін? (Мысалы, зиян келтіру).", 
            "ҚР-дағы «Цифрлық Қазақстан» бағдарламасы ЖИ-ді реттеуге қатысты қандай маңыздылыққа ие? (2 дәлел)."
        ],
        l3: [
            "ЖИ-ге қатысты арнайы заңның (мысалы, Еуропалық Одақтың ЖИ туралы Актісі) ҚР үшін қажеттілігін 3 аргументпен негіздеңіз."
        ]
    },
    questions: [
        { q: "Құқықтық нормалар нені білдіреді?", opts: ["Тек техникалық ережелерді", "Орындалуы міндетті жалпыға ортақ жүріс-тұрыс ережелерін", "Тек жеке пікірлерді"], a: 1 },
        { q: "ЖИ-дің жұмысын реттеудегі негізгі заң?", opts: ["Конституция", "Еңбек кодексі", "Әкімшілік кодекс"], a: 0 },
        { q: "«Цифрлық Қазақстан» бағдарламасы нені талқылауда?", opts: ["Ауыл шаруашылығын", "ЖИ-ді құқықтық реттеу мәселесін", "Спорттық жарыстарды"], a: 1 },
        { q: "Көптеген мемлекеттер ЖИ-ге арналған не әзірлеуде?", opts: ["Жаңа бағдарламалар", "Арнайы заңдар", "Жаңа компьютерлер"], a: 1 },
        { q: "Қылмыстық кодекс ЖИ қатысқан қандай әрекеттерді реттейді?", opts: ["Ауа райы болжамын", "Заңға қайшы әрекеттерді", "Күнделікті жұмыстарды"], a: 1 },
        { type: 'tf', q: "Құқықтық нормалар мемлекет белгілеген ережелер болып табылмайды.", a: false },
        { type: 'tf', q: "ЖИ жүйелерінің әрекеттері құқықтық нормаларға қайшы келмеуі керек.", a: true },
        { type: 'tf', q: "Азаматтық кодекс ЖИ-дің зиян келтіру мәселесін реттеуге қатысты емес.", a: false },
        { type: 'text', q: "ЖИ-ді құқықтық реттеу талқыланатын ҚР бағдарламасы (екі сөз)?", a: "Цифрлық Қазақстан" },
        { type: 'text', q: "Құқықтық нормаларды белгілейтін орган (бір сөз)?", a: "Мемлекет" }
    ]
};

// --- САБАҚ 3 ---
LESSON_DATA[3] = {
    lecture: `
        <p><strong>ЖИ-дің әрекет ету қабілеті</strong> (Legal Personality) – бұл ЖИ-ді заңды тұлға ретінде тану мүмкіндігі. Қазіргі таңда, ҚР заңнамасында да, әлемдік тәжірибеде де ЖИ-дің өзі жеке құқықтық субъект ретінде танылмайды. Жауапкершілік әрқашан оның иесіне, операторына немесе өндірушісіне жүктеледі.</p>
        <p>Алайда, ЖИ-дің өзіндік шешім қабылдау қабілеті дамыған сайын, құқықтық жүйелер осы мәселені қайта қарауға мәжбүр болуы мүмкін. Болашақта, жоғары автономды ЖИ-ге шектеулі құқықтық мәртебе беру ұсыныстары (мысалы, 'электрондық тұлға' – Electronic Person) талқылануда. Бұл құқықтық коллизияға әкеледі.</p>
    `,
    glossary: ["Әрекет ету қабілеті", "Legal Personality", "Құқықтық субъект", "Электрондық тұлға", "Автономды ЖИ", "Құқықтық коллизия"],
    tasks: {
        l1: [
            "ЖИ-дің 'Әрекет ету қабілеті' дегенді қазіргі құқықтық тұрғыдан түсіндіріңіз.", 
            "Қазіргі ҚР заңнамасында ЖИ-дің әрекеттері үшін жауапкершілік кімге жүктеледі? (3 иесін атаңыз)."
        ],
        l2: [
            "Неліктен жоғары автономды ЖИ-ге болашақта 'Электрондық тұлға' мәртебесін беру мәселесі туындайды? (2 себеп).", 
            "ЖИ-ге құқықтық мәртебе берудің 2 құқықтық коллизиясын (қайшылығын) атаңыз (Мысалы, ЖИ-ді жазалау мүмкін бе?)."
        ],
        l3: [
            "Сіздің ойыңызша, ЖИ-ге 'Электрондық тұлға' мәртебесін берудің 2 артықшылығы мен 2 кемшілігі қандай? Аргументтеріңізді негіздеңіз."
        ]
    },
    questions: [
        { q: "Қазіргі таңда ЖИ құқықтық субъект ретінде таныла ма?", opts: ["Иә", "Жоқ", "Тек ҚР-да"], a: 1 },
        { q: "Жауапкершілік кімге жүктеледі?", opts: ["Тек ЖИ-дің өзіне", "Иесіне, операторына немесе өндірушісіне", "Кездейсоқ қолданушыға"], a: 1 },
        { q: "Болашақта талқыланатын мәртебе?", opts: ["Техникалық құрылғы", "Электрондық тұлға", "Бағдарламалық қамтамасыз ету"], a: 1 },
        { q: "Құқықтық коллизия нені білдіреді?", opts: ["Заңдардың үйлесімділігін", "Құқықтық қайшылықты", "Заңдардың жылдамдығын"], a: 1 },
        { q: "ЖИ-дің әрекет ету қабілеті ағылшынша қалай аталады?", opts: ["Artificial Intelligence", "Legal Personality", "Digital Rights"], a: 1 },
        { type: 'tf', q: "ҚР заңнамасы ЖИ-ді жеке құқықтық субъект ретінде таниды.", a: false },
        { type: 'tf', q: "ЖИ-дің өзіндік шешім қабылдау қабілеті құқықтық мәселе тудырады.", a: true },
        { type: 'tf', q: "Автономды ЖИ-ге шектеулі құқықтық мәртебе беру ұсынылмайды.", a: false },
        { type: 'text', q: "ЖИ-дің өзіндік шешім қабылдау қабілеті (бір сөз)?", a: "Автономды" },
        { type: 'text', q: "ЖИ-ге берілуі мүмкін болашақ мәртебе (екі сөз)?", a: "Электрондық тұлға" }
    ]
};

// --- САБАҚ 4 ---
LESSON_DATA[4] = {
    lecture: `
        <p><strong>Құқықтық субъектілер</strong> – бұл өз атынан құқықтар мен міндеттерге ие бола алатын тұлғалар. ҚР-да олар жеке тұлғалар (азаматтар) және заңды тұлғалар (компаниялар, ұйымдар). ЖИ жүйесі құқықтық субъектілермен өзара әрекеттеседі, мысалы, келісім-шарттар жасауға көмектеседі немесе қызмет көрсетеді.</p>
        <p>Қазіргі құқықтық тұрғыдан, ЖИ жасаған келісім-шарттар үшін жауапкершілік әрқашан ЖИ-дің операторына немесе заңды тұлғаға жүктеледі. Құқықтық реттеудің мақсаты – ЖИ-дің адамдарға және заңды тұлғаларға зиян келтірмеуін қамтамасыз ету және құқықтық қатынастардағы ашықтықты сақтау.</p>
    `,
    glossary: ["Құқықтық субъектілер", "Жеке тұлға", "Заңды тұлға", "Келісім-шарт", "Құқықтық қатынастар", "Оператор"],
    tasks: {
        l1: [
            "Құқықтық субъектілерге анықтама беріңіз.", 
            "ҚР-дағы құқықтық субъектілердің 2 түрін атаңыз."
        ],
        l2: [
            "Егер ЖИ келісім-шарт жасауға көмектессе, жауапкершілік кімге жүктеледі? 2 мысал келтіріңіз.", 
            "ЖИ-дің қатысуымен болатын құқықтық қатынастарда ашықтықты сақтау неліктен маңызды? (2 себеп)."
        ],
        l3: [
            "ЖИ-дің заңды тұлғаларға (мысалы, компанияларға) әсер етуіне қатысты 2 құқықтық мәселені талдаңыз (Мысалы, ЖИ-дің коммерциялық құпияны ашу қаупі)."
        ]
    },
    questions: [
        { q: "Жеке тұлғалар дегеніміз кім?", opts: ["Компаниялар", "Азаматтар", "Бағдарламалар"], a: 1 },
        { q: "Заңды тұлғаларға не жатады?", opts: ["Азаматтар", "Ұйымдар, компаниялар", "Компьютерлер"], a: 1 },
        { q: "ЖИ жасаған келісім-шарттар үшін жауапкершілік кімде болады?", opts: ["ЖИ-дің өзінде", "Операторда немесе заңды тұлғада", "Кездейсоқ куәгерде"], a: 1 },
        { q: "Құқықтық қатынастарда ашықтықты сақтау ненің мақсаты?", opts: ["Техникалық дамудың", "Құқықтық реттеудің", "Арзандықтың"], a: 1 },
        { q: "Құқықтық субъектілер нені иелене алады?", opts: ["Тек ақшаны", "Құқықтар мен міндеттерді", "Тек бағдарламаларды"], a: 1 },
        { type: 'tf', q: "ЖИ жүйесі қазіргі таңда ҚР-да заңды тұлға болып танылады.", a: false },
        { type: 'tf', q: "Құқықтық реттеудің мақсаты – ЖИ-дің зиян келтірмеуін қамтамасыз ету.", a: true },
        { type: 'tf', q: "Құқықтық қатынастарда ашықтықты сақтау маңызды емес.", a: false },
        { type: 'text', q: "Өз атынан құқықтар мен міндеттерге ие болатын тұлғалар (екі сөз)?", a: "Құқықтық субъектілер" },
        { type: 'text', q: "ЖИ-ді басқаратын тұлға (бір сөз)?", a: "Оператор" }
    ]
};

// --- САБАҚ 5 ---
LESSON_DATA[5] = {
    lecture: `
        <p><strong>ЖИ-дің әділдігі</strong> (Fairness) – бұл ЖИ алгоритмдерінің нәсіліне, жынысына, жасына немесе әлеуметтік жағдайына байланысты адамдарды кемсітпеуін қамтамасыз ететін этикалық және құқықтық қағида. Әділдік принциптері деректерді жинаудан бастап, ЖИ шешімдерін қолдануға дейінгі барлық кезеңдерді қамтуы керек.</p>
        <p>Егер ЖИ жүйесі кемсітушілікке жол берсе (мысалы, несие беруден бас тарту), бұл ҚР Конституциясымен және кемсітушілікке қарсы заңдармен тыйым салынған адам құқықтарының бұзылуы болып саналады. Құқықтық реттеулер әділетсіздікке ұшыраған адамдарға **құқықтық қорғау** мен **апелляция** мүмкіндігін беруі керек.</p>
    `,
    glossary: ["ЖИ-дің әділдігі", "Fairness", "Кемсітушілік", "Апелляция", "Құқықтық қорғау", "Әділдік принциптері"],
    tasks: {
        l1: [
            "ЖИ-дің әділдігі дегеніміз не?", 
            "ЖИ кемсітушілікке жол берсе, бұл ҚР-дағы қандай құқықтың бұзылуы болып саналады?"
        ],
        l2: [
            "Несие берудегі кемсітушілікке жол беретін ЖИ-дің 2 нақты мысалын сипаттаңыз (мысалы, белгілі бір ауданда тұратындарға бас тарту).", 
            "Әділетсіздікке ұшыраған адамға берілуі керек 2 құқықтық мүмкіндікті атаңыз."
        ],
        l3: [
            "Әділдік қағидасын қамтамасыз ету үшін ЖИ алгоритмдерін **аудиттеуге** (тексеруге) қатысты ҚР заңнамасына енгізуге болатын 1 жаңа бапты ұсыныңыз. Оның мақсатын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Әділдік қағидасы неден кемсітпеуді қамтамасыз етеді?", opts: ["Тек техникалық білімнен", "Нәсіліне, жынысына, жасына байланысты", "Тек географиялық орнынан"], a: 1 },
        { q: "Кемсітушілікке жол берген ЖИ-дің әрекеті не болып саналады?", opts: ["Қалыпты жағдай", "Адам құқықтарының бұзылуы", "Тек техникалық қате"], a: 1 },
        { q: "Құқықтық реттеу әділетсіздікке ұшыраған адамдарға не беруі керек?", opts: ["Тек ақпарат", "Құқықтық қорғау мен апелляция мүмкіндігін", "Тек кеңес"], a: 1 },
        { q: "Әділдік принциптері қандай кезеңдерді қамтуы керек?", opts: ["Тек деректерді жинауды", "Барлық кезеңдерді", "Тек шешімдерді қолдануды"], a: 1 },
        { q: "Әділдік ағылшынша қалай аталады?", opts: ["Transparency", "Fairness", "Accountability"], a: 1 },
        { type: 'tf', q: "Әділдік қағидасы тек деректерді жинау кезеңінде ғана маңызды.", a: false },
        { type: 'tf', q: "Кемсітушілік ҚР Конституциясымен тыйым салынған.", a: true },
        { type: 'tf', q: "Құқықтық қорғау әділетсіздікке ұшыраған адамға берілмейді.", a: false },
        { type: 'text', q: "Әділетсіздікке қарсы шағымдану мүмкіндігі (бір сөз)?", a: "Апелляция" },
        { type: 'text', q: "Адамдарды жынысына немесе нәсіліне байланысты бөлу (бір сөз)?", a: "Кемсітушілік" }
    ]
};

// --- САБАҚ 6 ---
LESSON_DATA[6] = {
    lecture: `
        <p><strong>ЖИ-дің жауапкершілігі</strong> (Accountability) – бұл ЖИ жүйесінің қате немесе зиянды әрекеттері үшін кінәліні табу және оған заңды жауапкершілікті жүктеу. Қазіргі құқықта, бұл жауапкершілік көбіне ЖИ-дің иесіне немесе операторына, яғни **заңды тұлғаға** жүктеледі.</p>
        <p>Жауапкершіліктің 3 түрі бар: азаматтық (зиянды өтеу), әкімшілік (айыппұл) және қылмыстық (бас бостандығынан айыру). Жоғары автономды ЖИ-дің қатесі үшін жауапкершілікті дәлелдеу өте қиын, бұл құқықтық коллизияға әкеледі. ҚР заңнамасы ЖИ-дің қатысуымен жасалған зиян үшін заңды тұлғалардың жауапкершілігін күшейтуді қарастыруы қажет.</p>
    `,
    glossary: ["Жауапкершілік", "Accountability", "Заңды тұлға", "Азаматтық жауапкершілік", "Қылмыстық жауапкершілік", "Дәлелдеу"],
    tasks: {
        l1: [
            "ЖИ-дің жауапкершілігі дегеніміз не?", 
            "Жауапкершіліктің 2 түрін атаңыз (мысалы, Азаматтық)."
        ],
        l2: [
            "Жоғары автономды ЖИ-дің қатесі үшін жауапкершілікті дәлелдеу неліктен қиын? (2 себеп).", 
            "ҚР заңнамасы ЖИ-дің қатысуымен жасалған зиян үшін заңды тұлғалардың жауапкершілігін қалай күшейте алады? (2 ұсыныс)."
        ],
        l3: [
            "ЖИ-дің әрекеті үшін тек **қатаң жауапкершілік** (кінәсіз де жауапты болу) принципін енгізуді 3 аргументпен негіздеңіз. Бұл қандай салаларда қолданылуы керек?"
        ]
    },
    questions: [
        { q: "Жауапкершілік көбіне кімге жүктеледі?", opts: ["Тек ЖИ-дің өзіне", "Иесіне немесе операторына (заңды тұлғаға)", "Мемлекетке"], a: 1 },
        { q: "Қылмыстық жауапкершілік қандай жазаны қамтиды?", opts: ["Зиянды өтеуді", "Айыппұлды", "Бас бостандығынан айыруды"], a: 2 },
        { q: "Автономды ЖИ қатесі үшін жауапкершілікті дәлелдеу...", opts: ["Оңай", "Қиын", "Мүмкін емес"], a: 1 },
        { q: "Қатаң жауапкершілік нені білдіреді?", opts: ["Жауапты еместігін", "Кінәсіз де жауапты болуды", "Тек қылмыстық жауапкершілікті"], a: 1 },
        { q: "Жауапкершілік ағылшынша қалай аталады?", opts: ["Fairness", "Accountability", "Transparency"], a: 1 },
        { type: 'tf', q: "Азаматтық жауапкершілік бас бостандығынан айыруды білдіреді.", a: false },
        { type: 'tf', q: "Жауапкершіліктің бір түрі – әкімшілік.", a: true },
        { type: 'tf', q: "ҚР заңнамасы ЖИ зияны үшін тек жеке тұлғаның жауапкершілігін қарастырады.", a: false },
        { type: 'text', q: "Жауапкершіліктің зиянды өтеу түрі (бір сөз)?", a: "Азаматтық" },
        { type: 'text', q: "Жауапкершіліктің айыппұл түрі (бір сөз)?", a: "Әкімшілік" }
    ]
};

// --- САБАҚ 7 ---
LESSON_DATA[7] = {
    lecture: `
        <p><strong>ЖИ-дің ашықтығы</strong> (Transparency) – бұл ЖИ жүйесінің қалай жұмыс істейтінін, қалай шешім қабылдайтынын және қандай деректерді қолданатынын түсіндіру мүмкіндігі. Бұл этикалық және құқықтық қағида, ол ЖИ-дің әділдігі мен жауапкершілігін қамтамасыз ету үшін маңызды.</p>
        <p>Ашықтықтың болмауы ЖИ-дің **«қара жәшік»** (Black Box) мәселесіне әкеледі, бұл ЖИ-дің кемсітушілікке жол бергенін немесе қате шешім қабылдағанын дәлелдеуді мүмкін етпейді. Құқықтық реттеулер (мысалы, ЕО-дағы GDPR) ЖИ-дің шешіміне қарсы тұру құқығын және оны түсіндіруді талап етеді. ҚР-да да осы бағыттағы талаптарды енгізу қажет.</p>
    `,
    glossary: ["ЖИ-дің ашықтығы", "Transparency", "Қара жәшік (Black Box)", "Түсіндіру мүмкіндігі (Explainability)", "Шешім қабылдау"],
    tasks: {
        l1: [
            "ЖИ-дің ашықтығы дегеніміз не?", 
            "Ашықтықтың болмауы қандай мәселеге әкеледі? (Ағылшынша атауын жазыңыз)."
        ],
        l2: [
            "Неліктен ашықтық ЖИ-дің әділдігі мен жауапкершілігі үшін маңызды? (2 себеп).", 
            "Құқықтық реттеулер (мысалы, GDPR) ЖИ-дің шешіміне қатысты қандай 2 құқықты талап етеді?"
        ],
        l3: [
            "«Қара жәшік» мәселесін шешу үшін ЖИ-дің жұмыс істеу принципін түсіндіруге қатысты ҚР заңнамасына енгізуге болатын 1 арнайы талапты ұсыныңыз. Бұл талаптың құқықтық негізін түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Ашықтық нені түсіндіру мүмкіндігі?", opts: ["ЖИ-дің бағасын", "ЖИ-дің қалай жұмыс істейтінін", "ЖИ-дің дизайнын"], a: 1 },
        { q: "«Қара жәшік» мәселесі неге әкеледі?", opts: ["ЖИ-дің жұмысын түсінуге", "ЖИ-дің қате шешімін дәлелдеудің мүмкін еместігіне", "ЖИ-дің дамуына"], a: 1 },
        { q: "Ашықтық ағылшынша қалай аталады?", opts: ["Fairness", "Transparency", "Accountability"], a: 1 },
        { q: "ЕО-дағы GDPR қандай құқықты талап етеді?", opts: ["Тек деректерді жоюды", "ЖИ-дің шешіміне қарсы тұру құқығын", "Тек ЖИ-ді қолдануды"], a: 1 },
        { q: "Ашықтық қай қағидаларды қамтамасыз ету үшін маңызды?", opts: ["Жылдамдықты", "Әділдік пен жауапкершілікті", "Арзандықты"], a: 1 },
        { type: 'tf', q: "Ашықтық ЖИ-дің қалай жұмыс істейтінін жасыруды білдіреді.", a: false },
        { type: 'tf', q: "Қара жәшік мәселесі ЖИ-дің жауапкершілігін арттырады.", a: false },
        { type: 'tf', q: "Құқықтық реттеулер ЖИ шешімдерін түсіндіруді талап етеді.", a: true },
        { type: 'text', q: "ЖИ шешімінің түсінікті болуы (бір сөз)?", a: "Түсіндіру" },
        { type: 'text', q: "ЖИ-дің ішкі жұмысы белгісіз мәселе (екі сөз)?", a: "Қара жәшік" }
    ]
};

// --- САБАҚ 8 (I БӨЛІМНІҢ ҚОРЫТЫНДЫСЫ) ---
LESSON_DATA[8] = {
    lecture: `
        <p><strong>Бақылау жұмысы: ЖИ-дің құқықтық негіздері</strong>. Бұл сабақ ЖИ-дің құқықтық мәртебесі, жауапкершілігі, әділдігі және ашықтығы бойынша алған білімді жүйелеуге және бағалауға арналған. Бақылау жұмысы теориялық сұрақтар мен **шағын құқықтық кейстерді** талдауды қамтиды.</p>
        <p>Мақсат – оқушылардың ЖИ-ге қатысты негізгі құқықтық ұғымдарды (мысалы, 'Қатаң жауапкершілік', 'Құқықтық субъект') меңгеру деңгейін анықтау. Кейстерді шешу кезінде оқушылар ЖИ-дің әрекетіне қатысты ҚР заңнамасының тиісті баптарына сілтеме жасау қабілетін көрсетуі керек. Бұл I Бөлімнің қорытындысы.</p>
    `,
    glossary: ["Бақылау жұмысы", "Шағын құқықтық кейстер", "Құқықтық ұғымдар", "Жүйелеу", "Бағалау", "Қорытынды"],
    tasks: {
        l1: [
            "Бақылау жұмысы қандай 2 негізгі элементті қамтиды?", 
            "Бақылау жұмысының негізгі мақсаты не?"
        ],
        l2: [
            "ЖИ-дің қатысуымен болған 2 шағын құқықтық кейстің тақырыбын ұсыныңыз (Мысалы, ЖИ-дің қате кеңесінен туындаған шығын).", 
            "Кейстерді шешу кезінде оқушылар ҚР заңнамасына қатысты қандай дағдыны көрсетуі керек?"
        ],
        l3: [
            "Қорытынды бақылау үшін ЖИ-дің әділдігіне қатысты 1 күрделі сұрақты әзірлеңіз. Бұл сұрақтың бағалау критерийлерін (2 критерий) көрсетіңіз."
        ]
    },
    questions: [
        { q: "Бақылау жұмысы қандай білімді жүйелеуге арналған?", opts: ["Тек техникалық", "Құқықтық негіздер бойынша", "Тек этикалық"], a: 1 },
        { q: "Бақылау жұмысы не арқылы бағаланады?", opts: ["Тек код арқылы", "Теориялық сұрақтар мен кейстер арқылы", "Тек суреттер арқылы"], a: 1 },
        { q: "Құқықтық ұғымдарға не жатады?", opts: ["Қатаң жауапкершілік, Құқықтық субъект", "Тек бағдарлама атаулары", "Компьютер үлгілері"], a: 0 },
        { q: "Кейстерді шешу кезінде не маңызды?", opts: ["Әдемі жазу", "ҚР заңнамасының тиісті баптарына сілтеме жасау", "Жалпы сөздер"], a: 1 },
        { q: "Бақылау жұмысы қай бөлімнің қорытындысы?", opts: ["II Бөлімнің", "I Бөлімнің", "III Бөлімнің"], a: 1 },
        { type: 'tf', q: "Бақылау жұмысы тек жеңіл сұрақтардан тұрады.", a: false },
        { type: 'tf', q: "Құқықтық кейстерді талдау – бақылау жұмысының бір бөлігі.", a: true },
        { type: 'tf', q: "Бақылау жұмысы оқушының білімін бағалауға арналған.", a: true },
        { type: 'text', q: "Бақылау жұмысында талданатын оқиғалар (екі сөз)?", a: "Құқықтық кейстер" },
        { type: 'text', q: "Құқықтық ұғымдарды толық меңгеру (бір сөз)?", a: "Жүйелеу" }
    ]
};

// --- САБАҚ 9 (II БӨЛІМНІҢ БАСТАЛУЫ) ---
LESSON_DATA[9] = {
    lecture: `
        <p><strong>Авторлық құқықтың негіздері</strong> – бұл шығармашылық жұмыстарды (кітаптар, бағдарламалар, музыка, суреттер) жасаушыларға берілетін заңды құқықтар. Авторлық құқық жұмыстың көшірмесін жасауға, таратуға және көпшілікке көрсетуге қатысты құқықтарды қорғайды.</p>
        <p>Жасанды интеллекттің (ЖИ) шығармашылық жұмыстарды (мәтін, сурет, музыка) генерациялауы авторлық құқық саласында елеулі мәселелер туғызады. ҚР заңнамасы авторлық құқықты адамға немесе заңды тұлғаға ғана береді. ЖИ генерациялаған туындының авторы кім деген сұрақ, қазіргі құқықтық жүйе үшін **құқықтық коллизия** болып табылады.</p>
    `,
    glossary: ["Авторлық құқық", "Шығармашылық жұмыстар", "Генерациялау", "Құқықтық коллизия", "Автор"],
    tasks: {
        l1: [
            "Авторлық құқық дегеніміз не?", 
            "Авторлық құқықпен қорғалатын 2 шығармашылық жұмысты атаңыз."
        ],
        l2: [
            "ЖИ генерациялаған туындының авторы кім деген сұрақ неліктен құқықтық коллизия болып табылады? (2 себеп).", 
            "ҚР заңнамасы бойынша авторлық құқық кімге беріледі? (2 тұлғаны атаңыз)."
        ],
        l3: [
            "ЖИ генерациялаған туындыларға авторлық құқықты берудің 2 жаңа құқықтық моделін ұсыныңыз. Бұл модельдердің артықшылықтарын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Авторлық құқық кімге беріледі?", opts: ["Тек техникалық құралдарға", "Шығармашылық жұмыстарды жасаушыларға", "Кездейсоқ адамға"], a: 1 },
        { q: "ЖИ генерациялаған туындының авторы кім деген мәселе...", opts: ["Оңай шешіледі", "Құқықтық коллизия", "Маңызды емес"], a: 1 },
        { q: "ҚР заңнамасы авторлық құқықты кімге береді?", opts: ["Адамға немесе заңды тұлғаға", "Тек ЖИ-ге", "Тек мемлекетке"], a: 0 },
        { q: "Авторлық құқық нені қорғайды?", opts: ["Тек ақшаны", "Көшірмесін жасауға және таратуға қатысты құқықтарды", "Компьютердің жылдамдығын"], a: 1 },
        { q: "Генерациялау деген не?", opts: ["Көшіру", "Жасау, құру", "Жою"], a: 1 },
        { type: 'tf', q: "Авторлық құқық ЖИ генерациялаған жұмыстарға қатысты мәселе туғызбайды.", a: false },
        { type: 'tf', q: "Авторлық құқық тек кітаптарды қорғайды.", a: false },
        { type: 'tf', q: "Құқықтық коллизия – бұл заңдардағы қайшылық.", a: true },
        { type: 'text', q: "Шығармашылық жұмыстарды жасаушыға берілетін құқық (екі сөз)?", a: "Авторлық құқық" },
        { type: 'text', q: "ЖИ-дің контентті жасау процесі (бір сөз)?", a: "Генерациялау" }
    ]
};

// --- САБАҚ 10 ---
LESSON_DATA[10] = {
    lecture: `
        <p><strong>ЖИ-дің шығармашылық әлеуеті</strong> – бұл ЖИ-дің адамның қатысуынсыз немесе минималды қатысуымен бірегей және күрделі шығармашылық туындыларды (сурет, музыка, әдеби мәтін) жасау қабілеті. Бұл әлеует ЖИ-дің **машиналық оқыту** (Machine Learning) және **терең оқыту** (Deep Learning) технологияларына негізделген.</p>
        <p>Құқықтық тұрғыдан, егер шығармашылық нәтиже адамның шығармашылық үлесінсіз жасалса, ол **авторлық құқықпен қорғалмайды** деп саналады. Бұл ЖИ-дің дамуын ынталандыру және авторлық құқық нормаларын сақтау арасындағы тепе-теңдікті сақтауды талап етеді. Кейбір мемлекеттер ЖИ-ге шектеулі құқықтарды (мысалы, патенттерге) беру мүмкіндігін қарастыруда.</p>
    `,
    glossary: ["Шығармашылық әлеует", "Машиналық оқыту", "Терең оқыту", "Шығармашылық үлес", "Патенттер", "Тепе-теңдік"],
    tasks: {
        l1: [
            "ЖИ-дің шығармашылық әлеуеті дегеніміз не?", 
            "ЖИ-дің шығармашылық қабілеті қандай 2 технологияға негізделген?"
        ],
        l2: [
            "Неліктен адамның шығармашылық үлесінсіз жасалған туындылар авторлық құқықпен қорғалмайды деп саналады? (2 себеп).", 
            "ЖИ-дің дамуын ынталандыру және авторлық құқық нормаларын сақтау арасындағы тепе-теңдікті қалай сақтауға болады? (2 ұсыныс)."
        ],
        l3: [
            "ЖИ-дің шығармашылық нәтижелеріне патент беру мүмкіндігін құқықтық тұрғыдан талдаңыз. Патент және авторлық құқық арасындағы 2 негізгі айырмашылықты көрсетіңіз."
        ]
    },
    questions: [
        { q: "ЖИ-дің шығармашылық қабілеті неге негізделген?", opts: ["Тек жылдамдығына", "Машиналық және терең оқытуға", "Тек қуатына"], a: 1 },
        { q: "Адамның үлесінсіз жасалған туындылар авторлық құқықпен қорғала ма?", opts: ["Иә", "Жоқ", "Тек кейбір елдерде"], a: 1 },
        { q: "ЖИ-дің шығармашылық әлеуеті нені жасауға қабілетті?", opts: ["Тек қарапайым есептерді", "Бірегей және күрделі шығармашылық туындыларды", "Тек техникалық нұсқауларды"], a: 1 },
        { q: "Тепе-теңдікті немен сақтау керек?", opts: ["ЖИ-дің дамуын ынталандыру және авторлық құқық нормаларын сақтау арасында", "Тек қаржылық пайдамен", "Тек техникалық сипаттамамен"], a: 0 },
        { q: "Патенттер нені қорғайды?", opts: ["Жаңа өнертабыстарды", "Тек әдеби шығармаларды", "Музыканы"], a: 0 },
        { type: 'tf', q: "ЖИ-дің шығармашылық әлеуеті авторлық құқық мәселесін тудырмайды.", a: false },
        { type: 'tf', q: "Машиналық оқыту – ЖИ-дің шығармашылық технологиясы.", a: true },
        { type: 'tf', q: "Патент беру мүмкіндігі ЖИ үшін талқылануда.", a: true },
        { type: 'text', q: "ЖИ-дің күрделі шығармаларды жасау қабілеті (екі сөз)?", a: "Шығармашылық әлеует" },
        { type: 'text', q: "ЖИ-дің негізгі оқыту әдісі (екі сөз)?", a: "Машиналық оқыту" }
    ]
};

// --- САБАҚ 11 ---
LESSON_DATA[11] = {
    lecture: `
        <p><strong>Пайдалану құқығы және Лицензиялау</strong> – ЖИ жүйелерін (мысалы, чат-боттарды, сурет генераторларын) қолдануға және олардың нәтижелерін коммерциялық мақсатта пайдалануға мүмкіндік беретін құқықтық құжаттар. Қазақстандағы және халықаралық тәжірибедегі лицензиялық келісімдер ЖИ-дің қолдану шарттарын, жауапкершілігін және генерацияланған контенттің **авторлық құқық иесін** нақты анықтайды.</p>
        <p>Егер ЖИ генерациялаған туындылар пайдаланылса, бұл лицензиялық келісімдер **құқықтық қатынастардың** негізі болып табылады. Оқушылар ЖИ құралдарын пайдаланғанда, олардың лицензиялық шарттарын (ашық бастапқы кодты немесе коммерциялық) мұқият оқуы және сақтауы керек. Құқықтық міндеттемелерді бұзу – заңды салдарға әкеледі.</p>
    `,
    glossary: ["Пайдалану құқығы", "Лицензиялау", "Лицензиялық келісімдер", "Ашық бастапқы код", "Авторлық құқық иесі", "Құқықтық міндеттемелер"],
    tasks: {
        l1: [
            "Лицензиялау дегеніміз не?", 
            "Лицензиялық келісімдерде анықталатын 2 негізгі шартты атаңыз."
        ],
        l2: [
            "ЖИ құралдарын пайдаланғанда, оқушылар неліктен лицензиялық шарттарды мұқият оқуы керек? (2 себеп).", 
            "Ашық бастапқы кодты ЖИ құралы мен коммерциялық құралдың пайдалану құқығы арасындағы 2 айырмашылықты түсіндіріңіз."
        ],
        l3: [
            "ЖИ генерациялаған контентті коммерциялық мақсатта пайдалануға арналған шағын лицензиялық келісімнің 3 негізгі тармағын (мысалы, авторлық құқық иесі) ұсыныңыз. Бұл тармақтардың құқықтық маңыздылығын негіздеңіз."
        ]
    },
    questions: [
        { q: "Лицензиялық келісімдер нені анықтайды?", opts: ["Тек техникалық сипаттаманы", "Қолдану шарттарын, жауапкершілікті және авторлық құқық иесін", "Тек бағдарлама атауын"], a: 1 },
        { q: "Пайдалану құқығы нені білдіреді?", opts: ["ЖИ-дің нәтижелерін қолдануға мүмкіндік беретін құжаттарды", "Тек ақшаны пайдалануды", "ЖИ-ді сатып алуды"], a: 0 },
        { q: "Құқықтық міндеттемелерді бұзу неге әкеледі?", opts: ["Тек техникалық қатеге", "Заңды салдарға", "Көңіл-күйдің көтерілуіне"], a: 1 },
        { q: "Лицензиялық шарттар не үшін маңызды?", opts: ["Құқықтық қатынастардың негізі үшін", "Тек ЖИ-дің жұмысы үшін", "Тек жылдамдық үшін"], a: 0 },
        { q: "Ашық бастапқы кодты ЖИ құралы нені білдіреді?", opts: ["Коды жасырылған", "Коды ашық, тегін қолдануға болады", "Тек коммерциялық"], a: 1 },
        { type: 'tf', q: "Лицензиялық келісімдер авторлық құқық иесін нақты анықтамайды.", a: false },
        { type: 'tf', q: "Құқықтық міндеттемелерді бұзудың заңды салдары болады.", a: true },
        { type: 'tf', q: "Лицензиялау ЖИ-дің қолдану шарттарын реттейді.", a: true },
        { type: 'text', q: "ЖИ құралдарын қолдануға рұқсат беретін құжат (бір сөз)?", a: "Лицензиялау" },
        { type: 'text', q: "Келісімдерді сақтамаудың нәтижесі (екі сөз)?", a: "Заңды салдар" }
    ]
};

// --- САБАҚ 12 ---
LESSON_DATA[12] = {
    lecture: `
        <p><strong>ЖИ және Деректерді Қорғау</strong> – ЖИ жүйелерінің жеке деректерді (ПД) жинау, өңдеу және сақтау процесіндегі құқықтық талаптарды сақтауы. Қазақстан Республикасындағы «Жеке деректер және оларды қорғау туралы» Заң ЖИ-дің ПД-мен жұмысын реттейтін негізгі құжат болып табылады.</p>
        <p>Негізгі құқықтық принциптер: <strong>ақпараттандырылған келісім</strong> (ПД субъектісінің келісімі), <strong>мақсаттың шектеулігі</strong> (ПД-ны тек көрсетілген мақсатта қолдану) және <strong>құпиялылық</strong>. Егер ЖИ жүйесі ПД-ны заңсыз қолданса, бұл әкімшілік және азаматтық жауапкершілікке әкеледі. ЖИ-ді үйрету үшін қолданылатын деректер жиынтығы заңды болуы керек.</p>
    `,
    glossary: ["Деректерді Қорғау", "Жеке деректер (ПД)", "Ақпараттандырылған келісім", "Мақсаттың шектеулігі", "Құпиялылық"],
    tasks: {
        l1: [
            "ЖИ және Деректерді Қорғау дегеніміз не?", 
            "ҚР-да ПД-ны қорғауды реттейтін негізгі заңды атаңыз."
        ],
        l2: [
            "ЖИ жүйесі ПД-ны өңдегенде сақтауы керек 2 құқықтық принципті атаңыз.", 
            "Егер ЖИ жүйесі ПД-ны заңсыз қолданса, бұл қандай жауапкершіліктерге әкеледі?"
        ],
        l3: [
            "ЖИ-ді үйрету үшін деректер жиынтығын жинау кезінде 'Ақпараттандырылған келісім' қағидасын қалай тиімді жүзеге асыруға болады? (3 ұсыныс)."
        ]
    },
    questions: [
        { q: "ПД-ны қорғауды реттейтін ҚР заңы нені реттейді?", opts: ["Тек техникалық жабдықты", "ПД-ны жинау, өңдеу және сақтау процесін", "Тек ЖИ-дің бағасын"], a: 1 },
        { q: "Құпиялылық қағидасы нені білдіреді?", opts: ["ПД-ны көпшілікке таратуды", "ПД-ны қорғауды және жарияламауды", "Тек ақпарат беруді"], a: 1 },
        { q: "Мақсаттың шектеулігі деген не?", opts: ["ПД-ны кез келген мақсатта қолдану", "ПД-ны тек көрсетілген мақсатта қолдану", "ПД-ны жою"], a: 1 },
        { q: "ЖИ жүйесі ПД-ны заңсыз қолданса, бұл неге әкеледі?", opts: ["Тек техникалық жетілдіруге", "Әкімшілік және азаматтық жауапкершілікке", "Тек мақтауға"], a: 1 },
        { q: "Деректер жиынтығы қандай болуы керек?", opts: ["Қымбат", "Заңды", "Үлкен"], a: 1 },
        { type: 'tf', q: "ПД субъектісінің келісімін алу міндетті емес.", a: false },
        { type: 'tf', q: "Құпиялылық ЖИ және деректерді қорғаудың негізгі принциптерінің бірі.", a: true },
        { type: 'tf', q: "ПД-ны заңсыз қолданудың құқықтық салдары болмайды.", a: false },
        { type: 'text', q: "ПД-ны тек көрсетілген мақсатта қолдану (екі сөз)?", a: "Мақсаттың шектеулігі" },
        { type: 'text', q: "Азаматтың жеке ақпараты (екі сөз)?", a: "Жеке деректер" }
    ]
};

// --- САБАҚ 13 ---
LESSON_DATA[13] = {
    lecture: `
        <p><strong>GDPR және оның ЖИ-ге әсері</strong> – Еуропалық Одақтың Жеке деректерді қорғаудың жалпы регламенті (GDPR) ЖИ-ді реттеуге ең үлкен халықаралық әсер еткен құжат. GDPR-дің негізгі талаптары: ЖИ-дің автоматтандырылған шешімдеріне қарсы тұру құқығы, ПД-ны алып тастау құқығы және деректерді тасымалдау мүмкіндігі.</p>
        <p>ҚР заңнамасы GDPR-ге тікелей бағынбаса да, ЖИ-ді қолданатын қазақстандық компаниялар, егер олар ЕО азаматтарының деректерін өңдесе, GDPR талаптарын сақтауға міндетті. Бұл **халықаралық құқықтық нормалардың** ЖИ-дің дамуына және құқықтық реттелуіне әсер ететінін көрсетеді. ЖИ-дің 'қара жәшік' мәселесі GDPR талаптарына қайшы келеді.</p>
    `,
    glossary: ["GDPR", "Жалпы регламент", "Автоматтандырылған шешімдер", "ПД-ны алып тастау құқығы", "Тасымалдау мүмкіндігі", "Халықаралық құқықтық нормалар"],
    tasks: {
        l1: [
            "GDPR дегеніміз не? (Толық атауын жазыңыз).", 
            "GDPR-дің ЖИ-дің автоматтандырылған шешімдеріне қатысты қандай 1 негізгі құқықтық талабы бар?"
        ],
        l2: [
            "Неліктен ҚР компаниялары GDPR талаптарын сақтауға міндетті болуы мүмкін? (2 жағдайды атаңыз).", 
            "ЖИ-дің 'қара жәшік' мәселесі GDPR талаптарының қайсысына қайшы келеді? (Түсіндіріңіз)."
        ],
        l3: [
            "GDPR-дің ЖИ-ге қатысты 'ПД-ны алып тастау құқығы' талабын ҚР-дағы ПД туралы заңға енгізудің 2 артықшылығын құқықтық тұрғыдан дәлелдеңіз."
        ]
    },
    questions: [
        { q: "GDPR қандай ұйымның құжаты?", opts: ["ҚР", "Еуропалық Одақ", "АҚШ"], a: 1 },
        { q: "GDPR ЖИ-дің несіне қарсы тұру құқығын береді?", opts: ["Тек бағдарламалау тіліне", "Автоматтандырылған шешімдеріне", "Тек жылдамдығына"], a: 1 },
        { q: "ҚР компаниялары GDPR-ді қашан сақтауға міндетті?", opts: ["Әрқашан", "ЕО азаматтарының деректерін өңдесе", "Ешқашан"], a: 1 },
        { q: "Халықаралық құқықтық нормалар ЖИ-ге әсер ете ме?", opts: ["Жоқ", "Иә", "Сирек"], a: 1 },
        { q: "GDPR-дегі басты құқықтардың бірі:", opts: ["Тегін қолдану құқығы", "ПД-ны алып тастау құқығы", "ПД-ны жариялау құқығы"], a: 1 },
        { type: 'tf', q: "ҚР заңнамасы GDPR-ге тікелей бағынады.", a: false },
        { type: 'tf', q: "GDPR ЖИ-дің 'қара жәшік' мәселесін қолдайды.", a: false },
        { type: 'tf', q: "GDPR ЖИ-ді реттеуге үлкен әсер етті.", a: true },
        { type: 'text', q: "ЕО-ның деректерді қорғау құжаты (қысқартылған)?", a: "GDPR" },
        { type: 'text', q: "Адамның қатысуынсыз қабылданған шешімдер (екі сөз)?", a: "Автоматтандырылған шешімдер" }
    ]
};

// --- САБАҚ 14 ---
LESSON_DATA[14] = {
    lecture: `
        <p><strong>Құқықтық этика негіздері</strong> – бұл заңдылықпен қатар, ЖИ-дің әділ, адамгершілікті және қоғамға пайдалы болуын қамтамасыз ететін моральдық және этикалық нормалар жиынтығы. Құқықтық этика ЖИ-дің әлеуметтік салдарына (жұмыссыздық, теңсіздік) және оның адам өміріне әсеріне баса назар аударады.</p>
        <p>Этикалық қағидаларға <strong>зиян келтірмеу</strong> (Non-maleficence), <strong>пайдалы болу</strong> (Beneficence) және <strong>адамның автономиясын құрметтеу</strong> жатады. ҚР-да ЖИ-дің әлеуметтік әсерін реттейтін арнайы этикалық кодекс немесе ережелер әлі жоқ, бірақ бұл бағыттағы талқылаулар өзекті. Құқық пен этика бір-бірін толықтырып, ЖИ-дің қауіпсіз қолданылу мәдениетін қалыптастырады.</p>
    `,
    glossary: ["Құқықтық этика", "Моральдық нормалар", "Зиян келтірмеу (Non-maleficence)", "Пайдалы болу (Beneficence)", "Адам автономиясы"],
    tasks: {
        l1: [
            "Құқықтық этика дегеніміз не?", 
            "Этикалық қағидаларға жататын 2 негізгі ұғымды атаңыз (ағылшынша атауын жазу міндетті емес)."
        ],
        l2: [
            "ЖИ-дің әлеуметтік салдарларына қатысты 2 мәселені атаңыз (мысалы, теңсіздік).", 
            "Құқық пен этика ЖИ-дің қауіпсіз қолданылу мәдениетін қалай қалыптастырады? (2 сөйлеммен түсіндіріңіз)."
        ],
        l3: [
            "ЖИ-дің адам автономиясын құрметтеу қағидасын бұзуы мүмкін 2 жағдайды (кейсті) сипаттаңыз (Мысалы, ЖИ-дің адамның әрекетін манипуляциялауы). Оның этикалық маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Құқықтық этика нені қамтамасыз етеді?", opts: ["Тек заңдылықты", "ЖИ-дің әділ, адамгершілікті және пайдалы болуын", "Тек жылдамдықты"], a: 1 },
        { q: "Этикалық қағидаларға не жатады?", opts: ["Тек ақша табу", "Зиян келтірмеу, пайдалы болу", "Тек техникалық ережелер"], a: 1 },
        { q: "Құқық пен этика бір-бірін не істейді?", opts: ["Жояды", "Толықтырады", "Елемейді"], a: 1 },
        { q: "ҚР-да ЖИ-дің әлеуметтік әсерін реттейтін арнайы этикалық кодекс бар ма?", opts: ["Иә", "Әлі жоқ", "Тек техникалық кодекс бар"], a: 1 },
        { q: "Адам автономиясы нені білдіреді?", opts: ["Адамның таңдау және шешім қабылдау еркіндігін", "Тек физикалық күшті", "Тек қаржылық тәуелсіздікті"], a: 0 },
        { type: 'tf', q: "Этика ЖИ-дің тек техникалық аспектілеріне назар аударады.", a: false },
        { type: 'tf', q: "Құқықтық этика ЖИ-дің әлеуметтік салдарына баса назар аударады.", a: true },
        { type: 'tf', q: "Зиян келтірмеу (Non-maleficence) – этикалық қағида.", a: true },
        { type: 'text', q: "Қоғамға пайдалы болу қағидасы (бір сөз)?", a: "Пайдалы" },
        { type: 'text', q: "Заңдылықтан бөлек моральдық нормалар (екі сөз)?", a: "Құқықтық этика" }
    ]
};

// --- САБАҚ 15 ---
LESSON_DATA[15] = {
    lecture: `
        <p><strong>ЖИ-дің әлеуметтік жауапкершілігі</strong> – бұл ЖИ-дің дамушылары мен иелерінің өз өнімдерінің қоғамға әкелетін оң және теріс әсерлері үшін ерікті түрде жауапты болуы. Әлеуметтік жауапкершілік тек заңды талаптарды орындаумен шектелмейді, сонымен қатар этикалық міндеттемелерді қамтиды.</p>
        <p>Негізгі міндеттерге: ЖИ-дің тұрақты дамуын қамтамасыз ету, әділетсіздікті болдырмау, ЖИ-дің артықшылықтарын қоғамның барлық мүшелері үшін қолжетімді ету. ҚР компаниялары ЖИ-ді енгізу кезінде әлеуметтік жауапкершілік стратегияларын (мысалы, жұмысшыларды қайта оқыту бағдарламалары) қабылдауы қажет. Бұл этикалық міндеттемелер болашақта құқықтық нормаларға айналуы мүмкін.</p>
    `,
    glossary: ["Әлеуметтік жауапкершілік", "Ерікті жауапкершілік", "Тұрақты даму", "Әділетсіздікті болдырмау", "Әлеуметтік жауапкершілік стратегиялары"],
    tasks: {
        l1: [
            "ЖИ-дің әлеуметтік жауапкершілігі дегеніміз не?", 
            "Әлеуметтік жауапкершілік қандай 2 негізгі міндеттерді қамтиды?"
        ],
        l2: [
            "ЖИ иелерінің әлеуметтік жауапкершілігін көрсететін 2 нақты әрекетті ұсыныңыз (мысалы, жұмысшыларды қайта оқыту).", 
            "Неліктен әлеуметтік жауапкершілік тек заңды талаптарды орындаумен шектелмейді? (2 себеп)."
        ],
        l3: [
            "ЖИ-дің артықшылықтарын қоғамның барлық мүшелері үшін қолжетімді ету стратегиясын 3 аргументпен негіздеңіз. Бұл қандай әлеуметтік теңсіздікті азайтады?"
        ]
    },
    questions: [
        { q: "Әлеуметтік жауапкершілік деген не?", opts: ["Тек заңды талаптарды орындау", "Өнімдерінің қоғамға әсері үшін ерікті түрде жауапты болу", "Тек этикалық кодексті жазу"], a: 1 },
        { q: "Әлеуметтік жауапкершілікке не кіреді?", opts: ["Тек пайда табу", "Этикалық міндеттемелер", "Тек техникалық қауіпсіздік"], a: 1 },
        { q: "Әлеуметтік жауапкершілік нені болдырмауды көздейді?", opts: ["Дамуды", "Әділетсіздікті", "Бағдарламалауды"], a: 1 },
        { q: "ҚР компаниялары қандай стратегияларды қабылдауы қажет?", opts: ["Тек жарнамалық", "Әлеуметтік жауапкершілік стратегияларын", "Тек қаржылық"], a: 1 },
        { q: "Этикалық міндеттемелер болашақта неге айналуы мүмкін?", opts: ["Тек әдетке", "Құқықтық нормаларға", "Тек пікірге"], a: 1 },
        { type: 'tf', q: "Әлеуметтік жауапкершілік тек заңды талаптарды орындаумен шектеледі.", a: false },
        { type: 'tf', q: "Әлеуметтік жауапкершілік ЖИ-дің тұрақты дамуын қамтамасыз етеді.", a: true },
        { type: 'tf', q: "Жұмысшыларды қайта оқыту – әлеуметтік жауапкершілік стратегиясы.", a: true },
        { type: 'text', q: "ЖИ иелерінің ерікті түрдегі жауаптылығы (екі сөз)?", a: "Әлеуметтік жауапкершілік" },
        { type: 'text', q: "Болашақтағы дамуды қамтамасыз ету (екі сөз)?", a: "Тұрақты даму" }
    ]
};

// --- САБАҚ 16 (II БӨЛІМНІҢ ҚОРЫТЫНДЫСЫ) ---
LESSON_DATA[16] = {
    lecture: `
        <p><strong>Бақылау жұмысы: ЖИ және Авторлық құқық/Этика</strong>. Бұл сабақ ЖИ-дің шығармашылық әлеуеті, авторлық құқық коллизиялары, деректерді қорғау (GDPR), сондай-ақ құқықтық және әлеуметтік этика негіздері бойынша білімді тексеруге арналған. Жұмыс **кешенді тест** және **этикалық дилеммаларды** талдауды қамтиды.</p>
        <p>Мақсат – оқушының ЖИ генерациялаған туындылардың құқықтық мәртебесін анықтау, деректерді қорғау талаптарын түсіндіру және этикалық жағдайларда **дәлелді шешім** қабылдау қабілетін бағалау. Этикалық дилеммаларды шешу кезінде оқушылар ҚР заңнамасына және әмбебап этикалық қағидаларға сүйенуі керек. Бұл II Бөлімнің қорытындысы.</p>
    `,
    glossary: ["Кешенді тест", "Этикалық дилеммалар", "Дәлелді шешім", "Құқықтық мәртебе", "Авторлық құқық коллизиялары"],
    tasks: {
        l1: [
            "Бақылау жұмысы қандай 2 негізгі элементті қамтиды?", 
            "Бақылау жұмысының негізгі мақсаты не?"
        ],
        l2: [
            "ЖИ-ге қатысты 2 этикалық дилемманың тақырыбын ұсыныңыз (Мысалы, ЖИ шешімінің әділетсіздігі).", 
            "Этикалық дилеммаларды шешу кезінде оқушылар қандай 2 негізгі нормаға сүйенуі керек?"
        ],
        l3: [
            "Қорытынды бақылау үшін ЖИ-дің шығармашылық әлеуетіне қатысты 1 күрделі құқықтық сұрақты әзірлеңіз. Бұл сұрақтың бағалау критерийлерін (2 критерий) көрсетіңіз (Мысалы, 'Авторлық құқық иесін анықтау')."
        ]
    },
    questions: [
        { q: "Бақылау жұмысы не бойынша білімді тексеруге арналған?", opts: ["Тек техникалық білімді", "Авторлық құқық, этика, деректерді қорғау", "Тек қаржыны"], a: 1 },
        { q: "Этикалық дилеммаларды талдау нені қамтиды?", opts: ["Тек техникалық кодты", "Этикалық жағдайларды шешуді", "Тек сурет салуды"], a: 1 },
        { q: "Бақылау жұмысының бір форматы:", opts: ["Тек ән айту", "Кешенді тест", "Көлік жүргізу"], a: 1 },
        { q: "Дәлелді шешім қабылдау қабілеті немен бағаланады?", opts: ["Тек жылдамдықпен", "Этикалық дилеммаларды талдаумен", "Тек жаттап алумен"], a: 1 },
        { q: "Авторлық құқық коллизиялары нені білдіреді?", opts: ["Авторлық құқық мәселелеріндегі қайшылықтарды", "Тек техникалық қателерді", "Авторлық құқықтың жоқтығын"], a: 0 },
        { type: 'tf', q: "Бақылау жұмысы тек жеңіл тест сұрақтарынан тұрады.", a: false },
        { type: 'tf', q: "Этикалық дилеммаларды шешуде ҚР заңнамасына сүйену керек.", a: true },
        { type: 'tf', q: "Деректерді қорғау (GDPR) осы бөлімнің тақырыбына кіреді.", a: true },
        { type: 'text', q: "Құқықтық және этикалық мәселелердегі қайшылықтар (екі сөз)?", a: "Авторлық құқық коллизиялары" },
        { type: 'text', q: "Жағдайды талдап, негізделген шешім қабылдау (екі сөз)?", a: "Дәлелді шешім" }
    ]
};

// --- САБАҚ 17 (III БӨЛІМНІҢ БАСТАЛУЫ) ---
LESSON_DATA[17] = {
    lecture: `
        <p><strong>Deepfake технологиясының қауіптері</strong> – бұл жасанды интеллект (ЖИ) арқылы өте шынайы, бірақ жалған аудио және видео контентті (адамның сөзі, іс-әрекеті) жасау мүмкіндігі. Deepfake қоғамдық және жеке тұлғаларға, сондай-ақ саяси процестерге үлкен қауіп төндіреді.</p>
        <p>Құқықтық тәуекелдер: **жала жабу**, **алаяқтық**, **авторлық құқықты бұзу** және **жеке өмірге қол сұғу**. ҚР заңнамасында Deepfake-ті тікелей реттейтін арнайы баптар жоқ, бірақ бұл әрекеттер ҚР Қылмыстық кодексінің тиісті баптары (мысалы, ар-намыс пен қадір-қасиетті қорғау, алаяқтық) бойынша жауапкершілікке әкелуі мүмкін. Халықаралық тәжірибеде Deepfake-ке қарсы арнайы заңдар қабылдануда.</p>
    `,
    glossary: ["Deepfake", "Жалған контент", "Құқықтық тәуекелдер", "Жала жабу", "Алаяқтық", "Жеке өмірге қол сұғу"],
    tasks: {
        l1: [
            "Deepfake технологиясына анықтама беріңіз.", 
            "Deepfake-тің қоғамдық процестерге төндіретін 2 қаупін атаңыз."
        ],
        l2: [
            "Deepfake арқылы жасалуы мүмкін 3 құқықтық тәуекелді атаңыз.", 
            "ҚР Қылмыстық кодексінің Deepfake-ке қатысты қолданылуы мүмкін 2 бабын (тақырыптық атауын) ұсыныңыз."
        ],
        l3: [
            "Deepfake-тің зиянды қолданылуы үшін **қатаң жауапкершілік** принципін енгізуді 3 аргументпен негіздеңіз. Бұл қағиданы қолданудың құқықтық қиындықтарын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Deepfake деген не?", opts: ["Тек техникалық қате", "Жалған аудио және видео контент", "Жаңа компьютер үлгісі"], a: 1 },
        { q: "Deepfake қандай тәуекелдерді туғызады?", opts: ["Тек ақпараттық", "Жала жабу, алаяқтық, авторлық құқықты бұзу", "Тек қаржылық"], a: 1 },
        { q: "ҚР заңнамасында Deepfake-ті тікелей реттейтін арнайы баптар бар ма?", opts: ["Иә", "Жоқ", "Тек ескі заңдар бар"], a: 1 },
        { q: "Deepfake-ке қарсы арнайы заңдар қайда қабылдануда?", opts: ["Тек ҚР-да", "Халықаралық тәжірибеде", "Еш жерде"], a: 1 },
        { q: "Қылмыстық кодекстің Deepfake-ке қатысты қолданылуы мүмкін бабы:", opts: ["Ар-намыс пен қадір-қасиетті қорғау", "Тек техникалық талаптар", "Жол ережесі"], a: 0 },
        { type: 'tf', q: "Deepfake тек жеке тұлғаларға ғана қауіп төндіреді.", a: false },
        { type: 'tf', q: "Deepfake технологиясы өте шынайы жалған контент жасай алады.", a: true },
        { type: 'tf', q: "Deepfake жеке өмірге қол сұғуға әкелмейді.", a: false },
        { type: 'text', q: "ЖИ арқылы жасалған өте шынайы жалған контент (бір сөз)?", a: "Deepfake" },
        { type: 'text', q: "Deepfake арқылы жасалуы мүмкін заң бұзушылық (бір сөз)?", a: "Алаяқтық" }
    ]
};

// --- САБАҚ 18 ---
LESSON_DATA[18] = {
    lecture: `
        <p><strong>ЖИ және Алаяқтық</strong> – ЖИ құралдарын (мысалы, Deepfake, автоматтандырылған фишинг) қаржылық немесе басқа да пайда табу мақсатында заңсыз пайдалану. ЖИ қатысқан алаяқтық сценарийлері жылдам, кең ауқымды және анықтау қиын болады.</p>
        <p>Құқықтық реттеу: ҚР Қылмыстық кодексінің **«Алаяқтық»** бабы (190-бап). ЖИ-ді пайдалану алаяқтық әрекеттің техникалық құралы ретінде қарастырылады, бірақ жауапкершілік әрекетті жасаған адамға немесе қылмыстық топқа жүктеледі. Құқық қорғау органдарының ЖИ қатысқан қылмыстарды **цифрлық дәлелдер** арқылы тергеу қабілетін арттыру маңызды.</p>
    `,
    glossary: ["Алаяқтық", "Фишинг", "Заңсыз пайдалану", "Қылмыстық топ", "Цифрлық дәлелдер", "190-бап"],
    tasks: {
        l1: [
            "ЖИ қатысқан алаяқтық дегеніміз не?", 
            "Алаяқтық әрекеті үшін ҚР Қылмыстық кодексінің қандай бабы (тақырыптық атауын) қолданылады?"
        ],
        l2: [
            "ЖИ арқылы жасалуы мүмкін 2 нақты алаяқтық сценарийін сипаттаңыз (мысалы, Deepfake арқылы директордың дауысын қолдану).", 
            "ЖИ пайдаланылған алаяқтық үшін жауапкершілік кімге жүктеледі? (2 тұлғаны атаңыз)."
        ],
        l3: [
            "Құқық қорғау органдарының ЖИ қатысқан қылмыстарды тергеу қабілетін арттыру үшін 2 ұсыныс беріңіз. Осы ұсыныстардың құқықтық маңыздылығын түсіндіріңіз (мысалы, арнайы цифрлық криминалистикалық бөлім құру)."
        ]
    },
    questions: [
        { q: "ЖИ қатысқан алаяқтық қалай сипатталады?", opts: ["Баяу және оңай анықталатын", "Жылдам, кең ауқымды және анықтау қиын", "Тек қарапайым"], a: 1 },
        { q: "Алаяқтық үшін ҚР ҚК-нің қай бабы қолданылады?", opts: ["150-бап", "190-бап (Алаяқтық)", "250-бап"], a: 1 },
        { q: "ЖИ-ді пайдалану қалай қарастырылады?", opts: ["Тек жарнама", "Алаяқтық әрекеттің техникалық құралы ретінде", "Тек көмекші құрал"], a: 1 },
        { q: "Тергеу қабілетін арттыру не арқылы маңызды?", opts: ["Тек қағаз құжаттар", "Цифрлық дәлелдер арқылы", "Тек теориялық білім"], a: 1 },
        { q: "Фишинг деген не?", opts: ["Жаңа бағдарлама", "Жалған сайттар арқылы құпия деректерді ұрлау", "ЖИ-дің түрі"], a: 1 },
        { type: 'tf', q: "ЖИ қатысқан алаяқтық сценарийлері баяу болады.", a: false },
        { type: 'tf', q: "Алаяқтық үшін жауапкершілік әрекетті жасаған адамға жүктеледі.", a: true },
        { type: 'tf', q: "Құқық қорғау органдарының цифрлық дәлелдерді тергеу қабілетін арттыру маңызды.", a: true },
        { type: 'text', q: "Жалған сайттар арқылы құпия деректерді ұрлау (бір сөз)?", a: "Фишинг" },
        { type: 'text', q: "Алаяқтық үшін ҚР ҚК бабының нөмірі (бір сан)?", a: "190" }
    ]
};

// --- САБАҚ 19 ---
LESSON_DATA[19] = {
    lecture: `
        <p><strong>Алгоритмдік Әділетсіздік</strong> – бұл ЖИ алгоритмдерінің белгілі бір топтарды (нәсіліне, жынысына, әлеуметтік жағдайына байланысты) кемсітетін немесе әділетсіз шешімдер қабылдауы. Бұл әділетсіздік көбінесе ЖИ-ді үйрету үшін қолданылатын **бұрмаланған (көрсетілген) деректер** жиынтығынан туындайды.</p>
        <p>Құқықтық мәселе: Мұндай әрекеттер ҚР Конституциясымен және кемсітушілікке қарсы заңдармен тыйым салынған. Құқықтық реттеу ЖИ-дің шешім қабылдау процесіндегі **ашықтықты** (Transparency) және **әділдікті** (Fairness) қамтамасыз етуді талап етеді. Алгоритмдік әділетсіздікке ұшыраған адамдардың **құқықтық қорғалу** және **сотқа шағымдану** мүмкіндігі болуы керек.</p>
    `,
    glossary: ["Алгоритмдік Әділетсіздік", "Кемсіту", "Бұрмаланған деректер", "Ашықтық (Transparency)", "Әділдік (Fairness)"],
    tasks: {
        l1: [
            "Алгоритмдік әділетсіздік дегеніміз не?", 
            "Әділетсіздік неден туындайды?"
        ],
        l2: [
            "Алгоритмдік әділетсіздікке ұшыраған адамдардың 2 құқықтық мүмкіндігін атаңыз.", 
            "Алгоритмдік әділетсіздіктің 2 нақты мысалын сипаттаңыз (мысалы, жұмысқа қабылдаудағы кемсіту)."
        ],
        l3: [
            "ЖИ-дің әділетті жұмыс істеуін қамтамасыз ету үшін ҚР-дағы ЖИ алгоритмдеріне міндетті **тәуелсіз аудит** жүргізу туралы 1 ұсыныс беріңіз. Бұл ұсыныстың Конституциялық құқықтарды қорғау тұрғысынан маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Алгоритмдік әділетсіздік неге әкеледі?", opts: ["Тек жаңалықтарға", "Белгілі бір топтарды кемсітетін шешімдерге", "Тек техникалық қателерге"], a: 1 },
        { q: "Бұрмаланған деректер неден туындайды?", opts: ["Тек алаяқтықтан", "Алгоритмдік әділетсіздіктен", "Тек заңды әрекеттерден"], a: 1 },
        { q: "ЖИ-дің шешім қабылдау процесінде не қамтамасыз етілуі керек?", opts: ["Ашықтық және Әділдік", "Тек жылдамдық", "Тек пайда"], a: 0 },
        { q: "Кемсітушілікке қарсы заңдар қай құжатқа сүйенеді?", opts: ["Тек ережелерге", "ҚР Конституциясына", "Тек ішкі нұсқауларға"], a: 1 },
        { q: "Әділетсіздікке ұшыраған адамның құқығы:", opts: ["Сотқа шағымдану", "Тек жарнама беру", "Тек үндемеу"], a: 0 },
        { type: 'tf', q: "Алгоритмдік әділетсіздік тек техникалық қатеден туындайды.", a: false },
        { type: 'tf', q: "Әділетсіздікке ұшыраған адамның құқықтық қорғалу мүмкіндігі болуы керек.", a: true },
        { type: 'tf', q: "Алгоритмдік әділетсіздік ҚР Конституциясына қайшы келеді.", a: true },
        { type: 'text', q: "ЖИ-дің кемсітушілік шешімдері (екі сөз)?", a: "Алгоритмдік әділетсіздік" },
        { type: 'text', q: "Алгоритмнің қалай жұмыс істейтінін түсіну (бір сөз)?", a: "Ашықтық" }
    ]
};

// --- САБАҚ 20 ---
LESSON_DATA[20] = {
    lecture: `
        <p><strong>ЖИ және Демократиялық процестерге қауіптер</strong> – ЖИ-дің сайлауларға, саяси пікірлерді манипуляциялауға және қоғамдық пікірді бұрмалауға әсер ету қаупі. Deepfake, бот-фермалар және жеке деректерді заңсыз талдау сияқты ЖИ құралдары демократиялық институттардың тұтастығына қатер төндіреді.</p>
        <p>Құқықтық реттеу: ҚР-дағы **сайлау туралы заңнама**, **экстремизмге қарсы заңдар** және **жала жабуға қатысты баптар** осы қауіптерді реттеуге қолданылуы мүмкін. Құқықтық жүйе ЖИ-дің саяси мақсатта қолданылуындағы **ашықтық пен жауапкершілікті** талап етуі керек. Әсіресе, сайлау алдындағы науқандарда ЖИ-дің рөлін ашық көрсетуді міндеттеу қажет.</p>
    `,
    glossary: ["Демократиялық процестер", "Манипуляциялау", "Бот-фермалар", "Экстремизм", "Сайлау туралы заңнама", "Саяси пікірлер"],
    tasks: {
        l1: [
            "ЖИ демократиялық процестерге қалай қауіп төндіреді? (2 мысал).", 
            "ЖИ-дің саяси мақсатта қолданылуында не талап етілуі керек? (2 қағида)."
        ],
        l2: [
            "Бот-фермалар қоғамдық пікірді қалай бұрмалай алады? (2 сөйлеммен сипаттаңыз).", 
            "ҚР-дағы демократиялық процестерге қауіптерді реттеуге қолданылуы мүмкін 2 құқықтық құжатты атаңыз."
        ],
        l3: [
            "Сайлау алдындағы науқандарда ЖИ-дің рөлін ашық көрсетуді міндеттейтін 1 заңды ұсыныс беріңіз. Бұл талаптың қоғамдық пікірдің тұтастығын қорғау тұрғысынан маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "ЖИ демократиялық процестерге қандай қауіп төндіреді?", opts: ["Тек техникалық қате", "Саяси пікірлерді манипуляциялау", "Тек жаңалықтарды тарату"], a: 1 },
        { q: "Демократияға қатер төндіретін ЖИ құралы:", opts: ["Тек калькулятор", "Deepfake, бот-фермалар", "Тек интернет"], a: 1 },
        { q: "ҚР-дағы осы қауіптерді реттеуге қолданылатын заңнама:", opts: ["Тек салық кодексі", "Сайлау туралы заңнама", "Тек еңбек кодексі"], a: 1 },
        { q: "Бот-фермалар деген не?", opts: ["Ауыл шаруашылығы", "Автоматтандырылған аккаунттар желісі", "Жаңа технология"], a: 1 },
        { q: "Сайлау алдындағы науқандарда нені көрсету міндетті болуы керек?", opts: ["Тек кандидаттың суретін", "ЖИ-дің рөлін ашық көрсетуді", "Тек қаржыны"], a: 1 },
        { type: 'tf', q: "ЖИ қоғамдық пікірді бұрмалай алмайды.", a: false },
        { type: 'tf', q: "ЖИ-дің саяси мақсатта қолданылуында ашықтық талап етілуі керек.", a: true },
        { type: 'tf', q: "ҚР-да экстремизмге қарсы заңдар осы қауіптерді реттеуге қолданылуы мүмкін.", a: true },
        { type: 'text', q: "Саяси пікірлерге әсер ету (бір сөз)?", a: "Манипуляциялау" },
        { type: 'text', q: "Сайлауға қатысты заңдар (екі сөз)?", a: "Сайлау заңнамасы" }
    ]
};

// --- САБАҚ 21 ---
LESSON_DATA[21] = {
    lecture: `
        <p><strong>Медициналық және Құқықтық Кейстер</strong> – ЖИ-дің қатысуымен медицина (диагностика, емдеу) және құқық (сот шешімдері, тергеу) салаларында туындаған нақты қателер мен құқықтық дауларды талдау. Медицинада ЖИ-дің қате диагностикасы науқастың денсаулығына зиян келтіруі мүмкін, бұл **қатаң жауапкершілік** мәселесін тудырады.</p>
        <p>Құқықтық салада ЖИ-дің қате шешімі (мысалы, пробацияны тағайындау) адам құқықтарын бұзуға әкелуі мүмкін. Талдау мақсаты – оқушыларға ЖИ-дің техникалық қатесінің **нақты құқықтық салдарларын** көрсету. ҚР заңнамасы ЖИ-дің медициналық және құқықтық саладағы қолданылуына қатысты қауіпсіздік және аудит талаптарын енгізуі қажет.</p>
    `,
    glossary: ["Медициналық кейстер", "Құқықтық кейстер", "Қате диагностика", "Пробация", "Нақты құқықтық салдарлар", "Қатаң жауапкершілік"],
    tasks: {
        l1: [
            "Медицинада ЖИ-дің қатесі неге әкелуі мүмкін? (1 мысал).", 
            "Құқықтық салада ЖИ-дің қате шешімі қандай мәселені тудырады?"
        ],
        l2: [
            "ЖИ қатысқан 2 медициналық кейстің (диагнозға қатысты) тақырыбын ұсыныңыз. Бұл кейстерде қандай жауапкершілік түрі туындайды?", 
            "Құқықтық салада ЖИ-дің қатесінен туындаған 2 нақты құқықтық салдарын атаңыз."
        ],
        l3: [
            "Медициналық салада ЖИ қолданылуына қатысты **қатаң жауапкершілік** принципін енгізуді 3 аргументпен негіздеңіз. Бұл қағиданың науқастардың құқығын қорғау тұрғысынан маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Медицинада ЖИ-дің қатесі неге әкеледі?", opts: ["Тек техникалық қатеге", "Науқастың денсаулығына зиян келтіруге", "Тек жарнамаға"], a: 1 },
        { q: "Құқықтық салада ЖИ-дің қате шешімі нені бұзады?", opts: ["Тек ережені", "Адам құқықтарын", "Тек бағдарламаны"], a: 1 },
        { q: "Қатаң жауапкершілік мәселесі қайда туындайды?", opts: ["Тек спортта", "ЖИ-дің қате диагностикасында", "Тек өнерде"], a: 1 },
        { q: "Талдау мақсаты – ЖИ-дің техникалық қатесінің нені көрсету?", opts: ["Тек техникалық сипаттамасын", "Нақты құқықтық салдарларын", "Тек бағасын"], a: 1 },
        { q: "Пробация деген не?", opts: ["Ауыр диагноз", "Сот шешімінің бір түрі", "Жаңа технология"], a: 1 },
        { type: 'tf', q: "ЖИ-дің техникалық қатесінің құқықтық салдары болмайды.", a: false },
        { type: 'tf', q: "Қатаң жауапкершілік мәселесі медицинада туындауы мүмкін.", a: true },
        { type: 'tf', q: "ҚР заңнамасы ЖИ-дің медициналық саладағы қолданылуына қатысты аудит талаптарын енгізуі қажет.", a: true },
        { type: 'text', q: "ЖИ-дің қате анықтауы (екі сөз)?", a: "Қате диагностика" },
        { type: 'text', q: "Зиян үшін кінәсіз де жауапты болу (екі сөз)?", a: "Қатаң жауапкершілік" }
    ]
};

// --- САБАҚ 22 ---
LESSON_DATA[22] = {
    lecture: `
        <p><strong>ЖИ қауіптерін болдырмау стратегиялары</strong> – бұл ЖИ-дің зиянды қолданылуынан (Deepfake, алаяқтық, кемсітушілік) қорғану үшін қолданылатын техникалық, этикалық және құқықтық шаралар кешені. Негізгі стратегиялар: **алгоритмдік аудит** (әділдікті тексеру), **ашықтықты күшейту** және **пайдаланушыларды оқыту**.</p>
        <p>Құқықтық реттеу тұрғысынан, ҚР-да ЖИ-дің қауіпсіздігі мен тестіленуіне қатысты міндетті стандарттарды енгізу қажет. Этикалық деңгейде, ЖИ-ді әзірлеушілер **этикалық кодекске** сәйкес жұмыс істеуі керек. Оқушылар өздерінің цифрлық құқықтық сауаттылығын арттыру арқылы ЖИ қауіптерінен қорғана алады.</p>
    `,
    glossary: ["Болдырмау стратегиялары", "Шаралар кешені", "Алгоритмдік аудит", "Ашықтықты күшейту", "Міндетті стандарттар", "Этикалық кодекс"],
    tasks: {
        l1: [
            "ЖИ қауіптерін болдырмау стратегиялары дегеніміз не?", 
            "Негізгі стратегиялардың 2 түрін атаңыз (мысалы, Алгоритмдік аудит)."
        ],
        l2: [
            "Алгоритмдік аудит нені тексеруге бағытталған? (2 мәселені атаңыз).", 
            "ЖИ-дің зиянды қолданылуынан қорғану үшін пайдаланушыларды оқытудың 2 әдісін ұсыныңыз."
        ],
        l3: [
            "ҚР-да ЖИ-дің қауіпсіздігі мен тестіленуіне қатысты міндетті стандарттарды енгізудің 3 құқықтық артықшылығын негіздеңіз. Бұл қандай салаларда (мысалы, медицина) ең маңызды?"
        ]
    },
    questions: [
        { q: "Болдырмау стратегиялары нені қамтиды?", opts: ["Тек техникалық шараларды", "Техникалық, этикалық және құқықтық шаралар кешенін", "Тек қаржылық шараларды"], a: 1 },
        { q: "Алгоритмдік аудит нені тексеруге бағытталған?", opts: ["ЖИ-дің жылдамдығын", "ЖИ-дің әділдігін", "Тек бағдарламаның атауын"], a: 1 },
        { q: "ЖИ-дің әзірлеушілері неге сәйкес жұмыс істеуі керек?", opts: ["Тек жеке пікірге", "Этикалық кодекске", "Тек техникалық нұсқауға"], a: 1 },
        { q: "Құқықтық реттеу тұрғысынан не енгізу қажет?", opts: ["Тек жаңа бағдарламаларды", "Міндетті стандарттарды", "Тек жарнаманы"], a: 1 },
        { q: "Оқушылар қауіптерден қалай қорғана алады?", opts: ["Тек бағдарламалау арқылы", "Цифрлық құқықтық сауаттылығын арттыру арқылы", "Тек үй жұмысын орындау арқылы"], a: 1 },
        { type: 'tf', q: "Болдырмау стратегиялары Deepfake-тен қорғануды қамтиды.", a: true },
        { type: 'tf', q: "Ашықтықты күшейту – негізгі стратегиялардың бірі емес.", a: false },
        { type: 'tf', q: "ҚР-да ЖИ-дің қауіпсіздігіне қатысты міндетті стандарттарды енгізу қажет.", a: true },
        { type: 'text', q: "Әділдікті тексеруге бағытталған процесс (екі сөз)?", a: "Алгоритмдік аудит" },
        { type: 'text', q: "Қауіптен қорғану әрекеттері (екі сөз)?", a: "Шаралар кешені" }
    ]
};

// --- САБАҚ 23 (IV БӨЛІМНІҢ БАСТАЛУЫ) ---
LESSON_DATA[23] = {
    lecture: `
        <p><strong>ЖИ-ді жауапты қолдану мәдениеті</strong> – бұл Жасанды Интеллект (ЖИ) құралдарын пайдалану кезінде этикалық, құқықтық және әлеуметтік міндеттемелерді саналы түрде орындауды білдіретін қағидалар мен дағдылар жиынтығы. Бұл мәдениет ЖИ қауіптерінен қорғану және оның әлеуетін қоғам игілігіне бағыттау үшін қажет.</p>
        <p>Негізгі элементтер: <strong>саналы тұтыну</strong> (ЖИ нәтижелерін критикалық талдау), <strong>құқықтық сауаттылық</strong> (заңды талаптарды білу) және **өзара құрмет** (басқа адамдардың құқықтарын борұзға жол бермеу). Оқушылар ЖИ құралдарын пайдаланғанда, олардың **ашықтығына**, **әділдігіне** және **авторлық құқыққа** қатысты нормаларды сақтауды үйренуі керек.</p>
    `,
    glossary: ["Жауапты қолдану мәдениеті", "Саналы тұтыну", "Құқықтық сауаттылық", "Өзара құрмет", "Этикалық міндеттемелер"],
    tasks: {
        l1: [
            "ЖИ-ді жауапты қолдану мәдениеті дегеніміз не?", 
            "Жауапты қолдану мәдениетінің 2 негізгі элементін атаңыз."
        ],
        l2: [
            "Саналы тұтыну деген не? Ол Deepfake қаупінен қалай қорғайды? (2 сөйлеммен түсіндіріңіз).", 
            "ЖИ құралдарын пайдаланғанда сақтауға міндетті 3 құқықтық норманы атаңыз (мысалы, Авторлық құқық)."
        ],
        l3: [
            "ЖИ-ді жауапты қолдану мәдениетін қалыптастыру үшін ҚР білім беру жүйесіне енгізуге болатын 2 басты ұсынысты тұжырымдаңыз. Бұл ұсыныстардың әлеуметтік маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "ЖИ-ді жауапты қолдану мәдениеті нені білдіреді?", opts: ["Тек техникалық білімді", "Этикалық, құқықтық және әлеуметтік міндеттемелерді саналы түрде орындауды", "Тек бағдарламалауды"], a: 1 },
        { q: "Саналы тұтыну деген не?", opts: ["Тек көп қолдану", "ЖИ нәтижелерін критикалық талдау", "Тек ақша төлеу"], a: 1 },
        { q: "Құқықтық сауаттылық дегеніміз не?", opts: ["Тек техникалық білімді", "Заңды талаптарды білу", "Тек философияны"], a: 1 },
        { q: "ЖИ-дің әлеуетін неге бағыттау керек?", opts: ["Тек жеке пайдаға", "Қоғам игілігіне", "Тек техникалық дамуға"], a: 1 },
        { q: "Өзара құрмет нені білдіреді?", opts: ["Тек ЖИ-ді мақтауды", "Басқа адамдардың құқықтарын бұзуға жол бермеуді", "Тек бағдарламаны жасауды"], a: 1 },
        { type: 'tf', q: "Жауапты қолдану мәдениетінің негізгі элементі – құқықтық сауаттылық.", a: true },
        { type: 'tf', q: "Саналы тұтыну ЖИ нәтижелерін критикалық талдауды қамтиды.", a: true },
        { type: 'tf', q: "ЖИ құралдарын пайдаланғанда авторлық құқықты сақтау маңызды емес.", a: false },
        { type: 'text', q: "ЖИ нәтижелерін мұқият тексеру (екі сөз)?", a: "Саналы тұтыну" },
        { type: 'text', q: "ЖИ-ді қолданудың этикалық және құқықтық дағдылары (үш сөз)?", a: "Жауапты қолдану мәдениеті" }
    ]
};

// --- САБАҚ 24 ---
LESSON_DATA[24] = {
    lecture: `
        <p><strong>Мәліметтерді верификациялау дағдысы</strong> – бұл Жасанды Интеллект (ЖИ) арқылы генерацияланған немесе өңделген ақпараттың (мәтін, сурет, Deepfake) шынайылығын, дәлдігін және дереккөздерін тексеру қабілеті. Бұл дағды ЖИ қауіптеріне (жалған ақпарат, Deepfake) қарсы тұрудың негізгі құралы болып табылады.</p>
        <p>Верификациялаудың 3 негізгі әдісі: <strong>Дереккөзді бағалау</strong> (авторитетін тексеру), <strong>Мазмұнды салыстыру</strong> (басқа көздермен салыстыру) және **Контексті талдау** (жасалу уақыты мен мақсатын анықтау). Оқушылар ЖИ нәтижелерін заңды және этикалық тұрғыдан пайдалану үшін ақпаратты тексеруді күнделікті әдетке айналдыруы керек. Жалған ақпаратты тарату – ҚР заңнамасы бойынша жауапкершілікке әкеледі.</p>
    `,
    glossary: ["Верификациялау дағдысы", "Шынайылық", "Дәлдік", "Дереккөзді бағалау", "Мазмұнды салыстыру", "Контексті талдау"],
    tasks: {
        l1: [
            "Мәліметтерді верификациялау дағдысы дегеніміз не?", 
            "Верификациялаудың 2 негізгі әдісін атаңыз."
        ],
        l2: [
            "Неліктен Deepfake қаупіне қарсы тұру үшін верификациялау дағдысы маңызды? (2 себеп).", 
            "Егер сіз ЖИ генерациялаған ақпараттың жалған екенін анықтасаңыз, оны таратудың құқықтық салдары қандай? (2 салдар)."
        ],
        l3: [
            "ЖИ арқылы генерацияланған ақпараттың жалған екенін анықтау үшін 3 қадамдық алгоритм әзірлеңіз. Бұл қадамдардың мақсатын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Верификациялау дағдысы нені тексеру қабілеті?", opts: ["Тек бағдарламалау тілін", "Ақпараттың шынайылығын, дәлдігін және дереккөздерін", "Тек оқытушының сөзін"], a: 1 },
        { q: "Верификациялаудың бір әдісі:", opts: ["Тек техникалық код жазу", "Дереккөзді бағалау", "Тек сурет салу"], a: 1 },
        { q: "Жалған ақпаратты тарату неге әкеледі?", opts: ["Тек мақтауға", "ҚР заңнамасы бойынша жауапкершілікке", "Тек техникалық жетілдіруге"], a: 1 },
        { q: "Верификациялаудың негізгі құралы:", opts: ["Тек ақша", "ЖИ қауіптеріне қарсы тұру", "Тек жаңалықтарды оқу"], a: 1 },
        { q: "Контексті талдау нені анықтайды?", opts: ["Тек деректердің көлемін", "Жасалу уақыты мен мақсатын", "Тек ЖИ-дің түрін"], a: 1 },
        { type: 'tf', q: "Верификациялау ЖИ арқылы генерацияланған ақпаратқа қатысты емес.", a: false },
        { type: 'tf', q: "Дереккөзді бағалау – верификациялау әдісі.", a: true },
        { type: 'tf', q: "Жалған ақпаратты таратудың құқықтық салдары болмайды.", a: false },
        { type: 'text', q: "Ақпараттың шынайылығын тексеру (бір сөз)?", a: "Верификациялау" },
        { type: 'text', q: "Верификациялаудың мақсаты (екі сөз)?", a: "Шынайылық, дәлдік" }
    ]
};

// --- САБАҚ 25 ---
LESSON_DATA[25] = {
    lecture: `
        <p><strong>ЖИ құралдарын әділ пайдалану</strong> – бұл ЖИ жүйелерін өз мүддесі үшін қолдану кезінде басқа тұлғалардың құқықтарын, авторлық құқықты және жеке деректерді қорғауға қатысты этикалық және заңды нормаларды сақтау. Әділ пайдалану кемсітушілікке жол бермеуді және ЖИ-дің **этикалық қағидаларын** ұстануды талап етеді.</p>
        <p>Әділ пайдаланудың 2 негізгі міндеті: <strong>Авторлық құқықты құрметтеу</strong> (ЖИ генерациялаған контентті заңсыз көшірмеу) және **Деректердің құпиялылығын сақтау** (басқа адамдардың жеке деректерін ЖИ арқылы рұқсатсыз талдамау). ҚР заңнамасы авторлық құқықты бұзу және жеке өмірге қол сұғу үшін **қылмыстық және азаматтық жауапкершілікті** қарастырады. Оқушылар ЖИ-ді пайдаланғанда, жауапкершілік әрқашан адамға жүктелетінін түсінуі керек.</p>
    `,
    glossary: ["Әділ пайдалану", "Этикалық қағидалар", "Авторлық құқықты құрметтеу", "Деректердің құпиялылығын сақтау", "Жауапкершілік"],
    tasks: {
        l1: [
            "ЖИ құралдарын әділ пайдалану дегеніміз не?", 
            "Әділ пайдаланудың 2 негізгі міндетін атаңыз."
        ],
        l2: [
            "Егер ЖИ генерациялаған контентті заңсыз көшірсе, қандай 2 құқықтық жауапкершілік туындауы мүмкін?", 
            "ЖИ арқылы рұқсатсыз талдауға болмайтын деректердің 2 түрін атаңыз."
        ],
        l3: [
            "ЖИ-ді пайдалану кезіндегі **әділдік қағидасын** қамтамасыз ету үшін оқушыларға арналған 3 этикалық ережені тұжырымдаңыз. Бұл ережелердің маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Әділ пайдалану нені сақтауды талап етеді?", opts: ["Тек техникалық жылдамдықты", "Басқа тұлғалардың құқықтарын, авторлық құқықты және жеке деректерді", "Тек бағдарламаның бағасын"], a: 1 },
        { q: "Авторлық құқықты құрметтеу нені білдіреді?", opts: ["Тек ЖИ-ді сатып алуды", "ЖИ генерациялаған контентті заңсыз көшірмеуді", "Тек ақпаратты жариялауды"], a: 1 },
        { q: "Жеке өмірге қол сұғу үшін қандай жауапкершілік қарастырылады?", opts: ["Тек техникалық", "Қылмыстық және азаматтық", "Тек әкімшілік"], a: 1 },
        { q: "Жауапкершілік әрқашан кімге жүктеледі?", opts: ["Тек ЖИ-дің өзіне", "Адамға", "Тек мемлекетке"], a: 1 },
        { q: "Әділ пайдалану нені болдырмауды көздейді?", opts: ["Тек пайда табуды", "Кемсітушілікке жол бермеуді", "Тек дамуды"], a: 1 },
        { type: 'tf', q: "Әділ пайдалану тек техникалық нормаларды қамтиды.", a: false },
        { type: 'tf', q: "Деректердің құпиялылығын сақтау – әділ пайдалану міндеті.", a: true },
        { type: 'tf', q: "Авторлық құқықты бұзу үшін құқықтық жауапкершілік қарастырылмаған.", a: false },
        { type: 'text', q: "ЖИ-ді қолданудағы этикалық және заңды нормаларды сақтау (екі сөз)?", a: "Әділ пайдалану" },
        { type: 'text', q: "Жауапкершілік түрі (екі сөз)?", a: "Азаматтық жауапкершілік" }
    ]
};

// --- САБАҚ 26 ---
LESSON_DATA[26] = {
    lecture: `
        <p><strong>Құқықтық тәуекелдерді басқару</strong> – бұл ЖИ-ді әзірлеу және қолдану кезінде туындауы мүмкін құқықтық және этикалық тәуекелдерді (кемсітушілік, зиян келтіру, авторлық құқықты бұзу) алдын ала анықтау, талдау және азайту процесі. Тәуекелдерді тиімді басқару ЖИ-дің заңды және қауіпсіз жұмыс істеуін қамтамасыз етеді.</p>
        <p>Басқарудың 3 негізгі кезеңі: <strong>Тәуекелді анықтау</strong> (заңды коллизияларды табу), **Талдау** (зиянның ауқымын бағалау) және **Бақылау** (азайту шараларын енгізу, мысалы, **Алгоритмдік Аудит**). Құқықтық тәуекелдерді басқару ҚР заңнамасына енгізілуі мүмкін болашақ ЖИ реттеулеріне компаниялардың дайындығын арттырады.</p>
    `,
    glossary: ["Тәуекелдерді басқару", "Құқықтық тәуекелдер", "Тәуекелді анықтау", "Талдау", "Бақылау", "Алгоритмдік Аудит"],
    tasks: {
        l1: [
            "Құқықтық тәуекелдерді басқару дегеніміз не?", 
            "Басқарудың 2 негізгі кезеңін атаңыз."
        ],
        l2: [
            "ЖИ қолдану кезінде туындауы мүмкін 3 құқықтық тәуекелді атаңыз (мысалы, зиян келтіру).", 
            "Тәуекелдерді бақылау кезеңінде қолданылатын 2 шараны атаңыз (мысалы, Алгоритмдік Аудит)."
        ],
        l3: [
            "ЖИ-дің қатысуымен болатын құқықтық тәуекелдерді басқарудың 1 стратегиясын (мысалы,  принципін міндеттеу) ұсыныңыз. Бұл стратегияның құқықтық коллизияларды азайтудағы рөлін түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Тәуекелдерді басқару нені азайтуға бағытталған?", opts: ["Тек пайданы", "Құқықтық және этикалық тәуекелдерді", "Тек техникалық жылдамдықты"], a: 1 },
        { q: "Тәуекелді анықтау кезеңі нені білдіреді?", opts: ["Тек қаржыны бағалауды", "Заңды коллизияларды табуды", "Тек жаңалықтарды оқуды"], a: 1 },
        { q: "Бақылау кезеңінде не енгізіледі?", opts: ["Тек жаңа бағдарламалар", "Азайту шаралары (мысалы, Алгоритмдік Аудит)", "Тек ережелерді жазу"], a: 1 },
        { q: "Тәуекелдерді тиімді басқару нені қамтамасыз етеді?", opts: ["Тек ақшаны үнемдеуді", "ЖИ-дің заңды және қауіпсіз жұмыс істеуін", "Тек жоғары бағаны"], a: 1 },
        { q: "Тәуекелдерге не жатады?", opts: ["Кемсітушілік, зиян келтіру, авторлық құқықты бұзу", "Тек техникалық мәселелер", "Тек дизайн"], a: 0 },
        { type: 'tf', q: "Құқықтық тәуекелдерді басқару – ЖИ-дің заңды жұмысын қамтамасыз ету үшін қажет.", a: true },
        { type: 'tf', q: "Тәуекелді талдау зиянның ауқымын бағалауды қамтымайды.", a: false },
        { type: 'tf', q: "Алгоритмдік Аудит – тәуекелдерді басқару шарасы.", a: true },
        { type: 'text', q: "Құқықтық тәуекелдерді азайту процесі (үш сөз)?", a: "Тәуекелдерді басқару" },
        { type: 'text', q: "Қателіктерді тексеру процесі (екі сөз)?", a: "Алгоритмдік Аудит" }
    ]
};

// --- САБАҚ 27 ---
LESSON_DATA[27] = {
    lecture: `
        <p><strong>Құқықтық ұсыныстарды әзірлеу</strong> – бұл ЖИ-дің дамуына байланысты Қазақстан Республикасының (ҚР) заңнамасына енгізуге болатын жаңа нормативтік-құқықтық актілерді немесе қолданыстағы заңдарға өзгерістерді ұсыну процесі. Оқушылар ЖИ-дің құқықтық тәуекелдерін (I, II, III Бөлімдер) ескере отырып, **дәлелді және өзекті** ұсыныстарды әзірлеуді үйренеді.</p>
        <p>Ұсыныс әзірлеудің 3 кезеңі: <strong>Мәселені анықтау</strong> (ҚР заңындағы олқылық), **Шешімді ұсыну** (жаңа бап немесе ереже) және **Негіздеме** (неліктен бұл ұсыныс қажет екенін құқықтық нормаларға сүйеніп түсіндіру). Мысалы, Deepfake үшін **арнайы жауапкершілік** туралы немесе ЖИ-дің этикалық кодексі туралы заң жобасын ұсыну.</p>
    `,
    glossary: ["Құқықтық ұсыныстар", "Нормативтік-құқықтық актілер", "Мәселені анықтау", "Шешімді ұсыну", "Негіздеме", "Арнайы жауапкершілік"],
    tasks: {
        l1: [
            "Құқықтық ұсыныстарды әзірлеу дегеніміз не?", 
            "Ұсыныс әзірлеудің 2 негізгі кезеңін атаңыз."
        ],
        l2: [
            "ҚР заңнамасына енгізуге болатын 2 өзекті ұсыныстың тақырыбын ұсыныңыз (мысалы, Deepfake үшін арнайы жауапкершілік).", 
            "Неліктен ұсыныстарды әзірлеу кезінде құқықтық нормаларға сүйеніп негіздеме беру маңызды? (2 себеп)."
        ],
        l3: [
            "ЖИ-дің қате диагностикасы үшін медициналық мекемелерге **қатаң жауапкершілік** жүктеуге қатысты 1 құқықтық ұсыныс бабын тұжырымдаңыз. Бұл ұсыныстың науқастардың құқықтарын қорғау тұрғысынан маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Құқықтық ұсыныстарды әзірлеу нені ұсыну процесі?", opts: ["Тек техникалық есептерді", "Жаңа нормативтік-құқықтық актілерді", "Тек жарнаманы"], a: 1 },
        { q: "Құқықтық ұсыныстар негізінен неге сүйенуі керек?", opts: ["Тек жеке пікірге", "Дәлелді және өзекті мәселелерге", "Тек кездейсоқ ақпаратқа"], a: 1 },
        { q: "Ұсыныс әзірлеудің бір кезеңі:", opts: ["Тек код жазу", "Шешімді ұсыну", "Тек сурет салу"], a: 1 },
        { q: "Арнайы жауапкершілік туралы ұсыныс неге қатысты болуы мүмкін?", opts: ["Тек көліктерге", "Deepfake үшін", "Тек ғимараттарға"], a: 1 },
        { q: "Нормативтік-құқықтық актілер дегеніміз не?", opts: ["Тек техникалық құжаттар", "Заңдар, ережелер", "Тек газеттер"], a: 1 },
        { type: 'tf', q: "Құқықтық ұсыныстарды әзірлеу ҚР заңнамасына өзгерістер енгізуге бағытталған.", a: true },
        { type: 'tf', q: "Негіздеме беру ұсыныс әзірлеудің маңызды бөлігі емес.", a: false },
        { type: 'tf', q: "Құқықтық ұсыныстар ЖИ қауіптерін ескеруі керек.", a: true },
        { type: 'text', q: "Заңдарға өзгерістер енгізу (үш сөз)?", a: "Нормативтік-құқықтық актілер" },
        { type: 'text', q: "Ұсыныстың неліктен қажет екенін түсіндіру (бір сөз)?", a: "Негіздеме" }
    ]
};

// --- САБАҚ 28 ---
LESSON_DATA[28] = {
    lecture: `
        <p><strong>Заң жобасын талдау</strong> – бұл Қазақстан Республикасында (ҚР) немесе халықаралық деңгейде (мысалы, ЕО ЖИ Актісі) ЖИ-ді реттеуге қатысты әзірленген заң жобаларының құқықтық, этикалық және экономикалық салдарларын жан-жақты зерттеу. Талдау мақсаты – заң жобасының **тиімділігін**, **қайшылықтарын** және **адам құқықтарын** қорғау деңгейін бағалау.</p>
        <p>Талдаудың 3 негізгі аспектісі: **Құқықтық сәйкестік** (ҚР Конституциясына және қолданыстағы заңдарға сәйкестігі), **Этикалық аудит** (зиян келтірмеу, әділдік қағидаларын сақтау) және **Техникалық іске асырылу** (ЖИ-ді реттеу талаптарын техникалық тұрғыдан орындау мүмкіндігі). Оқушылар заң жобасының мәтініндегі **құқықтық коллизияларды** анықтауды үйренеді.</p>
    `,
    glossary: ["Заң жобасын талдау", "ЕО ЖИ Актісі", "Тиімділік", "Қайшылықтар", "Құқықтық сәйкестік", "Этикалық аудит", "Техникалық іске асырылу"],
    tasks: {
        l1: [
            "Заң жобасын талдау дегеніміз не?", 
            "Талдаудың 2 негізгі мақсатын атаңыз."
        ],
        l2: [
            "Заң жобасын талдаудың 2 негізгі аспектісін атаңыз (мысалы, Құқықтық сәйкестік).", 
            "ЕО ЖИ Актісі сияқты халықаралық заң жобасын талдау ҚР үшін неліктен маңызды? (2 себеп)."
        ],
        l3: [
            "ҚР-да ЖИ-ді реттеуге арналған заң жобасының 'Құқықтық сәйкестік' аспектісіне қатысты 1 мәселені тұжырымдаңыз. Бұл мәселенің ҚР Конституциясы тұрғысынан маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Заң жобасын талдау нені зерттеу?", opts: ["Тек техникалық сипаттаманы", "Құқықтық, этикалық және экономикалық салдарларды", "Тек қаржыны"], a: 1 },
        { q: "Талдау мақсаты – заң жобасының нені бағалау?", opts: ["Тек ұзындығын", "Тиімділігін, қайшылықтарын және адам құқықтарын қорғау деңгейін", "Тек стилін"], a: 1 },
        { q: "Құқықтық сәйкестік нені тексеру?", opts: ["Тек техникалық нұсқауды", "ҚР Конституциясына және қолданыстағы заңдарға сәйкестігін", "Тек этикалық кодексті"], a: 1 },
        { q: "Этикалық аудит нені қарастырады?", opts: ["Зиян келтірмеу, әділдік қағидаларын сақтау", "Тек экономикалық пайданы", "Тек техникалық іске асырылуды"], a: 0 },
        { q: "Талдау арқылы нені анықтауды үйренеді?", opts: ["Тек пайданы", "Құқықтық коллизияларды", "Тек жылдамдықты"], a: 1 },
        { type: 'tf', q: "Заң жобасын талдау тек техникалық іске асырылуға назар аударады.", a: false },
        { type: 'tf', q: "ЕО ЖИ Актісі – халықаралық заң жобасына мысал.", a: true },
        { type: 'tf', q: "Құқықтық коллизияларды анықтау заң жобасын талдаудың маңызды бөлігі.", a: true },
        { type: 'text', q: "ҚР Конституциясына сәйкестікті тексеру (екі сөз)?", a: "Құқықтық сәйкестік" },
        { type: 'text', q: "ЖИ-ді реттеуге қатысты ЕО құжаты (үш сөз)?", a: "ЕО ЖИ Актісі" }
    ]
};

// --- САБАҚ 29 ---
LESSON_DATA[29] = {
    lecture: `
        <p><strong>ЖИ және Патент құқығы</strong> – бұл Жасанды Интеллект (ЖИ) әзірлеген немесе ЖИ-дің көмегімен жасалған өнертабыстарды, жаңа әдістерді және өндірістік үлгілерді қорғауға арналған құқықтық жүйе. Патент құқығы өнертабысқа **шектеулі уақытқа монополиялық құқық** береді.</p>
        <p>Құқықтық мәселе: Патент құқығы бойынша өнертапқыш тек **жеке тұлға** немесе **заңды тұлға** болуы мүмкін. Егер өнертабысты ЖИ-дің өзі жасаса, оған патент беруге бола ма деген сұрақ – патенттік құқықтық коллизия болып табылады. Оқушылар ЖИ-дің шығармашылық нәтижелеріне (авторлық құқық) және техникалық нәтижелеріне (патент) қатысты құқықтық айырмашылықтарды түсінуі керек. Патент құқығы ЖИ-дің дамуын ынталандыру үшін маңызды.</p>
    `,
    glossary: ["Патент құқығы", "Өнертабыс", "Монополиялық құқық", "Өнертапқыш", "Патенттік құқықтық коллизия", "Техникалық нәтижелер"],
    tasks: {
        l1: [
            "Патент құқығы дегеніміз не?", 
            "Патент құқығы бойынша өнертапқыш кім болуы мүмкін? (2 тұлғаны атаңыз)."
        ],
        l2: [
            "Патент құқығының авторлық құқықтан 2 негізгі айырмашылығын атаңыз (Мысалы, қорғау мерзімі).", 
            "ЖИ өнертабысты жасаса, неліктен патенттік құқықтық коллизия туындайды? (2 себеп)."
        ],
        l3: [
            "ЖИ-дің техникалық нәтижелерін патенттеуді ынталандыру үшін ҚР заңнамасына енгізуге болатын 1 арнайы түзетуді ұсыныңыз (мысалы, 'ЖИ-дің көмегімен' жасалған өнертабыстар үшін). Оның маңыздылығын түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Патент құқығы нені қорғауға арналған?", opts: ["Тек суреттерді", "Өнертабыстарды, жаңа әдістерді", "Тек музыканы"], a: 1 },
        { q: "Патент құқығы қандай құқық береді?", opts: ["Тегін қолдану құқығын", "Шектеулі уақытқа монополиялық құқық", "Тек жарнама құқығын"], a: 1 },
        { q: "Өнертапқыш кім болуы керек?", opts: ["Тек ЖИ", "Жеке тұлға немесе заңды тұлға", "Тек студент"], a: 1 },
        { q: "Патенттік құқықтық коллизия неге қатысты?", opts: ["Тек бағаға", "ЖИ өнертабыс жасаса, оған патент беру мүмкіндігіне", "Тек ережелерге"], a: 1 },
        { q: "ЖИ-дің дамуын не ынталандыру үшін маңызды?", opts: ["Тек әдебиет", "Патент құқығы", "Тек музыка"], a: 1 },
        { type: 'tf', q: "Патент құқығы авторлық құқықтан айырмашылығы жоқ.", a: false },
        { type: 'tf', q: "Патент құқығы өнертабысқа шектеулі уақытқа монополиялық құқық береді.", a: true },
        { type: 'tf', q: "Патенттік құқықтық коллизия ЖИ-дің техникалық нәтижелеріне қатысты.", a: true },
        { type: 'text', q: "Жаңа әдісті жасаушы (бір сөз)?", a: "Өнертапқыш" },
        { type: 'text', q: "Патентпен берілетін ерекше құқық (екі сөз)?", a: "Монополиялық құқық" }
    ]
};

// --- САБАҚ 30 ---
LESSON_DATA[30] = {
    lecture: `
        <p><strong>Құқықтық сауаттылықты арттыру</strong> – бұл Жасанды Интеллект (ЖИ) саласындағы құқықтық нормалар, этикалық қағидалар және жауапкершілік мәселелері туралы ақпаратты алу және оны күнделікті өмірде қолдану қабілетін дамыту. Құқықтық сауаттылық – ЖИ қауіптерінен (алаяқтық, Deepfake, кемсітушілік) қорғанудың **алдын алу шарасы**.</p>
        <p>Арттырудың 3 негізгі әдісі: <strong>Үздіксіз білім алу</strong> (ЖИ-ге қатысты жаңа заңдарды оқу), **Құқықтық ресурстарды пайдалану** (ресми дереккөздерді қолдану) және **Өз құқықтарын қорғауды үйрену** (шағымдану, апелляция). Оқушылар ЖИ-дің әрекеттерінен туындаған құқықтық бұзушылықтарды анықтау және оларға қарсы тұру дағдысын меңгеруі керек. Бұл IV Бөлімнің негізгі мақсаты.</p>
    `,
    glossary: ["Құқықтық сауаттылықты арттыру", "Алдын алу шарасы", "Үздіксіз білім алу", "Құқықтық ресурстарды пайдалану", "Шағымдану", "Апелляция"],
    tasks: {
        l1: [
            "Құқықтық сауаттылықты арттыру дегеніміз не?", 
            "Сауаттылықты арттырудың 2 негізгі әдісін атаңыз."
        ],
        l2: [
            "Неліктен құқықтық сауаттылық ЖИ қауіптерінен қорғанудың алдын алу шарасы болып табылады? (2 себеп).", 
            "ЖИ-дің әрекеттерінен туындаған құқықтық бұзушылықтарға қарсы тұрудың 2 дағдысын атаңыз (мысалы, шағымдану)."
        ],
        l3: [
            "ҚР-да жастардың ЖИ-ге қатысты құқықтық сауаттылығын арттыруға арналған 1 білім беру бағдарламасының концепциясын ұсыныңыз. Бұл бағдарламаның 3 негізгі модулін көрсетіңіз."
        ]
    },
    questions: [
        { q: "Құқықтық сауаттылықты арттыру нені дамыту?", opts: ["Тек физикалық күшті", "Құқықтық нормалар туралы ақпаратты алу және қолдану қабілетін", "Тек спорттық шеберлікті"], a: 1 },
        { q: "Сауаттылық ненің алдын алу шарасы?", opts: ["Тек техникалық қателердің", "ЖИ қауіптерінің (алаяқтық, Deepfake)", "Тек қаржылық шығындардың"], a: 1 },
        { q: "Арттырудың бір әдісі:", opts: ["Тек ұйықтау", "Үздіксіз білім алу", "Тек тамақ ішу"], a: 1 },
        { q: "Құқықтық ресурстар деген не?", opts: ["Тек кітапхана", "Ресми дереккөздер (заңдар, ережелер)", "Тек газеттер"], a: 1 },
        { q: "Өз құқықтарын қорғауға не жатады?", opts: ["Шағымдану, апелляция", "Тек үндемеу", "Тек келісу"], a: 0 },
        { type: 'tf', q: "Құқықтық сауаттылықты арттыру – IV Бөлімнің негізгі мақсаты.", a: true },
        { type: 'tf', q: "Құқықтық сауаттылықты арттырудың қажеті жоқ.", a: false },
        { type: 'tf', q: "Үздіксіз білім алу – сауаттылықты арттыру әдісі.", a: true },
        { type: 'text', q: "Құқықтарды бұзушылыққа қарсы шағымдану (бір сөз)?", a: "Шағымдану" },
        { type: 'text', q: "Жаңа заңдарды оқу (екі сөз)?", a: "Үздіксіз білім" }
    ]
};

// --- САБАҚ 31 (ҚОСЫМША ТАЛДАУ) ---
LESSON_DATA[31] = {
    lecture: `
        <p><strong>Жаһандық және ҚР тәжірибесін салыстыру</strong> – бұл Жасанды Интеллекті (ЖИ) құқықтық реттеудегі халықаралық тәжірибені (ЕО, АҚШ, Қытай) Қазақстан Республикасының (ҚР) қолданыстағы заңнамасымен және даму стратегияларымен салыстырмалы талдау. Талдау мақсаты – ҚР заңнамасындағы **олқылықтарды** және **халықаралық стандарттарды** енгізу мүмкіндігін анықтау.</p>
        <p>Салыстырудың негізгі аспектілері: **Жауапкершілік модельдері** (қатаң жауапкершілік), **Деректерді қорғау талаптары** (GDPR), және **Этикалық қағидалар** (ашықтық, әділдік). Оқушылар халықаралық үлгілерге сүйене отырып, ҚР үшін ЖИ-ді реттеудің **үздік ұсыныстарын** тұжырымдауға дағдыланады. Бұл курстық жобаның (ЖИ қауіптері мен құқықтық тәуекелдер) негізін қалайды.</p>
    `,
    glossary: ["Жаһандық тәжірибе", "Салыстырмалы талдау", "Олқылықтар", "Халықаралық стандарттар", "Жауапкершілік модельдері", "Үздік ұсыныстар"],
    tasks: {
        l1: [
            "Жаһандық және ҚР тәжірибесін салыстырудың негізгі мақсаты не?", 
            "Салыстырудың 2 негізгі аспектісін атаңыз."
        ],
        l2: [
            "ЖИ-дің жауапкершілік моделіне қатысты (мысалы, қатаң жауапкершілік) ҚР және ЕО тәжірибесі арасындағы 2 айырмашылықты сипаттаңыз.", 
            "ҚР заңнамасындағы ЖИ-ді реттеудегі 2 негізгі олқылықты атаңыз."
        ],
        l3: [
            "Халықаралық стандарттарға (мысалы, GDPR талаптары) сүйене отырып, ҚР үшін ЖИ-дің деректерді қорғауын күшейтуге қатысты 3 үздік ұсынысты тұжырымдаңыз. Бұл ұсыныстардың өзектілігін түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Жаһандық тәжірибені салыстырудың мақсаты – нені анықтау?", opts: ["Тек қаржыны", "ҚР заңнамасындағы олқылықтарды және халықаралық стандарттарды енгізу мүмкіндігін", "Тек техникалық қателерді"], a: 1 },
        { q: "Салыстырудың бір аспектісі:", opts: ["Тек өндіріс көлемі", "Жауапкершілік модельдері", "Тек географиялық орналасуы"], a: 1 },
        { q: "Қатаң жауапкершілік ненің моделіне жатады?", opts: ["Тек этикалық", "Жауапкершілік модельдеріне", "Тек техникалық"], a: 1 },
        { q: "GDPR ненің талаптарын қамтиды?", opts: ["Тек этикалық", "Деректерді қорғау", "Тек техникалық"], a: 1 },
        { q: "Курстық жобаның негізі не болып табылады?", opts: ["Тек кітаптар", "ЖИ қауіптері мен құқықтық тәуекелдер", "Тек бағдарламалар"], a: 1 },
        { type: 'tf', q: "Салыстырмалы талдау ҚР үшін үздік ұсыныстарды тұжырымдауға көмектеседі.", a: true },
        { type: 'tf', q: "Қазақстан Республикасының заңнамасында ЖИ-ді реттейтін ешқандай олқылық жоқ.", a: false },
        { type: 'tf', q: "GDPR – халықаралық стандарттардың бір мысалы.", a: true },
        { type: 'text', q: "ҚР заңнамасындағы жетіспеушіліктер (бір сөз)?", a: "Олқылықтар" },
        { type: 'text', q: "Жауапкершіліктің бір түрі (екі сөз)?", a: "Қатаң жауапкершілік" }
    ]
};

// --- САБАҚ 32 ---
LESSON_DATA[32] = {
    lecture: `
        <p><strong>Қорытынды жоба қорғау</strong> – бұл оқушылардың курстық жұмысын (ЖИ қауіптері мен құқықтық тәуекелдер) сарапшылар немесе оқытушылар алдында қорғау рәсімі. Бұл сабақ оқушының тақырыпты қаншалықты терең меңгергенін, құқықтық және этикалық мәселелерді талдау және шешім қабылдау қабілетін бағалауға арналған.</p>
        <p>Қорғау процесінде оқушылар **қарсы сұрақтарға құқықтық нормаларға сүйене отырып жауап беруі**, жобаның құқықтық негіздерін түсіндіруі және ЖИ-дің зиянды қолданылуынан қорғанудың **өз ұсыныстарын** дәлелдеуі керек. Қорғаудың сәтті өтуі оқушының цифрлық құқықтық сауаттылығының жоғары деңгейде екенін көрсетеді.</p>
    `,
    glossary: ["Қорытынды жоба қорғау", "Қорғау рәсімі", "Сарапшылар", "Құқықтық негіздер", "Өз ұсыныстары", "Дәлелдеу"],
    tasks: {
        l1: [
            "Қорытынды жоба қорғаудың негізгі мақсаты не?", 
            "Қорғау кезінде оқушы не істеуі керек? (2 міндет)."
        ],
        l2: [
            "Егер сізге жобаңыздағы 'Deepfake-тің құқықтық жауапкершілігі' туралы қарсы сұрақ қойылса, қандай 3 заңды аргументті қолданасыз?", 
            "Жобаны сәтті қорғау үшін қажетті 2 негізгі дағдыны атаңыз (мысалы, сенімділік)."
        ],
        l3: [
            "Қорғау нәтижесінде, ЖИ-дің құқықтық реттелуіне қатысты ҚР заңнамасына енгізуге болатын 2 басты ұсынысыңызды тұжырымдаңыз. Бұл ұсыныстардың өзектілігін түсіндіріңіз."
        ]
    },
    questions: [
        { q: "Жоба қорғаудың басты міндеті:", opts: ["Тек оқытушыны тыңдау", "Талдау және шешім қабылдау қабілетін бағалау", "Тек презентация көрсету"], a: 1 },
        { q: "Қорғау кезінде жауап беру неге сүйенуі керек?", opts: ["Жеке пікірге", "Құқықтық нормаларға", "Әлеуметтік желіге"], a: 1 },
        { q: "Қорғаудың сәтті өтуі нені көрсетеді?", opts: ["Техникалық дағдыны", "Цифрлық құқықтық сауаттылықтың жоғары деңгейін", "Көңіл-күйді"], a: 1 },
        { q: "Қорғау процесінде не дәлелденуі керек?", opts: ["ЖИ-дің техникалық коды", "Өз ұсыныстары", "Басқалардың пікірі"], a: 1 },
        { q: "Қорғауды кім жүргізеді?", opts: ["Тек оқушылар", "Сарапшылар немесе оқытушылар", "Бәрі бірдей"], a: 1 },
        { type: 'tf', q: "Қорғау кезінде қарсы сұрақтарға жауап беру міндетті емес.", a: false },
        { type: 'tf', q: "Жобаның құқықтық негіздерін түсіндіру маңызды.", a: true },
        { type: 'tf', q: "Қорғаудың басты мақсаты – ЖИ-ді толығымен сынау.", a: false },
        { type: 'text', q: "Қорғау кезінде қойылатын сұрақтар (екі сөз)?", a: "Қарсы сұрақтар" },
        { type: 'text', q: "Жобаның сәтті өтуі нені көрсетеді (үш сөз)?", a: "Құқықтық сауаттылықтың жоғары деңгейі" }
    ]
};

// --- САБАҚ 33 ---
LESSON_DATA[33] = {
    lecture: `
        <p><strong>Рефлексия</strong> – бұл оқушылардың бүкіл курстық оқу процесін (ЖИ және Құқық) жан-жақты талдау, жетістіктері мен қиындықтарын бағалау сабағы. Оқушылар білімдерінің қалай өзгергенін, ЖИ-ге қатысты құқықтық және этикалық көзқарастарының қалай дамығанын бағалайды.</p>
        <p>Рефлексияның негізгі сұрақтары: «Мен нені үйрендім?», «Маған не қиын болды?», «Бұл білімді болашақта қалай қолданамын?». Рефлексия жазбасы ЖИ-дің зиянды қолданылуына қатысты өзгерген пікірлерді, сондай-ақ ҚР заңнамасына қатысты дайындаған ұсыныстардың маңыздылығын қамтуы керек. Бұл оқушының **үздіксіз дамуға** және **өзін-өзі бағалауға** деген қабілетін көрсетеді.</p>
    `,
    glossary: ["Рефлексия", "Жетістіктер", "Қиындықтар", "Көзқарас", "Үздіксіз даму", "Өзін-өзі бағалау"],
    tasks: {
        l1: [
            "Рефлексияның негізгі мақсаты не?", 
            "Рефлексиядағы 3 негізгі сұрақты атаңыз (Лекцияға сәйкес)."
        ],
        l2: [
            "Бүкіл курстағы ең маңызды деп тапқан 1 құқықтық ұғымды (мысалы, 'Қатаң жауапкершілік') және 1 этикалық ұғымды атап, неге олардың көзқарасыңызды өзгерткенін түсіндіріңіз.", 
            "ЖИ-дің зиянды қолданылуынан қорғануға қатысты қалыптасқан 2 жаңа дағдыңызды сипаттаңыз."
        ],
        l3: [
            "Болашақта ЖИ-дің құқықтық реттелуіне қатысты қандай 2 тақырыпты тереңірек зерттегіңіз келеді? Осы тақырыптардың ҚР үшін құқықтық өзектілігін дәлелдеңіз."
        ]
    },
    questions: [
        { q: "Рефлексияның мақсаты – нені талдау?", opts: ["Тек тест нәтижелерін", "Бүкіл курстық оқу процесін", "Тек бағдарламалау тілін"], a: 1 },
        { q: "Рефлексия нені бағалауға мүмкіндік береді?", opts: ["Жаңа компьютерді", "Жетістіктер мен қиындықтарды", "Басқа оқушылардың жұмысын"], a: 1 },
        { q: "Үздіксіз даму қабілетін не көрсетеді?", opts: ["Мұғалімнің бағасы", "Рефлексия жазбасы", "Көп демалу"], a: 1 },
        { q: "Оқушылар ненің қалай дамығанын бағалайды?", opts: ["Тек физикалық күштің", "Құқықтық және этикалық көзқарастардың", "Дұрыс тамақтанудың"], a: 1 },
        { q: "Болашақта үйренген білімді қолдануға арналған сұрақ:", opts: ["Не істеу керек?", "Нені үйрендім?", "Қалай қолданамын?"], a: 2 },
        { type: 'tf', q: "Рефлексия оқушының өзін-өзі бағалау қабілетін көрсетеді.", a: true },
        { type: 'tf', q: "Рефлексияда тек техникалық мәселелер қарастырылады.", a: false },
        { type: 'tf', q: "Құқықтық көзқарастың өзгеруі рефлексияның бөлігі болып саналады.", a: true },
        { type: 'text', q: "Оқу процесін жан-жақты талдау (бір сөз)?", a: "Рефлексия" },
        { type: 'text', q: "Өзін-өзі бағалауға мүмкіндік беретін қабілет (екі сөз)?", a: "Үздіксіз даму" }
    ]
};

// --- САБАҚ 34 ---
LESSON_DATA[34] = {
    lecture: `
        <p><strong>Қорытынды бағалау</strong> – бұл оқушының «Жасанды Интеллект және Құқық» курсы бойынша алған білімін кешенді бағалауға арналған соңғы кезең. Бағалау келесі бөлімдерді қамтиды: ЖИ-дің техникалық негіздері (I Бөлім), ЖИ-дің құқықтық және этикалық реттелуі (II Бөлім), ЖИ қауіптері мен тәуекелдері (III Бөлім) және ЖИ-ді жауапты қолдану мәдениеті (IV Бөлім).</p>
        <p>Бағалау жұмысы тест сұрақтарынан, құқықтық кейстерді шешуден және оқушылардың курстық жұмыс барысында жасаған ұсыныстарын талдаудан тұруы мүмкін. Мақсат – оқушының **критикалық ойлау** қабілетін, **құқықтық сауаттылығын** және ЖИ қатысқан мәселелер бойынша **дәлелді шешім** қабылдауға дайындығын анықтау. Сәтті бағалау осы саладағы болашақ оқу мен кәсіби дамуға негіз болады.</p>
    `,
    glossary: ["Қорытынды бағалау", "Кешенді бағалау", "Критикалық ойлау", "Дәлелді шешім", "Тест сұрақтары", "Болашақ даму"],
    tasks: {
        l1: [
            "Қорытынды бағалау қандай 4 негізгі бөлімді қамтиды?", 
            "Бағалау жұмысының 2 мүмкін форматын атаңыз (мысалы, тест)."
        ],
        l2: [
            "Қорытынды бағалауда оқушының критикалық ойлау қабілетін бағалау үшін қандай 3 сұрақтық тақырыпты ұсынуға болады? (Мысалы, 'Қатаң жауапкершілік туралы пікіріңіз').", 
            "Құқықтық сауаттылықты бағалау үшін, оқушы қандай 2 құқықтық дағдыны көрсетуі керек?"
        ],
        l3: [
            "Қорытынды бағалауға ЖИ-дің ҚР заңнамасына енгізуге қатысты 3 маңызды ұсынысты талдауды қамтитын сұрақты әзірлеңіз. Бұл сұрақтың бағалау критерийлерін (2 критерий) көрсетіңіз."
        ]
    },
    questions: [
        { q: "Қорытынды бағалаудың негізгі мақсаты не?", opts: ["Тек ЖИ-дің қауіптерін тексеру", "Оқушының білімін кешенді бағалау", "Тек рефлексия жасау"], a: 1 },
        { q: "Бағалауда не анықталады?", opts: ["Спорттық жетістіктер", "Критикалық ойлау қабілеті", "Код жазу жылдамдығы"], a: 1 },
        { q: "Дәлелді шешім қабылдау қабілеті неге қатысты?", opts: ["ЖИ қатысқан мәселелерге", "Тек қарапайым есептерге", "Тек техникалық аспектілерге"], a: 0 },
        { q: "Бағалау жұмысы нені талдаудан тұруы мүмкін?", opts: ["Тек жаңалықтарды", "Оқушылардың курстық жұмыс барысындағы ұсыныстарын", "Басқа оқушылардың бағаларын"], a: 1 },
        { q: "Сәтті бағалау неге негіз болады?", opts: ["Сабақты тоқтатуға", "Болашақ оқу мен кәсіби дамуға", "Тек жаңа технологияны сатып алуға"], a: 1 },
        { type: 'tf', q: "Қорытынды бағалау тек I Бөлімді ғана қамтиды.", a: false },
        { type: 'tf', q: "Құқықтық кейстерді шешу бағалау форматы болуы мүмкін.", a: true },
        { type: 'tf', q: "Қорытынды бағалау оқушының құқықтық сауаттылығын анықтамайды.", a: false },
        { type: 'text', q: "Оқушының мәселеге қатысты ойлау қабілеті (екі сөз)?", a: "Критикалық ойлау" },
        { type: 'text', q: "Қорытынды бағалаудың сипаты (бір сөз)?", a: "Кешенді" }
    ]
};
        // Бұл жерде қалған 3-34 сабақтардың мазмұны әзірше жоқ, оларға шаблон қолданылады.
        // Егер сіз келесі сабақтардың мазмұнын жібергіңіз келсе, оларды дәл осы LESSON_DATA құрылымына қоса аласыз.
        
        // --- GENERATE CONTENT FUNCTION (3-БӨЛІКТЕН КЕЛДІ) ---
        // Бұл функция осы LESSON_DATA объектісінен мазмұнды алады.
        function generateContent(lesson) {
            if (LESSON_DATA[lesson.id]) {
                return LESSON_DATA[lesson.id];
            } 
            
            // ЕСКЕРТУ: Егер мазмұн әлі жазылмаса, осы жерде "Құрылымдық шаблон" қайтарылады.
            const title = lesson.title;
            return {
                lecture: `
                    <p style="color:#DC2626; font-weight:bold;">⚠️ Бұл сабақтың мазмұны әлі толық жазылмаған.</p>
                    <p><strong>Тақырып: ${title}</strong>. Сабақ бұл бөлімде ЖИ-дің құқықтық немесе этикалық аспектілеріне тоқталады. Бұл мәтінді жобаны қорғау алдында толтыруыңыз қажет.</p>
                    <p>Сіздің талабыңыз бойынша, әр сабаққа бірегей 100 сөздік мәтін, 3 деңгейлі тапсырма және 10 сұрақтан тұратын тест жазылуы керек.</p>
                `,
                glossary: ["Жазылуда", "Толықтыру", "Құқық", "ЖИ"],
                tasks: {
                    l1: [`"${title}" бойынша негізгі терминдерді анықтаңыз.`],
                    l2: [`Тақырыпты қолдану арқылы 2 мысал келтіріңіз.`],
                    l3: [`Тақырыпқа байланысты 50 сөздік шағын эссе жазыңыз. (Үлгі)`]
                },
                questions: [
                    { q: "Тест сұрағы 1", opts: ["А", "B", "C"], a: 0 },
                    { q: "Тест сұрағы 2", opts: ["А", "B", "C"], a: 1 },
                    { q: "Тест сұрағы 3", opts: ["А", "B", "C"], a: 2 },
                    { q: "Тест сұрағы 4", opts: ["А", "B", "C"], a: 0 },
                    { q: "Тест сұрағы 5", opts: ["А", "B", "C"], a: 1 },
                    { type: 'tf', q: "Ақиқат/Жалған сұрағы 1", a: true },
                    { type: 'tf', q: "Ақиқат/Жалған сұрағы 2", a: false },
                    { type: 'tf', q: "Ақиқат/Жалған сұрағы 3", a: true },
                    { type: 'text', q: "Ашық сұрақ 1 (Жауабы)", a: "Үлгі" },
                    { type: 'text', q: "Ашық сұрақ 2 (Жауабы)", a: "Шаблон" }
                ]
            };
        }
        
        // --- 1. UI НАВИГАЦИЯСЫ ---
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            
            // Меню активтілігін жаңарту
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            const indexMap = { home: 0, modules: 1, 'lesson-list': 1, admin: 2, settings: 3 };
            const navIndex = indexMap[pageId] || 0;
            if(document.querySelectorAll('.nav-item')[navIndex]) {
                 document.querySelectorAll('.nav-item')[navIndex].classList.add('active');
            }
            
            // Сабақтар бетіне өткенде, егер ол Lesson-list болса, Modules-ты да актив ету
            if (pageId === 'lesson-list' || pageId === 'lesson-view') {
                document.querySelectorAll('.nav-item')[1].classList.add('active');
            }
            
            // Беттің жоғарысына жылжу
            document.getElementById('app-container').scrollTop = 0;
        }

        function openModule(modNum) {
            const container = document.getElementById('lessons-container');
            container.innerHTML = "";
            
            const moduleTitles = {
                1: "І Бөлім. ЖИ Негіздері (1-8 сабақ)",
                2: "ІІ Бөлім. Құқық және Этика (9-16 сабақ)",
                3: "III Бөлім. Қауіптер мен Тәуекелдер (17-26 сабақ)",
                4: "IV Бөлім. Қауіпсіздік Мәдениеті (27-34 сабақ)",
            };
            
            document.getElementById('module-title').innerText = moduleTitles[modNum];
            
            const modLessons = lessons.filter(l => l.mod === modNum);
            
            modLessons.forEach(l => {
                const div = document.createElement('div');
                div.className = "lesson-item";
                
                // Сабақтар тізіміне кішкене стикерлер қосу
                const icons = {
                    1: '💡', 2: '🧠', 3: '💻', 4: '🇰🇿', 5: '🛠️', 6: '📊', 7: '⚔️', 8: '📝',
                    9: '🌍', 10: '📜', 11: '©️', 12: '👤', 13: '🤝', 14: '✅', 15: '✍️', 16: '💯',
                    17: '🎭', 18: '🛑', 19: '💸', 20: '⚖️', 21: '😰', 22: '🚨', 23: '🔒', 24: '🧩',
                    25: '🛡️', 26: '✔️', 27: '🔑', 28: '🎓', 29: '🗣️', 30: '💡', 31: '📚', 32: '📢',
                    33: '🏆', 34: '💫'
                };
                
                div.innerHTML = `
                    <div class="lesson-icon">${icons[l.id] || '📚'}</div>
                    <div class="lesson-title">${l.title}</div>
                `;
                div.onclick = () => loadLesson(l.id);
                container.appendChild(div);
            });
            
            showPage('lesson-list');
        }
        
        // --- 2. САБАҚТЫ ЖҮКТЕУ ЛОГИКАСЫ ---
        
        let currentQuiz = []; // Ағымдағы тест сұрақтарын сақтау үшін
        
        function loadLesson(id) {
            const lesson = lessons.find(l => l.id === id);
            const content = generateContent(lesson);
            
            document.getElementById('lesson-header-title').innerText = lesson.title;
            
            // Лекция
            document.getElementById('lecture-text').innerHTML = content.lecture;
            
            // Глоссарий
            const glList = document.getElementById('glossary-list');
            glList.innerHTML = "";
            content.glossary.forEach(w => {
                let li = document.createElement('li');
                li.innerText = w;
                glList.appendChild(li);
            });

            // Тапсырмалар (Accordion арқылы толтыру)
            const taskContainer = document.getElementById('tasks-accordion');
            taskContainer.innerHTML = '';
            
            const taskLevels = {
                l1: { title: 'I Деңгей (Білу, Түсіну)', icon: '📘' },
                l2: { title: 'II Деңгей (Қолдану, Талдау)', icon: '🔬' },
                l3: { title: 'III Деңгей (Жинақтау, Бағалау)', icon: '🌟' }
            };

            ['l1', 'l2', 'l3'].forEach(levelKey => {
                const levelData = content.tasks[levelKey];
                const accBtn = document.createElement('button');
                accBtn.className = 'accordion';
                accBtn.innerHTML = `${taskLevels[levelKey].icon} ${taskLevels[levelKey].title}`;
                taskContainer.appendChild(accBtn);

                const panel = document.createElement('div');
                panel.className = 'panel';
                panel.innerHTML = levelData.map(t => `<p>${t}</p>`).join('');
                taskContainer.appendChild(panel);
            });
            
            initAccordion(); // Жаңадан қосылған accordion-дарды іске қосу

            // Тест
            currentQuiz = content.questions;
            renderQuiz(currentQuiz);

            showPage('lesson-view');
            switchTab('lecture');
        }
        
        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(t => t.style.display = 'none');
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            
            const tabMap = { 'lecture': 0, 'tasks': 1, 'quiz': 2 };
            const contentId = `tab-${tabName}`;
            
            document.getElementById(contentId).style.display = 'block';
            document.querySelectorAll('.tab-btn')[tabMap[tabName]].classList.add('active');
        }

        function initAccordion() {
            const acc = document.getElementsByClassName("accordion");
            for (let i = 0; i < acc.length; i++) {
                // Ескі тыңдаушыларды жою үшін клон жасаймыз
                let newEl = acc[i].cloneNode(true);
                acc[i].parentNode.replaceChild(newEl, acc[i]);
                
                newEl.addEventListener("click", function() {
                    this.classList.toggle("active-acc");
                    var panel = this.nextElementSibling;
                    if (panel.style.maxHeight) {
                        panel.style.maxHeight = null;
                    } else {
                        // 1.5 есеге көбейту, себебі контент көбейген сайын дұрыс ашылуы үшін
                        panel.style.maxHeight = panel.scrollHeight * 1.5 + "px"; 
                    }
                });
            }
        }
        
        
        // --- 3. ТЕСТ ЛОГИКАСЫ ---
        
        function renderQuiz(questions) {
            const form = document.getElementById('quiz-form');
            form.innerHTML = "";
            document.getElementById('quiz-result').innerText = "";

            questions.forEach((q, idx) => {
                const qNum = idx + 1;
                const div = document.createElement('div');
                div.style.marginBottom = "20px";
                div.innerHTML = `<p style="font-weight:bold; margin-bottom:10px;">${qNum}. ${q.q}</p>`;

                if(q.type === 'tf') { // Ақиқат/Жалған
                    div.innerHTML += `
                        <label class="quiz-option-label"><input type="radio" name="q${qNum}" value="true"> Ақиқат</label>
                        <label class="quiz-option-label"><input type="radio" name="q${qNum}" value="false"> Жалған</label>
                    `;
                } else if (q.type === 'text') { // Ашық сұрақ
                    div.innerHTML += `<input type="text" name="q${qNum}" placeholder="Жауап жазыңыз..." class="text-input" style="width:100%; padding:10px; border:1px solid #ccc; border-radius:10px;">`;
                } else { // Көп таңдаулы
                    q.opts.forEach((opt, optIdx) => {
                        div.innerHTML += `<label class="quiz-option-label"><input type="radio" name="q${qNum}" value="${optIdx}"> ${opt}</label>`;
                    });
                }
                form.appendChild(div);
            });
        }

        function checkQuiz() {
            let score = 0;
            const form = document.getElementById('quiz-form');
            const resultDiv = document.getElementById('quiz-result');

            currentQuiz.forEach((q, idx) => {
                const qNum = idx + 1;
                let isCorrect = false;

                if(q.type === 'text') {
                    const input = form.querySelector(`input[name="q${qNum}"]`);
                    if(input && input.value.toLowerCase().trim() === q.a.toLowerCase().trim()) isCorrect = true;
                } else {
                    const selected = form.querySelector(`input[name="q${qNum}"]:checked`);
                    if(selected) {
                        const val = selected.value;
                        if(q.type === 'tf') {
                            if((val === 'true' && q.a === true) || (val === 'false' && q.a === false)) isCorrect = true;
                        } else {
                            if(parseInt(val) === q.a) isCorrect = true;
                        }
                    }
                }

                if(isCorrect) score++;
                
                // Тест элементтерін түске бояу (міндетті емес, бірақ қосымшаға эстетика береді)
                const qDiv = form.querySelector(`p:nth-child(${qNum})`).parentNode;
                if(isCorrect) {
                    qDiv.style.border = '2px solid #059669'; // Жасыл
                } else {
                    qDiv.style.border = '2px solid #DC2626'; // Қызыл
                }
                qDiv.style.borderRadius = '20px';
                qDiv.style.padding = '10px';
                qDiv.style.transition = '0.3s';
            });

            resultDiv.innerText = `Нәтиже: ${score} / ${currentQuiz.length} ✅`;
            resultDiv.style.color = score >= 7 ? '#059669' : '#DC2626';
            resultDiv.style.background = score >= 7 ? '#D1FAE5' : '#FEE2E2';
        }
        
        
        // --- 4. ДИНАМИКАЛЫҚ ТҮС ТАНДАУ (Settings-ке арналған) ---
        function setTheme(color) {
            document.documentElement.style.setProperty('--primary-color', color);
            // Қосымша түстерді де өзгертуге болады, мысалы, secondary
            if (color === '#4F46E5') { // Blue
                 document.documentElement.style.setProperty('--secondary-color', '#0EA5E9');
            } else if (color === '#E54646') { // Red
                 document.documentElement.style.setProperty('--secondary-color', '#F87171');
            } else if (color === '#059669') { // Green
                 document.documentElement.style.setProperty('--secondary-color', '#34D399');
            } else if (color === '#F59E0B') { // Yellow
                 document.documentElement.style.setProperty('--secondary-color', '#FBBF24');
            }
            
            // Фонды қайта жүктеу (толық әсер үшін)
            updateCanvasColors(); 
        }

        // --- 5. 3D ФОН АНИМАЦИЯСЫ (НЕВРОНДЫҚ ЖЕЛІ ТҮРІНДЕ) ---
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');
        let width, height;
        let particles = [];
        const NUM_PARTICLES = 35; // Қалықтаушы элементтер саны

        function resize() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resize);
        resize();

        class Particle {
            constructor() {
                this.x = Math.random() * width;
                this.y = Math.random() * height;
                this.size = Math.random() * 5 + 1; // 1-6px
                this.speedX = (Math.random() - 0.5) * 0.5; // Баяу қозғалыс
                this.speedY = (Math.random() - 0.5) * 0.5;
                this.color = 'rgba(79, 70, 229, 0.4)'; // Ашық негізгі түс
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.x < 0 || this.x > width) this.speedX *= -1;
                if (this.y < 0 || this.y > height) this.speedY *= -1;
            }
            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }
        
        function updateCanvasColors() {
            // Түс ауысқанда бөлшектердің түсін жаңарту
            const color = getComputedStyle(document.documentElement).getPropertyValue('--primary-color').trim();
            particles.forEach(p => p.color = color.replace(')', ', 0.4)').replace('rgb', 'rgba'));
        }

        function initParticles() {
            particles = [];
            for(let i=0; i<NUM_PARTICLES; i++) particles.push(new Particle());
            updateCanvasColors(); // Түстерді орнату
        }
        initParticles();

        function connectParticles() {
            const connectionColor = getComputedStyle(document.documentElement).getPropertyValue('--primary-color').trim().replace(')', ', 0.1)').replace('rgb', 'rgba');
            let opacityValue = 1;
            for (let a = 0; a < particles.length; a++) {
                for (let b = a; b < particles.length; b++) {
                    let distance = ((particles[a].x - particles[b].x) ** 2 + (particles[a].y - particles[b].y) ** 2) ** 0.5;
                    if (distance < 150) {
                        opacityValue = 1 - (distance / 150);
                        ctx.strokeStyle = connectionColor.replace('0.1', opacityValue * 0.2); // Өте әлсіз сызықтар
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(particles[a].x, particles[a].y);
                        ctx.lineTo(particles[b].x, particles[b].y);
                        ctx.stroke();
                    }
                }
            }
        }

        function animate() {
            ctx.clearRect(0, 0, width, height);
            connectParticles(); // Бөлшектерді сызықпен байланыстыру
            
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animate);
        }
        animate();
        
    </script>
</body>
</html>
