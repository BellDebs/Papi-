# Papi-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Drakon Ascension</title>

<style>

body{
margin:0;
background:#000;
color:#00ffd5;
font-family:monospace;
overflow:hidden;
text-align:center;
}

/* MATRIX BACKGROUND */
canvas{
position:fixed;
top:0;
left:0;
z-index:-1;
}

/* CENTER */
.center{
position:absolute;
top:50%;
left:50%;
transform:translate(-50%,-50%);
width:90%;
max-width:600px;
}

.hidden{display:none}

/* CARD */
.card{
background:rgba(0,0,0,.75);
padding:30px;
border-radius:15px;
box-shadow:0 0 35px #00ffd5;
}

/* INPUT */
input{
padding:12px;
width:80%;
border:none;
border-radius:6px;
text-align:center;
}

/* BUTTON */
button{
padding:12px 22px;
margin-top:12px;
background:#00ffd5;
border:none;
border-radius:6px;
cursor:pointer;
font-weight:bold;
}

/* CURSOR */
.cursor{
display:inline-block;
width:8px;
height:18px;
background:#00ffd5;
animation:blink 1s infinite;
}
@keyframes blink{50%{opacity:0;}}

/* PERKS */
#perks{
opacity:0;
transform:scale(.8);
transition:1s;
color:gold;
margin-top:20px;
}
.show{
opacity:1;
transform:scale(1);
}

.dragon{
font-size:60px;
margin-bottom:10px;
}

</style>
</head>

<body>

<canvas id="matrix"></canvas>

<audio id="music" loop>
<source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_c8c8a73467.mp3">
</audio>

<!-- BOOT -->
<div id="boot" class="center">
<h2 id="bootText"></h2><span class="cursor"></span>
</div>

<!-- PASSWORD -->
<div id="unlockPanel" class="center hidden">
<div class="card">
<h2>HOST DETECTED</h2>

<p>
Emmanuel<br>
Sunbola<br>
Praise
</p>

<input id="nameInput" placeholder="Enter Password">
<br>
<button onclick="unlockSystem()">ACCESS SYSTEM</button>

<p id="error"></p>
</div>
</div>

<!-- GREETING -->
<div id="greeting" class="center hidden">
<div class="card">

<div class="dragon">🐉</div>

<h2>WELCOME, DRAKON</h2>

<p id="message"></p>

<button onclick="acceptReward()">ACCEPT REWARD</button>

</div>
</div>

<!-- REWARD -->
<div id="rewardPanel" class="center hidden">
<div class="card">

<h2>===== SYSTEM STATUS =====</h2>

<p>Name : Drakon</p>
<p>Race : Human</p>

<div id="perks">
⚡ PERKS INSTALLED ⚡<br><br>
💰 Wealth +100<br>
❤️ Health +100<br>
😊 Happiness +100
</div>

</div>
</div>

<script>

/* MATRIX RAIN */
const canvas=document.getElementById("matrix");
const ctx=canvas.getContext("2d");

canvas.height=window.innerHeight;
canvas.width=window.innerWidth;

const letters="DRKN01";
const fontSize=14;
const columns=canvas.width/fontSize;
const drops=[];

for(let x=0;x<columns;x++) drops[x]=1;

function draw(){
ctx.fillStyle="rgba(0,0,0,0.05)";
ctx.fillRect(0,0,canvas.width,canvas.height);

ctx.fillStyle="#00ffd5";
ctx.font=fontSize+"px monospace";

for(let i=0;i<drops.length;i++){
const text=letters[Math.floor(Math.random()*letters.length)];
ctx.fillText(text,i*fontSize,drops[i]*fontSize);

if(drops[i]*fontSize>canvas.height && Math.random()>0.975)
drops[i]=0;

drops[i]++;
}
}
setInterval(draw,35);

/* SYSTEM BOOT */
const bootLines=[
"SYSTEM INITIALIZING...",
"SCANNING HOST...",
"LOADING DESTINY FILES...",
"BINDING IDENTITY...",
"DRAKON PROTOCOL ACTIVATED"
];

let line=0,char=0;
const bootText=document.getElementById("bootText");

function boot(){
if(line<bootLines.length){
bootText.textContent+=bootLines[line].charAt(char);
char++;

if(char===bootLines[line].length){
bootText.textContent+="\n";
line++;char=0;
}

setTimeout(boot,35);

}else{
setTimeout(()=>{
document.getElementById("boot").classList.add("hidden");
document.getElementById("unlockPanel").classList.remove("hidden");
},900);
}
}
boot();

/* UNLOCK SYSTEM */
function unlockSystem(){

let name=document.getElementById("nameInput")
.value.trim().toLowerCase();

if(name==="drakon"){

document.getElementById("unlockPanel").classList.add("hidden");
document.getElementById("greeting").classList.remove("hidden");

/* MUSIC START */
document.getElementById("music").play().catch(()=>{});

typeMessage();

}else{
document.getElementById("error").textContent="ACCESS DENIED";
}
}

/* GREETING MESSAGE */
const msg=`Today marks more than a birthday.

Emmanuel.
Sunbola.
Praise.

May your life be filled with joy,
success,
and happiness.

May inspiration guide you.
May motivation strengthen you.

Soon,
you shall live the life you truly desire.

Happy Birthday, Drakon.`;

let i=0;

function typeMessage(){
if(i<msg.length){
document.getElementById("message")
.textContent+=msg.charAt(i);
i++;
setTimeout(typeMessage,25);
}
}

).classList.add("hidden");
document.getElementById("rewardPanel").classList.remove("hidden");

function acceptReward(){

document.getElementById("greeting").classList.add("hidden");
document.getElementById("rewardPanel").classList.remove("hidden");

const perks=[
"⚡ Installing System Rewards...",
"",
"💰 Wealth +100",
"❤️ Health +100",
"😊 Happiness +100",
"",
"✅ ASCENSION COMPLETE"
];

let i=0;
const container=document.getElementById("perks");

function loadPerk(){

if(i<perks.length){

let line=document.createElement("div");
line.style.margin="8px";
line.style.color="gold";
line.textContent=perks[i];

container.appendChild(line);

i++;
setTimeout(loadPerk,700);
}
}

loadPerk();
}

</script>

</body>
</html>
