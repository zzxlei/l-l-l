<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>🎂 Happy Birthday 🎂</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
    background: linear-gradient(135deg, #ffe0ec, #ffd6e0, #ffccd5);
    min-height: 100vh;
    overflow: hidden;
    color: #d4467a;
  }

  /* 密码页 */
  #passwordPage {
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    background: linear-gradient(135deg, #ffe0ec, #ffd6e0);
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    z-index: 1000;
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  #passwordPage.hide {
    opacity: 0; transform: scale(1.1); pointer-events: none;
  }
  .emoji-hint { font-size: 60px; margin-bottom: 20px; animation: bounce 1.5s infinite; }
  @keyframes bounce {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-15px); }
  }
  .pwd-title { font-size: 22px; margin-bottom: 25px; color: #c44569; font-weight: bold; }
  .pwd-input {
    width: 220px; padding: 14px 20px; border: 2px solid #f8a5c2;
    border-radius: 30px; font-size: 20px; text-align: center;
    outline: none; background: rgba(255,255,255,0.8); color: #d4467a;
    letter-spacing: 8px;
  }
  .pwd-input:focus { border-color: #d4467a; box-shadow: 0 0 15px rgba(212,70,122,0.3); }
  .pwd-btn {
    margin-top: 20px; padding: 12px 50px; background: linear-gradient(135deg, #f8a5c2, #d4467a);
    border: none; border-radius: 30px; color: white; font-size: 18px;
    cursor: pointer; box-shadow: 0 5px 20px rgba(212,70,122,0.4);
    transition: transform 0.3s;
  }
  .pwd-btn:active { transform: scale(0.95); }
  .pwd-error { color: #e74c3c; margin-top: 12px; font-size: 14px; min-height: 20px; }

  /* 主内容滚动容器 */
  #mainContent {
    height: 100vh; overflow-y: auto; scroll-behavior: smooth;
    -webkit-overflow-scrolling: touch;
    opacity: 0; transition: opacity 1s ease 0.5s;
  }
  #mainContent.show { opacity: 1; }

  /* 每个场景 */
  .scene {
    min-height: 100vh; display: flex; flex-direction: column;
    align-items: center; justify-content: center; padding: 40px 30px;
    position: relative;
  }

  /* 照片展示 */
  .photo-frame {
    width: 280px; height: 350px; border-radius: 20px;
    background: white; padding: 12px; box-shadow: 0 10px 40px rgba(212,70,122,0.2);
    margin-bottom: 30px; position: relative; overflow: hidden;
  }
  .photo-frame img {
    width: 100%; height: 100%; object-fit: cover; border-radius: 12px;
  }
  .photo-switch {
    display: flex; gap: 10px; margin-bottom: 20px;
  }
  .photo-dot {
    width: 12px; height: 12px; border-radius: 50%; background: #f8a5c2;
    cursor: pointer; transition: all 0.3s; border: none;
  }
  .photo-dot.active { background: #d4467a; transform: scale(1.3); }

  /* 文字样式 */
  .scene-title {
    font-size: 28px; font-weight: bold; margin-bottom: 15px;
    background: linear-gradient(135deg, #d4467a, #f8a5c2);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    text-align: center;
  }
  .scene-text {
    font-size: 16px; line-height: 1.8; color: #c44569;
    text-align: center; max-width: 320px; opacity: 0.9;
  }

  /* 祝福页特效 */
  .blessing-big {
    font-size: 42px; font-weight: bold; margin-bottom: 20px;
    animation: pulse 2s infinite;
    background: linear-gradient(135deg, #d4467a, #ff6b9d, #f8a5c2);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  @keyframes pulse {
    0%,100% { transform: scale(1); }
    50% { transform: scale(1.05); }
  }

  /* 飘落爱心 */
  .heart {
    position: fixed; top: -20px; font-size: 20px; color: #f8a5c2;
    animation: fall linear forwards; pointer-events: none; z-index: 999;
  }
  @keyframes fall {
    to { transform: translateY(110vh) rotate(360deg); opacity: 0; }
  }

  /* 滚动提示 */
  .scroll-hint {
    position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
    font-size: 12px; color: #d4467a; opacity: 0.6;
    animation: fadeInOut 2s infinite;
  }
  @keyframes fadeInOut {
    0%,100% { opacity: 0.3; }
    50% { opacity: 0.8; }
  }
</style>
</head>
<body>

<!-- 密码页 -->
<div id="passwordPage">
  <div class="emoji-hint">🎂</div>
  <div class="pwd-title">输入生日密码解锁惊喜</div>
  <input type="password" class="pwd-input" id="pwdInput" maxlength="4" placeholder="····">
  <button class="pwd-btn" id="pwdBtn">解锁 🎀</button>
  <div class="pwd-error" id="pwdError"></div>
</div>

<!-- 主内容 -->
<div id="mainContent">

  <!-- 场景1：开场 -->
  <div class="scene">
    <div class="scene-title">✨ 今天是个特别的日子 ✨</div>
    <div class="scene-text">
      有些日子， 
      值得被温柔记住。 
      比如今天， 
      比如你。🎀
    </div>
  </div>

  <!-- 场景2：照片展示 -->
  <div class="scene">
    <div class="scene-title">📸 我们的时光</div>
    <div class="photo-frame">
      <img id="currentPhoto" src="https://picsum.photos/400/500?random=1" alt="照片">
    </div>
    <div class="photo-switch" id="photoDots"></div>
    <div class="scene-text">每一帧，都是心动的证据 💕</div>
  </div>

  <!-- 场景3：回忆 -->
  <div class="scene">
    <div class="scene-title">🌸 关于你的小事</div>
    <div class="scene-text">
      喜欢你笑起来的弧度， 
      喜欢你认真时的侧脸， 
      喜欢你存在本身， 
      就是这个世界给我的 
      最好的礼物。🎁
    </div>
  </div>

  <!-- 场景4：祝福 -->
  <div class="scene">
    <div class="blessing-big">🎂 生日快乐 🎂</div>
    <div class="scene-title">愿你的新一岁</div>
    <div class="scene-text">
      被爱包围，被温柔以待， 
      想要的都拥有，得不到的都释怀， 
      眼里有光，心中有爱， 
      活成自己喜欢的模样。🌷  
      我会一直在。💗
    </div>
  </div>

</div>

<div class="scroll-hint" id="scrollHint">↓ 慢慢向下滑动 ↓</div>

<script>
  // ========== 照片配置（替换成你自己的照片链接）==========
  const photos = [
    "https://picsum.photos/400/500?random=1",
    "https://picsum.photos/400/500?random=2",
    "https://picsum.photos/400/500?random=3",
    "https://picsum.photos/400/500?random=4"
  ];
  // ========================================================

  let currentIdx = 0;
  const pwdInput = document.getElementById('pwdInput');
  const pwdBtn = document.getElementById('pwdBtn');
  const pwdError = document.getElementById('pwdError');
  const passwordPage = document.getElementById('passwordPage');
  const mainContent = document.getElementById('mainContent');
  const scrollHint = document.getElementById('scrollHint');

  // 密码验证
  function checkPassword() {
    if (pwdInput.value === '0823') {
      passwordPage.classList.add('hide');
      mainContent.classList.add('show');
      setTimeout(() => { passwordPage.style.display = 'none'; }, 800);
      startHearts();
      initPhotos();
    } else {
      pwdError.textContent = '密码不对哦，再试试～';
      pwdInput.value = '';
      pwdInput.style.borderColor = '#e74c3c';
      setTimeout(() => { pwdInput.style.borderColor = '#f8a5c2'; }, 1000);
    }
  }

  pwdBtn.addEventListener('click', checkPassword);
  pwdInput.addEventListener('keydown', e => { if (e.key === 'Enter') checkPassword(); });

  // 照片切换
  function initPhotos() {
    const dotsContainer = document.getElementById('photoDots');
    photos.forEach((_, i) => {
      const dot = document.createElement('button');
      dot.className = 'photo-dot' + (i === 0 ? ' active' : '');
      dot.addEventListener('click', () => switchPhoto(i));
      dotsContainer.appendChild(dot);
    });
    // 自动轮播
    setInterval(() => {
      switchPhoto((currentIdx + 1) % photos.length);
    }, 3000);
  }

  function switchPhoto(idx) {
    currentIdx = idx;
    const img = document.getElementById('currentPhoto');
    img.style.opacity = 0;
    setTimeout(() => {
      img.src = photos[idx];
      img.style.opacity = 1;
    }, 300);
    document.querySelectorAll('.photo-dot').forEach((d, i) => {
      d.classList.toggle('active', i === idx);
    });
  }

  // 飘落爱心
  function startHearts() {
    setInterval(() => {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.textContent = ['💕', '🎀', '✨', '🌸', '💗'][Math.floor(Math.random() * 5)];
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = (3 + Math.random() * 4) + 's';
      heart.style.fontSize = (14 + Math.random() * 16) + 'px';
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 7000);
    }, 400);
  }

  // 滚动到底隐藏提示
  mainContent.addEventListener('scroll', () => {
    if (mainContent.scrollTop > 100) scrollHint.style.display = 'none';
  });
</script>
</body>
</html>
