# newyear
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>2026 新年快乐 - 马年大吉</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; } body {
font-family: 'Microsoft YaHei', sans-serif;
background: linear-gradient(135deg, #8e0000 0%, #520000 100%);
color: #FFF;
min-height: 100vh;
overflow-x: hidden;
position: relative;
} /* 雪花动画 */
.snowflake {
position: absolute;
background: white;
border-radius: 50%;
filter: blur(1px);
animation: fall linear infinite;
} @keyframes fall {
to { transform: translateY(100vh) rotate(360deg); }
} /* 内容区域 */
.container {
position: relative;
z-index: 10;
text-align: center;
padding: 15vh 20px 5vh;
max-width: 1200px;
margin: 0 auto;
} h1 {
font-size: 4rem;
text-shadow: 0 0 20px #ffcc00, 0 0 30px #ff9900;
margin-bottom: 1rem;
animation: glow 2s infinite alternate;
} h2 {
font-size: 2rem;
margin-bottom: 2rem;
color: #FFD700;
} /* 倒计时样式 */
#countdown {
display: flex;
justify-content: center;
gap: 15px;
margin: 2rem 0;
} .countdown-unit {
background: rgba(0, 0, 0, 0.3);
padding: 15px;
border-radius: 10px;
min-width: 80px;
} .countdown-value {
font-size: 2.5rem;
font-weight: bold;
} /* 祝福按钮 */
.wish-btn {
background: #FFD700;
color: #8e0000;
border: none;
padding: 15px 40px;
font-size: 1.2rem;
border-radius: 50px;
cursor: pointer;
margin: 1rem;
transition: all 0.3s;
font-weight: bold;
} .wish-btn:hover {
transform: scale(1.05);
box-shadow: 0 0 20px #ffcc00;
} /* 祝福语弹出层 */
#wishModal {
position: fixed;
top: 50%;
left: 50%;
transform: translate(-50%, -50%) scale(0);
background: rgba(255, 255, 255, 0.95);
color: #8e0000;
padding: 30px;
border-radius: 15px;
max-width: 80%;
z-index: 100;
transition: transform 0.5s;
text-align: center;
} /* 祝福输入区 */
.wish-input-area {
margin: 40px auto;
max-width: 600px;
padding: 20px;
background: rgba(255, 255, 255, 0.1);
border-radius: 15px;
} textarea {
width: 100%;
height: 120px;
padding: 15px;
border-radius: 10px;
border: 2px solid #FFD700;
background: rgba(0, 0, 0, 0.3);
color: white;
font-size: 1rem;
resize: vertical;
margin-bottom: 15px;
} textarea::placeholder {
color: #ccc;
} /* 祝福展示页面 */
.wish-wall {
padding: 20px;
display: grid;
grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
gap: 20px;
margin: 20px auto;
max-width: 1200px;
} .wish-card {
background: linear-gradient(145deg, #ffcc0050, #ff990020);
border-radius: 15px;
padding: 20px;
border-left: 4px solid #FFD700;
box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
transition: transform 0.3s;
} .wish-card:hover {
transform: translateY(-5px);
} .wish-author {
display: flex;
align-items: center;
margin-bottom: 10px;
} .author-avatar {
width: 40px;
height: 40px;
border-radius: 50%;
background: #FFD700;
margin-right: 10px;
display: flex;
align-items: center;
justify-content: center;
font-weight: bold;
color: #8e0000;
} .author-name {
font-weight: bold;
color: #FFD700;
} .wish-content {
line-height: 1.6;
} .wish-time {
text-align: right;
font-size: 0.8rem;
color: #aaa;
margin-top: 10px;
} /* 响应式适配 */
@media (max-width: 768px) {
h1 { font-size: 2.5rem; }
h2 { font-size: 1.5rem; }
.countdown-value { font-size: 1.8rem; }
.wish-wall {
grid-template-columns: 1fr;
}
} /* 导航按钮 */
.nav-btn {
position: fixed;
top: 20px;
right: 20px;
z-index: 1000;
}
</style>
</head>
<body>
<!-- 雪花容器 -->
<div id="snowflakes"></div> <!-- 导航按钮 -->
<div class="nav-btn">
<button class="wish-btn" id="viewWallsBtn">查看祝福墙</button>
</div> <!-- 主内容区 -->
<div class="container">
<h1>2026 新年快乐</h1>
<h2>蛇年辞旧岁 · 马年迎新春</h2> <div id="countdown">
<div class="countdown-unit">
<div class="countdown-value" id="days">00</div>
<div>天</div>
</div>
<div class="countdown-unit">
<div class="countdown-value" id="hours">00</div>
<div>时</div>
</div>
<div class="countdown-unit">
<div class="countdown-value" id="minutes">00</div>
<div>分</div>
</div>
<div class="countdown-unit">
<div class="countdown-value" id="seconds">00</div>
<div>秒</div>
</div>
</div> <button class="wish-btn" id="randomWishBtn">接收新年祝福</button> <!-- 用户祝福输入区 -->
<div class="wish-input-area">
<h3>留下您的新年祝福</h3>
<textarea id="userWish" placeholder="写下您的新年祝福..."></textarea>
<div>
<input type="text" id="userName" placeholder="您的名字（可选）" style="width: 200px; padding: 10px; border-radius: 50px; border: 2px solid #FFD700; background: rgba(0,0,0,0.3); color: white; text-align: center; margin-right: 10px;">
<button class="wish-btn" id="submitWishBtn">提交祝福</button>
</div>
</div> <!-- 祝福墙展示区 -->
<div id="wishWallContainer" style="display: none;">
<h2 style="margin: 30px 0; color: #FFD700;">新年祝福墙</h2>
<div class="wish-wall" id="wishWall"></div>
<button class="wish-btn" id="backToHomeBtn">返回首页</button>
</div>
</div> <!-- 祝福弹窗 -->
<div id="wishModal">
<h3 style="margin-bottom: 20px;color: #d4af37">🎉 新年祝福 🎉</h3>
<p id="wishText" style="font-size: 1.2rem;line-height: 1.6;"></p >
</div> <script>
// 创建雪花
function createSnowflakes() {
const container = document.getElementById('snowflakes');
for (let i = 0; i < 50; i++) {
const snowflake = document.createElement('div');
snowflake.classList.add('snowflake'); // 随机属性
const size = Math.random() * 5 + 2;
const startX = Math.random() * 100;
const duration = Math.random() * 5 + 5;
const delay = Math.random() * 5; snowflake.style.width = `${size}px`;
snowflake.style.height = `${size}px`;
snowflake.style.left = `${startX}vw`;
snowflake.style.animationDuration = `${duration}s`;
snowflake.style.animationDelay = `${delay}s`; container.appendChild(snowflake);
}
} // 新年倒计时（2026年1月1日）
function updateCountdown() {
const now = new Date();
const newYear = new Date(2026, 0, 1);
const diff = newYear - now; const days = Math.floor(diff / (1000 * 60 * 60 * 24));
const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
const seconds = Math.floor((diff % (1000 * 60)) / 1000); document.getElementById('days').textContent = days.toString().padStart(2, '0');
document.getElementById('hours').textContent = hours.toString().padStart(2, '0');
document.getElementById('minutes').textContent = minutes.toString().padStart(2, '0');
document.getElementById('seconds').textContent = seconds.toString().padStart(2, '0');
} // 祝福语库
const wishes = [
"愿您在新的一年里，如骏马奔腾，事业蒸蒸日上！",
"蛇年丰收满载归，马年吉祥福满门！",
"祝您身体健康如龙马，财源广进似江海！",
"新年新气象，万事皆顺意，阖家幸福安康！",
"马蹄声声辞旧岁，福气满满迎新春！"
]; // 随机祝福语
function showRandomWish() {
const modal = document.getElementById('wishModal');
const text = document.getElementById('wishText'); text.textContent = wishes[Math.floor(Math.random() * wishes.length)];
modal.style.transform = 'translate(-50%, -50%) scale(1)'; // 3秒后关闭
setTimeout(() => {
modal.style.transform = 'translate(-50%, -50%) scale(0)';
}, 3000);
} // 祝福数据存储
const WISH_KEY = 'newYearWishes';
let wishList = JSON.parse(localStorage.getItem(WISH_KEY)) || []; // 保存祝福
function saveWish(wishText, userName) {
const newWish = {
id: Date.now(),
text: wishText,
author: userName || '匿名用户',
date: new Date().toLocaleString('zh-CN', {
year: 'numeric',
month: '2-digit',
day: '2-digit',
hour: '2-digit',
minute: '2-digit'
})
}; wishList.unshift(newWish);
localStorage.setItem(WISH_KEY, JSON.stringify(wishList));
} // 显示祝福墙
function showWishWall() {
document.querySelector('.container > h1').style.display = 'none';
document.querySelector('.container > h2').style.display = 'none';
document.getElementById('countdown').style.display = 'none';
document.getElementById('randomWishBtn').style.display = 'none';
document.querySelector('.wish-input-area').style.display = 'none';
document.getElementById('wishWallContainer').style.display = 'block'; renderWishWall();
} // 返回首页
function backToHome() {
document.querySelector('.container > h1').style.display = 'block';
document.querySelector('.container > h2').style.display = 'block';
document.getElementById('countdown').style.display = 'flex';
document.getElementById('randomWishBtn').style.display = 'inline-block';
document.querySelector('.wish-input-area').style.display = 'block';
document.getElementById('wishWallContainer').style.display = 'none';
} // 渲染祝福墙
function renderWishWall() {
const wishWall = document.getElementById('wishWall');
wishWall.innerHTML = ''; if (wishList.length === 0) {
wishWall.innerHTML = '<p style="grid-column:1/-1;text-align:center;padding:40px;">还没有祝福，快来留下第一条祝福吧！</p >';
return;
} wishList.forEach(wish => {
const wishCard = document.createElement('div');
wishCard.className = 'wish-card'; // 获取首字母作为头像
const firstLetter = wish.author.charAt(0).toUpperCase(); wishCard.innerHTML = `
<div class="wish-author">
<div class="author-avatar">${firstLetter}</div>
<div class="author-name">${wish.author}</div>
</div>
<div class="wish-content">${wish.text}</div>
<div class="wish-time">${wish.date}</div>
`; wishWall.appendChild(wishCard);
});
} // 初始化
document.addEventListener('DOMContentLoaded', () => {
createSnowflakes();
updateCountdown();
setInterval(updateCountdown, 1000); // 按钮事件绑定
document.getElementById('randomWishBtn').addEventListener('click', showRandomWish);
document.getElementById('viewWallsBtn').addEventListener('click', showWishWall);
document.getElementById('backToHomeBtn').addEventListener('click', backToHome); // 提交祝福
document.getElementById('submitWishBtn').addEventListener('click', () => {
const wishText = document.getElementById('userWish').value.trim();
const userName = document.getElementById('userName').value.trim(); if (!wishText) {
alert('请填写您的祝福内容');
return;
} saveWish(wishText, userName);
document.getElementById('userWish').value = '';
document.getElementById('userName').value = ''; // 显示成功提示
const modal = document.getElementById('wishModal');
const text = document.getElementById('wishText'); text.textContent = '您的祝福已成功提交！';
modal.style.transform = 'translate(-50%, -50%) scale(1)'; setTimeout(() => {
modal.style.transform = 'translate(-50%, -50%) scale(0)';
}, 2000);
});
});
</script>
</body>
</html>
