<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#111318">
<title>Diamond OS</title>
<style>
:root{color-scheme:dark;--bg:#111318;--panel:#1b1e25;--panel2:#222630;--line:#343945;--muted:#9ba3b4;--green:#b5f36b;--white:#f5f7fa;--red:#ff8c8c}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--white);font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif}
header{padding:24px 18px 17px;border-bottom:1px solid var(--line)}
.eyebrow{font-size:10px;letter-spacing:2px;color:var(--green);font-weight:800}
h1{font-size:29px;margin:7px 0 3px;letter-spacing:-1px}
h2{font-size:21px;margin:6px 0}
h3{font-size:14px;margin:0 0 11px}
p{color:var(--muted);line-height:1.5;margin:7px 0}
.sub{font-size:12px;color:var(--muted)}
nav{display:flex;gap:7px;padding:12px;overflow-x:auto;border-bottom:1px solid var(--line);position:sticky;top:0;background:var(--bg);z-index:4}
button,select,input,textarea{font:inherit}
button{border:1px solid var(--line);background:var(--panel2);color:var(--white);border-radius:10px;padding:11px 13px;font-weight:700;font-size:12px;cursor:pointer}
button.active,.primary{background:var(--green);color:#141710;border-color:var(--green)}
button:disabled{opacity:.4}
main{padding:17px;max-width:820px;margin:auto}
.hidden{display:none!important}
.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:9px;margin:14px 0}
.card{background:var(--panel);border:1px solid var(--line);border-radius:15px;padding:14px;margin:10px 0}
.metric{font-size:25px;font-weight:800;margin:6px 0 1px}
.metric-label{font-size:11px;color:var(--muted)}
.pill{display:inline-block;background:#293323;color:var(--green);padding:5px 8px;border-radius:6px;font-size:10px;font-weight:800}
.row{display:flex;gap:9px;align-items:center}
.row>*{min-width:0;flex:1}
.row.wrap{flex-wrap:wrap}
.section{margin-top:21px}
label{display:block;color:var(--muted);font-size:12px;margin:12px 0 6px}
input,select,textarea{width:100%;background:#111318;color:var(--white);border:1px solid var(--line);border-radius:9px;padding:11px;font-size:14px}
textarea{min-height:115px;resize:vertical;line-height:1.5}
.full{width:100%;margin-top:10px}
.day-list{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:8px}
.day{border:1px solid var(--line);background:var(--panel);border-radius:12px;padding:11px;text-align:left}
.day.selected{border-color:var(--green);box-shadow:inset 0 0 0 1px var(--green)}
.day .dow{font-size:10px;color:var(--muted);letter-spacing:1px}
.day .focus{font-size:12px;font-weight:800;margin:5px 0}
.day .done{font-size:10px;color:var(--green)}
.exercise{border-bottom:1px solid var(--line);padding:10px 0}
.exercise:last-child{border:0}
.exercise strong{font-size:13px}
.exercise p{font-size:12px;margin:4px 0}
.checkline{display:flex;align-items:center;gap:8px;margin-top:9px;font-size:12px;color:var(--muted)}
.checkline input{width:auto;accent-color:var(--green)}
.item{border-bottom:1px solid var(--line);padding:11px 0}
.item:last-child{border:0}
.smallbtn{padding:7px 9px;font-size:11px}
.canvas{width:100%;height:170px;display:block}
.notice{font-size:11px;border-left:3px solid var(--green);padding:9px 11px;background:#20251d;border-radius:0 8px 8px 0;color:#d9e6ce}
.mutedbtn{background:transparent}
.two{display:grid;grid-template-columns:1fr 1fr;gap:9px}
footer{text-align:center;padding:28px 12px;color:var(--muted);font-size:10px}
@media(min-width:600px){
main{padding:25px}
.grid{grid-template-columns:repeat(4,minmax(0,1fr))}
.day-list{grid-template-columns:repeat(3,minmax(0,1fr))}
}
</style>
</head>
<body>
<header>
<div class="eyebrow">PLAYER DEVELOPMENT SYSTEM</div>
<h1>DIAMOND OS<span style="color:var(--green)">.</span></h1>
<p class="sub">Your work. Your numbers. Your progress.</p>
</header>

<nav id="nav">
<button class="active" data-page="home">Dashboard</button>
<button data-page="calendar">Calendar</button>
<button data-page="program">Daily Plan</button>
<button data-page="log">Log Workout</button>
<button data-page="liftprogress">Lift Progress</button>
<button data-page="progress">Progress</button>
<button data-page="feelings">Feelings</button>
</nav>

<main>
<section id="home">
<span class="pill" id="today"></span>
<h2>Today's mission.</h2>
<p>Train with purpose. Recover with purpose. Track the work.</p>

<div class="grid">
<div class="card"><div class="metric" id="workouts">0</div><div class="metric-label">Workouts logged</div></div>
<div class="card"><div class="metric" id="weekDone">0/4</div><div class="metric-label">Planned training days this week</div></div>
<div class="card"><div class="metric" id="exitMetric">—</div><div class="metric-label">Latest exit velo · mph</div></div>
<div class="card"><div class="metric" id="throwMetric">—</div><div class="metric-label">Latest throwing velo · mph</div></div>
</div>

<div class="card">
<h3>MONTHLY GOALS</h3>
<div id="goalDashboard"></div>
<button class="full" onclick="showPage('goals')">Manage monthly goals</button>
</div>

<div class="card">
<h3>MORNING CHECK-IN</h3>
<p class="sub">Record your body weight as part of your daily morning check. Your entry is added to your body-weight history and graph.</p>
<label>Today's body weight (lb)</label>
<input id="morningWeight" type="number" min="1" step="0.1" placeholder="Enter weight in pounds">
<button class="primary full" onclick="saveMorningWeight()">Save morning check-in</button>
<div class="sub" id="morningWeightStatus" aria-live="polite"></div>
</div>

<div class="card">
<h3>BODY WEIGHT</h3>
<div class="row">
<div><div class="metric" id="latestBodyWeight">—</div><div class="metric-label">Latest entry · lb</div></div>
<button onclick="showPage('bodyweight')">Log weight</button>
</div>
<canvas id="bodyMiniChart" class="canvas"></canvas>
</div>

<div class="card">
<h3>UP NEXT</h3>
<div id="todaySummary"></div>
<button class="primary full" onclick="showPage('program')">Open today's plan</button>
</div>

<div class="card">
<h3>HOW I FEEL</h3>
<p class="sub">Write what is on your mind, how training is going, or anything you want to remember.</p>
<div id="feelingsPreview" class="sub">No check-in written yet.</div>
<button class="full" onclick="showPage('feelings')">Open feelings journal</button>
</div>

<div class="card">
<h3>RECENT WORK</h3>
<div id="recent"></div>
</div>

<div class="notice">Keep sprint reps fast and crisp, take full recovery, and stop for pain or unusual arm discomfort. Follow your coach's throwing plan.</div>
</section>

<section id="calendar" class="hidden">
<h2>Training calendar.</h2>
<p>Your fixed program runs October 12 through December 18. Pick any date in that range to view or edit the session.</p>
<div class="card">
<label>Training month</label>
<input id="monthPicker" type="month">
<div class="row" style="margin-top:10px">
<button onclick="shiftMonth(-1)">← Previous</button>
<button onclick="shiftMonth(1)">Next →</button>
</div>
</div>
<div class="card">
<div class="row">
<div><h3 id="monthTitle">MONTH</h3><div class="sub" id="phaseText"></div></div>
</div>
<div class="day-list" id="days"></div>
</div>
<div class="card">
<h3>PROGRAM PHASE</h3>
<div id="monthFocus"></div>
<p class="sub">This program stays fixed through December 18. The calendar lets you view each day; it will not automatically replace your plan every month.</p>
</div>
</section>

<section id="program" class="hidden">
<span class="pill" id="selectedDateLabel"></span>
<h2 id="planHeading">Daily plan.</h2>
<p id="planSub">Edit your session, then mark it complete.</p>
<div class="card">
<label>Session focus</label>
<select id="sessionFocus">
<option>Sprint / Acceleration</option>
<option>Top Speed</option>
<option>Agility / Change of Direction</option>
<option>Hitting</option>
<option>Throwing / Arm Care</option>
<option>Strength</option>
<option>Recovery / Mobility</option>
<option>Conditioning</option>
<option>Off Day</option>
<option>Custom</option>
</select>

<label>Warm-up and workout details</label>
<textarea id="sessionText" placeholder="Warm-up, coaching notes, extra details..."></textarea>

<div class="card">
<h3>EXERCISES IN THIS SESSION</h3>
<p class="sub">Add any exercise. Choose how you want to track it; timed holds can be recorded in seconds.</p>
<div id="exerciseList"></div>
<label>Exercise name</label>
<input id="newExerciseName" placeholder="e.g. Split squat iso hold">
<div class="two">
<div>
<label>Tracking type</label>
<select id="newExerciseType">
<option value="weight-reps">Weight + reps</option>
<option value="reps">Reps / bodyweight reps</option>
<option value="time">Timed hold / duration</option>
<option value="distance">Distance</option>
<option value="weight-time">Weight + time</option>
<option value="speed">Speed / time trial</option>
</select>
</div>
<div>
<label>Target / prescription</label>
<input id="newExerciseTarget" placeholder="e.g. 3 sets x 30 sec">
</div>
</div>
<button class="full" onclick="addExercise()">+ Add exercise to this day</button>
</div>

<label>Session notes / adjustment</label>
<textarea id="sessionNotes" style="min-height:70px" placeholder="How did it feel? What needs adjusting?"></textarea>
<div class="checkline">
<input type="checkbox" id="sessionDone">
<span>Mark this day's planned session complete</span>
</div>
<button class="primary full" onclick="saveSession()">Save daily plan</button>
<button class="full" onclick="showPage('log')">Log performance from this session</button>
</div>
<div class="notice">Starter plan is a template, not a substitute for your team's schedule or coach's instructions. Avoid stacking hard sprint sessions or extra throwing on top of team workload.</div>
</section>

<section id="log" class="hidden">
<h2>Log your work.</h2>
<p>Record measurements and what you actually completed.</p>
<div class="card">
<label>Date</label>
<input id="logDate" type="date">
<label>Workout type</label>
<select id="logType">
<option>Sprint / Speed</option>
<option>Hitting</option>
<option>Throwing</option>
<option>Lifting</option>
<option>Agility</option>
<option>Recovery</option>
<option>Conditioning</option>
<option>Team practice</option>
</select>
<div class="two">
<div><label>Exit velocity (mph)</label><input id="exit" type="number" step="0.1" placeholder="e.g. 93"></div>
<div><label>Bat speed (mph)</label><input id="bat" type="number" step="0.1" placeholder="e.g. 73"></div>
<div><label>Throwing velo (mph)</label><input id="throwing" type="number" step="0.1" placeholder="e.g. 89"></div>
<div><label>60-yard time (sec)</label><input id="sixty" type="number" step="0.01" placeholder="e.g. 6.80"></div>
</div>
<div class="two">
<div><label>Sets</label><input id="sets" type="number" min="0" placeholder="e.g. 3"></div>
<div><label>Reps</label><input id="reps" type="number" min="0" placeholder="e.g. 5"></div>
</div>
<label>Exercises, weights, sprint splits, etc.</label>
<textarea id="details" placeholder="Example: 4 x 10-yard starts; full recovery between reps."></textarea>
<label>Notes</label>
<textarea id="notes" style="min-height:70px" placeholder="Energy, technique, soreness, conditions..."></textarea>
<button class="primary full" onclick="saveWorkout()">Save workout</button>
</div>
</section>

<section id="progress" class="hidden">
<h2>Progress report.</h2>
<p>Only your logged measurements are shown here.</p>
<div class="card"><h3>EXIT VELOCITY · MPH</h3><canvas id="exitChart" class="canvas"></canvas><div class="sub" id="exitHistory"></div></div>
<div class="card"><h3>BAT SPEED · MPH</h3><canvas id="batChart" class="canvas"></canvas><div class="sub" id="batHistory"></div></div>
<div class="card"><h3>60-YARD TIME · SECONDS</h3><canvas id="sprintChart" class="canvas"></canvas><div class="sub" id="sprintHistory"></div></div>
<div class="card">
<h3>WORKOUT HISTORY</h3>
<div id="allLogs"></div>
<div class="row wrap">
<button onclick="exportData()">Export backup</button>
<button onclick="document.getElementById('importFile').click()">Import backup</button>
<input id="importFile" type="file" accept="application/json" class="hidden" onchange="importData(event)">
</div>
</div>
</section>

<section id="liftprogress" class="hidden">
<h2>Lift progress.</h2>
<p>Every exercise you add to a plan is available here automatically once you log it.</p>
<div class="card">
<label>Choose exercise</label>
<select id="liftExerciseSelect" onchange="renderLiftProgress()"><option value="">No exercise logs yet</option></select>
<label>Time range</label>
<select id="liftRange" onchange="renderLiftProgress()">
<option value="month">This month</option>
<option value="6months">6 months</option>
<option value="year">1 year</option>
<option value="all">All time</option>
</select>
<div class="grid">
<div><div class="metric" id="liftLatest">—</div><div class="metric-label">Latest result</div></div>
<div><div class="metric" id="liftBest">—</div><div class="metric-label">Best result</div></div>
</div>
<canvas id="liftChart" class="canvas"></canvas>
<div id="liftHistory"></div>
</div>
</section>

<section id="bodyweight" class="hidden">
<h2>Body weight.</h2>
<p>Record measurements when you choose and follow your trend over time.</p>
<div class="card">
<label>Date</label>
<input id="bwDate" type="date">
<label>Body weight (lb)</label>
<input id="bwValue" type="number" min="1" step="0.1" placeholder="Weight in pounds">
<label>Notes (optional)</label>
<input id="bwNotes" placeholder="Optional note">
<button class="primary full" onclick="saveBodyWeight()">Save body weight</button>
</div>
<div class="card">
<h3>WEIGHT HISTORY</h3>
<canvas id="bwChart" class="canvas"></canvas>
<div id="bwHistory"></div>
</div>
</section>

<section id="goals" class="hidden">
<h2>Monthly goals.</h2>
<p>Choose a measurable target and track your progress through the month.</p>
<div class="card">
<label>Goal month</label>
<input id="goalMonth" type="month">
<label>Goal</label>
<input id="goalName" placeholder="e.g. Bench press, 60-yard time, throwing velo">
<div class="two">
<div><label>Target value</label><input id="goalTarget" type="number" step="0.01" placeholder="e.g. 185"></div>
<div>
<label>Unit</label>
<select id="goalUnit">
<option>lb</option><option>mph</option><option>sec</option><option>reps</option><option>seconds</option><option>inches</option><option>sessions</option><option>custom</option>
</select>
</div>
</div>
<label>Goal category</label>
<select id="goalCategory">
<option>Strength</option><option>Speed</option><option>Hitting</option><option>Throwing</option><option>Body weight</option><option>Consistency</option><option>Custom</option>
</select>
<button class="primary full" onclick="saveGoal()">Add monthly goal</button>
</div>
<div class="card"><h3>GOALS FOR THIS MONTH</h3><div id="goalList"></div></div>
</section>

<section id="feelings" class="hidden">
<h2>How I feel.</h2>
<p>This is your private journal on this device. Write honestly about your mood, confidence, stress, recovery, or anything else on your mind.</p>
<div class="card">
<label>Date</label>
<input id="feelingDate" type="date">
<label>How are you feeling?</label>
<select id="feelingMood">
<option>Good</option><option>Motivated</option><option>Confident</option><option>Okay / neutral</option><option>Tired</option><option>Stressed</option><option>Frustrated</option><option>Down</option><option>Mixed feelings</option><option>Prefer not to label it</option>
</select>
<label>Write it out</label>
<textarea id="feelingText" style="min-height:180px" placeholder="What's on your mind today? How are you feeling physically or mentally? You can write as much or as little as you want."></textarea>
<button class="primary full" onclick="saveFeeling()">Save today's entry</button>
<div class="sub" id="feelingStatus" aria-live="polite"></div>
</div>
<div class="card">
<div class="row">
<div><h3>PAST ENTRIES</h3><p class="sub">Entries are saved in this browser on this device.</p></div>
<button class="smallbtn" onclick="clearFeelingForm()">New entry</button>
</div>
<div id="feelingHistory"></div>
</div>
</section>
</main>

<footer>DIAMOND OS · FREE · YOUR DATA STAYS IN THIS BROWSER</footer>

<script>
const $=id=>document.getElementById(id);
const read=(k,f=[])=>{try{return JSON.parse(localStorage.getItem(k))||f}catch{return f}};
let logs=read('diamondLogs'),plans=read('diamondPlans'),schedule=read('diamondSchedule',{}),exerciseLogs=read('diamondExerciseLogs'),bodyWeights=read('diamondBodyWeights'),monthlyGoals=read('diamondMonthlyGoals'),feelings=read('diamondFeelings'),exerciseTimers={};
const now=new Date();
const localDate=d=>{const x=new Date(d.getTime()-d.getTimezoneOffset()*60000);return x.toISOString().slice(0,10)};
const keyDate=d=>typeof d==='string'?d:localDate(d);
let selectedDate=localDate(now);
$('today').textContent=now.toLocaleDateString(undefined,{weekday:'long',month:'short',day:'numeric'}).toUpperCase();
$('logDate').value=selectedDate;
$('monthPicker').value=selectedDate.slice(0,7);

const dayNames=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
const programStart='2026-10-12',programEnd='2026-12-18';

function phaseForDate(k){
if(k<='2026-11-01')return {name:'PHASE 1 · BUILD STRENGTH',desc:'Build strength and trunk control. Keep reps crisp, leave 2–3 reps in reserve, and coordinate school/NOMAD lifts so you do not repeat hard work.'};
if(k<='2026-11-22')return {name:'PHASE 2 · ISOMETRICS & JOINT CONTROL',desc:'Maintain strength with moderate volume. Add controlled isometric holds and trunk stability. No painful holds or max straining.'};
if(k<='2026-12-13')return {name:'PHASE 3 · EXPLODE',desc:'Low-volume, high-quality power and acceleration. Stop before speed or technique drops. Throwing intensity still follows your medical/throwing protocol.'};
return {name:'TAPER · DECEMBER 14–18',desc:'Reduce training volume, stay fresh, and assess progress without maxing out while fatigued.'};
}

function planForDate(k){
const d=new Date(k+'T12:00:00'),dow=d.getDay(),phase=phaseForDate(k),p1=k<='2026-11-01',p2=k>='2026-11-02'&&k<='2026-11-22',taper=k>='2026-12-14';
let focus,text,exercises=[];
const add=(name,type,target)=>exercises.push({id:Date.now()+Math.floor(Math.random()*100000),name,type,target});

if(dow===1){
focus='Strength · School + NOMAD';
text=`${phase.name}
School and NOMAD are your main strength sessions today. Coordinate with both coaches and do not duplicate heavy lower-body work.

Strength emphasis if not already covered: one coach-approved hinge 3–4 x 3–6; one single-leg movement 2–3 x 5–6 each leg; calf/hamstring accessory 2 x 8–10. Keep 2–3 reps in reserve.

Core: Pallof press 3 x 8/side and side plank 3 x 25–35 sec/side. Skip any movement already done hard today.`;
add('Coach-approved hinge / deadlift','weight-reps','3–4 x 3–6 · only if not already done');
add('Rear-foot elevated split squat','weight-reps','2–3 x 5–6 each leg · only if not already done');
add('Romanian deadlift','weight-reps','3 x 6 · only if not already done');
add('Standing calf raise','weight-reps','2 x 10');
add('Pallof press','reps','3 x 8 each side');
add('Side plank hold','time','3 x 25–35 sec each side');
}
else if(dow===2){
focus='Acceleration + School Lift';
text=`${phase.name}
SPRINT: 6 x 10 yd + 4 x 15 yd accelerations; full recovery (60–120 sec), stop if speed or mechanics fall. Add 3 x 5 yd reaction starts only if fresh. Your usual warm-up is assumed.

SCHOOL LIFT: follow the assigned lift. If you can choose the emphasis, upper-body strength and trunk control are preferred so Monday's lower-body work can recover.

CORE: dead bug 3 x 8/side; suitcase carry 3 x 20 yd/side if not already included. This is your second session; keep it short.`;
add('10-yard acceleration','speed','6 reps · full recovery');
add('15-yard acceleration','speed','4 reps · full recovery');
add('Neutral-grip dumbbell bench / approved press','weight-reps','3 x 5–6 · only if not already done');
add('Chest-supported row','weight-reps','3 x 6–8 · only if not already done');
add('Pull-ups / assisted pull-ups','reps','3 x 6–8 · only if not already done');
add('PT-approved light external rotation','reps','2 x 12 · only if cleared');
add('Dead bug','reps','3 x 8 each side');
add('Suitcase carry','distance','3 x 20 yd each side');
}
else if(dow===3){
focus='School Lift · Hitting + Light Conditioning';
text=`${phase.name}
SCHOOL LIFT: complete the scheduled school session; avoid adding another hard lift. If the coach allows accessory work, use single-leg control and trunk stability rather than another max-strength block.

HITTING: tee work 3 x 5 through the middle, then 3 x 3 normal-bat intent swings with full rest. Count team hitting instead of doubling it.

LIGHT CONDITIONING: optional 6 x 60 yd at 60–70%, walk-back recovery, only if legs are fresh. Otherwise 10–15 min easy walk/bike.

THROWING: only on the days, distance, volume, and effort in your approved return-to-throw plan.`;
add('Step-up / reverse lunge','weight-reps','3 x 6 each leg · only if not already done');
add('Single-leg Romanian deadlift','weight-reps','2 x 6 each leg · only if not already done');
add('Hamstring curl','weight-reps','2 x 8 · only if not already done');
add('Bird dog','reps','2 x 8 each side');
add('Pallof press','reps','3 x 8 each side');
add('Tee swings','reps','3 x 5 quality swings');
add('Normal-bat intent swings','reps','3 x 3 · full rest');
add('Easy tempo run','distance','6 x 60 yd at 60–70% · optional if fresh');
}
else if(dow===4){
focus='NOMAD · Recovery + Arm Care';
text=`${phase.name}
NOMAD is the hard strength session today. Do not add a third lift or hard sprint session.

Afterward: easy mobility and only the shoulder/scapular exercises prescribed by your PT/clinician. No extra weighted-ball work.

Check arm symptoms and general recovery; protect Friday speed quality.`;
add('PT-prescribed arm-care routine','reps','Use your clinician’s exact exercises and dosage');
}
else if(dow===5){
focus='Speed + School Lift';
text=`${phase.name}
SPRINT: 4 x 10 yd + 4 x 20 yd, full 2–3 min rest between fast efforts. Progress to 2–3 x 30 yd only in Phase 3 if cleared, fresh, and mechanics stay sharp. During taper, cut volume about in half.

SCHOOL LIFT: use the scheduled program. If selecting accessories, choose a coach-approved hinge or row plus core; do not duplicate NOMAD's heavy work.

ROTATION: controlled band/cable chop 3 x 6/side only if shoulder-safe and cleared. No explosive upper-body rotational throws unless approved.`;
add('10-yard acceleration','speed','4 reps · full recovery');
add('20-yard sprint','speed','4 reps · full recovery');
add('Coach-approved hinge / deadlift','weight-reps','3 x 4–5 · only if not already done');
add('Chest-supported row','weight-reps','3 x 8 · only if not already done');
add('Split squat / step-up','weight-reps','2 x 6 each leg · only if not already done');
add('Band/cable chop','reps','3 x 6 each side · controlled and shoulder-safe');
add('Front plank hold','time','3 x 30–45 sec');
}
else if(dow===6){
focus='Supplemental Lift + Agility';
text=`${phase.name}
Keep this supplemental session to 20–30 minutes. If Friday fatigue remains, do the core only and skip the lift.

LIFT: Phase 1: coach-approved jump 3 x 3 if cleared, single-leg glute bridge 2 x 8/side, Pallof press 2 x 10/side, dead bug 2 x 8/side. Phase 2: add 3 x 20–40 sec comfortable split-squat or calf isometric holds only if pain-free and approved; reduce accessory volume. Phase 3: low-volume jumps 3–4 x 2–3 with full rest; no grinding. Taper: half volume.

AGILITY: 4 x shuffle 5 yd into 10 yd sprint; 4 reaction starts; 3 controlled cone cuts each side. Full recovery.

Throwing only if this is an approved throwing day.`;
add('Coach-approved jump variation','reps','3 x 3 · only if cleared');
add('Single-leg glute bridge','reps','2 x 8 each leg');
add('Split-squat or calf isometric hold','time','Phase 2 only · 3 x 20–40 sec, pain-free and approved');
add('Pallof press','reps','2 x 10 each side');
add('Dead bug','reps','2 x 8 each side');
add('Lateral shuffle to sprint','reps','4 reps · clean footwork');
add('Reaction start','reps','4 reps');
add('Cone change of direction','reps','3–4 reps each side');
}
else{
focus='Recovery + Check-in';
text=`${phase.name}
OFF / RECOVERY DAY. Optional easy walk 20–30 min, comfortable mobility, regular meals, hydration, and sleep. No make-up workouts.

Review the week: sprint quality, lifting fatigue, hitting metrics, and how your arm feels during throwing and the next morning.

Throw only if your approved throwing plan specifically schedules it. Do not add long toss, pulldowns, plyo-ball throws, or a bullpen just to hit a calendar date.`;
}

if(taper)text=text.replace('4 x 10 yd + 4 x 20 yd','2 x 10 yd + 2 x 20 yd');
return {focus,text,notes:'',done:false,exercises,phase:phase.name};
}

function ensureDay(date){
let k=keyDate(date);
if(!schedule[k]){
if(k>=programStart&&k<=programEnd)schedule[k]=planForDate(k);
else schedule[k]={focus:'Off Day',text:'This date is outside the fixed October 12–December 18 program. Rest or follow your current team/coach plan.',notes:'',done:false,exercises:[]};
}
if(!Array.isArray(schedule[k].exercises))schedule[k].exercises=[];
return schedule[k];
}

function installFixedProgram(){
if(localStorage.getItem('diamondFixedProgramVersion')==='2026-12-18-v1')return;
let d=new Date(programStart+'T12:00:00'),end=new Date(programEnd+'T12:00:00');
while(d<=end){let k=localDate(d);schedule[k]=planForDate(k);d.setDate(d.getDate()+1)}
saveSchedule();
localStorage.setItem('diamondFixedProgramVersion','2026-12-18-v1');
}

function showPage(page){
document.querySelectorAll('main section').forEach(s=>s.classList.toggle('hidden',s.id!==page));
document.querySelectorAll('nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===page));
if(page==='home')renderHome();
if(page==='calendar')renderCalendar();
if(page==='program')loadSession();
if(page==='progress')renderProgress();
if(page==='liftprogress')renderLiftProgress();
if(page==='bodyweight')renderBodyWeight();
if(page==='goals')renderGoals();
if(page==='feelings')renderFeelings();
window.scrollTo(0,0);
}
document.querySelectorAll('nav button').forEach(b=>b.addEventListener('click',()=>showPage(b.dataset.page)));

function saveSchedule(){localStorage.setItem('diamondSchedule',JSON.stringify(schedule))}
function openDate(k){selectedDate=k;showPage('program')}

function loadSession(){
let s=ensureDay(selectedDate);
$('selectedDateLabel').textContent=new Date(selectedDate+'T12:00:00').toLocaleDateString(undefined,{weekday:'long',month:'short',day:'numeric',year:'numeric'}).toUpperCase();
$('planHeading').textContent=dayNames[new Date(selectedDate+'T12:00:00').getDay()]+' plan.';
$('sessionFocus').value=s.focus;
$('sessionText').value=s.text;
$('sessionNotes').value=s.notes||'';
$('sessionDone').checked=!!s.done;
$('planSub').textContent=(s.phase||phaseForDate(selectedDate).name)+' · '+(s.done?'Session marked complete. You can still edit it.':'Fixed program through Dec 18. Adjust with your coaches and recovery.');
renderExerciseList();
}

function saveSession(){
let prior=ensureDay(selectedDate);
schedule[selectedDate]={...prior,focus:$('sessionFocus').value,text:$('sessionText').value,notes:$('sessionNotes').value,done:$('sessionDone').checked};
saveSchedule();
renderHome();
alert('Daily plan saved on this device.');
}

function renderCalendar(){
let m=$('monthPicker').value||selectedDate.slice(0,7);
$('monthPicker').value=m;
let [yy,mm]=m.split('-').map(Number);
let title=new Date(yy,mm-1,1);
$('monthTitle').textContent=title.toLocaleDateString(undefined,{month:'long',year:'numeric'}).toUpperCase();
let start=m+'-01',end=m+'-'+String(new Date(yy,mm,0).getDate()).padStart(2,'0');
let phase=phaseForDate(end<programStart?programStart:start>programEnd?programEnd:(start<programStart?programStart:start));
$('phaseText').textContent=phase.name;
$('monthFocus').innerHTML='<strong>'+esc(phase.name)+'</strong><p>'+esc(phase.desc)+'</p>';
let n=new Date(yy,mm,0).getDate(),html='';
for(let day=1;day<=n;day++){
let k=m+'-'+String(day).padStart(2,'0'),d=new Date(k+'T12:00:00');
if(k>=programStart&&k<=programEnd){
let s=ensureDay(k);
html+=`<button class="day ${k===selectedDate?'selected':''}" onclick="openDate('${k}')"><div class="dow">${dayNames[d.getDay()].slice(0,3).toUpperCase()} · ${day}</div><div class="focus">${esc(s.focus)}</div><div class="done">${s.done?'✓ COMPLETED':'Tap to view plan'}</div></button>`;
}else{
html+=`<div class="day" style="opacity:.35"><div class="dow">${dayNames[d.getDay()].slice(0,3).toUpperCase()} · ${day}</div><div class="focus">Outside program</div><div class="done">Oct 12–Dec 18 only</div></div>`;
}
}
$('days').innerHTML=html;
saveSchedule();
}
function shiftMonth(n){
let [y,m]=$('monthPicker').value.split('-').map(Number),d=new Date(y,m-1+n,1);
$('monthPicker').value=localDate(d).slice(0,7);
renderCalendar();
}
$('monthPicker').addEventListener('change',renderCalendar);

function saveWorkout(){
let obj={id:Date.now(),date:$('logDate').value||localDate(new Date()),type:$('logType').value,exit:$('exit').value,bat:$('bat').value,throwing:$('throwing').value,sixty:$('sixty').value,sets:$('sets').value,reps:$('reps').value,details:$('details').value,notes:$('notes').value};
if(!obj.details.trim()&&!obj.notes.trim()&&!obj.exit&&!obj.bat&&!obj.throwing&&!obj.sixty&&!obj.sets&&!obj.reps){alert('Add a measurement or workout detail first.');return}
logs.push(obj);
localStorage.setItem('diamondLogs',JSON.stringify(logs));
['exit','bat','throwing','sixty','sets','reps','details','notes'].forEach(id=>$(id).value='');
renderHome();
alert('Workout saved on this device.');
showPage('home');
}

function esc(v){return String(v??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}

function renderHome(){
let todayKey=localDate(new Date()),morningEntry=bodyWeights.filter(x=>x.date===todayKey).slice(-1)[0];
if($('morningWeight'))$('morningWeight').value=morningEntry?morningEntry.value:'';
if($('morningWeightStatus'))$('morningWeightStatus').textContent=morningEntry?'Morning weight saved today: '+morningEntry.value+' lb':'Not logged yet today.';
$('workouts').textContent=logs.length;
let monday=new Date(now);
monday.setHours(0,0,0,0);
monday.setDate(now.getDate()-((now.getDay()+6)%7));
let cnt=0;
[0,1,3,4].forEach(offset=>{
let d=new Date(monday);
d.setDate(monday.getDate()+offset);
if(ensureDay(localDate(d)).done)cnt++;
});
$('weekDone').textContent=cnt+'/4';
let last=k=>logs.slice().reverse().find(l=>l[k]!==''&&l[k]!=null);
$('exitMetric').textContent=last('exit')?.exit||'—';
$('throwMetric').textContent=last('throwing')?.throwing||'—';
let s=ensureDay(selectedDate);
$('todaySummary').innerHTML=`<span class="pill">${esc(s.focus)}</span><p>${esc(s.text.split('\n')[0])}</p><div class="sub">${s.done?'✓ Marked complete':'Not marked complete yet'}</div>`;
renderGoalDashboard();
renderBodyMini();
let latestFeeling=feelings.slice().sort((a,b)=>b.date.localeCompare(a.date))[0];
if($('feelingsPreview'))$('feelingsPreview').textContent=latestFeeling?(latestFeeling.date+' · '+latestFeeling.mood+' — '+(latestFeeling.text||'No written notes').slice(0,100)):'No check-in written yet.';
$('recent').innerHTML=logs.slice().reverse().slice(0,4).map(l=>`<div class="item"><strong>${esc(l.type)}</strong><div class="sub">${esc(l.date)} · ${esc(l.details||l.notes||'Measurement logged')}</div></div>`).join('')||'<p class="sub">No workouts logged yet.</p>';
}

function chart(id,key,lowerBetter=false){
let c=$(id),ctx=c.getContext('2d'),ratio=window.devicePixelRatio||1,w=c.clientWidth*ratio,h=170*ratio;
c.width=w;c.height=h;ctx.clearRect(0,0,w,h);
let arr=logs.filter(l=>l[key]!==''&&Number(l[key])>0).slice().sort((a,b)=>a.date.localeCompare(b.date));
if(!arr.length){ctx.fillStyle='#9ba3b4';ctx.font=`${12*ratio}px sans-serif`;ctx.fillText('Log measurements to see your trend',10*ratio,30*ratio);return}
let vals=arr.map(l=>Number(l[key])),min=Math.min(...vals),max=Math.max(...vals),pad=22*ratio;
ctx.strokeStyle='#343945';ctx.beginPath();ctx.moveTo(pad,pad);ctx.lineTo(pad,h-pad);ctx.lineTo(w-pad,h-pad);ctx.stroke();
ctx.strokeStyle='#b5f36b';ctx.lineWidth=2*ratio;ctx.beginPath();
vals.forEach((v,i)=>{
let x=pad+(vals.length===1?(w-2*pad)/2:i*(w-2*pad)/(vals.length-1)),y=h-pad-((v-min+(max===min?0:(max-min)*.08))/(max-min||1))*(h-2*pad);
if(i===0)ctx.moveTo(x,y);else ctx.lineTo(x,y);
});
ctx.stroke();ctx.fillStyle='#b5f36b';
vals.forEach((v,i)=>{
let x=pad+(vals.length===1?(w-2*pad)/2:i*(w-2*pad)/(vals.length-1)),y=h-pad-((v-min+(max===min?0:(max-min)*.08))/(max-min||1))*(h-2*pad);
ctx.beginPath();ctx.arc(x,y,3*ratio,0,Math.PI*2);ctx.fill();
});
}

function renderProgress(){
chart('exitChart','exit');
chart('batChart','bat');
chart('sprintChart','sixty');
let hist=k=>logs.filter(l=>l[k]!==''&&l[k]!=null).map(l=>`${esc(l.date)}: ${esc(l[k])}`).join(' · ')||'No measurements yet.';
$('exitHistory').textContent=hist('exit');
$('batHistory').textContent=hist('bat');
$('sprintHistory').textContent=hist('sixty');
$('allLogs').innerHTML=logs.slice().reverse().map(l=>`<div class="item"><strong>${esc(l.date)} — ${esc(l.type)}</strong><p class="sub">Exit: ${esc(l.exit||'—')} · Bat: ${esc(l.bat||'—')} · Throw: ${esc(l.throwing||'—')} · 60 yd: ${esc(l.sixty||'—')}</p><p>${esc(l.details)} ${esc(l.notes)}</p><button class="smallbtn" onclick="deleteLog(${l.id})">Delete</button></div>`).join('')||'<p class="sub">No saved workouts.</p>';
}
function deleteLog(id){logs=logs.filter(l=>l.id!==id);localStorage.setItem('diamondLogs',JSON.stringify(logs));renderProgress();renderHome()}

function exportData(){
let blob=new Blob([JSON.stringify({logs,plans,schedule,exerciseLogs,bodyWeights,monthlyGoals,feelings},null,2)],{type:'application/json'}),url=URL.createObjectURL(blob),a=document.createElement('a');
a.href=url;a.download='diamond-os-backup.json';a.click();setTimeout(()=>URL.revokeObjectURL(url),1000);
}
function importData(e){
let f=e.target.files[0];if(!f)return;
let r=new FileReader();
r.onload=()=>{
try{
let x=JSON.parse(r.result);
if(!confirm('Import backup and replace current saved workouts and plans? Export current data first if you need it.'))return;
logs=x.logs||[];plans=x.plans||[];schedule=x.schedule||{};exerciseLogs=x.exerciseLogs||[];bodyWeights=x.bodyWeights||[];monthlyGoals=x.monthlyGoals||[];feelings=x.feelings||[];
localStorage.setItem('diamondFeelings',JSON.stringify(feelings));
localStorage.setItem('diamondExerciseLogs',JSON.stringify(exerciseLogs));
localStorage.setItem('diamondBodyWeights',JSON.stringify(bodyWeights));
localStorage.setItem('diamondMonthlyGoals',JSON.stringify(monthlyGoals));
localStorage.setItem('diamondLogs',JSON.stringify(logs));
localStorage.setItem('diamondPlans',JSON.stringify(plans));
saveSchedule();renderHome();renderProgress();
alert('Backup imported.');
}catch{alert('Could not read that backup file.')}
};
r.readAsText(f);e.target.value='';
}

function addExercise(){
let name=$('newExerciseName').value.trim();
if(!name){alert('Enter an exercise name first.');return}
let s=ensureDay(selectedDate);
s.exercises.push({id:Date.now(),name,type:$('newExerciseType').value,target:$('newExerciseTarget').value.trim()});
saveSchedule();
$('newExerciseName').value='';
$('newExerciseTarget').value='';
renderExerciseList();
renderCalendar();
}

function renderExerciseList(){
let s=ensureDay(selectedDate),list=s.exercises||[];
$('exerciseList').innerHTML=list.map(ex=>{
let recent=exerciseLogs.filter(x=>x.name===ex.name).slice(-1)[0];
let fields=ex.type==='time'
?'<label>Timed hold (seconds)</label><div class="row"><input id="val-'+ex.id+'" type="number" min="0" step="0.1" placeholder="e.g. 30"><button class="smallbtn" id="timer-'+ex.id+'" onclick="toggleExerciseTimer('+ex.id+')">Start timer</button></div><div class="sub" id="clock-'+ex.id+'">00:00.0</div>'
:ex.type==='distance'
?'<label>Distance</label><input id="val-'+ex.id+'" type="number" min="0" step="0.1" placeholder="Distance">'
:ex.type==='reps'
?'<label>Reps completed</label><input id="val-'+ex.id+'" type="number" min="0" placeholder="Reps">'
:ex.type==='speed'
?'<label>Time (seconds)</label><input id="val-'+ex.id+'" type="number" min="0" step="0.01" placeholder="e.g. 6.8">'
:ex.type==='weight-time'
?'<div class="two"><div><label>Weight (lb)</label><input id="weight-'+ex.id+'" type="number" min="0" step="0.5"></div><div><label>Hold time (sec)</label><input id="val-'+ex.id+'" type="number" min="0" step="0.1"></div></div>'
:'<div class="two"><div><label>Weight (lb)</label><input id="weight-'+ex.id+'" type="number" min="0" step="0.5" placeholder="Weight"></div><div><label>Reps</label><input id="val-'+ex.id+'" type="number" min="0" placeholder="Reps"></div></div>';
return `<div class="exercise"><div class="row"><div><strong>${esc(ex.name)}</strong><p>${esc(ex.target||ex.type.replace('-',' + '))}${recent?' · Last: '+esc(recent.value)+(recent.unit?' '+esc(recent.unit):''):''}</p></div><button class="smallbtn" onclick="removeExercise(${ex.id})">Remove</button></div>${fields}<button class="smallbtn" onclick="logExercise(${ex.id})">Save result</button></div>`;
}).join('')||'<p class="sub">No exercises yet. Add the exercises you want to track for this day.</p>';
}

function removeExercise(id){
let s=ensureDay(selectedDate);
s.exercises=s.exercises.filter(e=>e.id!==id);
saveSchedule();
renderExerciseList();
}

function toggleExerciseTimer(id){
let t=exerciseTimers[id];
if(t&&t.running){
t.elapsed+=(Date.now()-t.startedAt);
t.running=false;
clearInterval(t.interval);
let seconds=t.elapsed/1000;
$('val-'+id).value=seconds.toFixed(1);
$('timer-'+id).textContent='Resume timer';
$('clock-'+id).textContent=seconds.toFixed(1)+' sec';
return;
}
if(!t)t=exerciseTimers[id]={elapsed:0,running:false};
t.startedAt=Date.now();t.running=true;
$('timer-'+id).textContent='Stop timer';
t.interval=setInterval(()=>{
let seconds=(t.elapsed+Date.now()-t.startedAt)/1000;
let el=$('clock-'+id);
if(el)el.textContent=seconds.toFixed(1)+' sec';
let input=$('val-'+id);
if(input)input.value=seconds.toFixed(1);
},100);
}

function logExercise(id){
let ex=ensureDay(selectedDate).exercises.find(e=>e.id===id);
if(!ex)return;
let val=$('val-'+id).value,weight=$('weight-'+id)?$('weight-'+id).value:'';
if(val===''&&weight===''){alert('Enter a result first.');return}
let unit=ex.type==='time'?'sec':ex.type==='speed'?'sec':ex.type==='distance'?'distance':ex.type==='reps'?'reps':ex.type==='weight-time'?'sec':'reps';
let rec={id:Date.now(),date:selectedDate,name:ex.name,type:ex.type,value:Number(val||0),weight:weight===''?null:Number(weight),unit,target:ex.target};
exerciseLogs.push(rec);
localStorage.setItem('diamondExerciseLogs',JSON.stringify(exerciseLogs));
renderExerciseList();
alert('Exercise result saved.');
}

function drawGenericChart(id,arr,valueFn){
let c=$(id);if(!c)return;
let ctx=c.getContext('2d'),ratio=window.devicePixelRatio||1,w=c.clientWidth*ratio,h=170*ratio;
c.width=w;c.height=h;ctx.clearRect(0,0,w,h);
if(!arr.length){ctx.fillStyle='#9ba3b4';ctx.font=`${12*ratio}px sans-serif`;ctx.fillText('Log results to see your trend',10*ratio,30*ratio);return}
let vals=arr.map(valueFn),min=Math.min(...vals),max=Math.max(...vals),pad=22*ratio;
ctx.strokeStyle='#343945';ctx.beginPath();ctx.moveTo(pad,pad);ctx.lineTo(pad,h-pad);ctx.lineTo(w-pad,h-pad);ctx.stroke();
ctx.strokeStyle='#b5f36b';ctx.lineWidth=2*ratio;ctx.beginPath();
vals.forEach((v,i)=>{
let x=pad+(vals.length===1?(w-2*pad)/2:i*(w-2*pad)/(vals.length-1)),y=h-pad-((v-min+(max===min?0:(max-min)*.08))/(max-min||1))*(h-2*pad);
if(i===0)ctx.moveTo(x,y);else ctx.lineTo(x,y);
});
ctx.stroke();ctx.fillStyle='#b5f36b';
vals.forEach((v,i)=>{
let x=pad+(vals.length===1?(w-2*pad)/2:i*(w-2*pad)/(vals.length-1)),y=h-pad-((v-min+(max===min?0:(max-min)*.08))/(max-min||1))*(h-2*pad);
ctx.beginPath();ctx.arc(x,y,3*ratio,0,Math.PI*2);ctx.fill();
});
}

function renderLiftProgress(){
let names=[...new Set([...exerciseLogs.map(x=>x.name),...Object.values(schedule).flatMap(s=>(s.exercises||[]).map(e=>e.name))])].sort(),sel=$('liftExerciseSelect'),old=sel.value;
sel.innerHTML=names.map(n=>`<option value="${esc(n)}">${esc(n)}</option>`).join('')||'<option value="">No exercises yet</option>';
if(names.includes(old))sel.value=old;
let name=sel.value,range=$('liftRange').value,arr=exerciseLogs.filter(x=>x.name===name).sort((a,b)=>a.date.localeCompare(b.date));
let cutoff=new Date();
if(range==='month')cutoff.setDate(1);
if(range==='6months')cutoff.setMonth(cutoff.getMonth()-6);
if(range==='year')cutoff.setFullYear(cutoff.getFullYear()-1);
if(range!=='all')arr=arr.filter(x=>new Date(x.date+'T12:00:00')>=cutoff);
let last=arr[arr.length-1],vals=arr.map(x=>x.weight!=null?x.weight:x.value).filter(v=>v!=null&&Number.isFinite(Number(v)));
$('liftLatest').textContent=last?(last.weight!=null?last.weight+' lb':last.value+' '+last.unit):'—';
$('liftBest').textContent=vals.length?Math.max(...vals)+'':'—';
drawGenericChart('liftChart',arr,x=>Number(x.weight!=null?x.weight:x.value));
$('liftHistory').innerHTML=arr.slice().reverse().map(x=>`<div class="item"><strong>${esc(x.date)} · ${esc(x.name)}</strong><p>${x.weight!=null?esc(x.weight)+' lb · ':''}${esc(x.value)} ${esc(x.unit||'')} ${x.target?'· Target: '+esc(x.target):''}</p></div>`).join('')||'<p class="sub">No results for this exercise in the selected range.</p>';
}

function saveMorningWeight(){
let value=Number($('morningWeight').value);
if(!value||value<=0){alert('Enter a valid body weight.');return}
let date=localDate(new Date()),existing=bodyWeights.findIndex(x=>x.date===date);
if(existing>=0){bodyWeights[existing]={...bodyWeights[existing],value,notes:bodyWeights[existing].notes||'Morning check-in'};}
else{bodyWeights.push({id:Date.now(),date,value,notes:'Morning check-in'});}
bodyWeights.sort((a,b)=>a.date.localeCompare(b.date));
localStorage.setItem('diamondBodyWeights',JSON.stringify(bodyWeights));
renderBodyMini();renderBodyWeight();
$('morningWeightStatus').textContent='Saved for today: '+value+' lb. Your body-weight graph has been updated.';
renderHome();
}

function saveBodyWeight(){
let value=Number($('bwValue').value);
if(!value||value<=0){alert('Enter a valid body weight.');return}
bodyWeights.push({id:Date.now(),date:$('bwDate').value||localDate(new Date()),value,notes:$('bwNotes').value});
bodyWeights.sort((a,b)=>a.date.localeCompare(b.date));
localStorage.setItem('diamondBodyWeights',JSON.stringify(bodyWeights));
$('bwValue').value='';$('bwNotes').value='';
renderBodyWeight();renderBodyMini();
alert('Body weight saved on this device.');
}

function renderBodyWeight(){
let arr=bodyWeights.slice().sort((a,b)=>a.date.localeCompare(b.date));
drawGenericChart('bwChart',arr,x=>x.value);
$('bwHistory').innerHTML=arr.slice().reverse().map(x=>`<div class="item"><strong>${esc(x.date)} · ${esc(x.value)} lb</strong>${x.notes?'<p>'+esc(x.notes)+'</p>':''}</div>`).join('')||'<p class="sub">No body-weight entries yet.</p>';
}

function renderBodyMini(){
let latest=bodyWeights.slice().sort((a,b)=>a.date.localeCompare(b.date)).slice(-1)[0];
if($('latestBodyWeight'))$('latestBodyWeight').textContent=latest?latest.value:'—';
drawGenericChart('bodyMiniChart',bodyWeights.slice().sort((a,b)=>a.date.localeCompare(b.date)),x=>x.value);
}

function saveFeeling(){
let date=$('feelingDate').value||localDate(new Date()),mood=$('feelingMood').value,textValue=$('feelingText').value.trim();
if(!textValue){alert('Write a few words first, or add a note about how you feel.');return}
let i=feelings.findIndex(x=>x.date===date);
let entry={id:i>=0?feelings[i].id:Date.now(),date,mood,text:textValue,updatedAt:new Date().toISOString()};
if(i>=0)feelings[i]=entry;else feelings.push(entry);
feelings.sort((a,b)=>a.date.localeCompare(b.date));
localStorage.setItem('diamondFeelings',JSON.stringify(feelings));
$('feelingStatus').textContent='Saved on this device.';
renderFeelings();renderHome();
}

function loadFeelingDate(){
let date=$('feelingDate').value||localDate(new Date()),entry=feelings.find(x=>x.date===date);
$('feelingMood').value=entry?.mood||'Good';
$('feelingText').value=entry?.text||'';
$('feelingStatus').textContent=entry?'Entry loaded for '+date+'.':'';
}

function clearFeelingForm(){
$('feelingDate').value=localDate(new Date());
$('feelingMood').value='Good';
$('feelingText').value='';
$('feelingStatus').textContent='New entry ready.';
}

function deleteFeeling(id){
if(!confirm('Delete this journal entry?'))return;
feelings=feelings.filter(x=>x.id!==id);
localStorage.setItem('diamondFeelings',JSON.stringify(feelings));
renderFeelings();renderHome();
}

function editFeeling(id){
let e=feelings.find(x=>x.id===id);if(!e)return;
$('feelingDate').value=e.date;
$('feelingMood').value=e.mood;
$('feelingText').value=e.text;
$('feelingStatus').textContent='Editing entry from '+e.date+'.';
window.scrollTo(0,0);
}

function renderFeelings(){
if(!$('feelingDate'))return;
if(!$('feelingDate').value)$('feelingDate').value=localDate(new Date());
loadFeelingDate();
$('feelingHistory').innerHTML=feelings.slice().sort((a,b)=>b.date.localeCompare(a.date)).map(e=>`<div class="item"><div class="row"><div><strong>${esc(e.date)} · ${esc(e.mood)}</strong></div><button class="smallbtn" onclick="editFeeling(${e.id})">Edit</button><button class="smallbtn" onclick="deleteFeeling(${e.id})">Delete</button></div><p>${esc(e.text).replace(/\n/g,'<br>')}</p></div>`).join('')||'<p class="sub">No journal entries yet. Your first entry can be short.</p>';
}
$('feelingDate').addEventListener('change',loadFeelingDate);

function saveGoal(){
let name=$('goalName').value.trim(),target=Number($('goalTarget').value),month=$('goalMonth').value||localDate(new Date()).slice(0,7);
if(!name||!Number.isFinite(target)){alert('Enter a goal name and target.');return}
monthlyGoals.push({id:Date.now(),month,name,target,unit:$('goalUnit').value,category:$('goalCategory').value});
localStorage.setItem('diamondMonthlyGoals',JSON.stringify(monthlyGoals));
$('goalName').value='';$('goalTarget').value='';
renderGoals();renderGoalDashboard();
alert('Monthly goal added.');
}

function renderGoals(){
let month=$('goalMonth')?.value||localDate(new Date()).slice(0,7),arr=monthlyGoals.filter(g=>g.month===month);
$('goalList').innerHTML=arr.map(g=>`<div class="item"><div class="row"><div><strong>${esc(g.name)}</strong><p class="sub">${esc(g.category)} · Target: ${esc(g.target)} ${esc(g.unit)}</p></div><button class="smallbtn" onclick="deleteGoal(${g.id})">Delete</button></div></div>`).join('')||'<p class="sub">No goals for this month yet.</p>';
renderGoalDashboard();
}

function deleteGoal(id){
monthlyGoals=monthlyGoals.filter(g=>g.id!==id);
localStorage.setItem('diamondMonthlyGoals',JSON.stringify(monthlyGoals));
renderGoals();renderGoalDashboard();
}

function renderGoalDashboard(){
let month=localDate(new Date()).slice(0,7),arr=monthlyGoals.filter(g=>g.month===month);
if(!$('goalDashboard'))return;
$('goalDashboard').innerHTML=arr.map(g=>`<div class="item"><strong>${esc(g.name)}</strong><p class="sub">Target: ${esc(g.target)} ${esc(g.unit)} · ${esc(g.category)}</p></div>`).join('')||'<p class="sub">No goals set for this month yet. Add goals to keep your focus visible.</p>';
}

// Install the fixed October 12–December 18 program once.
// Logs and other saved data remain intact.
installFixedProgram();
$('logDate').value=localDate(now);
$('bwDate').value=localDate(now);
$('goalMonth').value=localDate(now).slice(0,7);
$('goalMonth').addEventListener('change',renderGoals);
$('feelingDate').value=localDate(now);
renderHome();
renderGoals();
</script>
</body>
</html>
