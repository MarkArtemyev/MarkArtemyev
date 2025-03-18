<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Лютый Web Китч README</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600;700&display=swap');
    
    body {
      margin: 0;
      padding: 0;
      font-family: 'Fira Code', monospace;
      background: linear-gradient(45deg, #000000, #434343);
      color: #fff;
      overflow-x: hidden;
      animation: backgroundPulse 10s infinite alternate;
    }
    
    @keyframes backgroundPulse {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
    }
    
    header {
      text-align: center;
      margin-bottom: 40px;
      position: relative;
    }
    
    .waving-header {
      width: 100%;
      height: 200px;
      background: linear-gradient(45deg, #ff00ff, #00ffff, #ff00ff);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      border-radius: 0 0 50% 50% / 0 0 100% 100%;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      box-shadow: 0 10px 30px rgba(0, 255, 255, 0.5);
    }
    
    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    
    .header-text {
      font-size: 50px;
      font-weight: bold;
      color: #fff;
      text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff, 0 0 30px #00ffff;
      animation: glow 2s ease-in-out infinite alternate;
    }
    
    @keyframes glow {
      from { text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff; }
      to { text-shadow: 0 0 20px #00ffff, 0 0 30px #00ffff, 0 0 40px #00ffff; }
    }
    
    .typing-text {
      height: 60px;
      margin: 20px 0;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    
    .typing-text span {
      font-size: 30px;
      color: #00ffff;
      border-right: 4px solid #00ffff;
      padding-right: 8px;
      white-space: nowrap;
      overflow: hidden;
      animation: typing 4s steps(30) infinite, blink 1s infinite;
    }
    
    .typing-spans {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    .typing-spans span {
      display: none;
    }
    
    .typing-spans span:first-child {
      display: inline-block;
    }
    
    @keyframes typing {
      from { width: 0 }
      to { width: 100% }
    }
    
    @keyframes blink {
      50% { border-color: transparent }
    }
    
    .snake-animation {
      width: 100%;
      height: 200px;
      background: url('https://github.com/YourUsername/YourUsername/blob/output/github-contribution-grid-snake.svg') repeat-x;
      animation: snakeMove 20s linear infinite;
    }
    
    @keyframes snakeMove {
      from { background-position: 0 0; }
      to { background-position: -1000px 0; }
    }
    
    .about-me {
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      padding: 30px;
      border-radius: 15px;
      width: 80%;
      margin: 30px auto;
      box-shadow: 0 12px 24px rgba(0,0,0,0.2);
      animation: float 6s ease-in-out infinite;
      position: relative;
      overflow: hidden;
    }
    
    .about-me::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: linear-gradient(45deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0.8) 50%, rgba(255,255,255,0) 100%);
      transform: rotate(30deg);
      animation: shine 6s infinite;
    }
    
    @keyframes shine {
      0% { transform: scale(0) rotate(45deg); opacity: 0; }
      80% { transform: scale(0) rotate(45deg); opacity: 0.5; }
      81% { transform: scale(4) rotate(45deg); opacity: 1; }
      100% { transform: scale(50) rotate(45deg); opacity: 0; }
    }
    
    @keyframes float {
      0% { transform: translateY(0px); }
      50% { transform: translateY(-20px); }
      100% { transform: translateY(0px); }
    }
    
    .about-me h2 {
      color: #fff;
      text-shadow: 0 0 10px rgba(0,0,0,0.5);
    }
    
    .about-me p {
      color: #fff;
      font-size: 18px;
      text-shadow: 0 0 5px rgba(0,0,0,0.3);
    }
    
    .tech-stack {
      margin-top: 40px;
      text-align: center;
    }
    
    .tech-stack h2 {
      font-size: 28px;
      margin-bottom: 20px;
      text-shadow: 0 0 10px #00ffff;
    }
    
    .tech-badges {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }
    
    .tech-badge {
      padding: 10px 20px;
      border-radius: 10px;
      font-weight: bold;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
      transition: all 0.3s ease;
      animation: pulse 2s infinite;
    }
    
    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.05); }
      100% { transform: scale(1); }
    }
    
    .tech-badge:hover {
      transform: translateY(-10px) rotate(5deg);
      box-shadow: 0 15px 30px rgba(0,0,0,0.4);
    }
    
    .react { background: #61DAFB; color: black; }
    .javascript { background: #F7DF1E; color: black; }
    .laravel { background: #FF2D20; color: white; }
    .nodejs { background: #339933; color: white; }
    .docker { background: #0db7ed; color: white; }
    .cicd { background: #0077B5; color: white; }
    .typescript { background: #007ACC; color: white; }
    
    .projects {
      margin-top: 60px;
      text-align: center;
    }
    
    .projects h2 {
      font-size: 28px;
      margin-bottom: 20px;
      text-shadow: 0 0 10px #ff00ff;
    }
    
    .project-cards {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
      margin: 20px 0;
    }
    
    .project-card {
      width: 300px;
      padding: 20px;
      border-radius: 15px;
      color: #fff;
      box-shadow: 0 10px 20px rgba(0,0,0,0.25);
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
    }
    
    .project-card:hover {
      transform: translateY(-15px) scale(1.05);
      box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    }
    
    .project-card::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: linear-gradient(45deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0.8) 50%, rgba(255,255,255,0) 100%);
      transform: rotate(45deg);
      animation: shine 4s infinite;
    }
    
    .project-card h3 {
      font-size: 20px;
      margin-bottom: 10px;
    }
    
    .project-card p {
      font-size: 14px;
    }
    
    .project-card:nth-child(1) {
      background: linear-gradient(135deg, #667eea, #764ba2);
    }
    
    .project-card:nth-child(2) {
      background: linear-gradient(135deg, #f093fb, #f5576c);
    }
    
    .articles {
      background: linear-gradient(45deg, #ffe259, #ffa751);
      padding: 30px;
      border-radius: 15px;
      width: 80%;
      margin: 40px auto;
      box-shadow: 0 10px 30px rgba(255, 167, 81, 0.5);
    }
    
    .articles h2 {
      color: #333;
      text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
    }
    
    .articles ul {
      list-style: none;
      padding: 0;
      font-size: 16px;
      color: #333;
    }
    
    .articles ul li {
      margin: 10px 0;
    }
    
    .articles ul li a {
      color: #2b65ff;
      text-decoration: none;
      transition: all 0.3s ease;
      font-weight: bold;
    }
    
    .articles ul li a:hover {
      color: #0a4bff;
      text-shadow: 0 0 5px rgba(43, 101, 255, 0.5);
      transform: scale(1.1);
    }
    
    .stats {
      margin-top: 40px;
      text-align: center;
    }
    
    .stats-row {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
      margin: 20px 0;
    }
    
    .stats-card {
      max-width: 100%;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      transition: all 0.3s ease;
    }
    
    .stats-card:hover {
      transform: translateY(-10px);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
    }
    
    .contacts {
      background: linear-gradient(135deg, #fbc2eb, #a6c1ee);
      padding: 30px;
      border-radius: 15px;
      width: 80%;
      margin: 40px auto;
      box-shadow: 0 10px 30px rgba(166, 193, 238, 0.5);
      position: relative;
      overflow: hidden;
    }
    
    .contacts h2 {
      color: #333;
      text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
    }
    
    .contacts p {
      color: #555;
      font-size: 18px;
    }
    
    .contacts a {
      color: #2b65ff;
      text-decoration: none;
      transition: all 0.3s ease;
      font-weight: bold;
      position: relative;
    }
    
    .contacts a::after {
      content: '';
      position: absolute;
      bottom: -2px;
      left: 0;
      width: 100%;
      height: 2px;
      background: #2b65ff;
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.3s ease;
    }
    
    .contacts a:hover::after {
      transform: scaleX(1);
      transform-origin: left;
    }
    
    .footer {
      width: 100%;
      height: 140px;
      background: linear-gradient(45deg, #ff00ff, #00ffff, #ff00ff);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      border-radius: 50% 50% 0 0 / 100% 100% 0 0;
      margin-top: 40px;
    }
    
    .meme-container {
      text-align: center;
      margin: 20px 0;
    }
    
    .meme-img {
      max-width: 600px;
      width: 100%;
      border-radius: 15px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
      transition: all 0.3s ease;
    }
    
    .meme-img:hover {
      transform: scale(1.05);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
    }
    
    .neon-text {
      font-size: 30px;
      color: #fff;
      text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 30px #ff00ff;
      animation: neonGlow 1.5s ease-in-out infinite alternate;
    }
    
    @keyframes neonGlow {
      from { text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff; }
      to { text-shadow: 0 0 20px #ff00ff, 0 0 30px #ff00ff, 0 0 40px #ff00ff; }
    }
    
    .sparkles {
      position: absolute;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }
    
    .sparkle {
      position: absolute;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background-color: #fff;
      box-shadow: 0 0 10px #fff, 0 0 20px #ff00ff;
      animation: sparkle 2s infinite;
    }
    
    @keyframes sparkle {
      0% { transform: scale(0); opacity: 0; }
      50% { transform: scale(1); opacity: 1; }
      100% { transform: scale(0); opacity: 0; }
    }
    
    @media (max-width: 768px) {
      .about-me, .articles, .contacts {
        width: 95%;
      }
      
      .stats-row {
        flex-direction: column;
      }
      
      .header-text {
        font-size: 36px;
      }
      
      .typing-text span {
        font-size: 22px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="waving-header">
        <div class="header-text">Main Branch</div>
      </div>
      <div class="typing-text">
        <div class="typing-spans">
          <span>Добро пожаловать!</span>
          <span>Full-Stack и DevOps на максималках!</span>
          <span>React, Laravel, CI/CD, Docker...</span>
        </div>
      </div>
    </header>
    
    <div class="snake-animation"></div>
    
    <div class="about-me">
      <h2>Обо мне</h2>
      <p>
        Я Full-Stack разработчик. Работаю с Go, React, Laravel, Node.js и DevOps-инструментами, превращая творческие идеи в реальные проекты.
      </p>
    </div>
    
    <div class="tech-stack">
      <h2>🛠 Мой арсенал</h2>
      <div class="tech-badges">
        <div class="tech-badge react">React</div>
        <div class="tech-badge javascript">JavaScript</div>
        <div class="tech-badge laravel">Laravel</div>
        <div class="tech-badge nodejs">Node.js</div>
        <div class="tech-badge docker">Docker</div>
        <div class="tech-badge cicd">CI/CD</div>
        <div class="tech-badge typescript">TypeScript</div>
      </div>
    </div>
    
    <div class="projects">
      <h2 class="neon-text">🚀 Проекты</h2>
      <div class="project-cards">
        <div class="project-card">
          <h3>Lorem Ipsum</h3>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          </p>
        </div>
        <div class="project-card">
          <h3>Lorem Ipsum</h3>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          </p>
        </div>
      </div>
    </div>
    
    <div class="articles">
      <h2>📝 Последние статьи</h2>
      <ul>
        <li><a href="https://yourblog.com/post1">Lorem Ipsum</a></li>
        <li><a href="https://yourblog.com/post2">Lorem Ipsum</a></li>
      </ul>
    </div>
    
    <div class="stats">
      <div class="stats-row">
        <div class="stats-card">
          <img src="https://github-profile-trophy.vercel.app/?username=YourUsername&theme=onedark&no-frame=true&no-bg=true&row=1&column=6" alt="trophy" />
        </div>
      </div>
      <div class="stats-row">
        <div class="stats-card">
          <img src="/api/placeholder/800/300" alt="activity graph" />
        </div>
      </div>
      <div class="stats-row">
        <div class="stats-card">
          <img src="/api/placeholder/600/200" alt="streak stats" />
        </div>
      </div>
      <div class="stats-row">
        <div class="stats-card">
          <img src="/api/placeholder/450/180" alt="GitHub Stats" />
        </div>
        <div class="stats-card">
          <img src="/api/placeholder/450/180" alt="Top Languages" />
        </div>
      </div>
    </div>
    
    <div class="contacts">
      <h2>📫 Контакты</h2>
      <p>
        Пишите на <a href="mailto:your.email@example.com">email</a> 
        или найдите меня на <a href="https://www.linkedin.com/in/yourprofile">LinkedIn</a>.
      </p>
    </div>
    
    <div class="meme-container">
      <img class="meme-img" src="/api/placeholder/600/400" alt="Известный мем" />
    </div>
  </div>
  
  <div class="footer"></div>
  
  <div class="sparkles" id="sparkles"></div>
  
  <script>
    // Typing effect
    const typingSpans = document.querySelectorAll('.typing-spans span');
    let currentSpan = 0;
    
    setInterval(() => {
      typingSpans[currentSpan].style.display = 'none';
      currentSpan = (currentSpan + 1) % typingSpans.length;
      typingSpans[currentSpan].style.display = 'inline-block';
    }, 4000);
    
    // Create sparkles
    const sparklesContainer = document.getElementById('sparkles');
    const sparklesCount = 50;
    
    for (let i = 0; i < sparklesCount; i++) {
      const sparkle = document.createElement('div');
      sparkle.classList.add('sparkle');
      sparkle.style.left = `${Math.random() * 100}%`;
      sparkle.style.top = `${Math.random() * 100}%`;
      sparkle.style.animationDelay = `${Math.random() * 2}s`;
      sparklesContainer.appendChild(sparkle);
    }
  </script>
</body>
</html>
