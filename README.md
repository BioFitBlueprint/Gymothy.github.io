<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Atelier Fit — Workout Planner</title>
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' rx='22' fill='%23111'/%3E%3Ctext x='50' y='66' font-size='54' text-anchor='middle' fill='%23f4efe7' font-family='Georgia,serif'%3EA%3C/text%3E%3C/svg%3E">
<script>window.WORDS = window.WORDS || [];</script>
<style>
:root{
  --bg:#f4efe7; --card:#ffffff; --ink:#111111; --muted:#6f6b64; --line:#e4ded3;
  --soft:#faf7f2; --accent:#111111; --shadow:0 1px 2px rgba(17,17,17,.04),0 8px 24px rgba(17,17,17,.06);
}
*{box-sizing:border-box;margin:0;padding:0}
html{-webkit-text-size-adjust:100%}
body{
  font-family:system-ui,-apple-system,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  background:var(--bg);color:var(--ink);line-height:1.5;letter-spacing:.01em;
  padding:max(24px,env(safe-area-inset-top)) 16px max(40px,env(safe-area-inset-bottom));
  min-height:100vh;
}
.wrap{max-width:640px;margin:0 auto}
header{padding:8px 4px 20px}
.brand{font-size:12px;font-weight:600;letter-spacing:.22em;text-transform:uppercase;color:var(--muted)}
h1{font-size:30px;font-weight:600;letter-spacing:-.02em;margin-top:6px}
.date{font-size:14px;color:var(--muted);margin-top:2px}
.tabs{display:flex;gap:6px;overflow-x:auto;padding:4px 2px 14px;scrollbar-width:none}
.tabs::-webkit-scrollbar{display:none}
.tab{
  flex:1 0 auto;min-width:52px;padding:10px 12px;border-radius:12px;border:1px solid var(--line);
  background:var(--card);color:var(--ink);font:inherit;font-size:13px;font-weight:500;cursor:pointer;
  position:relative;transition:all .2s ease;
}
.tab:hover{border-color:#c9c2b5}
.tab.active{background:var(--ink);color:#fff;border-color:var(--ink)}
.tab.today::after{content:"";position:absolute;top:6px;right:7px;width:5px;height:5px;border-radius:50%;background:#b9a98c}
.tab.active.today::after{background:#d9c9a8}
.card{background:var(--card);border:1px solid var(--line);border-radius:20px;box-shadow:var(--shadow);padding:24px;margin-bottom:16px}
.card h2{font-size:22px;font-weight:600;letter-spacing:-.015em}
.focus{font-size:14px;color:var(--muted);margin-top:4px}
.progress{margin-top:20px}
.pmeta{display:flex;justify-content:space-between;font-size:12px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:var(--muted);margin-bottom:8px}
.bar{height:6px;background:#ece7dd;border-radius:99px;overflow:hidden}
.bar>i{display:block;height:100%;width:0;background:var(--ink);border-radius:99px;transition:width .35s ease}
.group-title{font-size:11px;font-weight:600;letter-spacing:.2em;text-transform:uppercase;color:var(--muted);margin-bottom:6px}
.row{
  display:flex;align-items:center;gap:14px;padding:14px 4px;border-bottom:1px solid var(--line);cursor:pointer;
  -webkit-tap-highlight-color:transparent;
}
.row:last-child{border-bottom:0}
.row input{position:absolute;opacity:0;pointer-events:none}
.box{
  flex:0 0 24px;height:24px;border-radius:8px;border:1.5px solid #bdb6a8;background:#fff;
  display:grid;place-items:center;transition:all .18s ease;
}
.box svg{width:14px;height:14px;stroke:#fff;fill:none;stroke-width:3;stroke-linecap:round;stroke-linejoin:round;opacity:0;transform:scale(.6);transition:all .18s ease}
.row input:checked + .box{background:var(--ink);border-color:var(--ink)}
.row input:checked + .box svg{opacity:1;transform:scale(1)}
.row input:focus-visible + .box{outline:2px solid #b9a98c;outline-offset:2px}
.txt{flex:1;min-width:0}
.name{font-size:16px;font-weight:500;transition:color .2s}
.detail{font-size:13px;color:var(--muted)}
.row input:checked ~ .txt .name{color:#a29c90;text-decoration:line-through;text-decoration-color:#c9c2b5}
.group + .group{margin-top:22px}
.rest{text-align:center;padding:44px 24px}
.rest .big{font-size:44px;line-height:1;margin-bottom:12px}
.rest p{color:var(--muted);font-size:15px;margin-top:6px}
.wordbtn{
  display:none;width:100%;margin-top:16px;padding:13px;border-radius:12px;border:1px solid var(--line);
  background:var(--soft);font:inherit;font-size:14px;font-weight:600;cursor:pointer;color:var(--ink)
}
.wordbtn.show{display:block}
.note{text-align:center;font-size:12px;color:var(--muted);margin-top:8px}
.overlay{
  position:fixed;inset:0;background:rgba(17,17,17,.55);backdrop-filter:blur(6px);-webkit-backdrop-filter:blur(6px);
  display:none;align-items:center;justify-content:center;padding:20px;z-index:50;
}
.overlay.show{display:flex;animation:fade .25s ease}
.modal{
  background:var(--card);border-radius:24px;max-width:440px;width:100%;padding:36px 28px 28px;text-align:center;
  box-shadow:0 24px 60px rgba(0,0,0,.28);animation:rise .35s cubic-bezier(.2,.8,.2,1);
}
.modal .eyebrow{font-size:11px;font-weight:600;letter-spacing:.24em;text-transform:uppercase;color:var(--muted)}
.modal .rule{width:36px;height:1px;background:#cfc8ba;margin:16px auto}
.modal h3{font-family:Georgia,"Times New Roman",serif;font-size:40px;font-weight:500;letter-spacing:-.01em;word-break:break-word}
.modal p{font-size:16px;color:#3b3935;margin-top:14px;line-height:1.6}
.modal button{
  margin-top:26px;padding:13px 32px;border-radius:12px;border:0;background:var(--ink);color:#fff;
  font:inherit;font-size:14px;font-weight:600;letter-spacing:.04em;cursor:pointer
}
@keyframes fade{from{opacity:0}to{opacity:1}}
@keyframes rise{from{opacity:0;transform:translateY(14px) scale(.98)}to{opacity:1;transform:none}}
@media (max-width:420px){h1{font-size:26px}.card{padding:20px}.modal h3{font-size:34px}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div class="brand">Atelier Fit</div>
    <h1 id="greet">Workout Planner</h1>
    <div class="date" id="dateLine"></div>
  </header>
  <nav class="tabs" id="tabs" aria-label="Days of the week"></nav>
  <main id="view"></main>
</div>

<div class="overlay" id="overlay" role="dialog" aria-modal="true" aria-labelledby="mWord">
  <div class="modal">
    <div class="eyebrow">Workout Complete · Word of the Day</div>
    <div class="rule"></div>
    <h3 id="mWord"></h3>
    <p id="mDef"></p>
    <button id="mClose">Continue</button>
  </div>
</div>

<script>
const SCHEDULE = {
  Monday:{title:"Abs & Lower Body A",focus:"Quads, Hamstrings, Glutes, Calves, Inner Thighs, & Core",groups:[
    ["Primary",[["Leg Extensions","3 x 12"],["Leg Press","3 x 12"],["Bulgarian Split Squats","3 x 10"],["Hamstring Curls","3 x 12"]]],
    ["Accessory",[["Lifted Calf Raises","4 x 12"],["Wide Dumbbell Sumo Squats","3 x 10"],["Ab Crunches","6 x 20"],["Plank","1 Minute"],["Russian Twists","4 x 30 Seconds"]]],
    ["Finish",[["Stretch",""],["Roll Out",""],["Treadmill Inclined Walking","30 Minutes"]]]]},
  Tuesday:{title:"Upper Body A",focus:"Chest, Back, Shoulders, Biceps, Triceps, & Forearms",groups:[
    ["Primary",[["Chest Press","4 x 12"],["Wide-Grip Lat Pulldown","3 x 12"],["Seated Cable Row","3 x 12"],["Shoulder Press","4 x 10"],["Lateral Raises","3 x 12"],["Machine Bicep Curls","4 x 10"]]],
    ["Accessory",[["Overhead Tricep Extensions","3 x 12"],["Hammer Curls","4 x 10"],["Dumbbell Bent-Over Reverse Flies","3 x 12"]]],
    ["Finish",[["Stretch",""],["Roll Out",""],["Treadmill Inclined Walking","45 Minutes"]]]]},
  Wednesday:{title:"Cardio + Abs + Lower Body B",focus:"Cardio, Glutes, Hamstrings, Quads, Calves, & Core",groups:[
    ["Primary",[["Single-Legged Leg Press","3 x 12"],["Hamstring Curls","3 x 12"]]],
    ["Accessory",[["Weighted Lunges","3 x 5 Laps"],["Side Plank","30 Seconds"],["Plank","1 Minute"]]],
    ["Finish",[["Stretch",""],["Roll Out",""],["Treadmill Inclined Walking","30 Minutes"]]]]},
  Thursday:{rest:true,title:"Rest Day"},
  Friday:{title:"Cardio + Upper Body B",focus:"Cardio, Chest, Back, Shoulders, Biceps, Triceps, & Forearms",groups:[
    ["Primary",[["Chest Press","3 x 10"],["Close Inside-Grip Lat Pulldowns","3 x 12"],["Rope Lat Pulldowns","3 x 12"],["Shoulder Press","3 x 10"]]],
    ["Accessory",[["Bent-Over Dumbbell Rows","3 x 12"],["Dumbbell Bent-Over Reverse Flies","3 x 12"],["Shoulder Shrugs","3 x 15"],["Reverse Dumbbell Curls","4 x 10"],["Kettlebell Wrist Curls","4 x 12"]]],
    ["Finish",[["Stretch",""],["Foam Roll",""],["Treadmill Inclined Walking","1 Hour"]]]]},
  Saturday:{rest:true,title:"Rest Day"},
  Sunday:{rest:true,title:"Rest Day"}
};
const ORDER = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"];
const JS_DAYS = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];

const store = {
  get(k,f){ try{ const v=localStorage.getItem(k); return v?JSON.parse(v):f; }catch(e){ return f; } },
  set(k,v){ try{ localStorage.setItem(k,JSON.stringify(v)); }catch(e){} }
};

const FALLBACK = ["Resilience: The ability to bounce back quickly after facing tough times or setbacks.","Momentum: The unstoppable forward speed and energy you build up once you get going.","Grit: Toughness, passion, and sticking with long-term goals even when it hurts."];

function getWords(){
  const seen = new Set(), out = [];
  (window.WORDS.length ? window.WORDS : FALLBACK).forEach(line=>{
    line = String(line).trim(); if(!line) return;
    const i = line.indexOf(": "); if(i<1) return;
    const w = line.slice(0,i).trim(); if(seen.has(w)) return;
    seen.add(w); out.push([w,line.slice(i+2).trim()]);
  });
  return out;
}

function pickWord(key){
  const all = getWords(), daily = store.get("af_daily",{});
  const existing = all.find(x=>x[0]===daily[key]);
  if(existing) return existing;
  let used = store.get("af_used",[]);
  let pool = all.filter(x=>!used.includes(x[0]));
  if(!pool.length){ used=[]; pool=all; }
  const w = pool[Math.floor(Math.random()*pool.length)];
  used.push(w[0]); daily[key]=w[0];
  store.set("af_used",used); store.set("af_daily",daily);
  return w;
}

function pad(n){ return String(n).padStart(2,"0"); }
function dateKeyFor(dayName){
  const now = new Date(), diff = JS_DAYS.indexOf(dayName) - now.getDay();
  const d = new Date(now.getFullYear(),now.getMonth(),now.getDate()+diff);
  return d.getFullYear()+"-"+pad(d.getMonth()+1)+"-"+pad(d.getDate());
}
function todayName(){ return JS_DAYS[new Date().getDay()]; }

let selected = todayName(), lastToday = selected;
const view = document.getElementById("view"), tabs = document.getElementById("tabs");

function buildTabs(){
  tabs.innerHTML = "";
  ORDER.forEach(d=>{
    const b = document.createElement("button");
    b.className = "tab"+(d===selected?" active":"")+(d===todayName()?" today":"");
    b.textContent = d.slice(0,3);
    b.setAttribute("aria-label",d);
    b.onclick = ()=>{ selected=d; buildTabs(); render(); };
    tabs.appendChild(b);
  });
}

function esc(s){ return s.replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c])); }

function render(){
  const day = SCHEDULE[selected], key = dateKeyFor(selected);
  document.getElementById("dateLine").textContent =
    new Date().toLocaleDateString(undefined,{weekday:"long",month:"long",day:"numeric"});
  document.getElementById("greet").textContent = selected===todayName() ? "Today’s Session" : selected+"’s Session";

  if(day.rest){
    view.innerHTML = '<div class="card rest"><div class="big">☾</div><h2>Rest Day</h2><p>Recovery is part of the program. Rest well.</p></div>';
    return;
  }
  const checks = (store.get("af_checks",{})[key]) || {};
  let total = 0, html = "";
  day.groups.forEach((g,gi)=>{
    html += '<div class="group"><div class="group-title">'+g[0]+'</div>';
    g[1].forEach((it,ii)=>{
      const id = gi+"-"+ii; total++;
      html += '<label class="row"><input type="checkbox" data-id="'+id+'"'+(checks[id]?" checked":"")+'>'+
        '<span class="box"><svg viewBox="0 0 24 24"><path d="M5 12.5l4.5 4.5L19 7.5"/></svg></span>'+
        '<span class="txt"><div class="name">'+esc(it[0])+'</div>'+(it[1]?'<div class="detail">'+esc(it[1])+'</div>':"")+'</span></label>';
    });
    html += '</div>';
  });
  view.innerHTML =
    '<div class="card"><h2>'+esc(day.title)+'</h2><div class="focus">'+esc(day.focus)+'</div>'+
    '<div class="progress"><div class="pmeta"><span>Progress</span><span id="pcount"></span></div><div class="bar"><i id="pbar"></i></div></div>'+
    '<button class="wordbtn" id="wordbtn">View Today’s Word</button></div>'+
    '<div class="card">'+html+'</div><div class="note">Progress saves automatically on this device.</div>';

  const boxes = [...view.querySelectorAll("input[type=checkbox]")];
  function update(){
    const done = boxes.filter(b=>b.checked).length;
    document.getElementById("pcount").textContent = done+" / "+total;
    document.getElementById("pbar").style.width = (done/total*100)+"%";
    document.getElementById("wordbtn").classList.toggle("show",done===total);
    return done===total;
  }
  update();
  document.getElementById("wordbtn").onclick = ()=>showWord(key);
  boxes.forEach(b=>b.addEventListener("change",()=>{
    const all = store.get("af_checks",{});
    all[key] = all[key] || {};
    if(b.checked) all[key][b.dataset.id] = true; else delete all[key][b.dataset.id];
    store.set("af_checks",all);
    if(update() && b.checked) setTimeout(()=>showWord(key),350);
  }));
}

const overlay = document.getElementById("overlay");
function showWord(key){
  const w = pickWord(key);
  document.getElementById("mWord").textContent = w[0];
  document.getElementById("mDef").textContent = w[1];
  overlay.classList.add("show");
}
function closeModal(){ overlay.classList.remove("show"); }
document.getElementById("mClose").onclick = closeModal;
overlay.addEventListener("click",e=>{ if(e.target===overlay) closeModal(); });
document.addEventListener("keydown",e=>{ if(e.key==="Escape") closeModal(); });

document.addEventListener("visibilitychange",()=>{
  if(!document.hidden && todayName()!==lastToday){ lastToday=todayName(); selected=lastToday; buildTabs(); render(); }
});

document.addEventListener("DOMContentLoaded",()=>{ buildTabs(); render(); });
</script>
</body>
</html>

<script>
window.WORDS = (window.WORDS || []).concat(`Pygmalion Effect: When high expectations from others actually lead you to perform better.
Amor Fati: Loving your fate—fully accepting everything that happens in life, good or bad, as necessary.
Ataraxia: A state of deep, unshakeable calm where nothing can disturb your peace of mind.
Metanoia: A profound, life-changing shift in how you think, feel, and see the world.
Autotelic: Doing something purely for the joy of doing it, rather than for a reward or outside validation.
Eudaimonia: True human flourishing; the deep happiness that comes from living a meaningful, virtuous life.
Catharsis: The emotional relief you feel after finally letting out pent-up feelings, like having a good cry.
Hubris: Dangerous overconfidence or arrogance that usually leads to a downfall.
Resilience: The ability to bounce back quickly after facing tough times or setbacks.
Ikigai: Your "reason for being"—the sweet spot where what you love, what you're good at, what the world needs, and what pays you all meet.
Rhapsody: An intense, overflowing burst of pure enthusiasm or joy.
Sonder: The sudden realization that every random stranger passing by has a life just as vivid, messy, and complex as yours.
Petrichor: That fresh, earthy smell in the air right after rain falls on dry ground.
Vellichor: The quiet, nostalgic feeling you get when walking through an old, used bookstore.
Meraki: Putting your absolute heart, soul, and creativity into whatever you are making or doing.
Chrysalis: A sheltered, transitional phase where you are quietly growing and changing before emerging stronger.
Evocative: Something that instantly brings strong memories, images, or emotions to mind.
Ineffable: Something so huge, beautiful, or intense that words just can't do it justice.
Luminous: Glowing brightly; shining with light or inspiration.
Resonant: Something that strikes a deep chord with you and lingers in your mind.
Tenacity: Stubborn determination; refusing to let go of a goal no matter how hard it gets.
Resolve: A firm, locked-in decision to see something through.
Audacity: The guts to take bold, surprising risks (or sometimes, just plain nerve).
Impetus: The initial push or spark of energy that gets things moving.
Momentum: The unstoppable forward speed and energy you build up once you get going.
Catalyst: A person or event that sparks a major, rapid change.
Fortitude: Quiet mental toughness and courage when dealing with pain or hard times.
Vigor: Strong physical and mental energy, health, and enthusiasm.
Mettle: Your true grit and spirit when tested under pressure.
Drive: A powerful inner hunger to achieve your goals.
Ephemeral: Lasting for only a brief, fleeting moment.
Numinous: Having a mysterious, spiritual, or awe-inspiring quality that feels bigger than yourself.
Liminal: Being in the "in-between" stage—standing on the threshold between what was and what's next.
Synergy: When two or more people or things work together to create something way better than they could alone.
Paradox: Something that seems completely contradictory at first, yet turns out to be true.
Zenith: The absolute highest peak of success, power, or achievement.
Nadir: The absolute lowest point or rock bottom.
Stoicism: Staying calm, self-controlled, and unbothered by things outside your control, without complaining.
Teleology: The idea that things exist for a specific ultimate purpose or end goal.
Pragmatism: Focusing on what actually works in the real world rather than just theories or ideals.
Pugnacious: Quick to argue, challenge, or pick a fight.
Indomitable: Impossible to break, defeat, or discourage.
Valiant: Showing genuine bravery and determination.
Dauntless: Fearless and impossible to intimidate.
Resolute: Purposeful, firm, and completely unwavering.
Steadfast: Loyal, steady, and refusing to budge from your path.
Tireless: Working with endless energy without giving up.
Relentless: Never slowing down, easing up, or stopping until the job is done.
Unfaltering: Steady and confident without hesitating or stumbling.
Formidable: So strong, capable, or intense that it commands instant respect (or fear).
Serendipity: Happily stumbling upon something wonderful completely by accident.
Epiphany: A sudden "aha!" moment where everything clicks into place.
Wonder: A feeling of pure amazement and curiosity at something extraordinary.
Sublime: So breathtakingly great or beautiful that it leaves you in awe.
Panacea: A cure-all solution for every problem.
Nebulous: Hazy, vague, or not clearly defined yet.
Halcyon: Looking back on a past time that felt completely peaceful, golden, and happy.
Solace: Comfort and peace when you are feeling sad or stressed.
Alacrity: Eager, cheerful readiness to jump into action.
Integrity: Doing the right thing and sticking to your morals, even when nobody is watching.
Veracity: Strict honesty and truthfulness.
Equanimity: Keeping a cool head and emotional balance during a crisis.
Magnanimity: Being big-hearted, generous, and forgiving—especially toward rivals or people with less power.
Benevolence: Genuine kindness and wanting the best for others.
Verve: Lively spirit, enthusiasm, and energy.
Gravitas: Natural weight, seriousness, and dignity that makes people take you seriously.
Sanguine: Staying genuinely optimistic and hopeful, even when things look rough.
Ascetic: Living simply with strict self-discipline, skipping luxuries to focus on higher goals.
Candid: Blunt, honest, and straightforward.
Kinetic: Full of active motion and energy.
Dynamic: Constantly evolving, energetic, and sparking change.
Mercurial: Unpredictable, lively, and quick to shift moods or ideas.
Fluorescent: Glowing vividly and brightly.
Scintillating: Sparkling brightly, or being brilliantly clever and engaging.
Effervescent: Bubbly, lively, and full of upbeat energy.
Ebullient: Overflowing with cheerfulness and excitement.
Zeal: Intense passion and energy for a cause or goal.
Fervor: Deep, burning passion and intensity.
Ardor: Warm, intense devotion or enthusiasm.
Aeon: An unimaginably long stretch of time.
Semper: A Latin word meaning "always" or "forever."
Eternity: Time without end.
Legacy: The lasting mark or impact you leave behind on the world.
Epoch: A major, defining chapter or era in history or your life.
Continuum: A seamless flow where things gradually blend from one stage into the next.
Genesis: The very beginning or origin of something.
Apex: The very top point or peak.
Faeloria: A made-up, fantasy-sounding name with no official dictionary meaning.
Patience: Staying calm and composed while waiting or dealing with delays and frustrations.
Insanity: Total madness, or doing something wildly irrational.
Defiance: Boldly refusing to obey or back down.
Sovereignty: Having total authority and control over yourself or a nation.
Autonomy: The freedom to govern yourself and make your own choices.
Metamorphosis: A complete, dramatic transformation into something entirely new.
Triumph: A massive victory or hard-won achievement.
Aplomb: Cool, effortless self-confidence under pressure.
Sisu: A Finnish word for extraordinary grit—pushing forward with sheer guts when you have nothing left in the tank.
Kaizen: The Japanese philosophy of making small, continuous improvements every single day.
Wabi Sabi: Finding beauty in imperfection, impermanence, and things that are worn or incomplete.
Kintsugi: The Japanese art of repairing broken pottery with gold, treating the cracks as part of its beauty rather than hiding them.
Fernweh: A deep ache to travel and explore faraway places you've never been.
Wanderlust: A strong, restless urge to travel the world.
Hiraeth: A Welsh feeling of deep homesickness for a place, time, or version of home you can't return to.
Ubuntu: An African philosophy meaning "I am because we are"—the idea that our humanity is tied to how we treat others.
Agape: Unconditional, selfless love for everyone.
Philotimo: A Greek ideal combining personal honor, pride, duty, and doing what is right for others.
Dadirri: An Indigenous Australian practice of deep, quiet inner listening and stillness.
Mudita: Taking pure joy in someone else's success or happiness without feeling jealous.
Sati: Being completely present, awake, and mindful in the current moment.
Samadhi: A state of deep, total focus reached through meditation where your mind becomes completely still.
Nirvana: A state of ultimate peace, liberation, and freedom from suffering.
Satori: A sudden flash of deep spiritual insight or awakening.
Kensho: A Zen term meaning "seeing your true nature"—an initial glimpse of enlightenment.
Zanshin: A state of relaxed, total awareness where you stay alert even after an action is finished.
Mushin: "No mind"—a flow state where you act purely on instinct without overthinking.
Shoshin: "Beginner's mind"—approaching things with curiosity, openness, and zero ego, no matter how much you already know.
Bushido: The strict samurai code of honor, loyalty, courage, and self-discipline.
Yuugen: A deep, mysterious sense of the universe's beauty that you feel rather than see directly.
Komorebi: Sunlight filtering through the leaves of trees.
Shinrin Yoku: "Forest bathing"—slowing down and soaking in the atmosphere of nature to recharge your mind and body.
Iktsuarpok: That restless excitement of waiting for someone to arrive that makes you keep checking outside.
Forelsket: The thrilling rush and euphoria of first falling in love.
Saudade: A bittersweet, nostalgic longing for someone or something you love that is far away or gone.
Sehnsucht: A deep, aching yearning for an ideal life or happiness that feels just out of reach.
Weltschmerz: Feeling heavy-hearted or weary because the real world falls short of how you wish it could be.
Sturm Und Drang: "Storm and stress"—a period or style of intense, turbulent emotion and rebellion.
Zeitgeist: The defining mood, vibe, and ideas of a specific generation or era.
Schadenfreude: Secretly feeling a little happy when something bad happens to someone else.
Fingerspitzengefühl: Having sharp intuition and tact—knowing instinctively how to handle delicate situations.
Eudaimonic: Anything that brings deep, lasting fulfillment and purpose rather than just quick pleasure.
Arete: Living up to your highest potential and pursuing excellence in everything you do.
Phronesis: Practical street-smarts and wisdom—knowing how to make the right call in real-life situations.
Sophrosyne: Self-control, balance, and soundness of mind; knowing how to avoid extremes.
Aletheia: Uncovering the raw, hidden truth of things.
Kairos: The exact right, golden moment to take action.
Chronos: Regular, ticking clock-time moving forward second by second.
Praxis: Putting ideas and theories into real-world action.
Techne: Practical craftsmanship, skill, and the art of making things.
Poiesis: Creating something brand new and bringing it into existence.
Logos: Logic, reason, and clear thinking.
Pathos: Deep emotion and the ability to move people's feelings.
Ethos: Your core character, credibility, and moral values.
Nous: Sharp intellect, common sense, and intuitive understanding.
Psyche: Your mind, soul, and inner emotional life.
Pneuma: Breath of life, spirit, or vital energy.
Anima: The inner feminine side of a person's psyche, or the soul.
Animus: The inner masculine side of a person's psyche, or driving spirit.
Imago: A mental blueprint of someone (often from childhood) that shapes how you view others; also the final adult stage of an insect.
Archetype: A classic, universal pattern or role model (like "the hero" or "the mentor") that shows up across cultures.
Individuation: The lifelong process of figuring out who you truly are as a unique, whole individual.
Sublimation: Channeling raw, intense impulses (like anger or frustration) into something positive, like art, sports, or hard work.`.split("\n"));
</script>
<script>
window.WORDS = (window.WORDS || []).concat(`Transcendence: Rising above ordinary limits to experience something higher.
Immanence: Being deeply present and woven into the physical world right here and now.
Apotheosis: Reaching the ultimate peak or highest possible version of something.
Ascension: Rising up to a higher level, rank, or state of mind.
Elevation: Lifting yourself or something else to a higher standard or perspective.
Exaltation: A feeling of intense joy, triumph, and spiritual uplift.
Jubilation: Loud, celebratory joy after a big win.
Euphoria: An overwhelming rush of intense happiness and excitement.
Elation: Feeling thrilled, proud, and on top of the world.
Beatitude: A state of deep, peaceful blessedness and joy.
Felicity: Pure happiness, or the knack for expressing yourself effortlessly.
Bliss: Complete, worry-free joy and contentment.
Rapture: Being completely swept away by intense joy or wonder.
Ecstasy: An overwhelming wave of pure happiness.
Transport: Being carried away by an emotion so strong you forget everything else.
Enthrallment: Being completely hooked, fascinated, and spellbound.
Captivation: Holding someone's total attention through charm or brilliance.
Fascination: Intense curiosity and attraction toward something intriguing.
Reverence: Deep, humble respect for something sacred or remarkable.
Veneration: Looking up to someone or something with deep admiration and respect.
Awe: A mix of amazement, wonder, and deep respect when facing something huge or extraordinary.
Sublimity: Greatness or beauty so vast it feels almost overwhelming.
Majesty: Impressive dignity, power, and royal beauty.
Grandeur: Magnificent scale, beauty, and impressiveness.
Splendor: Dazzling beauty and brilliance.
Magnificence: Extraordinary beauty, power, or impressiveness.
Radiance: Warm, glowing light or joy shining outward from someone.
Brilliance: Dazzling brightness, or razor-sharp talent and intelligence.
Incandescence: Glowing white-hot with light, energy, or passion.
Luminescence: Giving off a cool, steady glow without heat.
Phosphorescence: Continuing to glow softly in the dark even after the light source is gone.
Iridescence: Shifting through rainbow colors depending on the angle you look at it, like a soap bubble.
Opalescence: A soft, milky, shifting shimmer like an opal stone.
Effulgence: Shining out with brilliant, unstoppable radiance.
Refulgence: Glowing brightly and gloriously.
Lambency: A soft, gentle, flickering glow.
Resplendence: Dazzling, rich, and eye-catching beauty.
Luster: A soft, healthy sheen or glow.
Sheen: A smooth, soft shine on a surface.
Gleam: A brief, sharp flash or reflection of light.
Coruscation: A sudden, vivid flash or sparkle of light (or brilliance).
Scintillation: A quick, bright twinkle or spark; also a brilliantly witty remark.
Fulmination: A sudden, explosive flash like lightning, or speaking out fiercely against something.
Conflagration: A massive, roaring fire.
Ignition: The spark that lights a fire or kicks off an engine.
Kindling: Small twigs or sparks used to get a big fire started.
Combustion: Burning with intense heat, light, and chemical energy.
Incineration: Burning something completely to ashes.
Phoenix: A mythical bird that burns to ashes and rises again, reborn and stronger—a symbol of starting over after total failure.
Rebirth: Starting fresh with new life, energy, and purpose.
Renaissance: A major revival of creativity, learning, and energy after a quiet period.
Resurgence: Making a strong comeback after being down or quiet.
Revival: Bringing something back to life, strength, or popularity.
Rejuvenation: Restoring youthful energy, freshness, and vitality.
Regeneration: Regrowing, healing, and rebuilding what was damaged.
Renewal: Refreshing your energy, commitment, or outlook after a break.
Restoration: Repairing something and bringing it back to its original strength or beauty.
Redemption: Making up for past mistakes and turning things around for the better.
Absolution: Being completely freed from guilt, blame, or past burdens.
Emancipation: Breaking free from restrictions or control.
Liberation: Setting yourself or others free from limits or oppression.
Manumission: Formal release from slavery or bondage.
Deliverance: Being rescued or set free from a tough situation.
Salvation: Being saved from ruin, harm, or failure.
Providence: Timely guidance, good fortune, or smart preparation for the future.
Seraphic: Pure, radiant, and angelic.
Celestial: Relating to the sky, stars, or heavens.
Ethereal: So delicate, light, and graceful that it feels almost otherworldly.
Empyrean: The highest, purest part of the heavens.
Astral: Relating to the stars and outer space.
Cosmic: Vast, universal, and connected to the entire universe.
Sidereal: Measured by or relating to the distant stars.
Stelliferous: Filled or sparkling with stars.
Galactic: On the massive scale of an entire galaxy.
Infinite: Having no end, edge, or limit.
Boundless: Having no boundaries; endless in potential or space.
Limitless: With zero caps or restrictions on how far you can go.
Illimitable: Impossible to measure or limit.
Unfettered: Completely free from chains, rules, or obstacles holding you back.
Unbridled: Wild, unrestrained, and holding nothing back.
Untamed: Free, natural, and refusing to be controlled.
Unconquered: Never defeated or broken.
Invictus: Latin for "unconquered"—staying the master of your own fate no matter what happens.
Invincible: Too strong to ever be defeated.
Insuperable: Impossible to overcome or beat.
Insurmountable: Too huge or steep to get past.
Unassailable: Impossible to attack, shake, or defeat.
Impregnable: Built so strong that nothing can break through.
Inviolable: Sacred and impossible to break or disrespect.
Sacrosanct: Too important and valuable to ever be messed with.
Immutable: Permanent and impossible to change.
Inexorable: Unstoppable; moving forward no matter what stands in the way.
Implacable: Relentless and impossible to calm down or stop.
Unrelenting: Never giving up, slowing down, or backing off.
Unremitting: Constant and nonstop without taking a break.
Unyielding: Refusing to bend, cave in, or surrender under pressure.
Unbending: Firm, straight, and refusing to compromise on principles.
Unwavering: Steady, confident, and never second-guessing yourself.
Unflinching: Facing danger or hard truths head-on without blinking or backing down.
Intrepid: Bold, fearless, and ready for adventure.
Audacious: Fearlessly daring and willing to take big risks.
Temerarious: Recklessly bold; jumping in without worrying about danger.
Venturesome: Eager to take risks and try new, challenging paths.
Chivalrous: Honorable, courteous, and protective of others.
Gallant: Brave, noble, and heroic.
Heroic: Showing extraordinary courage and selflessness.
Herculean: Requiring massive strength, stamina, and effort.
Titanic: Giant in size, strength, or impact.
Promethean: Rebelliously creative and daring—willing to break rules to bring new ideas to the world.
Atlas: Someone carrying a massive weight or responsibility on their shoulders.
Goliath: A giant, powerhouse figure or obstacle.
Colossus: Something or someone of monumental size, power, or importance.
Leviathan: A massive, unstoppable sea creature or powerhouse force.
Behemoth: Something huge and overwhelmingly powerful.
Juggernaut: A massive, unstoppable force that crushes everything in its path.
Dynamo: A non-stop powerhouse of energy and action.
Powerhouse: Someone or something packed with immense strength, talent, or energy.
Vanguard: The leaders at the very front of a new movement or breakthrough.
Pioneer: One of the very first people to explore new territory or invent a new way of doing things.
Trailblazer: Someone who carves out a brand-new path for others to follow.
Pathfinder: Someone who goes ahead to scout out the way through uncharted territory.
Harbinger: A sign or messenger announcing that something big is about to arrive.
Forerunner: Someone or something that comes first and paves the way for what follows.
Precursor: An early version or signal that leads directly to something greater.
Progenitor: The original creator, ancestor, or starting point of a line or idea.
Architect: The mastermind who designs and builds a big vision from the ground up.
Virtuoso: A master with jaw-dropping skill in music or any craft.
Maestro: A brilliant master and leader in their field.
Savant: Someone with deep, exceptional knowledge or genius in a specific area.
Polymath: A Renaissance person who is wildly knowledgeable and skilled across many different subjects.
Prodigy: Someone—especially young—born with extraordinary natural talent.
Luminary: A brilliant leader who inspires and lights the way for others.
Paragon: The ultimate role model or shining example of a great quality.
Exemplar: A top-tier model worth copying or looking up to.
Quintessence: The purest, most concentrated form of what makes something great.
Epitome: The perfect embodiment or ultimate example of something.
Apogee: The highest point of achievement or development.
Culmination: The grand finale or peak result of long, hard work.
Pinnacle: The very top of success or achievement.
Summit: The highest peak of a mountain or your career.
Acme: The absolute peak of perfection or success.
Vertex: The highest tip or turning point.
Crest: The very top ridge of a hill or the peak of a rising wave.
Meridian: The highest point of power, prosperity, or brightness (like the sun at noon).
Solstice: A major turning point of the year (the longest or shortest day).
Equinox: A moment of perfect balance where day and night are equal.
Syzygy: A rare alignment where separate forces line up together in a straight line.
Convergence: Different paths, ideas, or people coming together to meet at one point.
Confluence: Two powerful streams flowing together into one stronger current.
Synthesis: Blending different ideas or parts together to create a brand-new whole.
Amalgamation: Combining multiple elements into one unified force.
Integration: Bringing separate pieces together so they work smoothly as one.
Harmony: Different elements working together in smooth, pleasing agreement.
Symphony: Many different parts coming together to create something grand and unified.
Euphony: Words or sounds that flow smoothly and sound great together.
Cadence: A steady, natural rhythm or flow in your voice or pace.
Rhythm: A strong, steady beat or pattern that keeps you moving.
Pulse: The steady, living beat of energy driving something forward.
Heartbeat: The central, vital force keeping everything alive and moving.
Lifeblood: The essential energy or factor that gives something its strength.
Essence: The core soul or defining quality of what makes something what it is.
Marrow: The deepest, most vital core inside something.
Core: The strong, central foundation at the heart of something.
Crux: The single most critical point that everything else hinges on.
Fulcrum: The central pivot point that gives a lever the power to lift heavy things.
Linchpin: The one key person or piece holding the entire operation together.
Cornerstone: The essential first stone that supports the entire structure.
Keystone: The central stone at the top of an arch that locks everything into place.
Bedrock: Solid, unshakeable ground you can safely build anything on.
Foundation: The solid base supporting everything you build on top of it.`.split("\n"));
</script>
<script>
window.WORDS = (window.WORDS || []).concat(`Bastion: A strong fortress that fiercely protects important values or people.
Citadel: A towering fortress overlooking and defending a city.
Bulwark: A solid defensive wall protecting you from setbacks or attacks.
Aegis: Powerful protection, support, or backing.
Vigilance: Staying wide awake, watchful, and ready for anything.
Perspicacity: Being sharp-eyed and quick to see through confusion to what really matters.
Acumen: Sharp, street-smart judgment that helps you make fast, smart decisions.
Sagacity: Deep wisdom paired with sharp practical judgment.
Sapience: Deep human wisdom and insight.
Erudition: Deep, impressive knowledge gained from serious study.
Omniscience: Knowing everything there is to know.
Clairvoyance: Sharp perception; being able to see clearly beyond the obvious.
Foresight: Looking ahead and preparing for what's coming next before it happens.
Prescience: Knowing or sensing how things will play out ahead of time.
Intuition: Your gut instinct—knowing something right away without having to overanalyze it.
Instinct: Your natural, built-in gut reaction.
Grit: Toughness, passion, and sticking with long-term goals even when it hurts.
Spunk: Feisty courage, spirit, and determination.
Moxie: Bold nerve, street-smarts, and refusing to be intimidated.
Panache: Doing things with bold style, flair, and confidence.
Elan: Energetic style, enthusiasm, and effortless grace.
Brio: Lively energy, spirit, and boldness.
Gustos: Doing things with real appetite, enjoyment, and enthusiasm (plural of gusto).
Zest: Energetic excitement and real enjoyment for life.
Piquancy: A sharp, exciting spark that keeps things interesting.
Vivacity: Being lively, bright, and full of life.
Ebullience: Bubbling over with high energy and cheerfulness.
Exuberance: Unstoppable excitement, energy, and positivity.
Effusiveness: Expressing warmth, gratitude, or excitement openly without holding back.
Buoyancy: The ability to stay afloat and bounce back up—keeping a light, cheerful spirit even under pressure.
Resiliency: Your natural ability to recover fast and adapt when knocked down.
Elasticity: Being flexible enough to stretch under stress and snap right back into shape.
Adaptability: Adjusting smoothly when plans or conditions suddenly change.
Versatility: Having a wide range of skills so you can handle almost any challenge.
Ingenuity: Cleverness and creativity in inventing smart solutions.
Resourcefulness: Finding clever ways to make things work using whatever you have on hand.
Inventiveness: Constantly coming up with fresh, original ideas.
Originality: Being authentic, creative, and refusing to just copy everyone else.
Authenticity: Being genuinely yourself without faking it.
Genuineness: Being real, honest, and sincere.
Sincerity: Meaning what you say and acting without fake motives.
Probity: Rock-solid honesty and strong moral character.
Rectitude: Straightforward moral goodness and doing what is right.
Uprightness: Standing tall with honesty, responsibility, and good character.
Nobility: Having high moral character, generosity, and dignity.
Chivalry: Acting with honor, courage, and respect toward others.
Altruism: Helping others selflessly without expecting anything in return.
Philanthropy: Generously giving your time, effort, or resources to improve the world.
Munificence: Extreme, big-hearted generosity.
Largesse: Generously sharing wealth, gifts, or kindness with others.
Clemency: Showing mercy and forgiveness instead of harshness.
Forbearance: Holding back anger and staying patient when someone tests your limits.
Longanimity: Quietly enduring tough times or provocations with patience and strength.
Composure: Staying calm, collected, and in control of yourself.
Sangfroid: Staying ice-cool and steady in high-stress or dangerous moments.
Poise: Graceful confidence, balance, and dignity under pressure.
Self Possession: Keeping complete control over your emotions and actions, no matter what happens.
Equilibrium: A steady state of balance where nothing throws you off center.
Homeostasis: Your body and mind's natural ability to keep things balanced and steady despite outside changes.
Serenity: Deep, untroubled peace and calm.
Tranquility: Quiet, peaceful stillness free from stress.
Placidity: Calm, smooth, and unbothered peace.
Quiescence: A quiet state of rest and stillness before new energy builds up.
Stillness: Complete calm without noise or restless movement.
Silence: Total quiet that gives your mind space to breathe.
Solitude: Being peacefully alone with your own thoughts by choice (not loneliness).
Contemplation: Taking quiet time to think deeply and thoughtfully about life.
Introspection: Looking inward to understand your own thoughts, feelings, and motives.
Reflection: Looking back thoughtfully on your experiences to learn and grow from them.
Meditation: Training your mind to focus, quiet the noise, and find clarity.
Mindfulness: Paying full, calm attention to what's happening right now without judging it.
Presence: Being fully locked into the current moment, or carrying a confident, magnetic aura.
Awareness: Being awake, alert, and tuned in to yourself and the world around you.
Sentience: The ability to feel, perceive, and experience life consciously.
Consciousness: Being fully awake, self-aware, and tuned in to reality.
Awakening: Waking up to a clearer, deeper understanding of yourself and life.
Enlightenment: Reaching deep clarity, wisdom, and freedom from confusion.
Illumination: A sudden flash of mental clarity or spiritual insight.
Revelation: A game-changing realization or truth suddenly becoming crystal clear.
Disillusionment: Letting go of false illusions and finally seeing reality for what it actually is.
Vindication: Being proven right after people doubted or criticized you.
Triumphant: Celebrating a hard-earned victory.
Victorious: Coming out on top as the winner.
Conquering: Defeating obstacles, fears, or challenges completely.
Overcoming: Successfully pushing past a tough barrier or struggle.
Surmounting: Climbing right over a major obstacle in your way.
Transcending: Rising completely above old limits, labels, or struggles.
Mastering: Developing total skill, confidence, and command over a craft or yourself.
Sovereign: Having full authority and rule over yourself.
Autonomous: Independent and free to steer your own life.
Self Reliant: Trusting your own abilities and resources to handle whatever comes your way.
Emancipated: Set completely free from restrictions or control.
Unchained: Broken free from anything holding you back.
Unbound: Untied, unrestricted, and free to move.
Free: Able to choose your own path without being controlled.
Wild: Untamed, bold, and true to your natural spirit.
Alive: Fully awake, energized, and actively living every moment.`.split("\n"));
</script>
