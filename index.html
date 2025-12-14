<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Simulation Géopolitique — Lya</title>

<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css"/>

<style>
body {
  margin:0;
  background:#0e0e0e;
  color:#eee;
  font-family: Arial, sans-serif;
}

#top {
  padding:10px;
  background:#151515;
  display:flex;
  gap:20px;
  align-items:center;
  flex-wrap:wrap;
}

.stat { font-size:14px; }

button {
  background:#1f1f1f;
  color:#fff;
  border:1px solid #444;
  padding:6px 10px;
  cursor:pointer;
}
button:hover { background:#333; }

#container {
  display:flex;
  height:calc(100vh - 60px);
}

#map {
  flex:1;
}

#right {
  width:420px;
  background:#111;
  display:flex;
  flex-direction:column;
}

#log {
  flex:1;
  padding:10px;
  overflow-y:auto;
  border-bottom:1px solid #333;
}

#actions {
  padding:10px;
}

textarea {
  width:100%;
  background:#000;
  color:#fff;
  border:1px solid #444;
  resize:none;
  margin-bottom:5px;
}
</style>
</head>

<body>

<div id="top">
  <div class="stat">💰 Économie : <span id="money">500000</span> €</div>
  <div class="stat">💪 Puissance : <span id="power">50</span></div>
  <div class="stat">🪖 Militaire : <span id="military">40</span></div>
  <div class="stat">👥 Population : <span id="population">65</span>M</div>
  <div class="stat">😊 Opinion : <span id="opinion">50</span>%</div>

  <button onclick="passTime(1)">+1 jour</button>
  <button onclick="passTime(7)">+1 semaine</button>
  <button onclick="passTime(30)">+1 mois</button>
  <button onclick="passTime(365)">+1 an</button>
</div>

<div id="container">
  <div id="map"></div>

  <div id="right">
    <div id="log"></div>

    <div id="actions">
      <b>⚡ Action libre</b>
      <textarea id="actionInput" rows="3" placeholder="Ex: ouvrir une entreprise militaire, insulter un président..."></textarea>
      <button onclick="sendAction()">Envoyer</button>

      <hr>

      <b>🧠 Assistant stratégique</b>
      <textarea id="assistantInput" rows="2" placeholder="Ex: Puis-je attaquer le Luxembourg ?"></textarea>
      <button onclick="assistant()">Demander à Lya</button>
    </div>
  </div>
</div>

<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<script>
let state = {
  money: 500000,
  power: 50,
  military: 40,
  population: 65,
  opinion: 50,
  history: []
};

const map = L.map('map').setView([20, 0], 2);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{ maxZoom:5 }).addTo(map);

function log(txt){
  const div = document.getElementById("log");
  div.innerHTML += "<p>"+txt+"</p>";
  div.scrollTop = div.scrollHeight;
}

function updateUI(){
  money.textContent = state.money;
  power.textContent = state.power;
  military.textContent = state.military;
  population.textContent = state.population;
  opinion.textContent = state.opinion;
}

/* ===== ACTION ===== */
async function sendAction(){
  const action = actionInput.value.trim();
  if(!action) return;

  log("⚡ Action : <b>"+action+"</b>");
  state.history.push(action);
  actionInput.value = "";

  const prompt = `
Tu es Lya, IA de simulation géopolitique.

Analyse cette action et applique des effets IMMÉDIATS.

Action :
"${action}"

IMPORTANT : Tous les montants d'argent doivent être écrits en euros simples (ex: +500000, -1200000)

FORMAT STRICT :
EXPLICATION:
(texte)

EFFETS:
argent:+/-nombre
puissance:+/-nombre
militaire:+/-nombre
population:+/-nombre
opinion:+/-nombre
`;

  const res = await callIA(prompt);
  applyIAResponse(res);
}

/* ===== TEMPS ===== */
async function passTime(days){
  log("📅 Temps écoulé : "+days+" jours");

  const prompt = `
Tu es Lya, IA de simulation géopolitique.

Actions passées :
${state.history.join(" | ")}

Temps écoulé : ${days} jours

Tu DOIS produire un résumé et des conséquences.

IMPORTANT : Tous les montants d'argent doivent être écrits en euros simples (ex: +500000, -1200000)

FORMAT STRICT :

RESUME:
(texte)

EFFETS:
argent:+/-nombre
puissance:+/-nombre
militaire:+/-nombre
population:+/-nombre
opinion:+/-nombre

JUSTIFICATION:
(texte)
`;

  const res = await callIA(prompt);
  applyIAResponse(res);
}

/* ===== ASSISTANT INTERACTIF ===== */
async function assistant(){
  const question = assistantInput.value.trim();
  if(!question) return;

  log("🧠 Question : <b>"+question+"</b>");
  assistantInput.value = "";

  const prompt = `
Tu es Lya, conseillère stratégique.

Situation actuelle :
Argent: ${state.money}
Puissance: ${state.power}
Militaire: ${state.military}
Population: ${state.population}
Opinion: ${state.opinion}

Question :
"${question}"

Réponds clairement, avec risques et conséquences.

IMPORTANT : Tous les montants d'argent doivent être écrits en euros simples (ex: +500000, -1200000)
`;

  const res = await callIA(prompt);
  log("🧠 Lya : "+res.replace(/\n/g,"<br>"));
}

/* ===== IA ===== */
async function callIA(prompt){
  const r = await fetch("http://localhost:11434/api/generate",{
    method:"POST",
    headers:{ "Content-Type":"application/json" },
    body:JSON.stringify({ model:"llama3", prompt, stream:false })
  });
  const d = await r.json();
  return d.response;
}

/* ===== APPLICATION DES EFFETS (ARGENT EN EUROS SIMPLES) ===== */
function extractEuroValue(line){
  // enlève tout sauf chiffres, +, -, espaces
  let cleaned = line.replace(/[^0-9+\- ]/g, "");
  cleaned = cleaned.replace(/\s+/g,'');
  const value = parseInt(cleaned,10);
  return isNaN(value)?0:value;
}

function applyIAResponse(text){
  log("📝 Lya explique :<br>"+text.replace(/\n/g,"<br>"));

  const effects = {
    argent:0,
    puissance:0,
    militaire:0,
    population:0,
    opinion:0
  };

  text.split("\n").forEach(line=>{
    const l = line.toLowerCase().trim();
    for(const k in effects){
      if(l.startsWith(k)){
        effects[k] = extractEuroValue(line);
      }
    }
  });

  state.money += effects.argent;
  state.power += effects.puissance;
  state.military += effects.militaire;
  state.population += effects.population;
  state.opinion += effects.opinion;

  // limites
  state.opinion = Math.max(0, Math.min(100, state.opinion));
  state.population = Math.max(1, state.population);

  log(`📊 Effets → 💰${effects.argent} € | 💪${effects.puissance} | 🪖${effects.militaire} | 👥${effects.population} | 😊${effects.opinion}%`);

  updateUI();
}
</script>

</body>
</html>
