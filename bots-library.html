<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<link rel="icon" type="image/svg+xml" href="favicon.svg">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>TickWealth – Bots</title>
<meta name="description" content="Independent bots: each with its own market, contract, rules, risk limits and optional Martingale. Add, delete, upload and export.">
<link rel="stylesheet" href="core.css">
<style>
.bw{max-width:1100px;margin:0 auto;padding:14px;display:grid;gap:14px}
.bt{display:flex;gap:10px;flex-wrap:wrap;align-items:center}.bt .btn{width:auto}
.bl{display:grid;gap:14px;grid-template-columns:repeat(auto-fill,minmax(330px,1fr))}
.bc{border:1px solid rgba(255,255,255,.12);border-radius:14px;padding:14px;background:rgba(255,255,255,.04)}
.bh{display:flex;gap:8px;align-items:center}.bh input{flex:1;font-weight:700}.bs{font-size:12px;color:#8e9ab3}.bs.on{color:#00ffa3}
.bg{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin:10px 0}.bg label{font-size:11px;color:#8e9ab3;display:block}
.bg input,.bg select,.bh input{width:100%;padding:6px 8px;border-radius:8px;border:1px solid rgba(255,255,255,.14);background:rgba(0,0,0,.35);color:#d7e0f2;font:inherit}
.bg .w{grid-column:1/-1}.br{display:flex;gap:8px;flex-wrap:wrap}.br button{width:auto;padding:8px 12px}
.bi{font-size:12.5px;margin-top:8px;color:#c9d3e8}.wn{border-left:3px solid #ff3b69;padding:10px 14px;border-radius:8px;background:rgba(255,59,105,.07);font-size:13px}
</style>
</head>
<body>
<div id="top"></div>
<div id="app"><div class="bw">
  <div class="wn"><b>Read this.</b> Bots follow your rules on live ticks. They cannot predict the next tick, and trading can lose your whole stake. Martingale multiplies the stake after each loss and can empty an account in a few trades, so it is off by default and capped by a step limit. Bots run in paper mode unless you are logged in and in live mode. Bots only run while this page is open.</div>
  <div class="bt"><button class="btn" id="add">+ New bot</button><button class="btn ghost" id="up">Upload bot (.json)</button><button class="btn ghost" id="ex">Load example bots</button><span id="md" class="bs"></span><input type="file" id="file" accept=".json,application/json" hidden></div>
  <div class="bl" id="list"></div>
</div></div>
<script src="config.js"></script>
<script src="core.js"></script>
<script src="ai.js"></script>
<script>
/* Independent bots. Each bot is plain JSON: its own market, contract, entry rule, risk limits and optional Martingale.
   Bots are stored in this browser. Upload, export or delete any of them. Nothing here predicts ticks. */
const $=TW.$, KEY='tw_bots2', CT=['CALL','PUT','DIGITOVER','DIGITUNDER','DIGITEVEN','DIGITODD','DIGITMATCH','DIGITDIFF'], CONDS=['even','odd','over','under','rise','fall'];
const MK=TW.VOLS.map(v=>[v.id,v.name]), R={};
const num=(v,lo,hi,d)=>{v=+v;return isFinite(v)?Math.min(hi,Math.max(lo,v)):d};
function clean(b){b=b&&typeof b==='object'?b:{};const r=b.rule||{},m=b.mart||{};return{id:'b'+Date.now()+Math.floor(Math.random()*1e5),name:String(b.name||'New bot').slice(0,40),symbol:TW.VOLS.some(v=>v.id===b.symbol)?b.symbol:'R_100',contract:CT.includes(b.contract)?b.contract:'DIGITOVER',barrier:num(b.barrier,0,9,4),duration:num(b.duration,1,10,1),stake:num(b.stake,0.35,1000,0.35),
 rule:{kind:r.kind==='every'?'every':'streak',cond:CONDS.includes(r.cond)?r.cond:'even',n:num(r.n,1,50,3),cb:num(r.cb,0,9,4)},mart:{on:!!m.on,mult:num(m.mult,1.1,5,2),steps:num(m.steps,1,8,3)},sl:num(b.sl,0,100000,5),tp:num(b.tp,0,100000,5),max:num(b.max,0,10000,0)}}
const EX=[{name:'Example: Under 7 after two 8-9s',symbol:'R_100',contract:'DIGITUNDER',barrier:7,duration:1,rule:{kind:'streak',cond:'over',cb:7,n:2}},{name:'Example: Even after three odds',symbol:'R_50',contract:'DIGITEVEN',duration:1,rule:{kind:'streak',cond:'odd',n:3}}];
function load(){try{const a=JSON.parse(localStorage.getItem(KEY));if(Array.isArray(a))return a.map(clean).map((b,i)=>Object.assign(b,{id:a[i].id||b.id}))}catch(e){}return EX.map(clean)}
let bots=load();const save=()=>localStorage.setItem(KEY,JSON.stringify(bots));
const opts=(l,s)=>l.map(x=>{const v=Array.isArray(x)?x[0]:x,t=Array.isArray(x)?x[1]:x;return`<option value="${TW.esc(v)}"${v==s?' selected':''}>${TW.esc(t)}</option>`}).join('');
const f=(l,k,v,x='')=>`<label>${l}<input data-k="${k}" type="number" value="${v}" ${x}></label>`;
function card(b){return`<div class="bc" data-id="${b.id}"><div class="bh"><input data-k="name" value="${TW.esc(b.name)}" aria-label="Bot name"><span class="bs" id="st-${b.id}">stopped</span></div>
<div class="bg"><label>Market<select data-k="symbol">${opts(MK,b.symbol)}</select></label><label>Contract<select data-k="contract">${opts(CT,b.contract)}</select></label>
${f('Barrier / digit','barrier',b.barrier,'min="0" max="9"')}${f('Ticks','duration',b.duration,'min="1" max="10"')}${f('Stake (USD)','stake',b.stake,'min="0.35" step="0.01"')}
<label>Entry rule<select data-k="rule.kind">${opts([['streak','After a streak'],['every','Every N ticks']],b.rule.kind)}</select></label>
<label>Condition<select data-k="rule.cond">${opts(CONDS,b.rule.cond)}</select></label>${f('Streak or N','rule.n',b.rule.n,'min="1" max="50"')}${f('Cond. digit (over/under)','rule.cb',b.rule.cb,'min="0" max="9"')}
${f('Stop-loss (USD, 0 = off)','sl',b.sl,'min="0"')}${f('Take-profit (USD, 0 = off)','tp',b.tp,'min="0"')}${f('Max trades (0 = no limit)','max',b.max,'min="0"')}
<label class="w"><input type="checkbox" data-k="mart.on"${b.mart.on?' checked':''}> Martingale (risky) &nbsp;multiplier <input data-k="mart.mult" type="number" step="0.1" min="1.1" max="5" value="${b.mart.mult}" style="width:70px"> &nbsp;max steps <input data-k="mart.steps" type="number" min="1" max="8" value="${b.mart.steps}" style="width:60px"></label></div>
<div class="br"><button class="btn" data-a="run">Start</button><button class="btn ghost" data-a="exp">Export</button><button class="btn ghost" data-a="del">Delete</button></div><div class="bi" id="in-${b.id}"></div></div>`}
function draw(){$('#list').innerHTML=bots.map(card).join('')||'<div class="bi">No bots yet. Add one, upload a .json file, or load the examples.</div>';bots.forEach(info);$('#md').textContent='Mode: '+TW.mode().toUpperCase()}
function info(b){const r=R[b.id],i=$('#in-'+b.id),s=$('#st-'+b.id);if(!i)return;const on=r&&r.on;s.textContent=on?'running':'stopped';s.className='bs'+(on?' on':'');
 i.textContent=r?`Trades ${r.n}, wins ${r.w}, P/L ${r.pnl.toFixed(2)} USD${r.step?`, Martingale step ${r.step}`:''}${r.msg?'. '+r.msg:''}`:'Not started yet.'}
const get=id=>bots.find(b=>b.id===id);
const cond=(c,cb,P,D,j)=>c==='rise'?P[j]>P[j-1]:c==='fall'?P[j]<P[j-1]:c==='over'?D[j]>cb:c==='under'?D[j]<cb:c==='even'?D[j]%2===0:D[j]%2===1;
function start(b){stop(b);const r=R[b.id]=Object.assign(R[b.id]||{n:0,w:0,pnl:0,step:0},{on:true,busy:false,k:0,msg:''});r.pnl=0;r.n=0;r.w=0;r.step=0;
 r.feed=TW.tickFeed(b.symbol,{primary:false,count:60,onTick:fd=>tick(b,fd)});info(b)}
function stop(b,why){const r=R[b.id];if(!r)return;r.on=false;if(r.feed){r.feed.close();r.feed=null}if(why)r.msg=why;info(b)}
function tick(b,fd){const r=R[b.id];if(!r||!r.on||r.busy)return;r.k++;const P=fd.prices,D=fd.digits,i=P.length-1;let go=false;
 if(b.rule.kind==='every')go=r.k%b.rule.n===0;else{let s=0;for(let j=i;j>=1&&s<b.rule.n&&cond(b.rule.cond,b.rule.cb,P,D,j);j--)s++;go=s>=b.rule.n}
 if(go)place(b,r)}
async function place(b,r){const st=+(b.stake*(b.mart.on?Math.pow(b.mart.mult,r.step):1)).toFixed(2);r.busy=true;
 try{const t=await TW.trade({contract_type:b.contract,symbol:b.symbol,amount:st,duration:b.duration,duration_unit:'t',barrier:/OVER|UNDER|MATCH|DIFF/.test(b.contract)?b.barrier:undefined,label:b.name,bot:b.name});
  const res=await t.done,p=+res.profit;r.n++;r.pnl+=p;if(p>0){r.w++;r.step=0}else r.step=b.mart.on?(r.step+1>=b.mart.steps?0:r.step+1):0;
  if(b.sl>0&&r.pnl<=-b.sl)stop(b,'Stopped: stop-loss reached');else if(b.tp>0&&r.pnl>=b.tp)stop(b,'Stopped: take-profit reached');else if(b.max>0&&r.n>=b.max)stop(b,'Stopped: max trades reached')}
 catch(e){stop(b,'Stopped: '+(e.message||e))}finally{r.busy=false;info(b)}}
$('#list').addEventListener('change',e=>{const c=e.target.closest('.bc');if(!c||!e.target.dataset.k)return;const b=get(c.dataset.id),p=e.target.dataset.k.split('.'),t=e.target;
 let v=t.type==='checkbox'?t.checked:t.type==='number'?+t.value:t.value;let o=b;for(let i=0;i<p.length-1;i++)o=o[p[i]];o[p[p.length-1]]=v;Object.assign(b,Object.assign(clean(b),{id:b.id}));save();if(R[b.id]&&R[b.id].on&&e.target.dataset.k==='symbol')start(b)});
$('#list').addEventListener('click',e=>{const a=e.target.dataset.a,c=e.target.closest('.bc');if(!a||!c)return;const b=get(c.dataset.id);
 if(a==='run'){const r=R[b.id];if(r&&r.on){stop(b,'Stopped by you');e.target.textContent='Start'}else{if(b.mart.on&&!confirm('Martingale doubles risk after each loss. Start this bot with Martingale on?'))return;if(TW.mode()==='live'&&!confirm('LIVE mode: this bot will use real money. Start it?'))return;start(b);e.target.textContent='Stop'}}
 if(a==='exp'){const x=Object.assign({},b);delete x.id;const u=URL.createObjectURL(new Blob([JSON.stringify(x,null,2)],{type:'application/json'})),l=document.createElement('a');l.href=u;l.download=(b.name.replace(/[^a-z0-9]+/gi,'-')||'bot')+'.json';l.click()}
 if(a==='del'&&confirm('Delete this bot?')){stop(b);delete R[b.id];bots=bots.filter(x=>x.id!==b.id);save();draw()}});
$('#add').onclick=()=>{bots.push(clean({}));save();draw()};
$('#ex').onclick=()=>{EX.forEach(x=>bots.push(clean(x)));save();draw()};
$('#up').onclick=()=>$('#file').click();
$('#file').onchange=async e=>{const fl=e.target.files[0];e.target.value='';if(!fl)return;if(fl.size>100000){TW.toast('File too large (max 100 KB).','err');return}
 try{const j=JSON.parse(await fl.text()),a=Array.isArray(j)?j:[j];if(bots.length+a.length>30)throw new Error('Too many bots (max 30).');a.forEach(x=>bots.push(clean(x)));save();draw();TW.toast('Uploaded '+a.length+' bot(s). Bots are checked and limited to safe values.','ok')}catch(x){TW.toast('Could not read bot file: '+x.message,'err',6000)}};
draw();
</script>
</body>
</html>
