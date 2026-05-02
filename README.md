<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Für meinen Guardian 🖤</title>

<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#000000">

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    color: #eaeaea;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    text-align: center;
    background: black;
    overflow: hidden;
}

/* Sternenhimmel */
#stars {
    position: fixed;
    top:0;
    left:0;
    width:100%;
    height:100%;
    z-index:0;
}

.card {
    position: relative;
    z-index: 1;
    background: rgba(255,255,255,0.04);
    padding: 40px 25px;
    border-radius: 18px;
    backdrop-filter: blur(14px);
    max-width: 720px;
    width: 90%;
    box-shadow: 0 0 60px rgba(0,0,0,0.9);
}

h1 {
    font-size: 2em;
}

.subtitle {
    opacity: 0.6;
    margin-bottom: 20px;
}

button {
    margin: 6px;
    padding: 10px 14px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background: white;
    color: black;
}

.memory {
    margin-top: 25px;
    font-size: 1.1em;
    line-height: 1.8;
    min-height: 240px;
    transition: 0.5s;
}

.fade { opacity: 0; }

.heart {
    font-size: 40px;
    animation: beat 1.6s infinite;
    margin-top: 10px;
}

@keyframes beat {
    0% { transform: scale(1); }
    30% { transform: scale(1.5); }
    60% { transform: scale(1); }
    100% { transform: scale(1); }
}
</style>
</head>

<body>

<!-- Intro -->
<div id="intro" style="
position:fixed;
top:0;left:0;
width:100%;height:100%;
background:black;
color:white;
display:flex;
justify-content:center;
align-items:center;
font-size:1.5em;
z-index:999;
transition:1.5s;
">
🖤
</div>

<canvas id="stars"></canvas>

<div class="card">
    <h1>Für meinen Guardian, Herr Anwalt 🖤</h1>
    <div class="subtitle">
        Dezember 2025 · 06.02.2026
    </div>

    <button onclick="show(0)">Kapitel I</button>
    <button onclick="show(1)">Kapitel II</button>
    <button onclick="show(2)">Kapitel III</button>
    <button onclick="show(3)">Kapitel IV</button>
    <button onclick="show(4)">Abspann</button>

    <div id="text" class="memory">
        Wähle ein Kapitel…
    </div>

    <div id="heart" class="heart" style="display:none;">🖤</div>
</div>

<audio id="music" loop>
    <source src="song.mp3" type="audio/mpeg">
</audio>

<script>

/* Intro Fade */
window.addEventListener("load", () => {
  setTimeout(() => {
    document.getElementById("intro").style.opacity = "0";
    setTimeout(() => {
      document.getElementById("intro").style.display = "none";
    }, 1500);
  }, 1000);
});

/* Sternenhimmel */
const canvas = document.getElementById("stars");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let stars = [];

for(let i=0;i<120;i++){
    stars.push({
        x: Math.random()*canvas.width,
        y: Math.random()*canvas.height,
        size: Math.random()*2,
        speed: Math.random()*0.3
    });
}

function animate(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle = "white";

    stars.forEach(s=>{
        s.y += s.speed;
        if(s.y > canvas.height) s.y = 0;
        ctx.fillRect(s.x, s.y, s.size, s.size);
    });

    requestAnimationFrame(animate);
}
animate();

/* Musik Fade */
function playMusicSmooth() {
    const music = document.getElementById("music");
    music.volume = 0;
    music.play().catch(()=>{});

    let vol = 0;
    let fade = setInterval(() => {
        if(vol < 0.6){
            vol += 0.05;
            music.volume = vol;
        } else {
            clearInterval(fade);
        }
    }, 200);
}

/* Kapitel */
const chapters = [

`Kapitel I<br><br>
Phasmophobia.<br>
Ein Spiel im Dunkeln.<br><br>
Und trotzdem der Moment, in dem etwas begann.`,

`Kapitel II<br><br>
Ich habe nicht gemerkt, wann es passiert ist.<br><br>
Nur, dass ich geblieben bin.<br>
Ohne es zu planen.`,

`Kapitel III<br><br>
Weißt du noch…<br>
als ich dir angeboten habe, mit mir über Lukas’ Account zu reden,<br>
weil es dir nicht gut ging?<br><br>
Da wurde aus Nähe etwas Echtes.`,

`Kapitel IV<br><br>
Aus Gesprächen wurden Nächte.<br>
Aus Nächten wurden Gewohnheiten.<br>
Aus Gewohnheiten wurde du.<br><br>
Und irgendwann war es kein Zufall mehr.`,

`Abspann<br><br>
Ich habe dich nicht gesucht.<br>
Aber ich habe dich gefunden.<br><br>

Und ich würde es wieder tun.<br><br>

Nicht einmal.<br>
Immer wieder.<br><br>

Die Entfernung zwischen uns ist nicht leicht.<br>
Manchmal fühlt sie sich an wie etwas,<br>
das gegen uns arbeitet.<br><br>

Und trotzdem…<br>
will ich kämpfen.<br><br>

Für dich.<br>
Für uns.<br><br>

Herr Anwalt…<br><br>

du bist nicht nur ein Teil meines Lebens.<br>
Du bist mein Lebens-Schicksal-Schatz.<br><br>

Und genau deshalb bleibe ich.<br>
Immer. 🖤`
];

function show(index) {
    const box = document.getElementById("text");

    if(index >= 2) playMusicSmooth();

    box.classList.add("fade");

    setTimeout(() => {
        box.innerHTML = "<div class='final'>" + chapters[index] + "</div>";
        box.classList.remove("fade");
    }, 300);

    if(index === 4){
        setTimeout(() => {
            document.getElementById("heart").style.display = "block";
        }, 1500);
    } else {
        document.getElementById("heart").style.display = "none";
    }
}

</script>

</body>
</html>
