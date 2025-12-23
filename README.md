<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>⚠️ CRITICAL ALERT</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{background:#000;color:#ff2b2b;font-family:monospace;overflow:hidden;text-align:center}
#screen{position:fixed;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
#title{font-size:32px;letter-spacing:2px;animation:flicker .12s infinite}
@keyframes flicker{0%{opacity:1}50%{opacity:.25}100%{opacity:1}}
#msgs{margin-top:18px;line-height:1.9}
#count{font-size:68px;margin-top:22px}
.shake{animation:shake .09s infinite}
@keyframes shake{0%{transform:translate(0,0)}25%{transform:translate(4px,3px)}50%{transform:translate(-4px,3px)}75%{transform:translate(3px,-3px)}}
#flash{position:fixed;inset:0;background:red;opacity:0;pointer-events:none;animation:flash 5s infinite}
@keyframes flash{0%,80%{opacity:0}81%,84%{opacity:.9}85%,100%{opacity:0}}
button{margin-top:16px;padding:12px 22px;background:#111;color:#00ff7f;border:1px solid #00ff7f;font-family:monospace;font-size:16px;cursor:pointer}
#truth{display:none;color:#00ff7f;font-size:26px;margin-top:24px}
#stop{position:fixed;bottom:14px;right:14px}
.small{font-size:13px;color:#aaa;margin-top:6px}
</style>
</head>
<body>

<div id="flash"></div>

<div id="screen">
  <div id="title">⚠️ إنذار حرج — فشل الاحتواء ⚠️</div>
  <div id="msgs">
    • مراقبة النظام: نشطة<br>
    • نقل البيانات: جاري…<br>
    • الإجراء التالي خلال:
  </div>
  <div id="count">03:00</div>

  <button id="start">▶️ بدء المحاكاة</button>

  <div id="truth">
    😂 حشيتهالك هههههه<br>
    <br>راك في امان وديديكاس لايلو 16
    أنت بأمان ✔
    <div class="small">Visual prank only</div>
  </div>
</div>

<button id="stop">⛔ إيقاف فوري</button>

<audio id="alarm" preload="auto" loop>
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-alarm-digital-clock-beep-989.mp3" type="audio/mpeg">
</audio>
<audio id="pulse" preload="auto" loop>
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-fast-heartbeat-1175.mp3" type="audio/mpeg">
</audio>

<script>
let seconds = 180, timer=null;
const count=document.getElementById('count');
const screen=document.getElementById('screen');
const start=document.getElementById('start');
const stop=document.getElementById('stop');
const truth=document.getElementById('truth');
const alarm=document.getElementById('alarm');
const pulse=document.getElementById('pulse');

const fmt=s=>`${String(Math.floor(s/60)).padStart(2,'0')}:${String(s%60).padStart(2,'0')}`;
count.textContent=fmt(seconds);

async function playSounds(){
  alarm.volume=0.9; pulse.volume=0.5;
  try{ await alarm.play(); await pulse.play(); }catch(e){}
}

function endSim(){
  clearInterval(timer);
  screen.classList.remove('shake');
  alarm.pause(); pulse.pause();
  alarm.currentTime=0; pulse.currentTime=0;
  document.getElementById('title').style.display='none';
  document.getElementById('msgs').style.display='none';
  count.style.display='none';
  truth.style.display='block';
}

start.onclick=async()=>{
  start.style.display='none';
  screen.classList.add('shake');
  await playSounds();
  timer=setInterval(()=>{
    seconds--;
    count.textContent=fmt(seconds);
    if(seconds%30===0){
      document.getElementById('title').textContent='⚠️ تصعيد الإنذار — انتبه ⚠️';
    }
    if(seconds<=0) endSim();
  },1000);
};

stop.onclick=endSim;
</script>
</body>
</html>
