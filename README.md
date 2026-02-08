<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Be My Valentine ❤️</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  height: 100vh;
  overflow: hidden;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(-45deg, #ff4d6d, #ff758c, #ff9a9e, #fad0c4);
  background-size: 400% 400%;
  animation: bgMove 10s ease infinite;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

@keyframes bgMove {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Floating hearts */
.heart {
  position: absolute;
  animation: floatUp linear infinite;
  opacity: 0.8;
}

@keyframes floatUp {
  from { transform: translateY(100vh); opacity: 0; }
  to { transform: translateY(-10vh); opacity: 1; }
}

.container {
  text-align: center;
  padding: 20px;
}

h1 { font-size: 2.2rem; }
h2 { font-weight: normal; }

.buttons {
  position: relative;
  height: 140px;
}

button {
  padding: 15px 35px;
  font-size: 1.2rem;
  border: none;
  border-radius: 30px;
  cursor: pointer;
}

#yesBtn {
  background: #fff;
  color: #ff4d6d;
}

#noBtn {
  position: absolute;
  background: #ff4d6d;
  color: white;
}

/* Shake animation */
@keyframes shake {
  0% { transform: translate(0); }
  25% { transform: translate(5px); }
  50% { transform: translate(-5px); }
  75% { transform: translate(5px); }
  100% { transform: translate(0); }
}

/* Final page */
#finalPage { display: none; }

.countdown {
  margin-top: 10px;
  font-size: 1.3rem;
}

img {
  margin-top: 20px;
  max-width: 90%;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}

/* Confetti */
.confetti {
  position: fixed;
  width: 10px;
  height: 10px;
  background: red;
  animation: fall 3s linear forwards;
}

@keyframes fall {
  to { transform: translateY(100vh) rotate(360deg); }
}
</style>
</head>

<body>

<audio id="music" loop>
  <source src="music.mp3" type="audio/mpeg">
</audio>

<div class="container" id="questionPage">
  <h1>Hey Kervi 💖<br>Will you be my Valentine?</h1>
  <div class="buttons">
    <button id="yesBtn">Yes ❤️</button>
    <button id="noBtn">No 🙄</button>
  </div>
</div>

<div class="container" id="finalPage">
  <h1>I knew you’d say yes 😌💘</h1>
  <h2>Then it’s a date 🥰</h2>
  <div class="countdown" id="countdown"></div>
  <img id="surprise" src="surprise.jpg" alt="Surprise">
</div>

<script>
const noBtn = document.getElementById("noBtn");
const yesBtn = document.getElementById("yesBtn");
const questionPage = document.getElementById("questionPage");
const finalPage = document.getElementById("finalPage");
const music = document.getElementById("music");
const surprise = document.getElementById("surprise");

let chaos = 1;

/* NO button chaos */
function moveNo() {
  chaos += 0.4;
  noBtn.style.animation = "shake 0.3s";
  setTimeout(() => noBtn.style.animation = "", 300);

  const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
  const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
  noBtn.style.left = x + "px";
  noBtn.style.top = y + "px";
}

noBtn.addEventListener("mouseenter", moveNo);
noBtn.addEventListener("touchstart", moveNo);

/* YES click */
yesBtn.addEventListener("click", () => {
  questionPage.style.display = "none";
  finalPage.style.display = "block";
  music.play();
  confettiBlast();
});

/* Hearts generator */
setInterval(() => {
  const h = document.createElement("div");
  h.className = "heart";
  h.innerHTML = "❤️";
  h.style.left = Math.random() * 100 + "vw";
  h.style.fontSize = Math.random() * 20 + 15 + "px";
  h.style.animationDuration = Math.random() * 3 + 4 + "s";
  document.body.appendChild(h);
  setTimeout(() => h.remove(), 7000);
}, 300);

/* Countdown */
const targetDate = new Date("Feb 14, 2026 19:00:00").getTime();
setInterval(() => {
  const now = Date.now();
  const d = targetDate - now;
  if (d <= 0) {
    countdown.innerHTML = "It's date time 😍";
    return;
  }
  const days = Math.floor(d / (1000*60*60*24));
  const hrs = Math.floor((d/(1000*60*60))%24);
  const mins = Math.floor((d/(1000*60))%60);
  countdown.innerHTML = `Countdown: ${days}d ${hrs}h ${mins}m 💕`;
}, 1000);

/* Confetti */
function confettiBlast() {
  for (let i = 0; i < 150; i++) {
    const c = document.createElement("div");
    c.className = "confetti";
    c.style.left = Math.random() * 100 + "vw";
    c.style.background = `hsl(${Math.random()*360},100%,50%)`;
    document.body.appendChild(c);
    setTimeout(() => c.remove(), 3000);
  }
}

/* Easter egg */
let pressTimer;
surprise.addEventListener("touchstart", () => {
  pressTimer = setTimeout(() => {
    alert("You’re stuck with me now 😏❤️");
  }, 800);
});
surprise.addEventListener("touchend", () => clearTimeout(pressTimer));
</script>

</body>
</html>