<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Rebelde Live — Centro de Control</title>
<style>
:root{
  --black:#080808; --ink:#111317; --panel:#17191e; --panel2:#20232a;
  --cyan:#25F4EE; --pink:#FE2C55; --white:#f7f7f7; --muted:#9ca3af;
  --green:#35d07f; --yellow:#ffd166; --line:#2b2f38;
}
*{box-sizing:border-box} body{margin:0;background:linear-gradient(135deg,#080808,#111318 55%,#160b10);color:var(--white);font-family:Inter,Segoe UI,Arial,sans-serif}
button,input,select,textarea{font:inherit} button{cursor:pointer}
.app{display:flex;min-height:100vh}.side{width:250px;background:#090a0c;border-right:1px solid var(--line);padding:22px 14px;position:sticky;top:0;height:100vh}
.brand{padding:8px 10px 22px}.brand h1{margin:0;font-size:21px}.brand span{display:inline-block;margin-top:7px;font-size:11px;color:var(--cyan);letter-spacing:1.5px;font-weight:800}
.nav button{width:100%;border:0;background:transparent;color:#cbd0d8;text-align:left;padding:12px 13px;border-radius:10px;margin:3px 0}
.nav button:hover,.nav button.active{background:linear-gradient(90deg,#211016,#101b1c);color:white;border-left:3px solid var(--pink)}
.main{flex:1;padding:26px;max-width:1600px;margin:auto;width:100%}.top{display:flex;justify-content:space-between;align-items:center;gap:15px;margin-bottom:22px}
.top h2{margin:0;font-size:28px}.top p{margin:5px 0 0;color:var(--muted)}
.actions{display:flex;gap:8px;flex-wrap:wrap}.btn{border:1px solid var(--line);background:var(--panel2);color:white;padding:10px 14px;border-radius:9px}.btn.primary{background:linear-gradient(90deg,var(--pink),#d91d46);border:0}.btn.cyan{background:linear-gradient(90deg,#0aa9aa,var(--cyan));color:#071010;border:0;font-weight:800}
.kpis{display:grid;grid-template-columns:repeat(5,1fr);gap:12px;margin-bottom:18px}.kpi{background:rgba(23,25,30,.92);border:1px solid var(--line);border-radius:14px;padding:16px;position:relative;overflow:hidden}.kpi:after{content:"";position:absolute;right:-20px;top:-20px;width:70px;height:70px;border-radius:50%;background:var(--pink);opacity:.13}.kpi:nth-child(2):after,.kpi:nth-child(5):after{background:var(--cyan)}.kpi small{color:var(--muted)}.kpi b{display:block;font-size:25px;margin-top:7px}
.progress{height:9px;background:#292c33;border-radius:20px;overflow:hidden;margin-top:10px}.bar{height:100%;background:linear-gradient(90deg,var(--cyan),var(--pink));width:0}
.grid{display:grid;grid-template-columns:1.3fr .7fr;gap:15px}.card{background:rgba(23,25,30,.95);border:1px solid var(--line);border-radius:14px;padding:18px}.card h3{margin:0 0 13px;font-size:16px}.tablewrap{overflow:auto}table{width:100%;border-collapse:collapse;min-width:850px}th,td{padding:10px 9px;border-bottom:1px solid var(--line);font-size:12px;text-align:left}th{color:var(--muted);font-weight:700}tr:hover td{background:#1b1e24}
.badge{padding:4px 8px;border-radius:20px;font-size:10px;font-weight:800;display:inline-block}.green{background:#123d2a;color:var(--green)}.red{background:#431722;color:#ff8094}.yellow{background:#493b14;color:var(--yellow)}.blue{background:#103b3c;color:var(--cyan)}
.filters{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:13px}.filters input,.filters select,.form input,.form select,.form textarea{background:#0e1014;border:1px solid var(--line);color:white;padding:9px;border-radius:8px;outline:none}.filters input:focus,.form input:focus{border-color:var(--cyan)}
.metric{display:flex;justify-content:space-between;padding:11px 0;border-bottom:1px solid var(--line)}.metric:last-child{border:0}.metric b{font-size:14px}.muted{color:var(--muted)}
.page{display:none}.page.active{display:block}
.formgrid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}.form label{font-size:11px;color:var(--muted);display:block;margin-bottom:5px}.form .full{grid-column:1/-1}
.modal{position:fixed;inset:0;background:#000b;display:none;align-items:center;justify-content:center;padding:20px;z-index:5}.modal.open{display:flex}.modalbox{background:#17191e;border:1px solid #343943;border-radius:15px;width:min(700px,100%);padding:20px}.modalhead{display:flex;justify-content:space-between;align-items:center;margin-bottom:15px}.x{background:none;border:0;color:white;font-size:22px}
.notice{border-left:3px solid var(--cyan);padding:10px 12px;background:#102123;margin:12px 0;border-radius:7px;color:#dceff0;font-size:12px}
.empty{text-align:center;color:var(--muted);padding:30px}
footer{color:#626873;font-size:11px;margin-top:20px}
@media(max-width:1050px){.kpis{grid-template-columns:repeat(2,1fr)}.grid{grid-template-columns:1fr}.side{width:210px}}
@media(max-width:700px){.side{display:none}.main{padding:15px}.kpis{grid-template-columns:1fr}.formgrid{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="app">
<aside class="side">
 <div class="brand"><h1>REBELDE LIVE</h1><span>CENTRO DE CONTROL</span></div>
 <div class="nav">
  <button class="active" data-page="dashboard">◈ Dashboard</button>
  <button data-page="managers">◉ Managers</button>
  <button data-page="reclutadores">◎ Reclutadores</button>
  <button data-page="afiliados">◇ Afiliados / Embajadores</button>
  <button data-page="microtareas">◆ Microtareas</button>
  <button data-page="creadores">● Creadores</button>
  <button data-page="campanas">★ Campañas</button>
  <button data-page="seguimiento">✓ Seguimiento 3 días</button>
  <button data-page="config">⚙ Configuración</button>
 </div>
</aside>

<main class="main">
 <div class="top">
  <div><h2 id="title">Dashboard general</h2><p id="subtitle">Control central de adquisición, activación, graduación y retención.</p></div>
  <div class="actions"><button class="btn" onclick="exportJSON()">Exportar JSON</button><button class="btn primary" onclick="openAdd()">+ Nuevo registro</button></div>
 </div>

 <section id="dashboard" class="page active">
  <div class="kpis">
   <div class="kpi"><small>Diamantes acumulados</small><b id="kDiamonds">0</b><div class="progress"><div class="bar" id="diamondBar"></div></div></div>
   <div class="kpi"><small>Meta 60 días</small><b id="kGoal">10.000.000</b><span class="muted">diamantes</span></div>
   <div class="kpi"><small>Creadores</small><b id="kCreators">0</b><span class="muted">registrados</span></div>
   <div class="kpi"><small>40K alcanzados</small><b id="k40">0</b><span class="muted">creadores</span></div>
   <div class="kpi"><small>80K / graduación</small><b id="k80">0</b><span class="muted">creadores</span></div>
  </div>
  <div class="grid">
   <div class="card"><h3>Embudo operativo</h3><div id="funnel"></div></div>
   <div class="card"><h3>Alertas de dueña</h3><div id="alerts"></div></div>
  </div>
  <div class="card" style="margin-top:15px"><h3>Actividad reciente</h3><div class="tablewrap"><table><thead><tr><th>Fecha</th><th>Tipo</th><th>Persona</th><th>Estado</th><th>Nota</th></tr></thead><tbody id="recent"></tbody></table></div></div>
 </section>

 <section id="managers" class="page"><div class="card"><h3>Managers — producción y acompañamiento</h3><div class="filters"><input id="managerSearch" placeholder="Buscar manager..." oninput="renderManagers()"><select id="managerStatus" onchange="renderManagers()"><option value="">Todos</option><option>Activo</option><option>En observación</option><option>Inactivo</option></select></div><div class="tablewrap"><table><thead><tr><th>Manager</th><th>Creadores</th><th>40K</th><th>80K</th><th>22D/90H</th><th>Diamantes</th><th>Estado</th><th>Acción</th></tr></thead><tbody id="managerRows"></tbody></table></div></div></section>

 <section id="reclutadores" class="page"><div class="card"><h3>Reclutadores — meta de 50 aprobados</h3><div class="filters"><input id="recSearch" placeholder="Buscar reclutador..." oninput="renderRecruiters()"></div><div class="tablewrap"><table><thead><tr><th>Reclutador</th><th>Contactos</th><th>Interesados</th><th>Aprobados</th><th>Ingresados</th><th>Meta</th><th>Estado</th><th>Acción</th></tr></thead><tbody id="recRows"></tbody></table></div></div></section>

 <section id="afiliados" class="page"><div class="card"><h3>Afiliados comerciales / Embajadores</h3><div class="filters"><input id="affSearch" placeholder="Buscar..." oninput="renderAffiliates()"></div><div class="tablewrap"><table><thead><tr><th>Nombre</th><th>Plataforma</th><th>Alcance</th><th>UGC</th><th>Referidos</th><th>Campañas</th><th>Estado</th><th>Acción</th></tr></thead><tbody id="affRows"></tbody></table></div></div></section>

 <section id="microtareas" class="page"><div class="card"><h3>Personas por microtareas</h3><p class="muted">Controla tareas puntuales de publicación, búsqueda, contacto y apoyo operativo.</p><div class="tablewrap"><table><thead><tr><th>Persona</th><th>Tarea</th><th>Fecha</th><th>Entregable</th><th>Estado</th><th>Pago</th><th>Acción</th></tr></thead><tbody id="microRows"></tbody></table></div></div></section>

 <section id="creadores" class="page"><div class="card"><h3>Creadores — 15 días → 40K → 80K</h3><div class="filters"><input id="creatorSearch" placeholder="Buscar creador..." oninput="renderCreators()"><select id="creatorStage" onchange="renderCreators()"><option value="">Todos</option><option>Nuevo</option><option>15 días</option><option>40K</option><option>80K</option><option>Riesgo</option></select></div><div class="tablewrap"><table><thead><tr><th>Creador</th><th>Manager</th><th>Días</th><th>Horas</th><th>Diamantes</th><th>Etapa</th><th>Último contacto</th><th>Acción</th></tr></thead><tbody id="creatorRows"></tbody></table></div></div></section>

 <section id="campanas" class="page"><div class="card"><h3>Campañas activas</h3><div id="campaignCards"></div></div></section>

 <section id="seguimiento" class="page"><div class="card"><h3>Reunión de seguimiento cada 3 días</h3><div class="notice">Usa esta sección para registrar compromisos. La reunión debe terminar con acciones concretas y responsables.</div><div class="tablewrap"><table><thead><tr><th>Fecha</th><th>Responsable</th><th>Tipo</th><th>Hallazgo</th><th>Acción próxima</th><th>Vencimiento</th><th>Estado</th><th>Acción</th></tr></thead><tbody id="followRows"></tbody></table></div></div></section>

 <section id="config" class="page"><div class="card"><h3>Configuración del objetivo</h3><div class="form" style="max-width:500px"><label>Meta de diamantes</label><input id="goalInput" type="number" value="10000000"><br><br><button class="btn cyan" onclick="saveGoal()">Guardar meta</button></div><div class="notice">Los datos de este tablero se guardan localmente en este navegador mediante localStorage. Puedes exportarlos a JSON como respaldo.</div></div></section>

 <footer>Rebelde Live — herramienta interna de seguimiento. No contiene logotipos de terceros.</footer>
</main>
</div>

<div class="modal" id="modal"><div class="modalbox"><div class="modalhead"><h3 id="modalTitle">Nuevo registro</h3><button class="x" onclick="closeModal()">×</button></div><div class="form"><div class="formgrid" id="formFields"></div><br><button class="btn primary" onclick="saveRecord()">Guardar</button></div></div></div>

<script>
const KEY='rebelde_control_v1';
let state=JSON.parse(localStorage.getItem(KEY)||'null')||{
 goal:10000000, records:[], followups:[], activities:[]
};
const pages={
 dashboard:['Dashboard general','Control central de adquisición, activación, graduación y retención.'],
 managers:['Managers','Producción, acompañamiento, 40K, 80K y conectividad.'],
 reclutadores:['Reclutadores','Meta de 50 creadores aprobados.'],
 afiliados:['Afiliados / Embajadores','UGC, campañas, alcance y referidos.'],
 microtareas:['Microtareas','Tareas puntuales y pagos por entrega.'],
 creadores:['Creadores','Seguimiento de los primeros 15 días, 40K y 80K.'],
 campanas:['Campañas','Campañas de adquisición y activación.'],
 seguimiento:['Seguimiento 3 días','Reuniones, hallazgos y acciones.'],
 config:['Configuración','Objetivo general y respaldo de datos.']
};
function persist(){localStorage.setItem(KEY,JSON.stringify(state))}
function esc(s){return String(s??'').replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]))}
function money(n){return '$'+Number(n||0).toLocaleString('es-CO')+' COP'}
function nav(id){document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));document.getElementById(id).classList.add('active');document.querySelectorAll('.nav button').forEach(x=>x.classList.toggle('active',x.dataset.page===id));document.getElementById('title').textContent=pages[id][0];document.getElementById('subtitle').textContent=pages[id][1];renderAll()}
document.querySelectorAll('.nav button').forEach(b=>b.onclick=()=>nav(b.dataset.page));

function addSampleData(){
 if(state.records.length)return;
 state.records=[
 {id:1,type:'manager',name:'Manager 01',creators:8,d40:3,d80:1,d22:4,diamonds:210000,status:'Activo'},
 {id:2,type:'recruiter',name:'Reclutador 01',contacts:120,interested:31,approved:18,joined:15,goal:50,status:'Activo'},
 {id:3,type:'affiliate',name:'Embajador 01',platform:'Instagram',reach:25000,ugc:3,referrals:7,campaigns:2,status:'Activo'},
 {id:4,type:'micro',name:'Persona micro 01',task:'Buscar 30 perfiles',date:'2026-09-05',deliverable:'Excel',status:'Pendiente',payment:30000},
 {id:5,type:'creator',name:'Creador 01',manager:'Manager 01',days:9,hours:31,diamonds:27000,stage:'15 días',last:'2026-09-05'},
 {id:6,type:'creator',name:'Creador 02',manager:'Manager 01',days:22,hours:90,diamonds:80000,stage:'80K',last:'2026-09-04'},
 ];
 state.activities=[{date:'2026-09-05',type:'Sistema',name:'Inicio',status:'Activo',note:'Panel configurado'}];
 persist();
}
addSampleData();

function typeLabel(t){return {manager:'Manager',recruiter:'Reclutador',affiliate:'Afiliado',micro:'Microtarea',creator:'Creador'}[t]||t}
function records(t){return state.records.filter(r=>r.type===t)}

function renderDashboard(){
 let cs=records('creator'), diamonds=cs.reduce((a,r)=>a+Number(r.diamonds||0),0);
 document.getElementById('kDiamonds').textContent=diamonds.toLocaleString('es-CO');
 document.getElementById('kGoal').textContent=Number(state.goal).toLocaleString('es-CO');
 document.getElementById('kCreators').textContent=cs.length;
 document.getElementById('k40').textContent=cs.filter(r=>r.diamonds>=40000).length;
 document.getElementById('k80').textContent=cs.filter(r=>r.diamonds>=80000).length;
 document.getElementById('diamondBar').style.width=Math.min(100,diamonds/state.goal*100)+'%';
 const m=records('manager'), rc=records('recruiter'), af=records('affiliate'), mi=records('micro');
 document.getElementById('funnel').innerHTML=[
  ['Managers',m.length],['Reclutadores',rc.length],['Afiliados / embajadores',af.length],['Microtareas',mi.length],['Creadores',cs.length],['Creadores 40K+',cs.filter(x=>x.diamonds>=40000).length],['Graduados 80K+',cs.filter(x=>x.diamonds>=80000).length]
 ].map(x=>`<div class="metric"><span>${x[0]}</span><b>${x[1]}</b></div>`).join('');
 let alerts=[];
 cs.filter(x=>x.stage==='Riesgo'||(x.days<15&&x.days>=7&&x.diamonds<10000)).forEach(x=>alerts.push(`⚠️ <b>${esc(x.name)}</b> requiere seguimiento`));
 m.filter(x=>(x.d22||0)<x.creators).forEach(x=>alerts.push(`⏱️ <b>${esc(x.name)}</b>: revisar conectividad`));
 rc.filter(x=>(x.approved||0)<10).forEach(x=>alerts.push(`🎯 <b>${esc(x.name)}</b>: acelerar reclutamiento`));
 document.getElementById('alerts').innerHTML=alerts.length?alerts.slice(0,8).map(x=>`<div class="metric"><span>${x}</span></div>`).join(''):'<div class="empty">Sin alertas críticas registradas.</div>';
 document.getElementById('recent').innerHTML=(state.activities||[]).slice(-10).reverse().map(a=>`<tr><td>${esc(a.date)}</td><td>${esc(a.type)}</td><td>${esc(a.name)}</td><td><span class="badge blue">${esc(a.status)}</span></td><td>${esc(a.note)}</td></tr>`).join('')||'<tr><td colspan="5" class="empty">Sin actividad.</td></tr>';
}

function renderManagers(){
 let q=(document.getElementById('managerSearch')?.value||'').toLowerCase(), s=document.getElementById('managerStatus')?.value||'';
 document.getElementById('managerRows').innerHTML=records('manager').filter(r=>(r.name||'').toLowerCase().includes(q)&&(!s||r.status===s)).map(r=>`<tr><td><b>${esc(r.name)}</b></td><td>${r.creators||0}</td><td>${r.d40||0}</td><td>${r.d80||0}</td><td>${r.d22||0}</td><td>${Number(r.diamonds||0).toLocaleString('es-CO')}</td><td><span class="badge ${r.status==='Activo'?'green':'yellow'}">${esc(r.status)}</span></td><td><button class="btn" onclick="editRecord(${r.id})">Editar</button></td></tr>`).join('')||'<tr><td colspan="8" class="empty">No hay managers.</td></tr>';
}
function renderRecruiters(){
 let q=(document.getElementById('recSearch')?.value||'').toLowerCase();
 document.getElementById('recRows').innerHTML=records('recruiter').filter(r=>(r.name||'').toLowerCase().includes(q)).map(r=>`<tr><td><b>${esc(r.name)}</b></td><td>${r.contacts||0}</td><td>${r.interested||0}</td><td>${r.approved||0}</td><td>${r.joined||0}</td><td>${r.goal||50}</td><td><span class="badge ${(r.approved||0)>=50?'green':'blue'}">${(r.approved||0)>=50?'Meta cumplida':'En proceso'}</span></td><td><button class="btn" onclick="editRecord(${r.id})">Editar</button></td></tr>`).join('')||'<tr><td colspan="8" class="empty">No hay reclutadores.</td></tr>';
}
function renderAffiliates(){
 let q=(document.getElementById('affSearch')?.value||'').toLowerCase();
 document.getElementById('affRows').innerHTML=records('affiliate').filter(r=>(r.name||'').toLowerCase().includes(q)).map(r=>`<tr><td><b>${esc(r.name)}</b></td><td>${esc(r.platform)}</td><td>${Number(r.reach||0).toLocaleString('es-CO')}</td><td>${r.ugc||0}</td><td>${r.referrals||0}</td><td>${r.campaigns||0}</td><td><span class="badge green">${esc(r.status)}</span></td><td><button class="btn" onclick="editRecord(${r.id})">Editar</button></td></tr>`).join('')||'<tr><td colspan="8" class="empty">No hay afiliados.</td></tr>';
}
function renderCreators(){
 let q=(document.getElementById('creatorSearch')?.value||'').toLowerCase(), s=document.getElementById('creatorStage')?.value||'';
 document.getElementById('creatorRows').innerHTML=records('creator').filter(r=>(r.name||'').toLowerCase().includes(q)&&(!s||r.stage===s)).map(r=>{
 let pct=Math.min(100,(r.diamonds||0)/80000*100), cls=r.stage==='80K'?'green':r.stage==='Riesgo'?'red':'blue';
 return `<tr><td><b>${esc(r.name)}</b></td><td>${esc(r.manager)}</td><td>${r.days||0}</td><td>${r.hours||0}</td><td>${Number(r.diamonds||0).toLocaleString('es-CO')}<div class="progress"><div class="bar" style="width:${pct}%"></div></div></td><td><span class="badge ${cls}">${esc(r.stage)}</span></td><td>${esc(r.last)}</td><td><button class="btn" onclick="editRecord(${r.id})">Editar</button></td></tr>`
 }).join('')||'<tr><td colspan="8" class="empty">No hay creadores.</td></tr>';
}
function renderMicro(){
 document.getElementById('microRows').innerHTML=records('micro').map(r=>`<tr><td>${esc(r.name)}</td><td>${esc(r.task)}</td><td>${esc(r.date)}</td><td>${esc(r.deliverable)}</td><td><span class="badge ${r.status==='Completada'?'green':'yellow'}">${esc(r.status)}</span></td><td>${money(r.payment)}</td><td><button class="btn" onclick="editRecord(${r.id})">Editar</button></td></tr>`).join('')||'<tr><td colspan="7" class="empty">No hay microtareas.</td></tr>';
}
function renderFollow(){
 document.getElementById('followRows').innerHTML=(state.followups||[]).map(r=>`<tr><td>${esc(r.date)}</td><td>${esc(r.owner)}</td><td>${esc(r.type)}</td><td>${esc(r.finding)}</td><td>${esc(r.action)}</td><td>${esc(r.due)}</td><td><span class="badge blue">${esc(r.status)}</span></td><td><button class="btn" onclick="deleteFollow(${r.id})">Eliminar</button></td></tr>`).join('')||'<tr><td colspan="8" class="empty">No hay seguimientos. Usa Nuevo registro.</td></tr>';
}
function renderCampaigns(){
 const c=[['🎤 Voces en Vivo','Cantantes','8 días · participación gratuita · captación + permanencia'],['💃 Dance Live','Bailarines','8 días · participación gratuita · captación + permanencia']];
 document.getElementById('campaignCards').innerHTML=c.map(x=>`<div class="card" style="margin:10px 0;background:#111318"><h3>${x[0]}</h3><b>${x[1]}</b><p class="muted">${x[2]}</p><span class="badge green">Activa</span></div>`).join('');
}
function renderAll(){renderDashboard();renderManagers();renderRecruiters();renderAffiliates();renderMicro();renderCreators();renderFollow();renderCampaigns()}

let editId=null;
function openAdd(){editId=null;document.getElementById('modalTitle').textContent='Nuevo registro';buildForm('manager');document.getElementById('modal').classList.add('open')}
function closeModal(){document.getElementById('modal').classList.remove('open')}
function buildForm(type,data={}){
 let fields='';
 const common={manager:[['name','Nombre'],['creators','Creadores asignados','number'],['d40','40K alcanzados','number'],['d80','80K graduados','number'],['d22','22D/90H','number'],['diamonds','Diamantes gestionados','number'],['status','Estado','select',['Activo','En observación','Inactivo']]],
 recruiter:[['name','Nombre'],['contacts','Contactos','number'],['interested','Interesados','number'],['approved','Aprobados','number'],['joined','Ingresados','number'],['goal','Meta','number'],['status','Estado','select',['Activo','En observación','Inactivo']]],
 affiliate:[['name','Nombre'],['platform','Plataforma'],['reach','Alcance','number'],['ugc','UGC entregados','number'],['referrals','Referidos','number'],['campaigns','Campañas','number'],['status','Estado','select',['Activo','En observación','Inactivo']]],
 micro:[['name','Nombre'],['task','Tarea'],['date','Fecha'],['deliverable','Entregable'],['status','Estado','select',['Pendiente','En proceso','Completada']],['payment','Pago COP','number']],
 creator:[['name','Creador'],['manager','Manager'],['days','Días LIVE','number'],['hours','Horas LIVE','number'],['diamonds','Diamantes','number'],['stage','Etapa','select',['Nuevo','15 días','40K','80K','Riesgo']],['last','Último contacto']]
 }[type]||[];
 fields+=`<div><label>Tipo de registro</label><select id="f_type" onchange="buildForm(this.value, currentFormData())">${Object.keys({manager:1,recruiter:1,affiliate:1,micro:1,creator:1}).map(x=>`<option ${x===type?'selected':''} value="${x}">${typeLabel(x)}</option>`).join('')}</select></div><div></div>`;
 fields+=common.map(f=>{let val=data[f[0]]??'';if(f[2]==='select')return `<div><label>${f[1]}</label><select id="f_${f[0]}">${f[3].map(o=>`<option ${o===val?'selected':''}>${o}</option>`).join('')}</select></div>`;return `<div><label>${f[1]}</label><input id="f_${f[0]}" type="${f[2]||'text'}" value="${esc(val)}"></div>`}).join('');
 document.getElementById('formFields').innerHTML=fields;
}
let formType='manager';
function currentFormData(){return {}}
function editRecord(id){let r=state.records.find(x=>x.id===id);if(!r)return;editId=id;formType=r.type;document.getElementById('modalTitle').textContent='Editar registro';buildForm(r.type,r);document.getElementById('modal').classList.add('open')}
function saveRecord(){
 let type=document.getElementById('f_type').value;
 const configs={manager:['name','creators','d40','d80','d22','diamonds','status'],recruiter:['name','contacts','interested','approved','joined','goal','status'],affiliate:['name','platform','reach','ugc','referrals','campaigns','status'],micro:['name','task','date','deliverable','status','payment'],creator:['name','manager','days','hours','diamonds','stage','last']};
 let r={id:editId||Date.now(),type};configs[type].forEach(k=>{let e=document.getElementById('f_'+k);r[k]=e?e.value:'';if(['creators','d40','d80','d22','diamonds','contacts','interested','approved','joined','goal','reach','ugc','referrals','campaigns','payment','days','hours'].includes(k))r[k]=Number(r[k]||0)});
 if(editId)state.records=state.records.map(x=>x.id===editId?r:x);else state.records.push(r);
 state.activities.push({date:new Date().toISOString().slice(0,10),type:typeLabel(type),name:r.name,status:'Actualizado',note:'Registro creado/actualizado por dueña'});
 persist();closeModal();renderAll();
}
function deleteFollow(id){state.followups=state.followups.filter(x=>x.id!==id);persist();renderFollow()}
function saveGoal(){state.goal=Number(document.getElementById('goalInput').value||10000000);persist();renderAll();alert('Meta guardada.')}
function exportJSON(){const blob=new Blob([JSON.stringify(state,null,2)],{type:'application/json'});const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='rebelde_live_control.json';a.click();URL.revokeObjectURL(a.href)}
document.getElementById('goalInput').value=state.goal;
renderAll();
</script>
</body>
</html>
