<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cuestionario interactivo - Introducción a la Termodinámica</title>
  <style>
    :root{
      --bg:#0f172a; --card:#111827; --soft:#1f2937; --text:#e5e7eb; --muted:#9ca3af;
      --accent:#38bdf8; --ok:#22c55e; --bad:#ef4444; --warn:#f59e0b; --white:#fff;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Arial,Helvetica,sans-serif;background:linear-gradient(135deg,#0f172a,#082f49,#111827);color:var(--text);min-height:100vh}
    header{padding:28px 18px;text-align:center;border-bottom:1px solid rgba(255,255,255,.08);background:rgba(2,6,23,.35);backdrop-filter: blur(10px)}
    h1{margin:0 0 8px;font-size:clamp(24px,4vw,42px)}
    .subtitle{color:var(--muted);max-width:900px;margin:0 auto;line-height:1.5}
    main{max-width:1100px;margin:0 auto;padding:22px 16px 60px}
    .panel{background:rgba(17,24,39,.86);border:1px solid rgba(255,255,255,.1);border-radius:22px;padding:20px;box-shadow:0 18px 50px rgba(0,0,0,.25);margin-bottom:18px}
    .controls{display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:center}
    button,select{border:0;border-radius:14px;padding:12px 16px;font-weight:700;cursor:pointer;font-size:15px}
    button{background:var(--accent);color:#002033;transition:.2s transform,.2s opacity}
    button:hover{transform:translateY(-1px);opacity:.94}
    button.secondary{background:var(--soft);color:var(--text);border:1px solid rgba(255,255,255,.12)}
    button.good{background:var(--ok);color:#06230f} button.danger{background:var(--bad);color:#fff}
    select{background:#0b1220;color:var(--text);border:1px solid rgba(255,255,255,.18)}
    .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}
    @media(max-width:850px){.grid{grid-template-columns:1fr}.stats{grid-template-columns:repeat(2,1fr)}}
    .topic{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);border-radius:18px;padding:16px;min-height:130px;position:relative;overflow:hidden}
    .topic h3{margin:0 0 8px;color:#bae6fd}.topic p{margin:0;color:#d1d5db;line-height:1.45}.tag{display:inline-block;margin-top:12px;font-size:12px;color:#93c5fd;border:1px solid rgba(147,197,253,.4);padding:5px 8px;border-radius:999px}
    .stats{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:18px}
    .stat{background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.1);border-radius:16px;padding:14px;text-align:center}.stat b{font-size:24px;display:block}.stat span{color:var(--muted);font-size:13px}
    .progress{height:12px;background:#020617;border-radius:99px;overflow:hidden;border:1px solid rgba(255,255,255,.09);margin:10px 0 4px}.bar{height:100%;width:0;background:linear-gradient(90deg,var(--accent),var(--ok));transition:width .35s}
    .question-card{padding:20px;background:rgba(15,23,42,.86);border:1px solid rgba(255,255,255,.12);border-radius:22px}.qtop{display:flex;gap:10px;justify-content:space-between;align-items:center;flex-wrap:wrap}.qbadge{color:#082f49;background:#bae6fd;border-radius:999px;padding:7px 10px;font-weight:700;font-size:13px}.question{font-size:22px;line-height:1.35;margin:18px 0}.options{display:grid;gap:10px}.option{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.13);padding:14px;border-radius:16px;text-align:left;color:var(--text);width:100%;transition:.15s}.option:hover{background:rgba(56,189,248,.16)}.option.correct{background:rgba(34,197,94,.20);border-color:var(--ok)}.option.wrong{background:rgba(239,68,68,.20);border-color:var(--bad)}
    .feedback{margin-top:14px;padding:14px;border-radius:16px;display:none;line-height:1.5}.feedback.ok{display:block;background:rgba(34,197,94,.16);border:1px solid rgba(34,197,94,.5)}.feedback.bad{display:block;background:rgba(239,68,68,.16);border:1px solid rgba(239,68,68,.5)}
    .flash{min-height:260px;display:flex;align-items:center;justify-content:center;text-align:center;perspective:1200px}.flash-inner{width:100%;min-height:240px;position:relative;transform-style:preserve-3d;transition:transform .6s}.flash.flip .flash-inner{transform:rotateY(180deg)}.side{position:absolute;inset:0;backface-visibility:hidden;background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.13);border-radius:20px;padding:22px;display:flex;align-items:center;justify-content:center;flex-direction:column}.back{transform:rotateY(180deg)}.side h2{color:#bae6fd}.side p{line-height:1.6;font-size:20px}.hidden{display:none}.formula{font-family:Georgia,serif;color:#fde68a;font-size:22px}.small{color:var(--muted);font-size:13px;line-height:1.5}.results{font-size:18px;line-height:1.6}.pill{display:inline-block;border-radius:999px;padding:4px 9px;background:rgba(255,255,255,.08);margin:3px;color:#e0f2fe}.footer-note{text-align:center;color:var(--muted);font-size:13px;margin-top:18px}
  </style>
</head>
<body>
<header>
  <h1>Termodinámica: teoría interactiva y cuestionario</h1>
  <p class="subtitle">Material dinámico basado en el PDF <b>“Introducción a la Termodinámica”</b>. Incluye resumen por temas, tarjetas de estudio y preguntas con alternativas, retroalimentación y puntaje.</p>
</header>
<main>
  <section class="panel">
    <div class="controls">
      <button onclick="showSection('teoria')">Ver teoría</button>
      <button onclick="showSection('flashcards')" class="secondary">Tarjetas</button>
      <button onclick="startQuiz()" class="good">Iniciar cuestionario</button>
      <select id="topicFilter" onchange="renderTheory()"><option value="todos">Todos los temas</option></select>
      <button onclick="shuffleQuiz()" class="secondary">Mezclar preguntas</button>
    </div>
  </section>

  <section id="teoria" class="panel">
    <h2>Resumen teórico por temas</h2>
    <div id="theoryGrid" class="grid"></div>
  </section>

  <section id="flashcards" class="panel hidden">
    <h2>Tarjetas de estudio</h2>
    <div class="flash" id="flash" onclick="flipCard()"><div class="flash-inner"><div class="side front"><h2 id="flashTitle"></h2><p id="flashPrompt"></p><span class="small">Haz clic para ver la respuesta</span></div><div class="side back"><h2>Respuesta</h2><p id="flashAnswer"></p><span class="small">Haz clic para volver</span></div></div></div>
    <div class="controls"><button class="secondary" onclick="prevCard()">Anterior</button><button onclick="nextCard()">Siguiente</button></div>
  </section>

  <section id="quiz" class="panel hidden">
    <div class="stats">
      <div class="stat"><b id="score">0</b><span>Puntaje</span></div>
      <div class="stat"><b id="correct">0</b><span>Correctas</span></div>
      <div class="stat"><b id="wrong">0</b><span>Incorrectas</span></div>
      <div class="stat"><b id="count">0/0</b><span>Avance</span></div>
    </div>
    <div class="progress"><div class="bar" id="bar"></div></div>
    <div class="question-card" id="questionBox"></div>
    <div class="controls" style="margin-top:16px"><button id="nextBtn" onclick="nextQuestion()" class="hidden">Siguiente pregunta</button><button onclick="restartQuiz()" class="secondary">Reiniciar</button></div>
  </section>

  <section id="final" class="panel hidden"><h2>Resultado final</h2><div class="results" id="finalText"></div><div class="controls"><button onclick="restartQuiz()">Intentar otra vez</button><button onclick="showSection('teoria')" class="secondary">Repasar teoría</button></div></section>
  <p class="footer-note">Consejo: usa primero las tarjetas, luego inicia el cuestionario y revisa las explicaciones de cada alternativa.</p>
</main>
<script>
const topics=[
 {t:'Sistema termodinámico',p:'Un sistema es una cantidad de materia o una región del espacio elegida para el análisis. Puede tener fronteras fijas, móviles, reales o imaginarias.',tag:'Sistema, frontera, alrededores'},
 {t:'Tipos de sistemas',p:'Sistema cerrado: no intercambia masa, pero puede intercambiar energía. Sistema abierto: intercambia masa y energía. Sistema aislado: no intercambia masa ni energía.',tag:'Cerrado, abierto, aislado'},
 {t:'Propiedades intensivas y extensivas',p:'Las intensivas no dependen de la masa, como temperatura, presión y densidad. Las extensivas dependen de la masa, como volumen, masa, energía interna y entalpía.',tag:'Propiedades'},
 {t:'Estado y equilibrio',p:'El estado es la condición definida por las propiedades del sistema. El equilibrio implica ausencia de fuerzas impulsoras; por ejemplo, temperatura uniforme en equilibrio térmico y presión uniforme en equilibrio mecánico.',tag:'Estado'},
 {t:'Postulado de estado',p:'El estado de un sistema compresible simple se especifica completamente con dos propiedades intensivas independientes.',tag:'Compresible simple'},
 {t:'Procesos',p:'Un proceso es el cambio de un estado de equilibrio a otro. Su recorrido se llama trayectoria. Si ocurre casi en equilibrio, se denomina cuasiestático o de cuasiequilibrio.',tag:'Proceso'},
 {t:'Procesos especiales',p:'Isobárico: presión constante. Isotérmico: temperatura constante. Isocórico: volumen constante. Estacionario: no cambia con el tiempo. Transitorio: cambia con el tiempo.',tag:'Clasificación'},
 {t:'Ciclo termodinámico',p:'Es una secuencia de procesos que inicia y termina en el mismo estado; al final, las propiedades vuelven a sus valores iniciales.',tag:'Ciclo'},
 {t:'Densidad y volumen específico',p:'La densidad es masa por unidad de volumen: ρ=m/V. El volumen específico es v=V/m=1/ρ. En líquidos y sólidos, la densidad depende principalmente de la temperatura.',tag:'ρ, v'},
 {t:'Temperatura y ley cero',p:'La temperatura expresa el nivel térmico. La ley cero permite afirmar que si A está en equilibrio térmico con B y B con C, entonces A está en equilibrio térmico con C.',tag:'Temperatura'},
 {t:'Escalas de temperatura',p:'Para temperatura absoluta: T(K)=T(°C)+273,15 y T(R)=T(°F)+459,67. Los cambios de temperatura cumplen ΔT(K)=ΔT(°C) y ΔT(R)=ΔT(°F).',tag:'K, °C, °F, R'},
 {t:'Presión',p:'La presión es fuerza normal por unidad de área: P=F/A. Unidades importantes: Pa=N/m², 1 bar=100 kPa y 1 atm=101,325 kPa.',tag:'P=F/A'},
 {t:'Presión hidrostática',p:'En un fluido en reposo, la presión aumenta con la profundidad: P=P_atm+ρgh. La presión manométrica o hidrostática es ρgh.',tag:'ρgh'},
 {t:'Presión absoluta, manométrica y vacío',p:'P_manométrica=P_abs-P_atm. P_vacío=P_atm-P_abs. Si no se indica lo contrario, una presión asignada suele interpretarse como absoluta.',tag:'Presiones'},
 {t:'Manómetros',p:'Los manómetros comparan presiones mediante columnas de fluido. En sistemas con dos fluidos puede usarse P1-P2=g·h(ρ2-ρ1), según la configuración.',tag:'Medición'}
];
const questions=[
 {topic:'Sistema',q:'¿Cómo se define un sistema en termodinámica?',o:['Una cantidad de materia o región del espacio elegida para el análisis','Solo un recipiente cerrado sin transferencia de energía','El conjunto de instrumentos de medición','Cualquier cuerpo que no tiene frontera'],a:0,e:'Un sistema es la porción de materia o región espacial seleccionada para estudiar sus interacciones.'},
 {topic:'Sistema',q:'¿Qué característica corresponde a un sistema cerrado?',o:['Existe ingreso y salida de masa','No existe ingreso ni salida de masa, pero puede cruzar energía','No existe ingreso ni salida de energía ni masa','Siempre tiene frontera imaginaria'],a:1,e:'En un sistema cerrado la masa permanece constante, aunque puede haber transferencia de calor o trabajo.'},
 {topic:'Sistema',q:'¿Cuál es un ejemplo típico de sistema abierto?',o:['Un termo ideal perfectamente aislado','Un compresor, una turbina o una tobera','Un gas contenido en pistón sin fuga de masa','Una masa sólida en reposo absoluto'],a:1,e:'Los dispositivos de flujo como compresores, turbinas y toberas tienen entrada y salida de masa y energía.'},
 {topic:'Propiedades',q:'¿Cuál de las siguientes propiedades es intensiva?',o:['Masa','Volumen total','Temperatura','Energía interna total'],a:2,e:'La temperatura no depende de la cantidad de masa del sistema.'},
 {topic:'Propiedades',q:'¿Cuál de las siguientes propiedades es extensiva?',o:['Presión','Densidad','Volumen','Temperatura'],a:2,e:'El volumen depende de la cantidad de materia; si el sistema se divide, el volumen también se divide.'},
 {topic:'Propiedades',q:'¿Qué son las propiedades específicas?',o:['Propiedades intensivas multiplicadas por presión','Propiedades extensivas por unidad de masa','Propiedades que solo existen en sistemas aislados','Propiedades que no pueden medirse'],a:1,e:'Ejemplos: volumen específico v=V/m y entalpía específica h=H/m.'},
 {topic:'Estado',q:'¿Qué representa el estado de un sistema?',o:['La ruta completa de todos los procesos','El conjunto de propiedades que define la condición del sistema','La energía transferida como trabajo','El valor de una sola propiedad intensiva'],a:1,e:'El estado queda definido por un conjunto de propiedades medibles o calculables.'},
 {topic:'Equilibrio',q:'Un sistema está en equilibrio térmico cuando:',o:['La presión es mayor en la parte inferior','La temperatura es la misma en todo el sistema','La masa aumenta con el tiempo','El volumen se mantiene constante'],a:1,e:'Equilibrio térmico significa uniformidad de temperatura dentro del sistema.'},
 {topic:'Equilibrio',q:'Un sistema está en equilibrio mecánico cuando:',o:['La presión es la misma en todo el sistema','La temperatura cambia por zonas','La densidad es cero','El proceso es siempre isotérmico'],a:0,e:'El equilibrio mecánico se asocia con ausencia de desequilibrios de presión.'},
 {topic:'Postulado',q:'Según el postulado de estado, un sistema compresible simple queda definido por:',o:['Una propiedad extensiva cualquiera','Dos propiedades intensivas independientes','Tres propiedades extensivas dependientes','Solo masa y volumen'],a:1,e:'El PDF indica que dos propiedades intensivas independientes especifican el estado de un sistema compresible simple.'},
 {topic:'Procesos',q:'¿Qué es un proceso termodinámico?',o:['Un cambio de un estado de equilibrio a otro','Una propiedad que no depende de la masa','Un sistema sin frontera','Una presión medida con barómetro'],a:0,e:'El proceso conecta estados; la serie de estados intermedios se llama trayectoria.'},
 {topic:'Procesos',q:'¿Qué caracteriza a un proceso cuasiestático?',o:['Ocurre tan rápido que las partículas no se distribuyen','El sistema permanece casi en equilibrio durante todo el proceso','No permite transferencia de energía','Solo ocurre en sistemas aislados'],a:1,e:'En un proceso cuasiestático, las propiedades cambian lentamente y de forma casi uniforme.'},
 {topic:'Procesos',q:'Un proceso isobárico es aquel que mantiene constante:',o:['La temperatura','El volumen','La presión','La masa molecular'],a:2,e:'Isobárico significa a presión constante.'},
 {topic:'Procesos',q:'Un proceso isotérmico mantiene constante:',o:['La presión','La temperatura','El volumen','La densidad relativa'],a:1,e:'Isotérmico significa a temperatura constante.'},
 {topic:'Procesos',q:'Un proceso isocórico mantiene constante:',o:['El volumen','La temperatura','La presión','La entalpía'],a:0,e:'Isocórico significa a volumen constante.'},
 {topic:'Ciclo',q:'¿Qué ocurre al final de un ciclo termodinámico?',o:['Todas las propiedades cambian permanentemente','El sistema termina en un estado distinto','Las propiedades vuelven a sus valores iniciales','La masa desaparece'],a:2,e:'Un ciclo inicia y termina en el mismo estado.'},
 {topic:'Densidad',q:'La densidad se define como:',o:['ρ=V/m','ρ=m/V','ρ=P/T','ρ=F/A'],a:1,e:'La densidad es la masa por unidad de volumen.'},
 {topic:'Densidad',q:'El volumen específico se expresa como:',o:['v=m/V','v=ρg','v=V/m=1/ρ','v=P/A'],a:2,e:'El volumen específico es volumen por unidad de masa, equivalente al inverso de la densidad.'},
 {topic:'Temperatura',q:'La ley cero de la termodinámica permite concluir que si TA=TB y TB=TC, entonces:',o:['TA≠TC','TA=TC','TB=0','TC depende de la presión'],a:1,e:'La ley cero fundamenta la medición de temperatura y el equilibrio térmico.'},
 {topic:'Temperatura',q:'¿Cuál es la relación correcta entre Kelvin y grados Celsius?',o:['T(K)=T(°C)-273,15','T(K)=T(°C)+273,15','T(K)=T(°F)+459,67','T(K)=5/9(°F-32)'],a:1,e:'La escala Kelvin se obtiene sumando 273,15 a la temperatura en °C.'},
 {topic:'Presión',q:'La presión se define como:',o:['P=F/A','P=m/V','P=ρ/V','P=V/m'],a:0,e:'La presión es fuerza normal dividida entre área.'},
 {topic:'Presión',q:'¿Cuál equivalencia es correcta?',o:['1 bar=10 kPa','1 bar=100 kPa','1 atm=10 kPa','1 Pa=100 kPa'],a:1,e:'El PDF indica 1 bar=10^5 Pa=100 kPa.'},
 {topic:'Hidrostática',q:'En un líquido en reposo, la presión absoluta a profundidad h se calcula como:',o:['Pabs=Patm-ρgh','Pabs=Patm+ρgh','Pabs=ρ/g/h','Pabs=F·A'],a:1,e:'La presión aumenta con la profundidad: Pabs=Patm+ρgh.'},
 {topic:'Presiones',q:'La presión manométrica se calcula como:',o:['Pman=Pabs-Patm','Pman=Patm-Pabs','Pman=Pabs+Patm','Pman=ρ/V'],a:0,e:'Cuando la presión del sistema supera la atmosférica se usa presión manométrica.'},
 {topic:'Presiones',q:'La presión de vacío se calcula como:',o:['Pvac=Pabs-Patm','Pvac=Patm-Pabs','Pvac=Patm+Pabs','Pvac=ρgh+Pabs'],a:1,e:'Se habla de vacío cuando la presión atmosférica es mayor que la presión del sistema.'},
 {topic:'Manómetro',q:'¿Para qué se usa un manómetro?',o:['Para medir volumen específico directamente','Para comparar o medir presiones mediante columnas de fluido','Para determinar masa molecular','Para convertir °C a K'],a:1,e:'El manómetro relaciona diferencias de presión con alturas y densidades de fluidos.'}
];
let quiz=[...questions],idx=0,score=0,correct=0,wrong=0,answered=false,card=0;
function init(){const sel=document.getElementById('topicFilter');[...new Set(topics.map(x=>x.tag.split(',')[0]))].forEach(t=>{let op=document.createElement('option');op.value=t;op.textContent=t;sel.appendChild(op)});renderTheory();renderFlash()}
function showSection(id){['teoria','flashcards','quiz','final'].forEach(x=>document.getElementById(x).classList.add('hidden'));document.getElementById(id).classList.remove('hidden')}
function renderTheory(){let f=document.getElementById('topicFilter').value;let data=f==='todos'?topics:topics.filter(x=>x.tag.includes(f)||x.t.includes(f));document.getElementById('theoryGrid').innerHTML=data.map(x=>`<article class="topic"><h3>${x.t}</h3><p>${x.p}</p><span class="tag">${x.tag}</span></article>`).join('')}
function shuffle(a){for(let i=a.length-1;i>0;i--){let j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a}
function shuffleQuiz(){quiz=shuffle([...questions]);restartQuiz()}
function startQuiz(){showSection('quiz');idx=0;score=0;correct=0;wrong=0;answered=false;renderQuestion()}
function restartQuiz(){idx=0;score=0;correct=0;wrong=0;answered=false;showSection('quiz');renderQuestion()}
function renderQuestion(){if(idx>=quiz.length){finish();return}answered=false;document.getElementById('nextBtn').classList.add('hidden');let q=quiz[idx];document.getElementById('score').textContent=score;document.getElementById('correct').textContent=correct;document.getElementById('wrong').textContent=wrong;document.getElementById('count').textContent=`${idx+1}/${quiz.length}`;document.getElementById('bar').style.width=`${(idx/quiz.length)*100}%`;document.getElementById('questionBox').innerHTML=`<div class="qtop"><span class="qbadge">Tema: ${q.topic}</span><span class="small">Pregunta ${idx+1} de ${quiz.length}</span></div><div class="question">${q.q}</div><div class="options">${q.o.map((op,i)=>`<button class="option" onclick="answer(${i})">${String.fromCharCode(65+i)}. ${op}</button>`).join('')}</div><div id="fb" class="feedback"></div>`}
function answer(i){if(answered)return;answered=true;let q=quiz[idx],opts=[...document.querySelectorAll('.option')],fb=document.getElementById('fb');opts[q.a].classList.add('correct');if(i===q.a){score+=10;correct++;fb.className='feedback ok';fb.innerHTML='<b>Correcto.</b> '+q.e}else{wrong++;opts[i].classList.add('wrong');fb.className='feedback bad';fb.innerHTML='<b>Incorrecto.</b> Respuesta correcta: <b>'+String.fromCharCode(65+q.a)+'</b>. '+q.e}document.getElementById('score').textContent=score;document.getElementById('correct').textContent=correct;document.getElementById('wrong').textContent=wrong;document.getElementById('nextBtn').classList.remove('hidden')}
function nextQuestion(){idx++;renderQuestion()}
function finish(){showSection('final');document.getElementById('bar').style.width='100%';let pct=Math.round((correct/quiz.length)*100);let msg=pct>=80?'Excelente dominio teórico.':pct>=60?'Buen avance, conviene repasar los temas fallados.':'Necesitas reforzar conceptos básicos antes de resolver problemas.';document.getElementById('finalText').innerHTML=`<p><b>Puntaje:</b> ${score} puntos</p><p><b>Correctas:</b> ${correct} de ${quiz.length} (${pct}%).</p><p>${msg}</p><p><span class="pill">Sistema</span><span class="pill">Propiedades</span><span class="pill">Procesos</span><span class="pill">Presión</span><span class="pill">Densidad</span></p>`}
function renderFlash(){let x=topics[card];document.getElementById('flash').classList.remove('flip');document.getElementById('flashTitle').textContent=x.t;document.getElementById('flashPrompt').textContent='¿Qué debes recordar sobre este tema?';document.getElementById('flashAnswer').textContent=x.p}
function flipCard(){document.getElementById('flash').classList.toggle('flip')}
function nextCard(){card=(card+1)%topics.length;renderFlash()}
function prevCard(){card=(card-1+topics.length)%topics.length;renderFlash()}
init();
</script>
</body>
</html>
