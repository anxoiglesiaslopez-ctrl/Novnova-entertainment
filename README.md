<!DOCTYPE html>
<html lang="gl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOVA 5.1</title>
<style>
:root { --color:#ff9800; }
* { box-sizing:border-box; font-family:Arial,sans-serif; }
body {
    margin:0;
    min-height:100vh;
    background:linear-gradient(135deg,var(--color),#121212);
    color:white;
    transition:0.4s;
    display:flex;
    flex-direction:column;
}
.tabs {
    display:flex;
    gap:10px;
    overflow-x:auto;
    padding:15px;
    background:rgba(0,0,0,.25);
}
.tab {
    border:none;
    border-radius:25px;
    padding:12px 18px;
    background:rgba(255,255,255,.15);
    color:white;
    cursor:pointer;
    font-weight:bold;
}
.tab.active {
    background:white;
    color:black;
}
.main {
    flex:1;
    display:flex;
    flex-direction:column;
    align-items:center;
    padding:20px;
}
.search {
    width:min(90%,700px);
    padding:18px;
    border:none;
    border-radius:40px;
    font-size:18px;
    margin:40px 0 20px;
}
.results {
    width:min(95%,800px);
}
.card {
    background:rgba(255,255,255,.12);
    padding:16px;
    border-radius:18px;
    margin-bottom:12px;
}
.logo {
    margin-top:auto;
    font-size:48px;
    font-weight:bold;
    padding:30px;
}
</style>
</head>
<body>

<div class="tabs">
<button class="tab active" onclick="change('Todo','#ff9800',this)">🌐 Todo</button>
<button class="tab" onclick="change('Música','#9c27b0',this)">🎵 Música</button>
<button class="tab" onclick="change('TV','#2196f3',this)">📺 TV</button>
<button class="tab" onclick="change('Videoxogos','#4caf50',this)">🎮 Xogos</button>
<button class="tab" onclick="change('Series','#f44336',this)">🎬 Series</button>
</div>

<div class="main">
<input class="search" id="search" placeholder="🔍 Buscar en NOVA..." oninput="searchNova()">
<div class="results" id="results"></div>
<div class="logo">✦ NOVA ✦</div>
</div>

<script>
const db = {
Música:["Taylor Swift","Shakira","Rosalía","Bad Bunny","Dua Lipa","The Weeknd","Ed Sheeran","Billie Eilish"],
TV:["La Voz","MasterChef","El Hormiguero","Operación Triunfo","The Simpsons"],
Videoxogos:["Minecraft","Fortnite","GTA VI","Elden Ring","Roblox","FIFA","Mario Kart","Zelda"],
Series:["Stranger Things","The Last of Us","Wednesday","Breaking Bad","The Witcher","Dune","Avatar"]
};

let current = "Todo";

function change(cat,color,btn){
    current = cat;
    document.documentElement.style.setProperty('--color', color);
    document.querySelectorAll('.tab').forEach(x=>x.classList.remove('active'));
    btn.classList.add('active');
    searchNova();
}

function searchNova(){
    const q = document.getElementById('search').value.toLowerCase().trim();
    const results = document.getElementById('results');

    if(!q){
        results.innerHTML = "";
        return;
    }

    let items = current === "Todo"
        ? Object.values(db).flat()
        : db[current];

    items = items.filter(x => x.toLowerCase().includes(q));

    if(items.length === 0){
        results.innerHTML = "<div class='card'>🔍 Sen resultados.</div>";
        return;
    }

    results.innerHTML = items.map(x =>
        `<div class='card'><h3>${x}</h3></div>`
    ).join("");
}
</script>

</body>
</html>
