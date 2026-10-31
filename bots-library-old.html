<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<link rel="icon" type="image/svg+xml" href="favicon.svg">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>TickWealth – Bots Library</title>
<meta name="description" content="Five rule-based trading bots that run on live Deriv ticks in paper or live mode, with stop-loss, take-profit and optional martingale.">
<link rel="stylesheet" href="core.css">
<style>
.bots{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:14px;margin-top:14px}
.bot{border-top:3px solid var(--c)}
.bot .nm{font-weight:800;color:var(--c);font-size:14px}.bot .bd{font-size:10px;font-weight:800;padding:3px 8px;border-radius:10px;background:#ffffff14;color:var(--mut)}
.bot .top2{display:flex;justify-content:space-between;align-items:center;gap:8px}
.bot .d{font-size:11px;color:var(--mut);margin:8px 0;line-height:1.5}
.bot .st{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;margin:8px 0}
.bot .st div{background:var(--p1);border:1px solid var(--line);border-radius:8px;padding:6px;text-align:center;font-size:9px;color:var(--dim)}.bot .st b{display:block;font-size:13px;color:var(--tx)}
.bot .f{display:grid;grid-template-columns:repeat(3,1fr);gap:6px}.bot .f label{font-size:9px;color:var(--dim);font-weight:800}.bot .f input{width:100%;margin-top:3px;background:#070a14;border:1px solid var(--line);color:#fff;border-radius:7px;padding:7px;font-size:12px}
.bot .lg{height:84px;background:#070a14;border:1px solid var(--line);border-radius:8px;padding:6px;font:10px ui-monospace,Menlo,monospace;overflow:auto;margin-top:8px;color:var(--mut)}
.bot .lg .w{color:var(--green)}.bot .lg .l{color:var(--red)}
.bar{display:flex;gap:10px;align-items:center;flex-wrap:wrap;margin-top:12px}
</style>
</head>
<body class="t-violet">
<div id="top"></div>
<div class="wrap">
  <div class="h">BOTS LIBRARY · 5 RULE-BASED BOTS</div>
  <div class="sub">Each bot watches live ticks on the market you pick and places trades by fixed rules. In <b>paper</b> mode (default) nothing is risked. No bot can promise profit — digits and prices on synthetic indices are random, and every result below is from real ticks, not a simulation of wins.</div>
  <div class="warn" id="liveWarn" style="display:none"></div>
  <div class="bar">
    <span class="lbl" style="margin:0">MARKET</span><select class="sel" id="mk"></select>
    <button class="btn red" id="stopAll">■ Stop all bots</button>
    <span class="spacer"></span>
    <span class="mono" style="font-size:12px">Total P/L <b id="tPnl">$0.00</b> · Running <b id="tRun">0/5</b> · Win <b id="tWin">—</b></span>
  </div>
  <div class="bots" id="bots"></div>

  <div class="card" style="margin-top:18px">
    <div class="h">EXPORT</div>
    <div class="sub">Download each bot's settings as JSON. <b>Experimental:</b> the Deriv Bot XML below is a basic trade loop (market, contract type, stake, buy, trade again) without this site's signal rules — import it at bot.deriv.com on a <b>demo</b> account first, and add your own conditions there. If Deriv Bot rejects a file, tell me the error and I'll fix the template.</div>
    <div id="exp" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:8px;margin-top:10px"></div>
  </div>
  <div class="notice" id="disc"></div>
</div>
<div class="foot">TickWealth is an independent tool and is not affiliated with Deriv.</div>
<script src="config.js"></script>
<script src="core.js"></script>
<script src="ai.js"></script>
<script>
TW.ready(function(){
  const $=TW.$, CFG=window.TW_CONFIG||{}; $('#disc').textContent=TW.DISCLAIMER;
  const mkt=TW.mountTop({active:'bots-library'});
  const sel=$('#mk'); const L=TW.VOLS.filter(v=>v.digits); sel.innerHTML=L.map(v=>`<option value="${v.id}">${v.name}</option>`).join(''); sel.value='1HZ100V';

  /* strategy rules — each returns an order or null */
  const lastN=(p,n)=>p.slice(-n);
  const BOTS=[
   {id:'phantom',name:'Phantom Mirror',badge:'MATCHES · FREE',c:'#a855f7',kind:'digit',dur:1,dsc:'Matches on the hottest digit when it appears ≥14% of recent ticks (normal 10%). 1-tick trades.',
    xml:{cat:'digits',type:'matchesdiffers',ct:'DIGITMATCH',pred:true,barrier:7,dur:1},
    sig:f=>{if(f.digits.length<60)return null;const a=TW.analyze(f.digits);return a.f[a.hot]>=.14?{contract_type:'DIGITMATCH',barrier:a.hot,label:'Matches '+a.hot,note:'hot '+a.hot+' '+(a.f[a.hot]*100).toFixed(1)+'%'}:null;}},
   {id:'raptor',name:'Raptor Rise',badge:'RISE · FREE',c:'#10b981',kind:'tick',dur:5,dsc:'Buys Rise (5 ticks) after 3 consecutive higher ticks — a simple momentum rule.',
    xml:{cat:'callput',type:'risefall',ct:'CALL',pred:false,dur:5},
    sig:f=>{const p=lastN(f.prices,4);return p.length===4&&p[1]>p[0]&&p[2]>p[1]&&p[3]>p[2]?{contract_type:'CALL',label:'Rise',note:'3 higher ticks'}:null;}},
   {id:'overlord',name:'Overlord Vault',badge:'OVER 4 · PREMIUM',c:'#ff8c00',kind:'digit',dur:1,dsc:'Over 4 when digits above 4 make up ≥55% of recent ticks (normal 50%).',
    xml:{cat:'digits',type:'overunder',ct:'DIGITOVER',pred:true,barrier:4,dur:1},
    sig:f=>{if(f.digits.length<60)return null;const a=TW.analyze(f.digits),o=a.pOver(4);return o>=.55?{contract_type:'DIGITOVER',barrier:4,label:'Over 4',note:'over '+(o*100).toFixed(1)+'%'}:null;}},
   {id:'eclipse',name:'Eclipse Parity',badge:'EVEN · PREMIUM',c:'#00d4ff',kind:'digit',dur:1,dsc:'Even when even digits make up ≥57% of recent ticks (normal 50%).',
    xml:{cat:'digits',type:'evenodd',ct:'DIGITEVEN',pred:false,dur:1},
    sig:f=>{if(f.digits.length<60)return null;const a=TW.analyze(f.digits);return a.pEven>=.57?{contract_type:'DIGITEVEN',label:'Even',note:'even '+(a.pEven*100).toFixed(1)+'%'}:null;}},
   {id:'falcon',name:'Falcon Fall',badge:'FALL · PREMIUM',c:'#ff3b3b',kind:'tick',dur:5,dsc:'Buys Fall (5 ticks) after 3 consecutive lower ticks — a simple momentum rule.',
    xml:{cat:'callput',type:'risefall',ct:'PUT',pred:false,dur:5},
    sig:f=>{const p=lastN(f.prices,4);return p.length===4&&p[1]<p[0]&&p[2]<p[1]&&p[3]<p[2]?{contract_type:'PUT',label:'Fall',note:'3 lower ticks'}:null;}}
  ];
  BOTS.forEach(b=>Object.assign(b,{run:false,pnl:0,t:0,w:0,open:false,loss:0,cool:0,logs:[]}));
  const unlocked=()=>!CFG.paymentsEnabled||!!TW.store.get('tw_unlock');
  const isFree=b=>!CFG.paymentsEnabled||(CFG.freeBots||[]).includes(b.id);

  $('#bots').innerHTML=BOTS.map(b=>`<div class="card bot" style="--c:${b.c}"><div class="top2"><span class="nm">${b.name}</span><span class="bd">${b.badge}</span></div><div class="d">${b.dsc}</div>
    <div class="st"><div><b id="p-${b.id}">$0.00</b>PROFIT</div><div><b id="w-${b.id}">—</b>WIN</div><div><b id="n-${b.id}">0</b>TRADES</div></div>
    <div class="f"><div><label>STAKE</label><input id="s-${b.id}" type="number" min="0.35" step="0.5" value="0.35"></div><div><label>STOP-LOSS $</label><input id="sl-${b.id}" type="number" min="0" step="1" value="5"></div><div><label>TAKE-PROFIT $</label><input id="tp-${b.id}" type="number" min="0" step="1" value="5"></div></div>
    <label class="switch"><span>Martingale (×${TW.settings.martMult} after loss, max ${TW.settings.martSteps} steps)</span><input type="checkbox" id="m-${b.id}"></label>
    <button class="btn full" id="go-${b.id}" style="margin-top:10px">▶ Start</button>
    <div class="lg" id="lg-${b.id}"><div>Idle.</div></div></div>`).join('');
  $('#exp').innerHTML=BOTS.map(b=>`<div class="card" style="padding:10px"><b style="color:${b.c};font-size:12px">${b.name}</b><div style="display:flex;gap:6px;margin-top:8px"><button class="btn ghost" style="flex:1" data-j="${b.id}">JSON</button><button class="btn ghost" style="flex:1" data-x="${b.id}">XML (exp.)</button></div></div>`).join('');

  const logTo=(b,m,c)=>{b.logs.unshift(`<div class="${c||''}">[${new Date().toLocaleTimeString().slice(0,8)}] ${TW.esc(m)}</div>`); b.logs.length=Math.min(b.logs.length,30); $('#lg-'+b.id).innerHTML=b.logs.join('');};
  function paint(){
    let pnl=0,run=0,t=0,w=0;
    BOTS.forEach(b=>{pnl+=b.pnl;t+=b.t;w+=b.w;if(b.run)run++;
      $('#p-'+b.id).textContent=TW.money(b.pnl); $('#p-'+b.id).style.color=b.pnl>=0?'var(--green)':'var(--red)';
      $('#w-'+b.id).textContent=b.t?Math.round(b.w/b.t*100)+'%':'—'; $('#n-'+b.id).textContent=b.t;
      const g=$('#go-'+b.id); g.textContent=b.run?'■ Stop':(isFree(b)||unlocked()?'▶ Start':'🔒 Unlock premium (KES '+CFG.priceKES+')'); g.className='btn full'+(b.run?' red':'');});
    $('#tPnl').textContent=TW.money(pnl); $('#tPnl').style.color=pnl>=0?'var(--green)':'var(--red)'; $('#tRun').textContent=run+'/5'; $('#tWin').textContent=t?Math.round(w/t*100)+'%':'—';
    const live=TW.mode()==='live', lw=$('#liveWarn'); lw.style.display=live?'block':'none'; if(live)lw.textContent=`LIVE MODE: bots will place trades on ${TW.account.loginid} (${TW.account.virtual?'demo':'REAL money'}) automatically. Max stake ${TW.settings.maxStake}, session stop-loss ${TW.settings.stopLoss||'off'}.`;
  }
  TW.on('account',paint); TW.on('trade',paint);

  /* one shared live feed drives all bots */
  let feed=null;
  function startFeed(){ if(feed)feed.close(); feed=TW.tickFeed(sel.value,{count:300,onStatus:s=>TW.setStatus(s),onError:m=>{TW.setStatus('error',m);BOTS.filter(b=>b.run).forEach(b=>logTo(b,'Market error: '+m,'l'));},onTick:onTick}); }
  sel.onchange=startFeed;
  function stake(b){ let s=parseFloat($('#s-'+b.id).value)||0.35; if($('#m-'+b.id).checked&&b.loss>0)s*=Math.pow(TW.settings.martMult,Math.min(b.loss,TW.settings.martSteps)); return +s.toFixed(2); }
  function stop(b,why){ b.run=false; logTo(b,'Stopped'+(why?': '+why:''),'l'); paint(); }
  function onTick(f){
    BOTS.forEach(b=>{
      if(!b.run) return; if(b.open) return; if(b.cool>0){b.cool--;return;}
      const sg=b.sig(f); if(!sg) return;
      b.open=true; const amount=stake(b);
      TW.trade({contract_type:sg.contract_type,symbol:f.symbol,amount,duration:b.dur,duration_unit:'t',barrier:sg.barrier,label:sg.label,bot:b.name},{silent:true}).then(t=>{
        logTo(b,`BUY ${sg.label} $${amount} (${sg.note})`);
        t.done.then(r=>{ b.open=false; b.cool=2; b.t++; b.pnl=+(b.pnl+r.profit).toFixed(2);
          if(r.profit>0){b.w++;b.loss=0;}else b.loss++;
          logTo(b,(r.profit>0?'WIN +':'LOSS ')+TW.money(r.profit),r.profit>0?'w':'l');
          const sl=parseFloat($('#sl-'+b.id).value)||0, tp=parseFloat($('#tp-'+b.id).value)||0;
          if(b.run&&sl>0&&b.pnl<=-sl)stop(b,'stop-loss hit'); else if(b.run&&tp>0&&b.pnl>=tp)stop(b,'take-profit hit'); else paint(); });
      }).catch(e=>{ b.open=false; if(!e.quiet)TW.toast(b.name+': '+e.message,'err',5000); stop(b,e.message); });
    });
  }
  async function toggle(b){
    if(b.run){stop(b);return;}
    if(!isFree(b)&&!unlocked()){ unlockFlow(); return; }
    if(TW.mode()==='live'){
      const ok=await TW.modal({title:'Start bot on '+(TW.account.virtual?'DEMO':'REAL')+' account?',html:`<div class="sub">${b.name} will trade by itself on ${TW.esc(TW.account.loginid)}.</div>${TW.account.virtual?'':'<div class="warn">This uses real money and can lose it all. Martingale increases losses fast.</div>'}`,buttons:[{label:'Cancel',cls:'ghost',value:false},{label:'Start bot',cls:TW.account.virtual?'':'red',value:true}]});
      if(!ok)return;
    }
    b.run=true; b.loss=0; b.cool=0; logTo(b,'Started on '+TW.volName(sel.value)+' ('+(TW.mode()==='live'?'LIVE':'paper')+')'); paint();
  }
  BOTS.forEach(b=>$('#go-'+b.id).onclick=()=>toggle(b));
  $('#stopAll').onclick=()=>{BOTS.filter(b=>b.run).forEach(b=>stop(b,'stopped by you'));};

  /* premium unlock — only active when config.js enables payments and a backend exists */
  function unlockFlow(){
    if(!CFG.mpesaApi){ TW.toast('Payments are not configured yet.','err'); return; }
    TW.modal({title:'Unlock premium bots',html:`<div class="sub">Pay KES ${CFG.priceKES} by M-Pesa. You will get an STK push on your phone; the bots unlock only after your server confirms the payment.</div><input id="ph" class="inp" type="tel" placeholder="2547XXXXXXXX" value="254"><div id="pm" class="sub"></div><div class="row"><button class="btn ghost" id="pc">Cancel</button><button class="btn" id="pg">Send STK push</button></div>`,buttons:[],init:(m,close)=>{
      const say=t=>{$('#pm',m).textContent=t;};
      $('#pc',m).onclick=()=>close();
      $('#pg',m).onclick=async()=>{
        const phone=$('#ph',m).value.trim(); if(!/^254\d{9}$/.test(phone)){say('Enter the number as 2547XXXXXXXX');return;}
        $('#pg',m).disabled=true; say('Sending STK push…');
        try{
          const r=await fetch(CFG.mpesaApi+'/stkpush',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({phone,amount:CFG.priceKES,product:'tickwealth-premium'})}).then(x=>x.json());
          if(!r.checkoutId) throw new Error(r.error||'The payment server did not accept the request.');
          say('Check your phone and enter your M-Pesa PIN…');
          for(let i=0;i<24;i++){ await new Promise(z=>setTimeout(z,5000));
            const s=await fetch(CFG.mpesaApi+'/status?id='+encodeURIComponent(r.checkoutId)).then(x=>x.json());
            if(s.paid&&s.unlock){ TW.store.set('tw_unlock',s.unlock); TW.toast('Payment confirmed — premium bots unlocked','ok'); close(); paint(); return; }
            if(s.failed) throw new Error(s.error||'Payment was cancelled or failed.'); }
          throw new Error('No confirmation received yet. If money was deducted, contact support with your M-Pesa code.');
        }catch(e){ say(e.message); $('#pg',m).disabled=false; }
      };
    }});
  }
  /* exports */
  const dl=(name,txt,type)=>{const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([txt],{type}));a.download=name;document.body.appendChild(a);a.click();a.remove();setTimeout(()=>URL.revokeObjectURL(a.href),1000);};
  function xml(b){const x=b.xml,sym=sel.value,st=parseFloat($('#s-'+b.id).value)||0.35;
    return `<xml xmlns="https://developers.google.com/blockly/xml" is_dbot="true" collection="false"><variables></variables>
<block type="trade_definition" deletable="false" x="0" y="0"><statement name="TRADE_OPTIONS">
<block type="trade_definition_market" deletable="false" movable="false"><field name="MARKET_LIST">synthetic_index</field><field name="SUBMARKET_LIST">random_index</field><field name="SYMBOL_LIST">${sym}</field><next>
<block type="trade_definition_tradetype" deletable="false" movable="false"><field name="TRADETYPECAT_LIST">${x.cat}</field><field name="TRADETYPE_LIST">${x.type}</field><next>
<block type="trade_definition_contracttype" deletable="false" movable="false"><field name="TYPE_LIST">${x.ct}</field><next>
<block type="trade_definition_candleinterval" deletable="false" movable="false"><field name="CANDLEINTERVAL_LIST">60</field><next>
<block type="trade_definition_restartbuysell" deletable="false" movable="false"><field name="TIME_MACHINE_ENABLED">FALSE</field><next>
<block type="trade_definition_restartonerror" deletable="false" movable="false"><field name="RESTARTONERROR">TRUE</field></block></next></block></next></block></next></block></next></block></next></block>
</statement><statement name="SUBMARKET"><block type="trade_definition_tradeoptions"><mutation xmlns="http://www.w3.org/1999/xhtml" has_first_barrier="false" has_second_barrier="false" has_prediction="${x.pred}"></mutation><field name="DURATIONTYPE_LIST">t</field><value name="DURATION"><shadow type="math_number_positive"><field name="NUM">${x.dur}</field></shadow></value><value name="AMOUNT"><shadow type="math_number_positive"><field name="NUM">${st}</field></shadow></value>${x.pred?`<value name="PREDICTION"><shadow type="math_number_positive"><field name="NUM">${x.barrier}</field></shadow></value>`:''}</block></statement></block>
<block type="before_purchase" deletable="false" x="0" y="400"><statement name="BEFOREPURCHASE_STACK"><block type="purchase"><field name="PURCHASE_LIST">${x.ct}</field></block></statement></block>
<block type="after_purchase" deletable="false" x="500" y="400"><statement name="AFTERPURCHASE_STACK"><block type="trade_again"></block></statement></block></xml>`; }
  $('#exp').onclick=e=>{const j=e.target.closest('[data-j]'),x=e.target.closest('[data-x]');
    if(j){const b=BOTS.find(z=>z.id===j.dataset.j);dl(b.id+'.json',JSON.stringify({name:b.name,description:b.dsc,market:sel.value,duration_ticks:b.dur,stake:+$('#s-'+b.id).value,stop_loss:+$('#sl-'+b.id).value,take_profit:+$('#tp-'+b.id).value,martingale:$('#m-'+b.id).checked,rule:b.dsc},null,2),'application/json');}
    if(x){const b=BOTS.find(z=>z.id===x.dataset.x);dl(b.id+'.xml',xml(b),'text/xml');}};

  paint(); startFeed();
});
</script>
<script src="advisor.js"></script>
</body>
</html>
