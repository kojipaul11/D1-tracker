# D1-tracker

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#111318">
<title>Diamond OS</title>
<style>
:root{color-scheme:dark;--bg:#111318;--panel:#1b1e25;--line:#30343e;--muted:#9ba3b4;--green:#b5f36b;--white:#f5f7fa}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--white);font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif}
header{padding:25px 18px 18px;border-bottom:1px solid var(--line)}
.eyebrow{font-size:11px;letter-spacing:2px;color:var(--green);font-weight:800}
h1{font-size:30px;margin:7px 0 3px;letter-spacing:-1px}
p{color:var(--muted);line-height:1.5}
header p{margin:0;font-size:13px}
nav{display:flex;gap:8px;padding:13px;overflow-x:auto;border-bottom:1px solid var(--line)}
nav button{white-space:nowrap}
button{border:1px solid var(--line);background:#242832;color:var(--white);border-radius:10px;padding:11px 14px;font-weight:700;font-size:13px}
button.active,.primary{background:var(--green);color:#141710;border-color:var(--green)}
main{padding:18px;max-width:760px;margin:auto}
h2{font-size:21px;margin:8px 0 5px}
h3{font-size:15px;margin:0 0 12px}
.small{font-size:12px;color:var(--muted)}
.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px;margin:17px 0}
.card{background:var(--panel);border:1px solid var(--line);border-radius:15px;padding:15px;margin:10px 0}
.metric{font-size:25px;font-weight:800;margin:8px 0 2px}
.metric-label{font-size:12px;color:var(--muted)}
.section{margin-top:22px}
label{display:block;color:var(--muted);font-size:12px;margin:12px 0 6px}
input,select,textarea{width:100%;background:#111318;color:var(--white);border:1px solid var(--line);border-radius:9px;padding:12px;font:inherit}
textarea{min-height:75px;resize:vertical}
.row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
button.full{width:100%;margin-top:12px}
.item{padding:12px 0;border-bottom:1px solid var(--line)}
.item:last-child{border-bottom:0}
.pill{display:inline-block;background:#293323;color:var(--green);padding:5px 8px;border-radius:6px;font-size:11px;font-weight:800}
.hidden{display:none}
footer{text-align:center;color:var(--muted);font-size:11px;padding:30px 10px}
canvas{width:100%;height:180px}
@media(min-width:600px){main{padding:26px}.grid{grid-template-columns:repeat(4,minmax(0,1fr))}}
</style>
</head>
<body>
<header>
  <div class="eyebrow">PLAYER DEVELOPMENT SYSTEM</div>
  <h1>DIAMOND OS<span style="color:var(--green)">.</span></h1>
  <p>Your work. Your numbers. Your progress.</p>
</header>
<nav id="nav">
  <button class="active" data-page="home">Dashboard</button>
  <button data-page="programs">Programs</button>
  <button data-page="log">Log Workout</button>
  <button data-page="progress">Progress</button>
</nav>
<main>
<section id="home">
  <div class="section">
    <span class="pill" id="today"></span>
    <h2>Today's mission.</h2>
    <p>Stack good days. Track the work. Trust the process.</p>
  </div>
  <div class="grid">
    <div class="card"><div class="metric" id="workouts">0</div><div class="metric-label">Workouts logged</div></div>
    <div class="card"><div class="metric" id="streak">0</div><div class="metric-label">Training days this week</div></div>
    <div class="card"><div class="metric" id="velo">—</div><div class="metric-label">Latest exit velo (mph)</div></div>
    <div class="card"><div class="metric" id="throw">—</div><div class="metric-label">Latest throwing velo (mph)</div></div>
  </div>
  <div class="card">
    <h3>QUICK ACTION</h3>
    <p>Finished training? Record the session while the details are fresh.</p>
    <button class="primary" onclick="showPage('log')">+ Log a workout</button>
  </div>
  <div class="card">
    <h3>RECENT TRAINING</h3>
    <div id="recent"><p class="small">Your logged workouts will show up here.</p></div>
  </div>
</section>

<section id="programs" class="hidden">
  <h2>Your training plan.</h2>
  <p>Edit your daily plan and organize your work across the week.</p>
  <div class="card">
    <label>Training date</label><input id="planDate" type="date">
    <label>Training category</label>
    <select id="planType"><option>Sprint / Speed</option><option>Hitting</option><option>Throwing</option><option>Lifting</option><option>Agility</option><option>Recovery</option><option>Conditioning</option></select>
    <label>Workout plan</label><textarea id="planText" placeholder="Example: Warm-up, 4 x 10-yard starts, 3 x 30-yard sprints, full recovery between reps."></textarea>
    <button class="primary full" onclick="savePlan()">Save training plan</button>
  </div>
  <div class="section"><h3>SAVED PLANS</h3><div id="planList"></div></div>
</section>

<section id="log" class="hidden">
  <h2>Log your work.</h2>
  <p>Save your session and keep your performance history on this device.</p>
  <div class="card">
    <label>Date</label><input id="logDate" type="date">
    <label>Workout type</label>
    <select id="logType"><option>Sprint / Speed</option><option>Hitting</option><option>Throwing</option><option>Lifting</option><option>Agility</option><option>Conditioning</option><option>Recovery</option></select>
    <div class="row">
      <div><label>Exit velocity (mph)</label><input id="exit" type="number" step="0.1" placeholder="e.g. 93"></div>
      <div><label>Bat speed (mph)</label><input id="bat" type="number" step="0.1" placeholder="e.g. 73"></div>
    </div>
    <div class="row">
      <div><label>Throwing velocity (mph)</label><input id="throwing" type="number" step="0.1" placeholder="e.g. 89"></div>
      <div><label>60-yard time (seconds)</label><input id="sixty" type="number" step="0.01" placeholder="e.g. 6.80"></div>
    </div>
    <label>Exercises, sets, reps, weights, sprint times</label>
    <textarea id="details" placeholder="Example: 3 x 10-yard starts; med ball rotational throws 3 x 5 each side."></textarea>
    <label>Notes</label><textarea id="notes" placeholder="How did the session feel? Anything to improve?"></textarea>
    <button class="primary full" onclick="saveWorkout()">Save workout</button>
  </div>
</section>

<section id="progress" class="hidden">
  <h2>Progress report.</h2>
  <p>Your saved measurements and training history.</p>
  <div class="card"><h3>EXIT VELOCITY</h3><canvas id="exitChart"></canvas><div id="exitHistory" class="small"></div></div>
  <div class="card"><h3>BAT SPEED</h3><canvas id="batChart"></canvas><div id="batHistory" class="small"></div></div>
  <div class="card"><h3>SPRINT TIMES — 60 YARDS</h3><canvas id="sprintChart"></canvas><div id="sprintHistory" class="small"></div></div>
  <div class="card"><h3>ALL WORKOUTS</h3><div id="allLogs"></div><button onclick="exportData()">Export my data</button> <button onclick="clearData()">Clear all data</button></div>
</section>
</main>
<footer>DIAMOND OS · BUILT FOR THE WORK · DATA STAYS IN THIS BROWSER</footer>
<script>
const $=id=>document.getElementById(id);
const read=(key,fallback=[])=>{try{return JSON.parse(localStorage.getItem(key))||fallback}catch{return fallback}};
let logs=read('diamondLogs'),plans=read('diamondPlans');
const today=new Date();
const localDate=d=>{const x=new Date(d.getTime()-d.getTimezoneOffset()*60000);return x.toISOString().slice(0,10)};
$('today').textContent=today.toLocaleDateString(undefined,{weekday:'long',month:'short',day:'numeric'}).toUpperCase();
$('logDate').value=localDate(today);$('planDate').value=localDate(today);
document.querySelectorAll('nav button').forEach(b=>b.addEventListener('click',()=>showPage(b.dataset.page)));
function showPage(page){
 document.querySelectorAll('main section').forEach(s=>s.classList.toggle('hidden',s.id!==page));
 document.querySelectorAll('nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===page));
 if(page==='home')renderHome();if(page==='programs')renderPlans();if(page==='progress')renderProgress();
 window.scrollTo(0,0);
}
function saveWorkout(){
 const obj={id:Date.now(),date:$('logDate').value||localDate(new Date()),type:$('logType').value,exit:$('exit').value,bat:$('bat').value,throwing:$('throwing').value,sixty:$('sixty').value,details:$('details').value,notes:$('notes').value};
 if(!obj.details.trim()&&!obj.notes.trim()&&!obj.exit&&!obj.bat&&!obj.throwing&&!obj.sixty){alert('Add a measurement or workout detail first.');return}
 logs.push(obj);localStorage.setItem('diamondLogs',JSON.stringify(logs));
 ['exit','bat','throwing','sixty','details','notes'].forEach(id=>$(id).value='');
 renderHome();alert('Workout saved on this device.');showPage('home');
}
function savePlan(){
 const obj={id:Date.now(),date:$('planDate').value||localDate(new Date()),type:$('planType').value,text:$('planText').value.trim()};
 if(!obj.text){alert('Add your workout plan first.');return}
 plans.push(obj);localStorage.setItem('diamondPlans',JSON.stringify(plans));$('planText').value='';renderPlans();alert('Training plan saved.');
}
function renderHome(){
 $('workouts').textContent=logs.length;
 const now=new Date(),monday=new Date(now);monday.setHours(0,0,0,0);monday.setDate(now.getDate()-((now.getDay()+6)%7));
 $('streak').textContent=new Set(logs.filter(l=>new Date(l.date+'T12:00:00')>=monday&&new Date(l.date+'T12:00:00')<=now).map(l=>l.date)).size;
 const last=(key)=>logs.slice().reverse().find(l=>l[key]!==''&&l[key]!=null);
 $('velo').textContent=last('exit')?.exit||'—';$('throw').textContent=last('throwing')?.throwing||'—';
 $('recent').innerHTML=logs.slice().reverse().slice(0,4).map(l=>`<div class="item"><strong>${esc(l.type)}</strong><div class="small">${esc(l.date)} · ${esc(l.details||l.notes||'Measurement logged')}</div></div>`).join('')||'<p class="small">No workouts logged yet.</p>';
}
function renderPlans(){
 $('planList').innerHTML=plans.slice().reverse().map(p=>`<div class="item"><span class="pill">${esc(p.type)}</span><p>${esc(p.date)}</p><div>${esc(p.text)}</div><button onclick="deletePlan(${p.id})">Delete</button></div>`).join('')||'<p class="small">No saved plans yet.</p>';
}
function deletePlan(id){plans=plans.filter(p=>p.id!==id);localStorage.setItem('diamondPlans',JSON.stringify(plans));renderPlans()}
function esc(v){return String(v??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function chart(id,key){
 const c=$(id),ctx=c.getContext('2d'),w=c.width=c.clientWidth*devicePixelRatio,h=c.height=180*devicePixelRatio;ctx.clearRect(0,0,w,h);
 const arr=logs.filter(l=>l[key]!==''&&Number(l[key])>0).slice().sort((a,b)=>a.date.localeCompare(b.date));
 if(!arr.length){ctx.fillStyle='#9ba3b4';ctx.font=`${12*devicePixelRatio}px sans-serif`;ctx.fillText('Log measurements to see your trend',12*devicePixelRatio,35*devicePixelRatio);return}
 const vals=arr.map(l=>Number(l[key])),min=Math.min(...vals),max=Math.max(...vals),pad=25*devicePixelRatio;
 ctx.strokeStyle='#30343e';ctx.lineWidth=devicePixelRatio;ctx.beginPath();ctx.moveTo(pad,pad);ctx.lineTo(pad,h-pad);ctx.lineTo(w-pad,h-pad);ctx.stroke();
 ctx.strokeStyle='#b5f36b';ctx.lineWidth=2*devicePixelRatio;ctx.beginPath();
 vals.forEach((v,i)=>{const x=pad+(vals.length===1?(w-2*pad)/2:i*(w-2*pad)/(vals.length-1)),y=h-pad-(v-min+(max===min?1:(max-min)*.1))/(max-min||1)*(h-2*pad);if(i===0)ctx.moveTo(x,y);else ctx.lineTo(x,y)});
 ctx.stroke();ctx.fillStyle='#b5f36b';vals.forEach((v,i)=>{const x=pad+(vals.length===1?(w-2*pad)/2:i*(w-2*pad)/(vals.length-1)),y=h-pad-(v-min+(max===min?1:(max-min)*.1))/(max-min||1)*(h-2*pad);ctx.beginPath();ctx.arc(x,y,3*devicePixelRatio,0,Math.PI*2);ctx.fill()});
}
function renderProgress(){
 chart('exitChart','exit');chart('batChart','bat');chart('sprintChart','sixty');
 const hist=(key)=>logs.filter(l=>l[key]!==''&&l[key]!=null).map(l=>`${esc(l.date)}: ${esc(l[key])}`).join(' · ')||'No measurements yet.';
 $('exitHistory').textContent=hist('exit');$('batHistory').textContent=hist('bat');$('sprintHistory').textContent=hist('sixty');
 $('allLogs').innerHTML=logs.slice().reverse().map(l=>`<div class="item"><strong>${esc(l.date)} — ${esc(l.type)}</strong><p class="small">Exit: ${esc(l.exit||'—')} · Bat: ${esc(l.bat||'—')} · Throw: ${esc(l.throwing||'—')} · 60 yd: ${esc(l.sixty||'—')}</p><p>${esc(l.details)} ${esc(l.notes)}</p><button onclick="deleteLog(${l.id})">Delete</button></div>`).join('')||'<p class="small">No saved workouts.</p>';
}
function deleteLog(id){logs=logs.filter(l=>l.id!==id);localStorage.setItem('diamondLogs',JSON.stringify(logs));renderProgress();renderHome()}
function exportData(){
 const blob=new Blob([JSON.stringify({logs,plans},null,2)],{type:'application/json'}),url=URL.createObjectURL(blob),a=document.createElement('a');
 a.href=url;a.download='diamond-os-backup.json';a.click();URL.revokeObjectURL(url);
}
function clearData(){if(confirm('Delete all saved workouts and plans on this device? This cannot be undone.')){logs=[];plans=[];localStorage.removeItem('diamondLogs');localStorage.removeItem('diamondPlans');renderProgress();renderHome()}}
renderHome();
</script>
</body>
</html>
