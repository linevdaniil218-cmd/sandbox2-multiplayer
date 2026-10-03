<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Admin Abuse City</title>
<style>
*{box-sizing:border-box}html,body{margin:0;height:100%;overflow:hidden;font-family:Arial;background:#111;color:white}button{border:0;border-radius:10px;padding:10px 14px;font-weight:bold;color:white;background:#334155}button:active{transform:scale(.96)}
#menu{position:fixed;inset:0;z-index:50;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,#111827,#312e81)}
.card{width:min(430px,92vw);padding:28px;border-radius:22px;background:#172033;text-align:center;box-shadow:0 20px 60px #0009}.card h1{font-size:34px;margin:0 0 10px}.card p{color:#cbd5e1}.main{width:100%;margin-top:12px;background:#22c55e;font-size:20px}.card button:not(.main){width:100%;margin-top:10px}
#game{display:none;position:fixed;inset:0;background:#6fa451}
#view{position:absolute;inset:0;overflow:hidden}
#world{position:absolute;width:3000px;height:2000px;background:#71a553}
.road{position:absolute;background:#414141;border:4px solid #555}.hr{height:160px;left:0;right:0}.vr{width:160px;top:0;bottom:0}
.build{position:absolute;background:#aeb7c0;border:6px solid #7c8792;border-radius:8px}
.window{position:absolute;width:20px;height:28px;background:#7dd3fc;border:2px solid #334155}
.park{position:absolute;background:#4d9148;border:5px solid #347037;border-radius:20px}
.tree{position:absolute;width:44px;height:44px;border-radius:50%;background:#216b2a;border:5px solid #174d20}
.car{position:absolute;width:78px;height:42px;background:#dc2626;border:4px solid #111;border-radius:12px;z-index:5}.car:nth-of-type(even){background:#2563eb}
.car .glass{position:absolute;left:19px;top:5px;width:32px;height:17px;background:#9bd6e8;border-radius:4px}.car:before,.car:after{content:"";position:absolute;width:14px;height:14px;background:#111;border-radius:50%;bottom:-8px}.car:before{left:8px}.car:after{right:8px}.occupied{outline:4px solid #facc15}.car.wheelspin:before,.car.wheelspin:after{animation:wheel .18s linear infinite}@keyframes wheel{to{transform:rotate(360deg)}}
.npc,.player{position:absolute;width:32px;height:40px;border:3px solid white;border-radius:12px 12px 8px 8px;background:#64748b;text-align:center;font-size:18px;z-index:7}.player{background:#f59e0b}.tag{position:absolute;top:-22px;left:50%;transform:translateX(-50%);font-size:11px;white-space:nowrap}
.bank{position:absolute;background:#166534;border:7px solid #14532d;border-radius:12px;z-index:3;color:#fff;font-weight:bold;text-align:center;padding-top:18px;font-size:20px}.bank:before{content:"🏦";display:block;font-size:40px}.bankHint{position:absolute;z-index:12;background:#111d;padding:9px 12px;border-radius:10px;display:none}
#hud{position:absolute;top:10px;left:10px;right:10px;z-index:15;display:flex;justify-content:space-between}.box{background:#111c;padding:10px;border-radius:12px;backdrop-filter:blur(5px)}
#players{position:absolute;right:10px;top:60px;z-index:14;min-width:145px}
#admin{display:none;position:absolute;left:10px;top:60px;z-index:20;width:270px;background:#101827ee;padding:14px;border-radius:14px}.adminGrid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-top:8px}.adminGrid button{font-size:12px}
#hint{position:absolute;left:50%;bottom:90px;transform:translateX(-50%);z-index:10;background:#111c;padding:9px 13px;border-radius:10px;white-space:nowrap}
#move{position:absolute;bottom:15px;left:15px;z-index:20;display:grid;grid-template-columns:55px 55px 55px;gap:5px}.move{width:55px;height:55px;background:#111b;font-size:22px;touch-action:none}.up{grid-column:2}.left{grid-column:1;grid-row:2}.down{grid-column:2;grid-row:2}.right{grid-column:3;grid-row:2}
#actions{position:absolute;right:15px;bottom:15px;z-index:20;display:flex;gap:7px}.action{background:#111c}
#toast{display:none;position:absolute;left:50%;top:75%;transform:translate(-50%,-50%);z-index:40;background:#000d;padding:12px 18px;border-radius:12px}
#rainbow{display:none;position:absolute;z-index:9;left:50%;top:70px;transform:translateX(-50%);font-size:130px;filter:drop-shadow(0 5px 5px #0005)}
#shake{position:absolute;inset:0;pointer-events:none;z-index:30;display:none;border:6px solid #facc15}
.night #world{filter:brightness(.38) saturate(.8)}.rain:after{content:"";position:absolute;inset:0;z-index:25;pointer-events:none;background:repeating-linear-gradient(115deg,transparent 0 16px,#9bd6e866 17px 19px);animation:rain .3s linear infinite}@keyframes rain{to{background-position:30px 50px}}
</style>
</head>
<body>
<div id="menu"><div class="card"><h1>👑 ADMIN ABUSE CITY</h1><p>Открытый мир • машины • события • админ-панель</p><button class="main" onclick="play()">▶ ИГРАТЬ</button><button onclick="rules()">📜 ПРАВИЛА</button><button onclick="settings()">⚙ НАСТРОЙКИ</button></div></div>
<div id="game">
<div id="view"><div id="world"></div></div>
<div id="hud"><div class="box">❤️ <b id="hp">100</b> &nbsp; 💰 <b id="money">500</b></div><button onclick="toggleAdmin()">👑 ADMIN</button></div>
<div id="players" class="box">👤 Игрок: Ты<br>🤖 NPC: 8</div>
<div id="admin"><b>👑 ADMIN PANEL</b><div class="adminGrid">
<button onclick="eventDo('meteor')">☄️ Метеориты</button><button onclick="eventDo('rainbow')">🌈 Радуга</button>
<button onclick="eventDo('night')">🌙 Ночь</button><button onclick="eventDo('day')">☀️ День</button>
<button onclick="eventDo('quake')">🌍 Землетрясение</button><button onclick="eventDo('rain')">🌧️ Дождь</button>
<button onclick="eventDo('snow')">❄️ Снег</button><button onclick="eventDo('storm')">🌪️ Шторм</button>
<button onclick="admin('speed')">⚡ Скорость</button><button onclick="admin('jump')">🦘 Прыжок</button>
<button onclick="admin('launch')">🚀 Запуск</button><button onclick="admin('gravity')">🌙 Гравитация</button>
<button onclick="admin('heal')">❤️ Heal</button><button onclick="respawn()">🔄 Спавн</button>
</div></div>
<div id="rainbow">🌈</div><div id="shake"></div><div id="toast"></div>
<div id="hint">WASD / стрелки — ходьба • E — машина • 👊 — действие</div>
<div id="move"><button class="move up" data-k="w">▲</button><button class="move left" data-k="a">◀</button><button class="move down" data-k="s">▼</button><button class="move right" data-k="d">▶</button></div>
<div id="actions"><button class="action" onclick="car()">🚗 E</button><button class="action" onclick="hit()">👊</button><button class="action" onclick="bankWork()">🏦 Банк</button></div>
</div>
<script>
const W=3000,H=2000,world=document.getElementById('world');let started=false,keys={},speed=4,jump=0,gravity=1,inCar=null,money=500,hp=100,night=false;
let p={x:1480,y:980},cars=[{x:1180,y:900,id:1},{x:1600,y:900,id:2},{x:2050,y:1080,id:3},{x:1050,y:1400,id:4},{x:1800,y:1450,id:5},{x:2400,y:1420,id:6}];
function el(cls,x,y,parent=world){let e=document.createElement('div');e.className=cls;e.style.left=x+'px';e.style.top=y+'px';parent.appendChild(e);return e}
let npcData=[];
function spawnNPC(n){
 let e=el('npc',n.x,n.y); e.innerHTML='<span class="tag">NPC</span>🙂';
 e.dataset.hp=n.hp; e.dataset.alive='1'; e.style.transition='left .12s,top .12s,opacity .2s';
 n.el=e; n.alive=true;
}
function makeMap(){
 for(let i=0;i<8;i++){let r=el('road hr',0,120+i*230);r.style.top=120+i*230+'px'}
 for(let i=0;i<7;i++){let r=el('road vr',170+i*430,0);r.style.left=170+i*430+'px'}
 for(let i=0;i<30;i++){let b=el('build',30+(i%6)*500,20+Math.floor(i/6)*380);b.style.width=220+(i%3)*40+'px';b.style.height=145+(i%2)*50+'px';for(let q=0;q<4;q++){let w=el('window',20+(q%2)*80,20+Math.floor(q/2)*55,b)}}
 for(let i=0;i<8;i++){let pa=el('park',90+(i%4)*700,190+Math.floor(i/4)*850);pa.style.width='260px';pa.style.height='170px';for(let t=0;t<4;t++){let tr=el('tree',20+t*55,35+(t%2)*65,pa)}}
 let bank=el('bank',1370,760);bank.style.width='260px';bank.style.height='120px';bank.textContent='БАНК';bank.id='bank';
 cars.forEach(c=>{let e=el('car',c.x,c.y);e.dataset.id=c.id;e.innerHTML='<div class="glass"></div>'});
 for(let i=0;i<8;i++){
   let n={x:1250+(i%4)*220,y:1040+Math.floor(i/4)*100,hp:100,alive:true,el:null};
   npcData.push(n); spawnNPC(n);
 }
}
function play(){started=true;menu.style.display='none';game.style.display='block';toast('📍 Ты появился на спавне');}
function rules(){alert('Правила:\\n• Игровые действия и админские события работают только внутри игры.\\n• E — сесть/выйти из машины.\\n• 👊 — атака без графики.\\n• 🏦 — деньги можно заработать только работой в банке.\\n• Админ-панель предназначена для игровых событий.')}
function settings(){alert('Настройки:\\n🎮 Управление: WASD/стрелки\\n📱 На телефоне: экранные кнопки\\n🔊 Звук: отключён в этой версии')}
function toggleAdmin(){admin.style.display=admin.style.display==='block'?'none':'block'}
function toast(s){toastEl=document.getElementById('toast');toastEl.textContent=s;toastEl.style.display='block';clearTimeout(window.tt);window.tt=setTimeout(()=>toastEl.style.display='none',1400)}
function admin(a){if(a==='speed'){speed=speed===4?9:4;toast('⚡ Скорость '+speed)}if(a==='jump'){jump=jump?0:1;toast('🦘 Суперпрыжок '+(jump?'ON':'OFF'))}if(a==='launch'){p.y=Math.max(50,p.y-300);toast('🚀 Запуск')}if(a==='gravity'){gravity=gravity===1?.45:1;toast('🌙 Гравитация изменена')}if(a==='heal'){hp=100;toast('❤️ Здоровье восстановлено')}}
function eventDo(a){
 if(a==='night'){night=true;game.classList.add('night');toast('🌙 Наступила ночь')}
 if(a==='day'){night=false;game.classList.remove('night');toast('☀️ Наступил день')}
 if(a==='rainbow'){rainbow.style.display='block';setTimeout(()=>rainbow.style.display='none',6000);toast('🌈 Радуга появилась')}
 if(a==='rain'){game.classList.add('rain');setTimeout(()=>game.classList.remove('rain'),7000);toast('🌧️ Начался дождь')}
 if(a==='snow'){toast('❄️ Начался снег!');snow()}
 if(a==='storm'){game.classList.add('rain');toast('🌪️ Начался шторм!');setTimeout(()=>game.classList.remove('rain'),7000)}
 if(a==='quake'){let s=document.getElementById('shake');s.style.display='block';let n=0;let q=setInterval(()=>{world.style.marginLeft=(Math.random()*16-8)+'px';world.style.marginTop=(Math.random()*16-8)+'px';if(++n>28){clearInterval(q);world.style.marginLeft='0';world.style.marginTop='0';s.style.display='none'}},70);toast('🌍 ЗЕМЛЕТРЯСЕНИЕ!')}
 if(a==='meteor'){for(let i=0;i<14;i++){let m=el('meteor',p.x+(Math.random()-.5)*700,p.y-600-Math.random()*500);m.textContent='☄️';m.style.position='absolute';m.style.fontSize='34px';m.animate([{transform:'translateY(0)'},{transform:'translateY(800px)'}],{duration:700+Math.random()*600}).onfinish=()=>m.remove()}toast('☄️ Метеоритный дождь!')}
}
function snow(){for(let i=0;i<30;i++){let s=el('snow',Math.random()*W,Math.random()*H);s.textContent='❄️';s.style.position='absolute';s.style.fontSize='18px';s.animate([{transform:'translateY(-100px)'},{transform:'translateY(300px)'}],{duration:2000+Math.random()*3000,iterations:2}).onfinish=()=>s.remove()}}
let engineOn=false, audioCtx=null, engineOsc=null, engineGain=null;
function startEngineSound(){
 if(engineOn)return;
 try{
  audioCtx=audioCtx||new (window.AudioContext||window.webkitAudioContext)();
  engineOsc=audioCtx.createOscillator(); engineGain=audioCtx.createGain();
  engineOsc.type='sawtooth'; engineOsc.frequency.value=85; engineGain.gain.value=.025;
  engineOsc.connect(engineGain);engineGain.connect(audioCtx.destination);engineOsc.start();engineOn=true;
 }catch(e){}
}
function stopEngineSound(){
 if(!engineOn)return;
 try{engineOsc.stop();engineOsc.disconnect();engineGain.disconnect()}catch(e){}
 engineOn=false;
}
function car(){
 if(inCar){let c=cars.find(c=>c.id===inCar);p.x=c.x+100;p.y=c.y;inCar=null;stopEngineSound();toast('🚶 Вышел из машины');return}
 let near=cars.map(c=>({c,d:Math.hypot(c.x-p.x,c.y-p.y)})).sort((a,b)=>a.d-b.d)[0];
 if(near&&near.d<120){inCar=near.c.id;startEngineSound();toast('🚗 Ты сел в машину')}else toast('Подойди ближе к машине')}
function hit(){
 if(!started)return;
 if(inCar){toast('🚗 Выйди из машины');return}
 let living=npcData.filter(n=>n.alive);
 if(!living.length){toast('Все NPC временно недоступны');return}
 let target=living.map(n=>({n,d:Math.hypot(n.x-p.x,n.y-p.y)})).sort((a,b)=>a.d-b.d)[0];
 if(target.d>95){toast('Подойди ближе к NPC');return}
 let n=target.n;
 n.hp-=35;
 let dx=n.x-p.x,dy=n.y-p.y,len=Math.hypot(dx,dy)||1;
 n.x+=dx/len*75;n.y+=dy/len*75;
 n.x=Math.max(20,Math.min(W-60,n.x));n.y=Math.max(20,Math.min(H-70,n.y));
 n.el.style.left=n.x+'px';n.el.style.top=n.y+'px';
 n.el.style.transform='translate('+(dx/len*18)+'px,'+(dy/len*18)+'px)';
 setTimeout(()=>{if(n.el)n.el.style.transform='translate(0,0)'},140);
 if(n.hp<=0){
   n.alive=false;n.el.style.opacity='0';
   toast('👊 NPC получил урон и выбыл');
   setTimeout(()=>{
     if(n.el)n.el.remove();
     n.hp=100;n.x=1250+(Math.random()*650);n.y=1000+(Math.random()*300);
     n.el=null;n.alive=true;spawnNPC(n);
     toast('🤖 NPC снова появился');
   },4000);
 }else{
   toast('👊 Удар! HP NPC: '+n.hp);
 }
}
function rob(){toast('🏦 Деньги можно заработать только работой в банке')}
function bankWork(){
 let bank={x:1370+130,y:760+60};
 let d=Math.hypot(p.x-bank.x,p.y-bank.y);
 if(d>210){toast('🏦 Подойди к банку');return}
 if(inCar){toast('🚗 Выйди из машины');return}
 money+=50;
 document.getElementById('money').textContent=money;
 toast('🏦 Работа в банке: +50');
}
function respawn(){p.x=1480;p.y=980;inCar=null;hp=100;toast('📍 Респавн')}
addEventListener('keydown',e=>{let k=e.key.toLowerCase();if(k==='e')car();keys[k]=true});addEventListener('keyup',e=>keys[e.key.toLowerCase()]=false);
document.querySelectorAll('.move').forEach(b=>{let k=b.dataset.k;b.addEventListener('pointerdown',e=>{e.preventDefault();keys[k]=true});['pointerup','pointercancel','pointerleave'].forEach(x=>b.addEventListener(x,()=>keys[k]=false))});
function loop(){if(started){let dx=(keys.d||keys.arrowright?1:0)-(keys.a||keys.arrowleft?1:0),dy=(keys.s||keys.arrowdown?1:0)-(keys.w||keys.arrowup?1:0);if(dx||dy){let l=Math.hypot(dx,dy);dx/=l;dy/=l;let s=inCar?speed+3:speed;p.x+=dx*s;p.y+=dy*s}p.x=Math.max(20,Math.min(W-50,p.x));p.y=Math.max(20,Math.min(H-60,p.y));if(inCar){
 let c=cars.find(c=>c.id===inCar);c.x=p.x;c.y=p.y;
 let moving=!!(dx||dy);
 let ce=document.querySelector('.car[data-id="'+inCar+'"]');
 if(ce)ce.classList.toggle('wheelspin',moving);
 if(engineOn&&engineOsc)engineOsc.frequency.value=moving?125:75;
}render()}requestAnimationFrame(loop)}
function render(){document.querySelectorAll('.car').forEach(e=>{let c=cars.find(c=>c.id==e.dataset.id);e.style.left=c.x+'px';e.style.top=c.y+'px';e.classList.toggle('occupied',inCar==c.id)});let old=document.querySelector('.me');if(old)old.remove();let me=el('player',p.x,p.y);me.classList.add('me');me.innerHTML='<span class="tag">Ты</span>😎';let cx=Math.max(0,Math.min(W-innerWidth,p.x-innerWidth/2)),cy=Math.max(0,Math.min(H-innerHeight,p.y-innerHeight/2));world.style.transform=`translate(${-cx}px,${-cy}px)`;document.getElementById('money').textContent=money;document.getElementById('hp').textContent=hp;document.getElementById('players').innerHTML='👤 Игрок: Ты<br>🤖 NPC: '+npcData.filter(n=>n.alive).length}
makeMap();loop();
</script>
</body></html>
