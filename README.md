# divide-et-impera
Proiect informatica
<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Divide et Impera — Aplicații</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0a0a0f;
  --surface: #13131a;
  --surface2: #1c1c27;
  --accent: #6c63ff;
  --accent2: #00e5a0;
  --accent3: #ff6b6b;
  --amber: #ffa94d;
  --text: #e8e6f0;
  --muted: #6b6980;
  --border: rgba(108,99,255,0.2);
  --radius: 12px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{background:var(--bg);color:var(--text);font-family:'Syne',sans-serif;min-height:100vh;overflow-x:hidden}
body::before{content:'';position:fixed;top:0;left:0;width:100%;height:100%;background:radial-gradient(ellipse at 20% 20%,rgba(108,99,255,0.08) 0%,transparent 60%),radial-gradient(ellipse at 80% 80%,rgba(0,229,160,0.05) 0%,transparent 60%);pointer-events:none;z-index:0}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:100;background:rgba(10,10,15,0.85);backdrop-filter:blur(16px);border-bottom:1px solid var(--border);padding:0 2rem;display:flex;align-items:center;gap:0;height:60px}
.nav-logo{font-family:'Space Mono',monospace;font-size:13px;color:var(--accent);letter-spacing:0.05em;margin-right:auto;white-space:nowrap}
.nav-logo span{color:var(--accent2)}
.nav-links{display:flex;gap:4px;overflow-x:auto;scrollbar-width:none}
.nav-links::-webkit-scrollbar{display:none}
.nav-btn{background:none;border:none;color:var(--muted);font-family:'Syne',sans-serif;font-size:12px;font-weight:600;padding:6px 12px;border-radius:6px;cursor:pointer;white-space:nowrap;transition:all .2s;letter-spacing:0.03em}
.nav-btn:hover{color:var(--text);background:var(--surface2)}
.nav-btn.active{color:var(--accent);background:rgba(108,99,255,0.12)}

/* PAGES */
.page{display:none;padding-top:80px;min-height:100vh;position:relative;z-index:1}
.page.active{display:block}

/* HOME */
.home-hero{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:calc(100vh - 60px);padding:2rem;text-align:center}
.home-hero h1{font-size:clamp(2.5rem,8vw,6rem);font-weight:800;line-height:1;margin-bottom:1rem;background:linear-gradient(135deg,var(--text) 0%,var(--accent) 50%,var(--accent2) 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.home-hero p{font-size:1.1rem;color:var(--muted);max-width:500px;line-height:1.7;margin-bottom:3rem}
.cards-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:16px;max-width:900px;width:100%;margin:0 auto}
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:1.5rem;cursor:pointer;transition:all .25s;text-align:left;position:relative;overflow:hidden}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:var(--card-accent,var(--accent));opacity:0;transition:opacity .25s}
.card:hover{border-color:var(--card-accent,var(--accent));transform:translateY(-3px)}
.card:hover::before{opacity:1}
.card-icon{font-size:2rem;margin-bottom:0.75rem}
.card h3{font-size:1rem;font-weight:600;margin-bottom:0.4rem;color:var(--text)}
.card p{font-size:12px;color:var(--muted);line-height:1.5}
.badge{display:inline-block;font-size:10px;font-family:'Space Mono',monospace;padding:2px 8px;border-radius:4px;margin-top:0.75rem;background:rgba(108,99,255,0.12);color:var(--accent);border:1px solid var(--border)}

/* ANIM PAGE */
.anim-page{padding:80px 1.5rem 2rem;max-width:900px;margin:0 auto}
.anim-header{margin-bottom:1.5rem}
.anim-header h2{font-size:1.8rem;font-weight:800;margin-bottom:0.3rem}
.anim-header p{font-size:14px;color:var(--muted)}
.anim-tag{font-family:'Space Mono',monospace;font-size:11px;color:var(--accent2);margin-bottom:0.5rem;display:block}

/* CONTROLS */
.ctrl-box{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:1rem;margin-bottom:1rem}
.cfg-row{display:flex;flex-wrap:wrap;gap:12px;align-items:flex-end;margin-bottom:0.75rem}
.cfg-grp{display:flex;flex-direction:column;gap:4px}
.cfg-grp label{font-size:11px;color:var(--muted);font-weight:600;letter-spacing:0.04em;text-transform:uppercase}
.cfg-grp input[type=number]{width:70px;background:var(--surface2);border:1px solid var(--border);color:var(--text);font-family:'Space Mono',monospace;font-size:13px;padding:6px 10px;border-radius:6px;outline:none}
.cfg-grp input[type=number]:focus{border-color:var(--accent)}
.arr-row{display:flex;flex-wrap:wrap;gap:6px;align-items:center;margin-bottom:0.75rem}
.arr-row input[type=number]{width:52px;background:var(--surface2);border:1px solid var(--border);color:var(--accent2);font-family:'Space Mono',monospace;font-size:13px;padding:5px 8px;border-radius:6px;outline:none;text-align:center}
.arr-row input[type=number]:focus{border-color:var(--accent2)}
.btn{background:var(--surface2);border:1px solid var(--border);color:var(--text);font-family:'Syne',sans-serif;font-size:13px;font-weight:600;padding:7px 16px;border-radius:8px;cursor:pointer;transition:all .2s}
.btn:hover{background:rgba(108,99,255,0.15);border-color:var(--accent);color:var(--accent)}
.btn.primary{background:rgba(108,99,255,0.15);border-color:var(--accent);color:var(--accent)}
.btn-sm{padding:5px 10px;font-size:12px}

/* CANVAS */
.canvas-box{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:1rem;margin-bottom:1rem;position:relative}
canvas{display:block;width:100%;height:260px;border-radius:8px}
.step-bar{display:flex;align-items:center;gap:10px;margin-top:0.75rem;flex-wrap:wrap}
.step-info{font-size:12px;color:var(--muted);font-family:'Space Mono',monospace;margin-left:auto}
.info-text{font-size:13px;color:var(--text);padding:0.6rem 1rem;background:var(--surface2);border-radius:8px;border-left:2px solid var(--accent);min-height:36px;margin-top:0.5rem;line-height:1.5}

/* FRACTAL */
.frac-tabs{display:flex;gap:8px;margin-bottom:1rem;flex-wrap:wrap}
.ftab{background:var(--surface);border:1px solid var(--border);color:var(--muted);font-family:'Syne',sans-serif;font-size:13px;font-weight:600;padding:8px 18px;border-radius:8px;cursor:pointer;transition:all .2s}
.ftab.on{background:rgba(0,229,160,0.1);border-color:var(--accent2);color:var(--accent2)}
.iter-row{display:flex;align-items:center;gap:12px;margin-top:0.75rem}
.iter-row label{font-size:12px;color:var(--muted);font-weight:600;white-space:nowrap}
.iter-row input[type=range]{flex:1;accent-color:var(--accent2)}
.iter-val{font-family:'Space Mono',monospace;font-size:13px;color:var(--accent2);min-width:20px}

/* BACK BTN */
.back-btn{display:inline-flex;align-items:center;gap:6px;background:none;border:1px solid var(--border);color:var(--muted);font-family:'Syne',sans-serif;font-size:13px;padding:6px 14px;border-radius:8px;cursor:pointer;margin-bottom:1.5rem;transition:all .2s}
.back-btn:hover{color:var(--text);border-color:var(--muted)}

@media(max-width:600px){
  nav{padding:0 1rem}
  .nav-logo{font-size:11px}
  .anim-page{padding:80px 1rem 2rem}
}
</style>
</head>
<body>

<nav>
  <div class="nav-logo">D<span>/</span>I — Aplicații</div>
  <div class="nav-links">
    <button class="nav-btn active" onclick="showPage('home')">Acasă</button>
    <button class="nav-btn" onclick="showPage('merge')">Merge Sort</button>
    <button class="nav-btn" onclick="showPage('quick')">Quick Sort</button>
    <button class="nav-btn" onclick="showPage('hanoi')">Hanoi</button>
    <button class="nav-btn" onclick="showPage('sume')">Sume</button>
    <button class="nav-btn" onclick="showPage('fractali')">Fractali</button>
  </div>
</nav>

<!-- HOME -->
<div class="page active" id="page-home">
  <div class="home-hero">
    <h1>Divide et Impera</h1>
    <p>Explorează vizual cei mai importanți algoritmi bazați pe metoda Divide et Impera — animații interactive pas cu pas.</p>
    <div class="cards-grid">
      <div class="card" style="--card-accent:#6c63ff" onclick="showPage('merge')">
        <div class="card-icon">🔀</div>
        <h3>Merge Sort</h3>
        <p>Sortare prin interclasare — împarte, sortează și combină</p>
        <span class="badge">O(n log n)</span>
      </div>
      <div class="card" style="--card-accent:#ffa94d" onclick="showPage('quick')">
        <div class="card-icon">⚡</div>
        <h3>Quick Sort</h3>
        <p>Sortare rapidă prin pivot — partiționare și recursivitate</p>
        <span class="badge">O(n log n)</span>
      </div>
      <div class="card" style="--card-accent:#ff6b6b" onclick="showPage('hanoi')">
        <div class="card-icon">🗼</div>
        <h3>Turnurile Hanoi</h3>
        <p>Mută discurile recursiv respectând regulile matematice</p>
        <span class="badge">O(2ⁿ)</span>
      </div>
      <div class="card" style="--card-accent:#00e5a0" onclick="showPage('sume')">
        <div class="card-icon">∑</div>
        <h3>Sume</h3>
        <p>Calculul sumei unui șir prin împărțire recursivă</p>
        <span class="badge">O(n)</span>
      </div>
      <div class="card" style="--card-accent:#a78bfa" onclick="showPage('fractali')">
        <div class="card-icon">❄</div>
        <h3>Fractali</h3>
        <p>Koch, Sierpiński, Curba Dragonului — recursivitate vizuală</p>
        <span class="badge">3 fractali</span>
      </div>
    </div>
  </div>
</div>

<!-- MERGE SORT -->
<div class="page" id="page-merge">
<div class="anim-page">
  <button class="back-btn" onclick="showPage('home')">← Înapoi</button>
  <div class="anim-header">
    <span class="anim-tag">// algoritm de sortare</span>
    <h2>Merge Sort</h2>
    <p>Împarte array-ul în jumătăți până la elemente singure, apoi le reunește sortat.</p>
  </div>
  <div class="ctrl-box">
    <div class="cfg-row">
      <div class="cfg-grp"><label>Nr. elemente</label><input type="number" id="m-n" min="2" max="12" value="6" onchange="mChangeN(+this.value)"></div>
      <div class="cfg-grp"><label>Min</label><input type="number" id="m-min" min="1" max="99" value="3"></div>
      <div class="cfg-grp"><label>Max</label><input type="number" id="m-max" min="2" max="999" value="90"></div>
      <div class="cfg-grp"><label style="opacity:0">.</label><button class="btn" onclick="mRandom()">Aleator</button></div>
    </div>
    <div class="arr-row" id="m-arr-row"></div>
  </div>
  <div class="canvas-box">
    <canvas id="m-cv"></canvas>
    <div class="info-text" id="m-info"></div>
    <div class="step-bar">
      <button class="btn btn-sm" onclick="mPrev()">← Înapoi</button>
      <button class="btn btn-sm" onclick="mNext()">Înainte →</button>
      <button class="btn btn-sm primary" onclick="mAuto()">▶ Auto</button>
      <button class="btn btn-sm" onclick="mReset()">↺ Reset</button>
      <span class="step-info" id="m-step">1/1</span>
    </div>
  </div>
</div>
</div>

<!-- QUICK SORT -->
<div class="page" id="page-quick">
<div class="anim-page">
  <button class="back-btn" onclick="showPage('home')">← Înapoi</button>
  <div class="anim-header">
    <span class="anim-tag">// algoritm de sortare</span>
    <h2>Quick Sort</h2>
    <p>Alege un pivot, plasează elementele mai mici la stânga și mai mari la dreapta, recursiv.</p>
  </div>
  <div class="ctrl-box">
    <div class="cfg-row">
      <div class="cfg-grp"><label>Nr. elemente</label><input type="number" id="q-n" min="2" max="12" value="7" onchange="qChangeN(+this.value)"></div>
      <div class="cfg-grp"><label>Min</label><input type="number" id="q-min" min="1" max="99" value="3"></div>
      <div class="cfg-grp"><label>Max</label><input type="number" id="q-max" min="2" max="999" value="90"></div>
      <div class="cfg-grp"><label style="opacity:0">.</label><button class="btn" onclick="qRandom()">Aleator</button></div>
    </div>
    <div class="arr-row" id="q-arr-row"></div>
  </div>
  <div class="canvas-box">
    <canvas id="q-cv"></canvas>
    <div class="info-text" id="q-info"></div>
    <div class="step-bar">
      <button class="btn btn-sm" onclick="qPrev()">← Înapoi</button>
      <button class="btn btn-sm" onclick="qNext()">Înainte →</button>
      <button class="btn btn-sm primary" onclick="qAuto()">▶ Auto</button>
      <button class="btn btn-sm" onclick="qReset()">↺ Reset</button>
      <span class="step-info" id="q-step">1/1</span>
    </div>
  </div>
</div>
</div>

<!-- HANOI -->
<div class="page" id="page-hanoi">
<div class="anim-page">
  <button class="back-btn" onclick="showPage('home')">← Înapoi</button>
  <div class="anim-header">
    <span class="anim-tag">// puzzle matematic clasic</span>
    <h2>Turnurile din Hanoi</h2>
    <p>Mută toate discurile de pe tija A pe ultima tijă, fără a pune un disc mare peste unul mic.</p>
  </div>
  <div class="ctrl-box">
    <div class="cfg-row">
      <div class="cfg-grp"><label>Nr. discuri (1-8)</label><input type="number" id="h-discs" min="1" max="8" value="3" onchange="hRebuild()"></div>
      <div class="cfg-grp"><label>Nr. tije (3-4)</label><input type="number" id="h-pegs" min="3" max="4" value="3" onchange="hRebuild()"></div>
      <div class="cfg-grp"><label style="opacity:0">.</label><button class="btn" onclick="hRebuild()">Aplică</button></div>
    </div>
    <div style="font-size:12px;color:var(--muted);font-family:'Space Mono',monospace" id="h-moves-info"></div>
  </div>
  <div class="canvas-box">
    <canvas id="h-cv"></canvas>
    <div class="info-text" id="h-info"></div>
    <div class="step-bar">
      <button class="btn btn-sm" onclick="hPrev()">← Înapoi</button>
      <button class="btn btn-sm" onclick="hNext()">Înainte →</button>
      <button class="btn btn-sm primary" onclick="hAuto()">▶ Auto</button>
      <button class="btn btn-sm" onclick="hReset()">↺ Reset</button>
      <span class="step-info" id="h-step">1/1</span>
    </div>
  </div>
</div>
</div>

<!-- SUME -->
<div class="page" id="page-sume">
<div class="anim-page">
  <button class="back-btn" onclick="showPage('home')">← Înapoi</button>
  <div class="anim-header">
    <span class="anim-tag">// divide et impera pe șir</span>
    <h2>Sume prin Divide et Impera</h2>
    <p>Calculul sumei unui șir prin împărțire recursivă în două jumătăți.</p>
  </div>
  <div class="ctrl-box">
    <div class="cfg-row">
      <div class="cfg-grp"><label>Nr. elemente</label><input type="number" id="s-n" min="2" max="10" value="6" onchange="sChangeN(+this.value)"></div>
      <div class="cfg-grp"><label>Min</label><input type="number" id="s-min" min="1" max="99" value="1"></div>
      <div class="cfg-grp"><label>Max</label><input type="number" id="s-max" min="2" max="99" value="20"></div>
      <div class="cfg-grp"><label style="opacity:0">.</label><button class="btn" onclick="sRandom()">Aleator</button></div>
    </div>
    <div class="arr-row" id="s-arr-row"></div>
  </div>
  <div class="canvas-box">
    <canvas id="s-cv"></canvas>
    <div class="info-text" id="s-info"></div>
    <div class="step-bar">
      <button class="btn btn-sm" onclick="sPrev()">← Înapoi</button>
      <button class="btn btn-sm" onclick="sNext()">Înainte →</button>
      <button class="btn btn-sm primary" onclick="sAuto()">▶ Auto</button>
      <button class="btn btn-sm" onclick="sReset()">↺ Reset</button>
      <span class="step-info" id="s-step">1/1</span>
    </div>
  </div>
</div>
</div>

<!-- FRACTALI -->
<div class="page" id="page-fractali">
<div class="anim-page">
  <button class="back-btn" onclick="showPage('home')">← Înapoi</button>
  <div class="anim-header">
    <span class="anim-tag">// structuri auto-similare recursive</span>
    <h2>Fractali</h2>
    <p>Forme generate prin Divide et Impera — aceeași regulă aplicată recursiv la infinit.</p>
  </div>
  <div class="frac-tabs">
    <button class="ftab on" onclick="setFractal('koch')">Fulgul lui Koch</button>
    <button class="ftab" onclick="setFractal('sierpinski')">Triunghiul Sierpiński</button>
    <button class="ftab" onclick="setFractal('dragon')">Curba Dragonului</button>
  </div>
  <div class="canvas-box">
    <canvas id="f-cv" style="height:320px"></canvas>
    <div class="info-text" id="f-info"></div>
    <div class="iter-row">
      <label>Iterații:</label>
      <input type="range" min="0" max="6" value="0" id="f-iter" step="1" oninput="fSetIter(+this.value)">
      <span class="iter-val" id="f-iter-val">0</span>
      <button class="btn btn-sm primary" onclick="fAuto()">▶ Auto</button>
      <button class="btn btn-sm" onclick="fReset()">↺ Reset</button>
    </div>
  </div>
</div>
</div>

<script>
/* ===== NAVIGATION ===== */
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  const idx={'home':0,'merge':1,'quick':2,'hanoi':3,'sume':4,'fractali':5};
  document.querySelectorAll('.nav-btn')[idx[id]].classList.add('active');
  window.scrollTo(0,0);
  if(id==='merge') mInit();
  if(id==='quick') qInit();
  if(id==='hanoi') hInit();
  if(id==='sume') sInit();
  if(id==='fractali') fInit();
}

/* ===== HELPERS ===== */
function rr(ctx,x,y,w,h,r=6){
  ctx.beginPath();
  ctx.moveTo(x+r,y);ctx.lineTo(x+w-r,y);ctx.quadraticCurveTo(x+w,y,x+w,y+r);
  ctx.lineTo(x+w,y+h-r);ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
  ctx.lineTo(x+r,y+h);ctx.quadraticCurveTo(x,y+h,x,y+h-r);
  ctx.lineTo(x,y+r);ctx.quadraticCurveTo(x,y,x+r,y);
  ctx.closePath();ctx.fill();ctx.stroke();
}
function setupCanvas(cv){
  const rect=cv.getBoundingClientRect();
  cv.width=rect.width*devicePixelRatio;
  cv.height=rect.height*devicePixelRatio;
  const c=cv.getContext('2d');
  c.scale(devicePixelRatio,devicePixelRatio);
  return c;
}
function CW(cv){return cv.getBoundingClientRect().width;}
function CH(cv){return cv.getBoundingClientRect().height;}

const COLORS={
  blue:'#6c63ff',blueL:'rgba(108,99,255,0.15)',
  green:'#00e5a0',greenL:'rgba(0,229,160,0.15)',
  amber:'#ffa94d',amberL:'rgba(255,169,77,0.15)',
  red:'#ff6b6b',redL:'rgba(255,107,107,0.15)',
  purple:'#c084fc',purpleL:'rgba(192,132,252,0.15)',
  teal:'#22d3ee',tealL:'rgba(34,211,238,0.15)',
  text:'#e8e6f0',muted:'#6b6980',
};

/* ===== MERGE SORT ===== */
let mArr=[38,27,43,3,9,82], mSteps=[], mIdx=0, mTimer=null, mCtx=null;

function mInit(){
  const cv=document.getElementById('m-cv');
  if(!cv.getBoundingClientRect().width) return;
  mCtx=setupCanvas(cv);
  mBuildArr();
}

function mBuildArr(){
  const row=document.getElementById('m-arr-row');
  row.innerHTML='';
  mArr.forEach((v,i)=>{
    const inp=document.createElement('input');
    inp.type='number';inp.value=v;inp.min=1;inp.max=999;
    inp.onchange=e=>{mArr[i]=+e.target.value;mRebuild();};
    row.appendChild(inp);
  });
  const add=document.createElement('button');add.className='btn btn-sm';add.textContent='+';
  add.onclick=()=>{if(mArr.length<12){mArr.push(Math.floor(Math.random()*80)+5);mBuildArr();mRebuild();}};
  row.appendChild(add);
  if(mArr.length>2){
    const rem=document.createElement('button');rem.className='btn btn-sm';rem.textContent='−';
    rem.onclick=()=>{mArr.pop();mBuildArr();mRebuild();};
    row.appendChild(rem);
  }
  mRebuild();
}

function mChangeN(n){n=Math.max(2,Math.min(12,n));while(mArr.length<n)mArr.push(Math.floor(Math.random()*80)+5);mArr.length=n;mBuildArr();}
function mRandom(){const vmin=+document.getElementById('m-min').value||3,vmax=+document.getElementById('m-max').value||90;mArr=Array.from({length:mArr.length},()=>Math.floor(Math.random()*(vmax-vmin+1))+vmin);mBuildArr();}

function mBuildSteps(arr){
  const res=[],a=[...arr];
  res.push({arr:[...a],active:[],groups:[a.map((_,i)=>i)],label:`Array original: [${a.join(', ')}]`});
  function rec(indices){
    if(indices.length<=1) return;
    const mid=Math.floor(indices.length/2);
    const L=indices.slice(0,mid),R=indices.slice(mid);
    res.push({arr:[...a],active:[],groups:[L,R],label:`Divide: [${L.map(i=>a[i]).join(',')}] | [${R.map(i=>a[i]).join(',')}]`});
    rec(L);rec(R);
    const sv=[...indices].map(i=>a[i]).sort((x,y)=>x-y);
    indices.forEach((idx,i)=>a[idx]=sv[i]);
    res.push({arr:[...a],active:indices,groups:[indices],label:`Combine: [${sv.join(', ')}] sortat`});
  }
  rec(arr.map((_,i)=>i));
  return res;
}

function mRebuild(){mSteps=mBuildSteps([...mArr]);mIdx=0;mDraw();}

function mDraw(){
  if(!mCtx) return;
  const cv=document.getElementById('m-cv');
  const s=mSteps[mIdx];
  const w=CW(cv),h=CH(cv);
  mCtx.clearRect(0,0,w,h);
  const n=s.arr.length,bw=Math.min(56,Math.max(18,(w-80)/n-6));
  const gap=Math.max(4,(w-80-n*bw)/(n-1||1));
  const sx=(w-(n*bw+(n-1)*gap))/2;
  const maxV=Math.max(...s.arr,1);
  s.arr.forEach((v,i)=>{
    const x=sx+i*(bw+gap),bh=Math.max(20,(v/maxV)*(h-75));
    const act=s.active.includes(i);
    mCtx.fillStyle=act?COLORS.greenL:COLORS.blueL;
    mCtx.strokeStyle=act?COLORS.green:COLORS.blue;
    mCtx.lineWidth=1.5;
    rr(mCtx,x,h-50-bh,bw,bh,4);
    mCtx.fillStyle=act?COLORS.green:COLORS.blue;
    mCtx.font=`bold ${Math.min(13,bw-2)}px 'Space Mono',monospace`;
    mCtx.textAlign='center';
    mCtx.fillText(v,x+bw/2,h-55);
  });
  s.groups.forEach((g,gi)=>{
    if(g.length<2)return;
    const x1=sx+g[0]*(bw+gap)-4,x2=sx+g[g.length-1]*(bw+gap)+bw+4;
    mCtx.strokeStyle=gi%2===0?COLORS.purple:COLORS.teal;
    mCtx.lineWidth=2;mCtx.setLineDash([5,4]);
    mCtx.beginPath();mCtx.moveTo(x1,h-40);mCtx.lineTo(x2,h-40);mCtx.stroke();
    mCtx.setLineDash([]);
  });
  document.getElementById('m-info').textContent=s.label;
  document.getElementById('m-step').textContent=`${mIdx+1}/${mSteps.length}`;
}

function mNext(){if(mIdx<mSteps.length-1){mIdx++;mDraw();}}
function mPrev(){if(mIdx>0){mIdx--;mDraw();}}
function mReset(){clearInterval(mTimer);mTimer=null;mIdx=0;mDraw();}
function mAuto(){if(mTimer){clearInterval(mTimer);mTimer=null;return;}mTimer=setInterval(()=>{if(mIdx<mSteps.length-1){mIdx++;mDraw();}else{clearInterval(mTimer);mTimer=null;}},1100);}

/* ===== QUICK SORT ===== */
let qArr=[38,27,43,3,9,82,10], qSteps=[], qIdx=0, qTimer=null, qCtx=null;

function qInit(){
  const cv=document.getElementById('q-cv');
  if(!cv.getBoundingClientRect().width)return;
  qCtx=setupCanvas(cv);qBuildArr();
}

function qBuildArr(){
  const row=document.getElementById('q-arr-row');row.innerHTML='';
  qArr.forEach((v,i)=>{
    const inp=document.createElement('input');inp.type='number';inp.value=v;inp.min=1;inp.max=999;
    inp.onchange=e=>{qArr[i]=+e.target.value;qRebuild();};row.appendChild(inp);
  });
  const add=document.createElement('button');add.className='btn btn-sm';add.textContent='+';
  add.onclick=()=>{if(qArr.length<12){qArr.push(Math.floor(Math.random()*80)+5);qBuildArr();qRebuild();}};row.appendChild(add);
  if(qArr.length>2){const rem=document.createElement('button');rem.className='btn btn-sm';rem.textContent='−';rem.onclick=()=>{qArr.pop();qBuildArr();qRebuild();};row.appendChild(rem);}
  qRebuild();
}

function qChangeN(n){n=Math.max(2,Math.min(12,n));while(qArr.length<n)qArr.push(Math.floor(Math.random()*80)+5);qArr.length=n;qBuildArr();}
function qRandom(){const vmin=+document.getElementById('q-min').value||3,vmax=+document.getElementById('q-max').value||90;qArr=Array.from({length:qArr.length},()=>Math.floor(Math.random()*(vmax-vmin+1))+vmin);qBuildArr();}

function qBuildSteps(arr){
  const res=[],a=[...arr];
  res.push({arr:[...a],pivot:-1,left:[],right:[],done:[],label:`Array original: [${a.join(', ')}]`});
  const done=new Set();
  function qs(idx){
    if(idx.length<=1){if(idx.length===1)done.add(idx[0]);return;}
    const pi=idx[0],pv=a[pi];
    const L=idx.slice(1).filter(i=>a[i]<=pv),R=idx.slice(1).filter(i=>a[i]>pv);
    res.push({arr:[...a],pivot:pi,left:L,right:R,done:[...done],label:`Pivot=${pv}: stânga[${L.map(i=>a[i]).join(',')||'∅'}] dreapta[${R.map(i=>a[i]).join(',')||'∅'}]`});
    const sorted=[...L,...R].sort((x,y)=>a[x]-a[y]);
    const newI=[...sorted.slice(0,L.length),pi,...sorted.slice(L.length)];
    newI.forEach((oi,ni)=>{const tmp=a[idx[ni]];a[idx[ni]]=a[oi];});
    const sv=idx.map(i=>a[i]).sort((x,y)=>x-y);
    idx.forEach((ii,ni)=>a[ii]=sv[ni]);
    idx.forEach(i=>done.add(i));
    res.push({arr:[...a],pivot:-1,left:[],right:[],done:[...done],label:`Partiție sortată: [${idx.map(i=>a[i]).join(', ')}]`});
    const mid=Math.floor(idx.length/2);
    qs(idx.slice(0,mid));qs(idx.slice(mid));
  }
  qs(arr.map((_,i)=>i));
  res.push({arr:[...a],pivot:-1,left:[],right:[],done:a.map((_,i)=>i),label:`Sortat complet: [${a.join(', ')}]`});
  return res;
}

function qRebuild(){qSteps=qBuildSteps([...qArr]);qIdx=0;qDraw();}

function qDraw(){
  if(!qCtx)return;
  const cv=document.getElementById('q-cv');const s=qSteps[qIdx];
  const w=CW(cv),h=CH(cv);qCtx.clearRect(0,0,w,h);
  const n=s.arr.length,bw=Math.min(56,Math.max(18,(w-80)/n-6));
  const gap=Math.max(4,(w-80-n*bw)/(n-1||1));
  const sx=(w-(n*bw+(n-1)*gap))/2;
  const maxV=Math.max(...s.arr,1);
  s.arr.forEach((v,i)=>{
    const x=sx+i*(bw+gap),bh=Math.max(20,(v/maxV)*(h-75));
    let fl=COLORS.blueL,st=COLORS.blue;
    if(i===s.pivot){fl=COLORS.amberL;st=COLORS.amber;}
    else if(s.left.includes(i)){fl=COLORS.tealL;st=COLORS.teal;}
    else if(s.right.includes(i)){fl=COLORS.redL;st=COLORS.red;}
    else if(s.done.includes(i)){fl=COLORS.greenL;st=COLORS.green;}
    qCtx.fillStyle=fl;qCtx.strokeStyle=st;qCtx.lineWidth=1.5;
    rr(qCtx,x,h-50-bh,bw,bh,4);
    qCtx.fillStyle=st;
    qCtx.font=`bold ${Math.min(13,bw-2)}px 'Space Mono',monospace`;qCtx.textAlign='center';
    qCtx.fillText(v,x+bw/2,h-55);
    if(i===s.pivot){qCtx.fillStyle=COLORS.amber;qCtx.font='10px sans-serif';qCtx.fillText('pivot',x+bw/2,h-38);}
  });
  document.getElementById('q-info').textContent=s.label;
  document.getElementById('q-step').textContent=`${qIdx+1}/${qSteps.length}`;
}

function qNext(){if(qIdx<qSteps.length-1){qIdx++;qDraw();}}
function qPrev(){if(qIdx>0){qIdx--;qDraw();}}
function qReset(){clearInterval(qTimer);qTimer=null;qIdx=0;qDraw();}
function qAuto(){if(qTimer){clearInterval(qTimer);qTimer=null;return;}qTimer=setInterval(()=>{if(qIdx<qSteps.length-1){qIdx++;qDraw();}else{clearInterval(qTimer);qTimer=null;}},1100);}

/* ===== HANOI ===== */
let hSteps=[], hIdx=0, hTimer=null, hCtx=null;

function hInit(){
  const cv=document.getElementById('h-cv');
  if(!cv.getBoundingClientRect().width)return;
  hCtx=setupCanvas(cv);hRebuild();
}

function hRebuild(){
  const n=Math.max(1,Math.min(8,+document.getElementById('h-discs').value));
  const p=Math.max(3,Math.min(4,+document.getElementById('h-pegs').value));
  hSteps=hBuildSteps(n,p);hIdx=0;
  const moves=hSteps.length-1;
  document.getElementById('h-moves-info').textContent=`Număr total mutări: ${moves} (2^${n}-1=${Math.pow(2,n)-1})`;
  if(hCtx) hDraw();
}

function hBuildSteps(n,pegs){
  const res=[];
  const state=Array.from({length:pegs},(_,i)=>i===0?Array.from({length:n},(_,j)=>n-j):[]);
  res.push({pegs:state.map(p=>[...p]),move:'',label:`Start: ${n} discuri pe tija A. Mutări necesare: ${Math.pow(2,n)-1}`});
  function hanoi(k,from,to,aux){
    if(k===0)return;
    const h2=aux.length>0?aux[0]:1;
    const rest=aux.filter(x=>x!==h2);
    hanoi(k-1,from,h2,[to,...rest]);
    state[to].push(state[from].pop());
    res.push({pegs:state.map(p=>[...p]),move:`${String.fromCharCode(65+from)} → ${String.fromCharCode(65+to)}`,label:`Mutarea ${res.length}: disc ${state[to][state[to].length-1]} de pe ${String.fromCharCode(65+from)} pe ${String.fromCharCode(65+to)}`});
    hanoi(k-1,h2,to,[from,...rest]);
  }
  const aux=Array.from({length:pegs-1},(_,i)=>i+1);
  hanoi(n,0,pegs-1,aux.slice(0,pegs-2));
  return res;
}

function hDraw(){
  if(!hCtx)return;
  const cv=document.getElementById('h-cv');const s=hSteps[hIdx];
  const w=CW(cv),h=CH(cv);hCtx.clearRect(0,0,w,h);
  const np=s.pegs.length;
  const pegXs=Array.from({length:np},(_,i)=>w*(i+1)/(np+1));
  const discColors=['#ff6b6b','#ffa94d','#6c63ff','#00e5a0','#c084fc','#22d3ee','#f472b6','#a3e635'];
  const maxD=Math.max(...s.pegs.flat(),1);
  const baseY=h-30,pegH=h-70;
  pegXs.forEach((px,i)=>{
    hCtx.fillStyle='#2a2a3a';hCtx.fillRect(px-3,baseY-pegH,6,pegH);
    hCtx.fillRect(px-Math.min(65,w/(np+1)*0.88/2),baseY,Math.min(130,w/(np+1)*0.88),8);
    hCtx.fillStyle=COLORS.muted;hCtx.font='13px Syne,sans-serif';hCtx.textAlign='center';
    hCtx.fillText(String.fromCharCode(65+i),px,h-8);
  });
  s.pegs.forEach((peg,pi)=>{
    const px=pegXs[pi];
    const maxW=Math.min(w/(np+1)*0.82,130);
    peg.forEach((disc,di)=>{
      const dw=(disc/maxD)*maxW+20;
      const dh=Math.min(24,Math.max(14,(pegH-20)/Math.max(8,1)-3));
      hCtx.fillStyle=discColors[(disc-1)%discColors.length];
      hCtx.strokeStyle=discColors[(disc-1)%discColors.length];
      hCtx.lineWidth=0.5;
      rr(hCtx,px-dw/2,baseY-(di+1)*(dh+2),dw,dh,5);
      if(dw>30){
        hCtx.fillStyle='rgba(255,255,255,0.9)';hCtx.font=`bold 12px 'Space Mono',monospace`;hCtx.textAlign='center';
        hCtx.fillText(disc,px,baseY-(di+1)*(dh+2)+dh/2+4);
      }
    });
  });
  if(s.move){hCtx.fillStyle=COLORS.amber;hCtx.font='bold 14px Syne,sans-serif';hCtx.textAlign='center';hCtx.fillText(s.move,w/2,22);}
  document.getElementById('h-info').textContent=s.label;
  document.getElementById('h-step').textContent=`${hIdx+1}/${hSteps.length}`;
}

function hNext(){if(hIdx<hSteps.length-1){hIdx++;hDraw();}}
function hPrev(){if(hIdx>0){hIdx--;hDraw();}}
function hReset(){clearInterval(hTimer);hTimer=null;hIdx=0;hDraw();}
function hAuto(){if(hTimer){clearInterval(hTimer);hTimer=null;return;}const spd=hSteps.length>50?400:1100;hTimer=setInterval(()=>{if(hIdx<hSteps.length-1){hIdx++;hDraw();}else{clearInterval(hTimer);hTimer=null;}},spd);}

/* ===== SUME ===== */
let sArr=[3,7,2,9,4,6], sSteps=[], sIdx=0, sTimer=null, sCtx=null;

function sInit(){
  const cv=document.getElementById('s-cv');
  if(!cv.getBoundingClientRect().width)return;
  sCtx=setupCanvas(cv);sBuildArr();
}

function sBuildArr(){
  const row=document.getElementById('s-arr-row');row.innerHTML='';
  sArr.forEach((v,i)=>{
    const inp=document.createElement('input');inp.type='number';inp.value=v;inp.min=1;inp.max=99;
    inp.onchange=e=>{sArr[i]=+e.target.value;sRebuild();};row.appendChild(inp);
  });
  const add=document.createElement('button');add.className='btn btn-sm';add.textContent='+';
  add.onclick=()=>{if(sArr.length<10){sArr.push(Math.floor(Math.random()*15)+1);sBuildArr();sRebuild();}};row.appendChild(add);
  if(sArr.length>2){const rem=document.createElement('button');rem.className='btn btn-sm';rem.textContent='−';rem.onclick=()=>{sArr.pop();sBuildArr();sRebuild();};row.appendChild(rem);}
  sRebuild();
}

function sChangeN(n){n=Math.max(2,Math.min(10,n));while(sArr.length<n)sArr.push(Math.floor(Math.random()*15)+1);sArr.length=n;sBuildArr();}
function sRandom(){const vmin=+document.getElementById('s-min').value||1,vmax=+document.getElementById('s-max').value||20;sArr=Array.from({length:sArr.length},()=>Math.floor(Math.random()*(vmax-vmin+1))+vmin);sBuildArr();}

function sBuildSteps(arr){
  const res=[];
  res.push({phase:'start',arr:[...arr],label:`Șirul: [${arr.join(', ')}] — suma totală = ${arr.reduce((a,b)=>a+b,0)}`});
  function rec(indices){
    if(indices.length===1){
      res.push({phase:'single',arr:[...arr],indices,label:`Caz de bază: element singur ${arr[indices[0]]}`});
      return arr[indices[0]];
    }
    const mid=Math.floor(indices.length/2);
    const L=indices.slice(0,mid),R=indices.slice(mid);
    res.push({phase:'divide',arr:[...arr],left:L,right:R,label:`Divide: [${L.map(i=>arr[i]).join(',')}] și [${R.map(i=>arr[i]).join(',')}]`});
    const sl=rec(L),sr=rec(R);
    res.push({phase:'combine',arr:[...arr],left:L,right:R,sumL:sl,sumR:sr,total:sl+sr,label:`Combine: ${sl} + ${sr} = ${sl+sr}`});
    return sl+sr;
  }
  rec(arr.map((_,i)=>i));
  return res;
}

function sRebuild(){sSteps=sBuildSteps([...sArr]);sIdx=0;sDraw();}

function sDraw(){
  if(!sCtx)return;
  const cv=document.getElementById('s-cv');const s=sSteps[sIdx];
  const w=CW(cv),h=CH(cv);sCtx.clearRect(0,0,w,h);
  const arr=s.arr,n=arr.length;
  const bw=Math.min(56,Math.max(24,(w-60)/n-8));
  const gap=Math.max(4,(w-60-n*bw)/(n-1||1));
  const sx=(w-(n*bw+(n-1)*gap))/2;
  const drawBox=(i,fl,st,y,bww)=>{
    const x=sx+i*(bw+gap);
    sCtx.fillStyle=fl;sCtx.strokeStyle=st;sCtx.lineWidth=1.5;
    rr(sCtx,x,y-20,bww||bw,40,6);
    sCtx.fillStyle=st;sCtx.font=`bold 14px 'Space Mono',monospace`;sCtx.textAlign='center';
    sCtx.fillText(arr[i],x+(bww||bw)/2,y+6);
  };
  if(s.phase==='start'){
    arr.forEach((_,i)=>drawBox(i,COLORS.blueL,COLORS.blue,h/2));
  } else if(s.phase==='divide'){
    s.left.forEach(i=>drawBox(i,COLORS.tealL,COLORS.teal,h/2));
    s.right.forEach(i=>drawBox(i,COLORS.amberL,COLORS.amber,h/2));
    const lx=sx+(s.left[s.left.length-1]+0.5)*(bw+gap);
    sCtx.strokeStyle='rgba(255,255,255,0.15)';sCtx.lineWidth=1;sCtx.setLineDash([6,5]);
    sCtx.beginPath();sCtx.moveTo(lx+2,20);sCtx.lineTo(lx+2,h-20);sCtx.stroke();sCtx.setLineDash([]);
  } else if(s.phase==='combine'){
    s.left.forEach(i=>drawBox(i,COLORS.tealL,COLORS.teal,h*.28));
    s.right.forEach(i=>drawBox(i,COLORS.amberL,COLORS.amber,h*.28));
    const lcx=sx+(s.left[0]+s.left[s.left.length-1])/2*(bw+gap)+bw/2;
    const rcx=sx+(s.right[0]+s.right[s.right.length-1])/2*(bw+gap)+bw/2;
    sCtx.fillStyle=COLORS.tealL;sCtx.strokeStyle=COLORS.teal;sCtx.lineWidth=2;
    rr(sCtx,lcx-34,h*.62-22,68,44,8);
    sCtx.fillStyle=COLORS.teal;sCtx.font=`bold 16px 'Space Mono',monospace`;sCtx.textAlign='center';
    sCtx.fillText(s.sumL,lcx,h*.62+8);
    sCtx.fillStyle=COLORS.amberL;sCtx.strokeStyle=COLORS.amber;sCtx.lineWidth=2;
    rr(sCtx,rcx-34,h*.62-22,68,44,8);
    sCtx.fillStyle=COLORS.amber;sCtx.font=`bold 16px 'Space Mono',monospace`;sCtx.textAlign='center';
    sCtx.fillText(s.sumR,rcx,h*.62+8);
    sCtx.fillStyle=COLORS.greenL;sCtx.strokeStyle=COLORS.green;sCtx.lineWidth=2.5;
    rr(sCtx,w/2-44,h*.86-24,88,48,10);
    sCtx.fillStyle=COLORS.green;sCtx.font=`bold 20px 'Space Mono',monospace`;sCtx.textAlign='center';
    sCtx.fillText(s.total,w/2,h*.86+10);
    sCtx.fillStyle=COLORS.muted;sCtx.font='11px sans-serif';sCtx.textAlign='center';
    sCtx.fillText(`${s.sumL}+${s.sumR}`,w/2,h*.86+28);
  } else if(s.phase==='single'){
    s.indices.forEach(i=>drawBox(i,COLORS.purpleL,COLORS.purple,h/2));
  }
  document.getElementById('s-info').textContent=s.label;
  document.getElementById('s-step').textContent=`${sIdx+1}/${sSteps.length}`;
}

function sNext(){if(sIdx<sSteps.length-1){sIdx++;sDraw();}}
function sPrev(){if(sIdx>0){sIdx--;sDraw();}}
function sReset(){clearInterval(sTimer);sTimer=null;sIdx=0;sDraw();}
function sAuto(){if(sTimer){clearInterval(sTimer);sTimer=null;return;}sTimer=setInterval(()=>{if(sIdx<sSteps.length-1){sIdx++;sDraw();}else{clearInterval(sTimer);sTimer=null;}},1200);}

/* ===== FRACTALI ===== */
let fType='koch', fIter=0, fTimer=null, fCtx=null;

function fInit(){
  const cv=document.getElementById('f-cv');
  if(!cv.getBoundingClientRect().width)return;
  fCtx=setupCanvas(cv);fDraw();
}

function setFractal(t){
  clearInterval(fTimer);fTimer=null;fType=t;fIter=0;
  const maxI=t==='dragon'?12:t==='sierpinski'?7:6;
  const sl=document.getElementById('f-iter');sl.max=maxI;sl.value=0;
  document.getElementById('f-iter-val').textContent='0';
  document.querySelectorAll('.ftab').forEach((b,i)=>b.classList.toggle('on',['koch','sierpinski','dragon'][i]===t));
  if(fCtx) fDraw();
}

function fSetIter(v){fIter=v;document.getElementById('f-iter-val').textContent=v;document.getElementById('f-iter').value=v;if(fCtx)fDraw();}
function fReset(){clearInterval(fTimer);fTimer=null;fSetIter(0);}
function fAuto(){
  if(fTimer){clearInterval(fTimer);fTimer=null;return;}
  const maxI=fType==='dragon'?12:fType==='sierpinski'?7:6;
  fTimer=setInterval(()=>{if(fIter<maxI){fIter++;document.getElementById('f-iter-val').textContent=fIter;document.getElementById('f-iter').value=fIter;if(fCtx)fDraw();}else{clearInterval(fTimer);fTimer=null;}},700);
}

function fDraw(){
  if(!fCtx)return;
  const cv=document.getElementById('f-cv');
  const w=CW(cv),h=CH(cv);fCtx.clearRect(0,0,w,h);
  if(fType==='koch') drawKoch(w,h);
  else if(fType==='sierpinski') drawSierpinski(w,h);
  else drawDragon(w,h);
}

function kochSeg(x1,y1,x2,y2,iter){
  if(iter===0){fCtx.moveTo(x1,y1);fCtx.lineTo(x2,y2);return;}
  const dx=x2-x1,dy=y2-y1;
  const ax=x1+dx/3,ay=y1+dy/3;
  const bx=x1+2*dx/3,by=y1+2*dy/3;
  const angle=-Math.PI/3;
  const cx=ax+(dx/3)*Math.cos(angle)-(dy/3)*Math.sin(angle);
  const cy=ay+(dx/3)*Math.sin(angle)+(dy/3)*Math.cos(angle);
  kochSeg(x1,y1,ax,ay,iter-1);kochSeg(ax,ay,cx,cy,iter-1);
  kochSeg(cx,cy,bx,by,iter-1);kochSeg(bx,by,x2,y2,iter-1);
}

function drawKoch(w,h){
  const sz=Math.min(w,h)*0.7;const cx=w/2,cy=h/2+sz*0.1;
  const p1={x:cx-sz/2,y:cy+sz*Math.sqrt(3)/6};
  const p2={x:cx+sz/2,y:cy+sz*Math.sqrt(3)/6};
  const p3={x:cx,y:cy-sz*Math.sqrt(3)/3};
  fCtx.beginPath();fCtx.strokeStyle='#6c63ff';fCtx.lineWidth=Math.max(0.5,1.5-fIter*0.18);
  kochSeg(p1.x,p1.y,p2.x,p2.y,fIter);kochSeg(p2.x,p2.y,p3.x,p3.y,fIter);kochSeg(p3.x,p3.y,p1.x,p1.y,fIter);
  fCtx.stroke();
  document.getElementById('f-info').textContent=`Iterația ${fIter} — ${3*Math.pow(4,fIter)} segmente — perimetrul crește la ∞, aria rămâne finită`;
}

function sierpTri(x1,y1,x2,y2,x3,y3,iter){
  if(iter===0){fCtx.beginPath();fCtx.moveTo(x1,y1);fCtx.lineTo(x2,y2);fCtx.lineTo(x3,y3);fCtx.closePath();fCtx.fill();return;}
  const m12x=(x1+x2)/2,m12y=(y1+y2)/2;
  const m23x=(x2+x3)/2,m23y=(y2+y3)/2;
  const m13x=(x1+x3)/2,m13y=(y1+y3)/2;
  sierpTri(x1,y1,m12x,m12y,m13x,m13y,iter-1);
  sierpTri(m12x,m12y,x2,y2,m23x,m23y,iter-1);
  sierpTri(m13x,m13y,m23x,m23y,x3,y3,iter-1);
}

function drawSierpinski(w,h){
  const sz=Math.min(w,h)*0.8;const cx=w/2,cy=h/2;
  fCtx.fillStyle='#00e5a0';
  sierpTri(cx,cy-sz/2,cx-sz/2,cy+sz/3,cx+sz/2,cy+sz/3,fIter);
  document.getElementById('f-info').textContent=`Iterația ${fIter} — ${Math.pow(3,fIter)} triunghiuri — fiecare se divide în 3`;
}

function drawDragon(w,h){
  let dirs=[0];
  for(let i=0;i<fIter;i++){const rev=[...dirs].reverse().map(d=>(d+1)%4);dirs=[...dirs,1,...rev];}
  const seg=Math.max(3,Math.min(18,180/Math.pow(2,fIter/2)));
  const dx=[seg,0,-seg,0],dy=[0,seg,0,-seg];
  let x=w/2-seg,y=h/2,dir=0;
  fCtx.beginPath();fCtx.moveTo(x,y);
  dirs.forEach(turn=>{dir=(dir+turn)%4;x+=dx[dir];y+=dy[dir];fCtx.lineTo(x,y);});
  fCtx.strokeStyle='#c084fc';fCtx.lineWidth=Math.max(0.5,1.5-fIter*0.08);fCtx.lineJoin='round';fCtx.stroke();
  document.getElementById('f-info').textContent=`Iterația ${fIter} — ${Math.pow(2,fIter)} segmente — fiecare segment se îndoaie la 90°`;
}

/* ===== RESIZE ===== */
function resizeAll(){
  ['m','q','h','s'].forEach(id=>{
    const cv=document.getElementById(id+'-cv');
    if(!cv) return;
    const r=cv.getBoundingClientRect();
    if(!r.width) return;
    cv.width=r.width*devicePixelRatio;
    cv.height=r.height*devicePixelRatio;
    const c=cv.getContext('2d');c.scale(devicePixelRatio,devicePixelRatio);
    if(id==='m'){mCtx=c;mDraw();}
    if(id==='q'){qCtx=c;qDraw();}
    if(id==='h'){hCtx=c;hDraw();}
    if(id==='s'){sCtx=c;sDraw();}
  });
  const fcv=document.getElementById('f-cv');
  if(fcv&&fcv.getBoundingClientRect().width){
    const r=fcv.getBoundingClientRect();
    fcv.width=r.width*devicePixelRatio;fcv.height=r.height*devicePixelRatio;
    const c=fcv.getContext('2d');c.scale(devicePixelRatio,devicePixelRatio);fCtx=c;fDraw();
  }
}

window.addEventListener('resize',()=>setTimeout(resizeAll,100));
setTimeout(()=>{
  mInit();
},300);
</script>
</body>
</html>
