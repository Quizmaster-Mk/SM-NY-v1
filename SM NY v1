<!doctype html>
<html lang="fr">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Spider-Man : Nuit à New York — V1</title>
<meta name="description" content="Mini-jeu Spider-Man : QTE, poursuite, combats - comics coloré" />
<style>
  :root{
    --bg:#0b1b2b; --panel:#112635; --accent:#ff385c; --accent2:#ffd166;
    --text:#f7f7f7; --muted:#b9c6d0;
  }
  *{box-sizing:border-box}
  html,body{height:100%;margin:0;background:linear-gradient(180deg,#09121b,#071218);color:var(--text);font-family:Inter,system-ui,Segoe UI,Roboto,Arial;padding:12px}
  .wrap{max-width:880px;margin:12px auto;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.04));border-radius:14px;padding:12px;border:1px solid rgba(255,255,255,0.03);box-shadow:0 20px 60px rgba(1,7,12,0.7)}
  header{display:flex;align-items:center;justify-content:space-between;gap:12px}
  h1{margin:.2rem 0;font-size:20px}
  .muted{color:var(--muted);font-size:13px}
  .panel{background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.003));padding:12px;border-radius:10px;margin-top:10px;border:1px solid rgba(255,255,255,0.02)}
  .center{display:flex;align-items:center;justify-content:center}
  .btn{background:var(--accent);border:none;color:#fff;padding:10px 14px;border-radius:10px;font-weight:700;cursor:pointer;margin:6px}
  .btn.secondary{background:#153d58}
  .row{display:flex;gap:8px;align-items:center}
  .col{flex:1}
  .hud{display:flex;gap:12px;align-items:center}
  .avatar{font-size:46px}
  .pvbar{height:14px;background:#07202a;border-radius:10px;overflow:hidden;border:1px solid rgba(255,255,255,0.03);width:200px}
  .fill{height:100%;background:linear-gradient(90deg,var(--accent2),#ff7b7b);transition:width .45s}
  #log{height:180px;overflow:auto;padding:8px;background:rgba(0,0,0,0.12);border-radius:8px;color:var(--muted);font-size:13px}
  .actions{display:flex;gap:8px;margin-top:10px;flex-wrap:wrap}
  .action{flex:1;padding:10px;border-radius:8px;background:#071827;border:1px solid rgba(255,255,255,0.03);cursor:pointer;font-weight:800;color:var(--text)}
  .floating{position:fixed;pointer-events:none;font-weight:900;text-shadow:0 6px 18px rgba(0,0,0,0.7);animation:floatUp 1000ms ease-out forwards;z-index:9999}
  @keyframes floatUp{from{opacity:1;transform:translate(-50%,0) scale(1)}to{opacity:0;transform:translate(-50%,-120px) scale(1.06)}}
  .attackAnim{position:fixed;padding:6px 10px;border-radius:10px;background:rgba(255,255,255,0.02);font-weight:900;z-index:9998;transition:transform .36s,opacity .36s}
  .shake{animation:shakeAnim .35s}
  @keyframes shakeAnim{0%{transform:translateY(0)}25%{transform:translateY(-6px)}50%{transform:translateY(4px)}75%{transform:translateY(-3px)}100%{transform:translateY(0)}}
  .particle{position:fixed;border-radius:50%;pointer-events:none;z-index:1200;opacity:0.95}
  .small{font-size:12px;padding:6px 8px;border-radius:8px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03)}
  /* Mobile */
  @media(max-width:720px){ .hud{flex-direction:column;align-items:flex-start} .pvbar{width:140px} .actions{flex-direction:column} }
</style>
</head>
<body>
<div class="wrap" id="app">
  <header>
    <div>
      <h1>🕷️ Spider-Man : Nuit à New York</h1>
      <div class="muted">V1 — comics coloré · QTE, poursuites & combats</div>
    </div>
    <div class="small">PV: <span id="uiPV">—</span> · Score: <span id="uiScore">0</span></div>
  </header>

  <!-- ---------- SCREENS ---------- -->
  <main id="mainArea">
    <!-- START -->
    <section id="screenStart" class="panel">
      <h2>La ville a besoin de toi</h2>
      <p class="muted">Choisis la difficulté — plus dur raccourcit les temps et augmente les dégâts ennemis.</p>
      <div class="row">
        <button class="btn" data-diff="easy">😃 Facile</button>
        <button class="btn" data-diff="normal">😐 Normal</button>
        <button class="btn" data-diff="hard">😈 Difficile</button>
      </div>
      <div style="margin-top:10px" class="muted">Tu auras plusieurs missions cette nuit. Prépare-toi !</div>
    </section>

    <!-- MISSION / GAME -->
    <section id="screenGame" class="panel" style="display:none">
      <div class="hud">
        <div class="avatar" id="playerAvatar">🕷️</div>
        <div class="col">
          <div style="display:flex;align-items:center;justify-content:space-between">
            <strong id="playerName">Spider-Man</strong>
            <div class="muted">PV: <span id="playerPV">0</span>/<span id="playerMax">0</span></div>
          </div>
          <div class="pvbar"><div id="playerFill" class="fill" style="width:100%"></div></div>
          <div class="muted" id="playerNote">Pouvoir: agile</div>
        </div>

        <div style="width:180px;text-align:right">
          <div class="small">Mission: <span id="missionTitle">—</span></div>
          <div style="margin-top:8px" class="small">Difficulté: <span id="diffLabel">—</span></div>
        </div>
      </div>

      <div class="panel" style="margin-top:12px">
        <div id="missionArea" class="center"><!-- mission content injected --></div>
        <div id="qteArea" style="margin-top:10px"></div>
      </div>

      <div class="actions" id="actionButtons" style="margin-top:12px">
        <!-- actions injected per mission or combat -->
      </div>

      <div style="margin-top:12px">
        <div id="log" ></div>
      </div>
    </section>

    <!-- END -->
    <section id="screenEnd" class="panel" style="display:none">
      <h2 id="endTitle">—</h2>
      <p id="endText" class="muted"></p>
      <div style="margin-top:12px">
        <button class="btn" id="btnReplay">🔁 Rejouer</button>
        <button class="btn secondary" id="btnToStart">🏠 Menu</button>
      </div>
    </section>
  </main>
</div>

<!-- canvas overlay for particles if needed -->
<canvas id="fxCanvas" style="position:fixed;left:0;top:0;width:100%;height:100%;pointer-events:none;z-index:1200"></canvas>

<script>
/* ============================
   Spider-Man : Nuit à New York
   V1 — Complete playable file
   ============================ */

/* ---------- Game configuration ---------- */
const MISSIONS = [
  { id:'bus',    title:'Sauvetage: Bus en feu', type:'qte', desc:'Tisse une toile avant que le bus ne bascule.', failDamage:18 },
  { id:'jump',   title:'Saut de gratte-ciel', type:'timing', desc:'Attrape la façade au bon moment.', failDamage:12 },
  { id:'pursuit',title:'Poursuite de voleur', type:'choice', desc:'Choisis la bonne direction pour rattraper le voleur.', failDamage:14 },
  { id:'fight',  title:'Combat contre un vilain', type:'combat', desc:'Affronte le vilain en tour par tour (3 tours max).', failDamage:0 }
];
const VILLAINS = [
  { id:'rhino',   name:'Rhino', emoji:'🦏', pv:42, dmg:[6,10] },
  { id:'electro', name:'Electro', emoji:'⚡', pv:36, dmg:[5,9] },
  { id:'goblin',  name:'Bouffon Vert', emoji:'🎃', pv:40, dmg:[6,11] }
];

/* difficulty modifiers */
const DIFFS = {
  easy:   { qteTime:1600,  enemyMult:0.85, playerMax:120 },
  normal: { qteTime:1200,  enemyMult:1.0,  playerMax:100 },
  hard:   { qteTime:900,   enemyMult:1.18, playerMax:85  }
};

/* ---------- DOM refs ---------- */
const $ = id => document.getElementById(id);
const screenStart = $('screenStart');
const screenGame  = $('screenGame');
const screenEnd   = $('screenEnd');
const playerPVEl  = $('playerPV');
const playerMaxEl = $('playerMax');
const playerFill  = $('playerFill');
const missionTitleEl = $('missionTitle');
const missionArea = $('missionArea');
const actionButtons = $('actionButtons');
const logEl = $('log');
const diffLabel = $('diffLabel');
const uiScore = $('uiScore');
const uiPV = $('uiPV');

/* ---------- FX canvas ---------- */
const fxCanvas = document.getElementById('fxCanvas');
const fxCtx = fxCanvas.getContext('2d');
function resizeCanvas(){ fxCanvas.width = innerWidth; fxCanvas.height = innerHeight; }
addEventListener('resize', resizeCanvas);
resizeCanvas();
let fxParticles = [];

/* ---------- Audio (WebAudio tiny synth) ---------- */
let audioCtx = null;
function ensureAudio(){ if(!audioCtx) audioCtx = new (window.AudioContext||window.webkitAudioContext)(); }
function beep(freq=440,dur=0.08,type='sine,') {
  ensureAudio();
  const o = audioCtx.createOscillator(), g = audioCtx.createGain();
  o.type = 'sine'; o.frequency.value = freq;
  g.gain.value = 0.06;
  o.connect(g); g.connect(audioCtx.destination);
  o.start(); g.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + dur);
  setTimeout(()=> o.stop(), dur*1000+20);
}
function soundAttack(){ beep(560,0.07); }
function soundHit(){ beep(160,0.14); }
function soundWin(){ beep(760,0.12); setTimeout(()=>beep(880,0.08),120); }
function soundLose(){ beep(120,0.35); }

/* ---------- State ---------- */
let STATE = {
  difficulty: 'normal',
  player: { pv:100, max:100 },
  missions: [],   // will be randomized order of MISSIONS
  currentIndex: 0,
  score: 0,
  currentMission: null,
  inCombat: false,
  currentVillain: null,
  qteTimeoutId: null
};

/* ---------- Helpers UI ---------- */
function showScreen(s){ screenStart.style.display='none'; screenGame.style.display='none'; screenEnd.style.display='none'; 
  if(s==='start') screenStart.style.display='block';
  if(s==='game')  screenGame.style.display='block';
  if(s==='end')   screenEnd.style.display='block';
}
function log(msg){ const d = document.createElement('div'); d.innerHTML = msg; logEl.prepend(d); }
function setPVUI(){ playerPVEl.textContent = STATE.player.pv; playerMaxEl.textContent = STATE.player.max; uiPV.textContent = STATE.player.pv; uiScore.textContent = STATE.score; playerFill.style.width = Math.max(0,STATE.player.pv/STATE.player.max*100) + '%'; }
function shakeScreen(){ document.querySelector('.wrap').classList.add('shake'); setTimeout(()=> document.querySelector('.wrap').classList.remove('shake'),360); }
function spawnFloating(text, targetEl, color='#ffb3b3'){ if(!targetEl) return; const r = targetEl.getBoundingClientRect(); const f = document.createElement('div'); f.className='floating'; f.textContent=text; f.style.left = (r.left + r.width/2) + 'px'; f.style.top = (r.top - 10) + 'px'; f.style.color = color; document.body.appendChild(f); setTimeout(()=> f.remove(),1000); }

/* ---------- Particle engine (simple) ---------- */
function spawnFX(x,y,color='orange',count=18,sizeRange=[4,12]){
  for(let i=0;i<count;i++){
    fxParticles.push({
      x,y,
      vx:(Math.random()-0.5)*6,
      vy:(Math.random()-0.8)*6 - 2,
      life: 60 + Math.random()*30,
      size: sizeRange[0] + Math.random()*(sizeRange[1]-sizeRange[0]),
      color
    });
  }
}
function updateFX(){
  fxCtx.clearRect(0,0,fxCanvas.width,fxCanvas.height);
  for(let i=fxParticles.length-1;i>=0;i--){
    const p = fxParticles[i];
    p.x += p.vx; p.y += p.vy; p.vy += 0.15; p.life--;
    fxCtx.globalAlpha = Math.max(p.life/90,0);
    fxCtx.fillStyle = p.color;
    fxCtx.beginPath(); fxCtx.arc(p.x,p.y,p.size,0,Math.PI*2); fxCtx.fill();
    if(p.life<=0) fxParticles.splice(i,1);
  }
  requestAnimationFrame(updateFX);
}
updateFX();

/* ---------- Init difficulty buttons ---------- */
document.querySelectorAll('.btn[data-diff]').forEach(btn=>{
  btn.addEventListener('click', (e)=>{
    const d = btn.getAttribute('data-diff');
    startGame(d);
  });
});

/* ---------- Start / Setup ---------- */
function startGame(difficulty){
  // unlock audio on first gesture
  ensureAudio();

  STATE.difficulty = difficulty;
  const conf = DIFFS[difficulty];
  STATE.player.max = conf.playerMax;
  STATE.player.pv = conf.playerMax;
  // shuffle missions order
  STATE.missions = shuffleArray(MISSIONS.slice());
  STATE.currentIndex = 0;
  STATE.score = 0;
  STATE.inCombat = false;
  setPVUI();
  diffLabel.textContent = difficulty;
  log(`<i>Mode: ${difficulty}</i> — La nuit commence...`);
  showScreen('game');
  nextMission();
}

/* Fisher-Yates */
function shuffleArray(arr){
  for(let i=arr.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [arr[i],arr[j]] = [arr[j],arr[i]];
  }
  return arr;
}

/* ---------- Mission flow ---------- */
function nextMission(){
  clearTimeout(STATE.qteTimeoutId);
  actionButtons.innerHTML = '';
  missionArea.innerHTML = '';
  if(STATE.currentIndex >= STATE.missions.length){
    // all missions done => final check
    finishRun(true);
    return;
  }
  const m = STATE.currentMission = STATE.missions[STATE.currentIndex];
  missionTitleEl.textContent = m.title;
  log(`<b>Mission:</b> ${m.title} — ${m.desc}`);
  // render based on type
  if(m.type==='qte') renderBusQTE(m);
  else if(m.type==='timing') renderJump(m);
  else if(m.type==='choice') renderPursuit(m);
  else if(m.type==='combat') renderCombat(m);
}

/* ---------- MISSION: BUS QTE ---------- */
function renderBusQTE(m){
  missionArea.innerHTML = `<div style="text-align:left">
    <div style="font-size:28px">🚌 <strong>Bus en feu</strong></div>
    <p class="muted">${m.desc}</p>
    </div>`;
  // show QTE button
  const btn = document.createElement('button'); btn.className='btn'; btn.textContent='Tisser la toile 🕸️';
  const qteArea = $('qteArea'); qteArea.innerHTML = '';
  qteArea.appendChild(btn);
  // timer depends on difficulty
  const time = DIFFS[STATE.difficulty].qteTime;
  let success = false;
  const tid = setTimeout(()=> {
    if(!success){
      failMission(m);
    }
  }, time);
  btn.addEventListener('click', ()=>{
    success = true;
    clearTimeout(tid);
    // success animation
    const rect = btn.getBoundingClientRect();
    spawnFX(rect.left+rect.width/2, rect.top, '#ffd166', 22, [6,18]);
    soundAttack();
    log('✅ Tu as tissé la toile et sauvé le bus !');
    STATE.score += 12;
    STATE.currentIndex++;
    setPVUI();
    setTimeout(()=> { $('qteArea').innerHTML=''; nextMission(); }, 700);
  });
  STATE.qteTimeoutId = tid;
}

/* ---------- MISSION: JUMP timing ---------- */
function renderJump(m){
  missionArea.innerHTML = `<div style="text-align:left">
    <div style="font-size:28px">🏙️ <strong>Saut entre immeubles</strong></div>
    <p class="muted">${m.desc}</p>
    <div style="margin-top:8px" class="muted">Clique au bon moment pour attraper la façade.</div>
    </div>`;
  // show moving indicator bar
  const bar = document.createElement('div'); bar.style.position='relative'; bar.style.height='32px'; bar.style.marginTop='12px'; bar.style.background='rgba(255,255,255,0.02)'; bar.style.borderRadius='8px';
  const mover = document.createElement('div'); mover.style.position='absolute'; mover.style.left='0%'; mover.style.top='6px'; mover.style.width='28px'; mover.style.height='20px'; mover.style.background= 'linear-gradient(90deg,#ff7b7b,#ffd166)'; mover.style.borderRadius='6px';
  bar.appendChild(mover); missionArea.appendChild(bar);
  const btn = document.createElement('button'); btn.className='btn'; btn.textContent='Sauter';
  missionArea.appendChild(btn);
  // animate mover back and forth
  let dir = 1; let pos = 0; const speed = (STATE.difficulty==='easy')?0.8:(STATE.difficulty==='hard')?1.8:1.2;
  let animId;
  function animateMover(){
    pos += dir*speed;
    if(pos > 72){ dir = -1; pos = 72; }
    if(pos < 0){ dir = 1; pos = 0; }
    mover.style.left = pos + '%';
    animId = requestAnimationFrame(animateMover);
  }
  animateMover();
  btn.addEventListener('click', ()=>{
    cancelAnimationFrame(animId);
    // success zone = center 28%-50% (tweak)
    const center = 36; // optimal center percent
    const dist = Math.abs(pos - center);
    if(dist < 18){ // success
      soundAttack(); spawnFX(bar.getBoundingClientRect().left + pos/100*bar.offsetWidth + 20, bar.getBoundingClientRect().top, '#9be7ff', 16, [6,14]);
      log('✅ Saut réussi ! Tu as attrapé la façade.');
      STATE.score += 10;
    } else {
      log('❌ Saut raté, tu t’es blessé en tombant.');
      applyDamage(m.failDamage);
    }
    STATE.currentIndex++;
    setPVUI();
    setTimeout(()=> nextMission(), 700);
  });
}

/* ---------- MISSION: PURSUIT choice ---------- */
function renderPursuit(m){
  missionArea.innerHTML = `<div style="text-align:left">
    <div style="font-size:28px">🏃 <strong>Poursuite</strong></div>
    <p class="muted">${m.desc}</p>
    <div style="margin-top:8px" class="muted">Choisis une direction rapidement (gauche / droite / haut).</div>
    </div>`;
  actionButtons.innerHTML = '';
  ['← Gauche','→ Droite','↑ Haut'].forEach((label, idx)=>{
    const a = document.createElement('button'); a.className='action'; a.textContent = label;
    a.addEventListener('click', ()=> {
      // random correct direction
      const correct = Math.floor(Math.random()*3); // 0/1/2
      if(idx === correct){
        soundAttack();
        spawnFX( innerWidth/2, innerHeight/2, '#ffd166', 14, [6,14]);
        log('✅ Bonne direction — tu rattrapes le voleur !');
        STATE.score += 11;
      } else {
        log('❌ Mauvaise direction — le voleur gagne du terrain.');
        applyDamage(m.failDamage);
      }
      actionButtons.innerHTML = '';
      STATE.currentIndex++;
      setPVUI();
      setTimeout(()=> nextMission(), 700);
    });
    actionButtons.appendChild(a);
  });
  // also auto-fail if no choice within time (timer depends on diff)
  const time = DIFFS[STATE.difficulty].qteTime * 1.4;
  STATE.qteTimeoutId = setTimeout(()=> {
    log('⌛ Trop lent — le voleur t’échappe et tu te blesses.');
    applyDamage(m.failDamage);
    actionButtons.innerHTML = '';
    STATE.currentIndex++;
    setPVUI();
    nextMission();
  }, time);
}

/* ---------- MISSION: COMBAT ---------- */
function renderCombat(m){
  // pick villain scaled by difficulty
  const base = VILLAINS[Math.floor(Math.random()*VILLAINS.length)];
  const mult = DIFFS[STATE.difficulty].enemyMult;
  const villain = { ...base, pv: Math.round(base.pv * mult), max: Math.round(base.pv * mult) };
  STATE.currentVillain = villain;
  STATE.inCombat = true;
  missionArea.innerHTML = `<div style="display:flex;gap:12px;align-items:center">
    <div style="font-size:48px">${villain.emoji}</div>
    <div style="flex:1;text-align:left">
      <div style="font-weight:800">${villain.name}</div>
      <div class="muted">PV: <span id="villainPV">${villain.pv}</span>/<span id="villainMax">${villain.max}</span></div>
      <div style="margin-top:8px" class="muted">${m.desc}</div>
    </div></div>`;
  actionButtons.innerHTML = '';
  // actions: light, heavy, web, defend
  const attacks = [
    { id:'light', label:'👊 Coup léger', dmg:[4,8] },
    { id:'heavy', label:'💥 Coup fort', dmg:[8,14] },
    { id:'web', label:'🕸️ Toile (ralentit)', dmg:[3,6], effect:'slow' },
    { id:'dodge', label:'↩️ Esquive', dmg:[0,0], effect:'dodge' }
  ];
  attacks.forEach(a=>{
    const btn = document.createElement('button'); btn.className='action'; btn.textContent = a.label;
    btn.addEventListener('click', ()=> playerAttack(a));
    actionButtons.appendChild(btn);
  });
  // combat state: rounds count
  STATE.combatRounds = 0;
  updateVillainUI();
  log(`⚔️ Combat engagé contre ${villain.name} (${villain.pv} PV)`);
}

function updateVillainUI(){
  const vp = $('villainPV');
  if(vp) vp.textContent = STATE.currentVillain.pv;
  const vm = $('villainMax'); if(vm) vm.textContent = STATE.currentVillain.max;
}

/* ---------- Combat logic ---------- */
function playerAttack(attack){
  if(!STATE.inCombat || !STATE.currentVillain) return;
  // compute dmg
  const [minD,maxD] = attack.dmg;
  let dmg = (minD && maxD)? rand(minD,maxD) : 0;
  // heavy has chance to stagger -> spawn smoke and bigger fx
  const isCrit = Math.random() < 0.14;
  if(isCrit){ dmg = Math.round(dmg*1.6); log('✨ Coup critique !'); spawnFloating('CRIT', $('playerAvatar'), '#fff3a6'); }
  // apply player boosts? (none for now)
  // animate attack
  animateAttack($('playerAvatar'), $('villainPV') || missionArea, STATE.playerIcon || '🕷️', ()=>{
    STATE.currentVillain.pv -= dmg;
    spawnFloating('-'+dmg, $('villainPV') || missionArea, '#ffb3b3');
    spawnFXAtVillain('#ff7b7b');
    soundAttack();
    updateVillainUI();
    STATE.combatRounds++;
    log(`➡️ Tu infliges ${dmg} PV à ${STATE.currentVillain.name}`);
    // check villain dead
    if(STATE.currentVillain.pv <= 0){
      log(`✅ ${STATE.currentVillain.name} neutralisé !`);
      STATE.score += 18;
      STATE.inCombat = false;
      STATE.currentIndex++;
      // reward small heal
      const heal = Math.min( Math.round(STATE.player.max*0.12), STATE.player.max - STATE.player.pv );
      if(heal>0){ STATE.player.pv += heal; log(`💚 Tu récupères ${heal} PV après le combat.`); }
      setPVUI();
      setTimeout(()=> nextMission(), 900);
      return;
    }
    // villain retaliates after small delay
    setTimeout(()=> enemyTurn(), 700);
  });
}

function enemyTurn(){
  if(!STATE.inCombat || !STATE.currentVillain) return;
  // villain attacks
  const v = STATE.currentVillain;
  const dmg = rand(Math.floor(v.dmg[0]*DIFFS[STATE.difficulty].enemyMult), Math.ceil(v.dmg[1]*DIFFS[STATE.difficulty].enemyMult));
  // simple dodge chance if player used dodge recently? For now dodge reduces damage by half with chance
  let final = dmg;
  // basic apply
  STATE.player.pv -= final;
  spawnFloating('-'+final, $('playerFill'), '#ff9aa2');
  spawnFXAtPlayer('#ff6b6b');
  soundHit();
  shakeScreen();
  setPVUI();
  log(`💥 ${v.name} riposte et te fait ${final} PV.`);
  if(STATE.player.pv <= 0){
    finishRun(false);
    return;
  }
  // allow next action (player) - combat continues
}

/* ---------- Utilities ---------- */
function rand(min,max){ return Math.floor(Math.random()*(max-min+1))+min; }
function applyDamage(amount){
  soundHit(); spawnFX(innerWidth/2, innerHeight/2, '#ff6b6b', 20, [8,20]); shakeScreen();
  STATE.player.pv -= amount;
  if(STATE.player.pv < 0) STATE.player.pv = 0;
  log(`❌ Tu perds ${amount} PV.`);
  setPVUI();
  if(STATE.player.pv <= 0) finishRun(false);
}

/* ---------- Attack animation helpers ---------- */
function animateAttack(fromEl, toEl, icon, cb){
  if(!fromEl){ if(cb) cb(); return; }
  const r1 = fromEl.getBoundingClientRect();
  let r2;
  if(toEl && toEl.getBoundingClientRect) r2 = toEl.getBoundingClientRect();
  else { r2 = { left: innerWidth/2, top: innerHeight/2, width:40, height:40 }; }
  const anim = document.createElement('div'); anim.className='attackAnim'; anim.textContent = icon;
  anim.style.left = (r1.left + r1.width/2) + 'px';
  anim.style.top = (r1.top + r1.height/2) + 'px';
  anim.style.opacity = '0.98'; document.body.appendChild(anim);
  requestAnimationFrame(()=>{ anim.style.transform = `translate(${r2.left + r2.width/2 - (r1.left + r1.width/2)}px, ${r2.top + r2.height/2 - (r1.top + r1.height/2)}px)`; anim.style.opacity='0.92'; });
  setTimeout(()=>{ anim.remove(); if(cb) cb(); }, 380);
}
function spawnFXAtVillain(color='#ff9a3b'){ const el = document.querySelector('#villainPV') || missionArea; const r = el.getBoundingClientRect(); spawnFX(r.left + r.width/2, r.top + 20, color, 22, [6,18]); }
function spawnFXAtPlayer(color='#ff9a3b'){ const el = $('playerFill'); const r = el.getBoundingClientRect(); spawnFX(r.left + r.width/2, r.top - 10, color, 16, [6,14]); }

/* ---------- Finish run ---------- */
function finishRun(victory){
  // stop any QTE timers
  clearTimeout(STATE.qteTimeoutId);
  actionButtons.innerHTML = '';
  missionArea.innerHTML = '';
  STATE.inCombat = false;
  if(victory){
    soundWin();
    $('endTitle').textContent = '🏆 Mission accomplie !';
    $('endText').textContent = `La nuit est sauvée — Score final: ${STATE.score}. Tu veilles sur New York.`;
    log('🎉 Tu as terminé la session avec succès !');
  } else {
    soundLose();
    $('endTitle').textContent = '💀 Tu es KO';
    $('endText').textContent = `Tu as été mis hors de combat. Score: ${STATE.score}. Rejoue pour faire mieux.`;
    log('⚠️ Tu as été vaincu pendant la nuit.');
  }
  showScreen('end');
}

/* ---------- Buttons: replay / menu ---------- */
$('btnReplay').addEventListener('click', ()=> { showScreen('start'); });
$('btnToStart').addEventListener('click', ()=> { location.reload(); });

/* ---------- Misc: bind unlock audio on first gesture ---------- */
document.body.addEventListener('click', function unlock(){ ensureAudio(); document.body.removeEventListener('click', unlock); }, { once:true });

/* ---------- Spawn FX utilities ---------- */
function spawnFX(x,y,color,count=22,sizeRange=[6,16]){
  // reuse fxParticles factory
  for(let i=0;i<count;i++){
    fxParticles.push({
      x,y,
      vx:(Math.random()-0.5)*8,
      vy:(Math.random()*-6)-2,
      life: 60 + Math.random()*30,
      size: sizeRange[0] + Math.random()*(sizeRange[1]-sizeRange[0]),
      color
    });
  }
}

/* ---------- Start state defaults ---------- */
showScreen('start');
setPVUI();
uiScore.textContent = 0;

/* ---------- END of script ---------- */
</script>
</body>
</html>
