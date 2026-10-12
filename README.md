
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#101318">
<title>Diamond OS</title>
<style>
:root{color-scheme:dark;--bg:#101318;--panel:#1b2028;--line:#303744;--text:#f5f7fa;--muted:#a4adba;--accent:#c6f36a}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--text);font:16px -apple-system,BlinkMacSystemFont,sans-serif}
header{padding:24px 18px 16px;background:#171c23;border-bottom:1px solid var(--line)}
h1{margin:0;font-size:27px;letter-spacing:-1px}h1 span{color:var(--accent)}
header p{color:var(--muted);margin:7px 0 0;font-size:13px}
main{max-width:760px;margin:auto;padding:16px 14px 90px}
nav{display:flex;gap:8px;overflow:auto;padding:12px 0}
button,.tab{border:1px solid var(--line);background:var(--panel);color:var(--text);padding:11px 13px;border-radius:10px;font-weight:650;cursor:pointer}
button.primary,.tab.active{background:var(--accent);color:#111;border-color:var(--accent)}
button.danger{color:#ff9d9d}
.card{background:var(--panel);border:1px solid var(--line);border-radius:15px;padding:15px;margin:12px 0}
h2{font-size:19px;margin:0 0 13px}h3{font-size:15px;margin:0 0 10px}
label{display:block;color:var(--muted);font-size:12px;margin:10px 0 5px}
input,select,textarea{width:100%;padding:12px;border-radius:9px;border:1px solid var(--line);background:#11151b;color:var(--text);font:inherit}
textarea{min-height:75px;resize:vertical}
.row{display:flex;gap:9px;align-items:center}.row>*{flex:1;min-width:0}
.small{font-size:12px;color:var(--muted)}.muted{color:var(--muted)}
.exercise{border:1px solid var(--line);padding:12px;border-radius:12px;margin:9px 0}
.exercise-top{display:flex;gap:10px;align-items:center}
.exercise-top input[type=checkbox]{width:21px;height:21px;accent-color:var(--accent);flex-shrink:0}
.exercise-name{font-weight:700;flex:1}
.exercise-fields{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:8px}
.exercise-fields input{padding:9px}
.stats{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px}
.stat{background:#11151b;padding:14px;border-radius:12px}
.stat strong{font-size:23px;display:block}.stat span{font-size:12px;color:var(--muted)}
.hidden{display:none!important}
.metric{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.barrow{margin:12px 0}.barlabel{display:flex;justify-content:space-between;font-size:13px;margin-bottom:5px}
.barbg{height:10px;border-radius:20px;background:#303744;overflow:hidden}
.bar{height:100%;background:var(--accent);border-radius:20px}
footer{color:var(--muted);font-size:12px;text-align:center;padding:16px}
@media(min-width:600px){.stats{grid-template-columns:repeat(4,minmax(0,1fr))}}
</style>
</head>
<body>
<header>
  <h1>DIAMOND <span>OS</span></h1>
  <p>YOUR TRAINING. YOUR DATA. YOUR PROGRESS.</p>
</header>
<main>
  <div class="stats">
    <div class="stat"><strong id="doneCount">0</strong><span>Exercises completed today</span></div>
    <div class="stat"><strong id="sleepStat">—</strong><span>Hours of sleep</span></div>
    <div class="stat"><strong id="streakStat">0%</strong><span>Today's completion</span></div>
    <div class="stat"><strong id="monthStat">—</strong><span>Current program month</span></div>
  </div>

  <nav>
    <button class="tab active" data-page="workout">Workout</button>
    <button class="tab" data-page="program">Build program</button>
    <button class="tab" data-page="progress">Progress</button>
    <button class="tab" data-page="checkin">Daily check-in</button>
  </nav>

  <section id="workout" class="page">
    <div class="card">
      <h2>Today's training</h2>
      <div class="row">
        <div><label for="workDate">Workout date</label><input id="workDate" type="date"></div>
        <div><label for="workDay">Training day</label><select id="workDay">
          <option>Monday</option><option>Tuesday</option><option>Wednesday</option>
          <option>Thursday</option><option>Friday</option><option>Saturday</option><option>Sunday</option>
        </select></div>
      </div>
      <p class="small">Your selected month's exercises repeat each week on their assigned days.</p>
    </div>
    <div class="card">
      <h2 id="dayTitle">Exercises</h2>
      <div id="exerciseList"></div>
      <button class="primary" id="saveWorkout">Save workout</button>
      <p id="saveStatus" class="small"></p>
    </div>
  </section>

  <section id="program" class="page hidden">
    <div class="card">
      <h2>Monthly program builder</h2>
      <label for="programMonth">Choose program month</label>
      <input type="month" id="programMonth">
      <p class="small">Build a separate program for each month. Your weekday exercises repeat each week until you change the month.</p>
      <label for="programDay">Choose weekday</label>
      <select id="programDay">
        <option>Monday</option><option>Tuesday</option><option>Wednesday</option>
        <option>Thursday</option><option>Friday</option><option>Saturday</option><option>Sunday</option>
      </select>
      <div id="builderList"></div>
      <div class="row">
        <button class="primary" id="addExercise">+ Add exercise</button>
        <button id="saveProgram">Save day</button>
      </div>
      <p id="programStatus" class="small"></p>
    </div>
    <div class="card">
      <h3>Morning reminders</h3>
      <p class="small">For a reliable reminder on your iPhone, open the Reminders app and create a daily reminder for your chosen morning time. A GitHub Pages website alone cannot guarantee notifications when closed.</p>
      <button id="reminderHelp">Show reminder steps</button>
      <p id="reminderSteps" class="small hidden">1. Open Apple's Reminders app. 2. Create a reminder called “Diamond OS — morning check-in.” 3. Set the date and your preferred morning time. 4. Choose Repeat → Daily.</p>
    </div>
  </section>

  <section id="progress" class="page hidden">
    <div class="card">
      <h2>Record performance</h2>
      <label for="metricDate">Date measured</label><input id="metricDate" type="date">
      <div class="metric">
        <div><label>Exit velocity (mph)</label><input id="exitVelo" type="number" step=".1" placeholder="e.g. 93"></div>
        <div><label>Bat speed (mph)</label><input id="batSpeed" type="number" step=".1" placeholder="e.g. 73"></div>
        <div><label>Throwing velocity (mph)</label><input id="throwVelo" type="number" step=".1" placeholder="e.g. 89"></div>
        <div><label>60-yard time (seconds)</label><input id="sixtyTime" type="number" step=".01" placeholder="e.g. 6.80"></div>
      </div>
      <button class="primary" id="saveMetrics" style="margin-top:14px">Save measurements</button>
      <p id="metricStatus" class="small"></p>
    </div>
    <div class="card">
      <h2>Progress graphs</h2>
      <label for="graphMetric">Choose metric</label>
      <select id="graphMetric">
        <option value="exitVelo">Exit velocity (mph)</option>
        <option value="batSpeed">Bat speed (mph)</option>
        <option value="throwVelo">Throwing velocity (mph)</option>
        <option value="sixtyTime">60-yard time (seconds)</option>
        <option value="sleep">Sleep (hours)</option>
      </select>
      <div id="graph"></div>
      <div id="metricHistory" class="small"></div>
    </div>
  </section>

  <section id="checkin" class="page hidden">
    <div class="card">
      <h2>Daily check-in</h2>
      <label for="checkDate">Date</label><input id="checkDate" type="date">
      <label for="sleepHours">Hours of sleep</label><input id="sleepHours" type="number" min="0" max="24" step=".25" placeholder="e.g. 8">
      <label for="feeling">How are you feeling today?</label>
      <select id="feeling"><option>Great</option><option>Good</option><option>Okay</option><option>Tired</option><option>Sore</option><option>Need recovery</option></select>
      <label for="dailyNotes">Notes, soreness, energy, or how the workout felt</label>
      <textarea id="dailyNotes" placeholder="How did you feel? What went well?"></textarea>
      <button class="primary" id="saveCheckin" style="margin-top:12px">Save check-in</button>
      <p id="checkinStatus" class="small"></p>
      <p class="small">Sleep must be entered manually. This website cannot directly read Apple Health sleep data.</p>
    </div>
  </section>
  <footer>Diamond OS · Saved locally in this browser on this device.</footer>
</main>

<script>
const $=id=>document.getElementById(id);
const days=["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"];
const today=new Date();
const dateStr=d=>d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0")+"-"+String(d.getDate()).padStart(2,"0");
const monthStr=d=>d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0");
$("workDate").value=dateStr(today);
$("checkDate").value=dateStr(today);
$("metricDate").value=dateStr(today);
$("programMonth").value=monthStr(today);
$("workDay").value=days[(today.getDay()+6)%7];

function read(key,fallback){try{return JSON.parse(localStorage.getItem(key))??fallback}catch{return fallback}}
function write(key,value){localStorage.setItem(key,JSON.stringify(value))}
let programs=read("diamondProgramsV2",{});
let sessions=read("diamondSessionsV2",{});
let metrics=read("diamondMetricsV2",[]);
let checkins=read("diamondCheckinsV2",{});
const programKey=()=> $("programMonth").value||monthStr(today);
const dayKey=()=> $("programDay").value;
const sessionKey=()=> $("workDate").value||dateStr(today);
const checkKey=()=> $("checkDate").value||dateStr(today);
function exercises(month,day){return programs[month]?.[day]||[]}

function showPage(name){
 document.querySelectorAll(".page").forEach(p=>p.classList.toggle("hidden",p.id!==name));
 document.querySelectorAll(".tab").forEach(b=>b.classList.toggle("active",b.dataset.page===name));
 if(name==="workout")renderWorkout();
 if(name==="program")renderBuilder();
 if(name==="progress")renderGraph();
 if(name==="checkin")loadCheckin();
}
document.querySelectorAll(".tab").forEach(b=>b.onclick=()=>showPage(b.dataset.page));

function renderWorkout(){
 const date=sessionKey(),day=$("workDay").value,month=date.slice(0,7);
 $("dayTitle").textContent=day+" · "+month;
 const plan=exercises(month,day);
 const saved=sessions[date]||{items:[]};
 $("exerciseList").innerHTML="";
 if(!plan.length){
  $("exerciseList").innerHTML='<p class="muted">No exercises planned for this day yet. Open Build program to add them.</p>';
 }else plan.forEach((ex,i)=>{
  const actual=saved.items?.[i]||{};
  const el=document.createElement("div");el.className="exercise";
  el.innerHTML=`<div class="exercise-top"><input type="checkbox" class="done" ${actual.done?"checked":""} aria-label="Exercise completed"><div class="exercise-name"></div></div><p class="small planned"></p><div class="exercise-fields"><div><label>Weight</label><input class="weight" placeholder="lb" value=""></div><div><label>Actual reps</label><input class="reps" type="number" placeholder="reps" value=""></div><div><label>Sets done</label><input class="sets" type="number" placeholder="sets" value=""></div></div>`;
  el.querySelector(".exercise-name").textContent=ex.name;
  el.querySelector(".planned").textContent=`Plan: ${ex.sets||"—"} sets × ${ex.reps||"—"} reps · ${ex.rest||"—"} rest`;
  el.querySelector(".weight").value=actual.weight||"";
  el.querySelector(".reps").value=actual.reps||"";
  el.querySelector(".sets").value=actual.sets||"";
  el.dataset.index=i;$("exerciseList").appendChild(el);
 });
 updateStats();
}
function collectWorkout(){
 const date=sessionKey(),day=$("workDay").value,month=date.slice(0,7),plan=exercises(month,day);
 const items=[...$("exerciseList").querySelectorAll(".exercise")].map(el=>({
  done:el.querySelector(".done").checked,weight:el.querySelector(".weight").value,
  reps:el.querySelector(".reps").value,sets:el.querySelector(".sets").value
 }));
 sessions[date]={day,items,planNames:plan.map(e=>e.name)};
 write("diamondSessionsV2",sessions);updateStats();
}
$("saveWorkout").onclick=()=>{collectWorkout();$("saveStatus").textContent="Workout saved on this device."};
$("workDate").onchange=()=>{$("workDay").value=days[(new Date(sessionKey()+"T12:00:00").getDay()+6)%7];renderWorkout()};
$("workDay").onchange=renderWorkout;

function renderBuilder(){
 const day=dayKey(),list=exercises(programKey(),day);
 $("builderList").innerHTML="";
 if(!list.length)$("builderList").innerHTML='<p class="muted">No exercises yet. Add your first exercise below.</p>';
 list.forEach((ex,i)=>{
  const el=document.createElement("div");el.className="exercise";
  el.innerHTML=`<label>Exercise name</label><input class="ename"><div class="exercise-fields"><div><label>Sets</label><input class="esets" type="number"></div><div><label>Reps / distance</label><input class="ereps"></div><div><label>Rest</label><input class="erest"></div></div><button class="danger remove" style="margin-top:10px">Remove</button>`;
  el.querySelector(".ename").value=ex.name;
  el.querySelector(".esets").value=ex.sets||"";
  el.querySelector(".ereps").value=ex.reps||"";
  el.querySelector(".erest").value=ex.rest||"";
  el.querySelector(".remove").onclick=()=>{list.splice(i,1);setPlan(day,list);renderBuilder()};
  $("builderList").appendChild(el);
 });
}
function setPlan(day,list){
 programs[programKey()] ||= {};
 programs[programKey()][day]=list;write("diamondProgramsV2",programs);
}
$("addExercise").onclick=()=>{
 const day=dayKey(),list=[...exercises(programKey(),day),{name:"New exercise",sets:3,reps:"8",rest:"90 sec"}];
 setPlan(day,list);renderBuilder();
};
$("saveProgram").onclick=()=>{
 const list=[...$("builderList").querySelectorAll(".exercise")].map(el=>({
  name:el.querySelector(".ename").value.trim()||"Exercise",
  sets:el.querySelector(".esets").value,
  reps:el.querySelector(".ereps").value,
  rest:el.querySelector(".erest").value
 }));
 setPlan(dayKey(),list);$("programStatus").textContent="Monthly weekday plan saved.";
 renderWorkout();
};
$("programMonth").onchange=renderBuilder;
$("programDay").onchange=renderBuilder;
$("reminderHelp").onclick=()=>$("reminderSteps").classList.toggle("hidden");

function loadCheckin(){
 const c=checkins[checkKey()]||{};
 $("sleepHours").value=c.sleep??"";
 $("feeling").value=c.feeling||"Good";
 $("dailyNotes").value=c.notes||"";
}
$("checkDate").onchange=loadCheckin;
$("saveCheckin").onclick=()=>{
 checkins[checkKey()]={sleep:$("sleepHours").value,feeling:$("feeling").value,notes:$("dailyNotes").value};
 write("diamondCheckinsV2",checkins);$("checkinStatus").textContent="Check-in saved.";
 updateStats();
};
$("saveMetrics").onclick=()=>{
 const entry={date:$("metricDate").value||dateStr(today)};
 ["exitVelo","batSpeed","throwVelo","sixtyTime"].forEach(k=>{const v=$(k).value;if(v!=="")entry[k]=Number(v)});
 if(!Object.keys(entry).some(k=>k!=="date")){$("metricStatus").textContent="Enter at least one measurement.";return}
 metrics=metrics.filter(m=>m.date!==entry.date);metrics.push(entry);
 metrics.sort((a,b)=>a.date.localeCompare(b.date));write("diamondMetricsV2",metrics);
 $("metricStatus").textContent="Measurements saved.";renderGraph();
};
$("graphMetric").onchange=renderGraph;
function renderGraph(){
 const key=$("graphMetric").value;
 let values=key==="sleep"?Object.entries(checkins).filter(([d,c])=>c.sleep!==""&&c.sleep!=null).map(([date,c])=>({date,value:Number(c.sleep)})):
 metrics.filter(m=>m[key]!=null).map(m=>({date:m.date,value:Number(m[key])}));
 values.sort((a,b)=>a.date.localeCompare(b.date));
 const graph=$("graph");graph.innerHTML="";
 if(!values.length){graph.innerHTML='<p class="muted">No measurements yet. Save a measurement to start your graph.</p>';$("metricHistory").textContent="";return}
 const max=Math.max(...values.map(v=>v.value)),min=Math.min(...values.map(v=>v.value));
 values.forEach(v=>{
  const row=document.createElement("div");row.className="barrow";
  const label=document.createElement("div");label.className="barlabel";
  const d=document.createElement("span");d.textContent=v.date;
  const n=document.createElement("strong");n.textContent=v.value;
  label.append(d,n);
  const bg=document.createElement("div");bg.className="barbg";
  const bar=document.createElement("div");bar.className="bar";
  bar.style.width=(max===min?100:Math.max(5,((v.value-min)/(max-min))*100))+"%";
  bg.appendChild(bar);row.append(label,bg);graph.appendChild(row);
 });
 $("metricHistory").textContent=values.length+" saved measurements. For the 60-yard time, a lower number is faster.";
}
function updateStats(){
 const date=sessionKey(),s=sessions[date]||{items:[]};
 const total=s.items.length,done=s.items.filter(i=>i.done).length;
 $("doneCount").textContent=done;
 $("streakStat").textContent=(total?Math.round(done/total*100):0)+"%";
 $("monthStat").textContent=date.slice(0,7);
 const c=checkins[date]||{};$("sleepStat").textContent=c.sleep?c.sleep+"h":"—";
}
renderWorkout();renderBuilder();loadCheckin();updateStats();
</script>
</body>
</html>
