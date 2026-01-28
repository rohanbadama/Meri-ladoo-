<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For Someone Special 💖</title>

<style>
body{
  margin:0;
  font-family:'Segoe UI',sans-serif;
  background:radial-gradient(circle at top,#4b0d4f,#1f0524);
  color:white;
  text-align:center;
  overflow:hidden;
  transition:background 5s linear;
}

.screen{display:none;height:100vh;padding:30px;box-sizing:border-box;}
.active{display:block;animation:fade 1s;}
@keyframes fade{from{opacity:0;transform:translateY(20px)}to{opacity:1}}

button{
  background:linear-gradient(45deg,#ff4d88,#ff85a2);
  border:none;padding:12px 28px;border-radius:30px;
  color:white;font-size:18px;margin-top:20px;cursor:pointer;
  box-shadow:0 0 10px #ff4d88;
}

.cat{font-size:80px;animation:float 2.5s ease-in-out infinite;}
@keyframes float{50%{transform:translateY(-18px)}}

.bar{width:80%;height:15px;background:#ffffff22;margin:20px auto;border-radius:10px;}
.fill{height:100%;width:0;background:#ff4d88;transition:width 0.2s;}
.shake{animation:shake 0.4s linear 4;}
@keyframes shake{25%{transform:translateX(-8px)}50%{transform:translateX(8px)}75%{transform:translateX(-8px)}}

.reveal-box{background:#ffffff15;padding:15px;margin:12px;border-radius:15px;cursor:pointer;transition:0.3s;}
.revealed{background:#ff4d88;transform:scale(1.05)}

#typingText{
  max-width:90%;
  margin:auto;
  font-size:18px;
  line-height:1.6;
  min-height:140px;
  border-right:2px solid white;
}

.love-text{font-size:52px;color:#ff9acb;text-shadow:0 0 20px #ff4da6}

.text-shard{
  position:fixed;
  font-weight:bold;
  animation:fall 6s linear forwards;
}
@keyframes fall{
  to{transform:translateY(110vh) rotate(50deg);opacity:0;}
}

#fadeOverlay{
  position:fixed;inset:0;background:black;opacity:0;
  pointer-events:none;transition:opacity 6s linear;
}

/* Final black screen text */
#finalLine{
  position:fixed;
  inset:0;
  display:flex;
  align-items:center;
  justify-content:center;
  text-align:center;
  padding:20px;
  font-size:20px;
  line-height:1.6;
  opacity:0;
  color:white;
  background:black;
  transition:opacity 4s ease 3s;
}
</style>
</head>
<body>

<div id="fadeOverlay"></div>
<div id="finalLine">
Dekho itni pyaari ho ki “I Love You” bhi sambhal nahi paya…  
Aapko dekh ke vo bhi pighal ke gir gaya 🫠💖
</div>

<!-- 1 -->
<div class="screen active" id="s1">
  <div class="cat">😺</div>
  <h1>Hey cutiepie 🥰</h1>
  <p>Do you know how cute you are?</p>
  <button onclick="startExperience()">Let's check 💖</button>
</div>

<!-- 2 -->
<div class="screen" id="s2">
  <h2>Measuring your cuteness... ⏳</h2>
  <h1 id="percent">0%</h1>
  <div class="bar"><div class="fill" id="fill"></div></div>
  <p id="warn" style="display:none;">⚠️ TOO CUTE TO HANDLE!</p>
  <button id="next2" style="display:none;" onclick="next(3)">Continue ➜</button>
</div>

<!-- 3 -->
<div class="screen" id="s3">
  <h2>Tap each one 💌</h2>
  <div class="reveal-box" onclick="reveal(this,1)">Tap to reveal</div>
  <div class="reveal-box" onclick="reveal(this,2)">Tap to reveal</div>
  <div class="reveal-box" onclick="reveal(this,3)">Tap to reveal</div>
  <button onclick="next(4)">See more ➜</button>
</div>

<!-- 4 -->
<div class="screen" id="s4">
  <h2>A little note 💗</h2>
  <p>I’m truly sorry if I ever made you sad. You deserve only love and happiness 🌹</p>
  <button onclick="next(5); startTyping();">Open my heart ➜</button>
</div>

<!-- 5 -->
<div class="screen" id="s5">
  <div class="cat">😿</div>
  <p id="typingText"></p>
  <button onclick="next(6)">Last thing… ❤️</button>
</div>

<!-- 6 -->
<div class="screen" id="s6">
  <h1 class="love-text" id="loveText">I Love You ❤️</h1>
  <button onclick="shatterLove()">Touch My Heart 💔</button>
</div>

<audio id="music" loop>
  <source src="https://cdn.pixabay.com/audio/2022/10/25/audio_946f4dd0a6.mp3" type="audio/mp3">
</audio>

<script>
const music=document.getElementById("music");

function startExperience(){
  music.play().catch(()=>{});
  next(2);
  startMeter();
}

function next(n){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('s'+n).classList.add('active');
}

function startMeter(){
  let p=0;
  let i=setInterval(()=>{
    p+=2;
    percent.innerText=p+"%";
    fill.style.width=p+"%";
    if(p>=120){
      clearInterval(i);
      warn.style.display="block";
      next2.style.display="inline-block";
      s2.classList.add("shake");
    }
  },40);
}

function reveal(el,n){
  if(el.classList.contains("revealed")) return;
  if(n===1) el.innerText="I'm really sorry if I hurt you 🥺";
  if(n===2) el.innerText="You mean the world to me 💖";
  if(n===3) el.innerText="Please forgive me… I never want to lose you 💔";
  el.classList.add("revealed");
}

const message=`I never wanted to hurt you… not even for a second.
If my words ever made you feel small, I’m truly sorry.
You are the most beautiful part of my life.
Your smile is my peace, your happiness is my wish.
I promise to be better, to love you louder, and hold you tighter.
Please forgive me… because my heart has always been yours. 💔`;

function startTyping(){
  let i=0;
  const el=document.getElementById("typingText");
  function type(){
    if(i<message.length){
      el.innerHTML+=message.charAt(i);
      i++;
      setTimeout(type,35);
    } else {
      el.style.borderRight="none";
    }
  }
  type();
}

function shatterLove(){
  const textEl=document.getElementById("loveText");
  const rect=textEl.getBoundingClientRect();
  const words=["I","Love","You","❤️"];
  textEl.style.visibility="hidden";

  words.forEach((word,i)=>{
    const span=document.createElement("div");
    span.className="text-shard";
    span.innerText=word;
    span.style.left=(rect.left + i*rect.width/4)+"px";
    span.style.top=rect.top+"px";
    span.style.fontSize="42px";
    document.body.appendChild(span);
  });

  document.getElementById("fadeOverlay").style.opacity=1;

  // show final line after fade
  setTimeout(()=>{
    document.getElementById("finalLine").style.opacity=1;
  },4000);
}
</script>

</body>
</html>
