# WebBoost-SEO-Analyzer
A Smart SEO Analyzer Tool built using HTML, CSS and JavaScript.

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>WebBoost - Smart SEO Analyzer</title>

<style>

body{
font-family:Arial;
background:linear-gradient(to right,#4facfe,#00f2fe);
text-align:center;
margin:0;
}

header{
background:black;
color:white;
padding:15px;
}

.card{
background:white;
width:400px;
margin:60px auto;
padding:20px;
border-radius:10px;
box-shadow:0 5px 15px rgba(0,0,0,0.2);
}

input,textarea{
width:90%;
padding:10px;
margin:8px 0;
border-radius:5px;
border:1px solid #ccc;
}

button{
padding:10px 15px;
background:#4CAF50;
color:white;
border:none;
cursor:pointer;
border-radius:5px;
}

.report{
background:#f5f5f5;
padding:10px;
margin-top:15px;
text-align:left;
border-radius:5px;
}

.progress{
background:#ddd;
margin-top:10px;
border-radius:10px;
}

.progress-bar{
height:18px;
width:0%;
background:green;
border-radius:10px;
transition:0.5s;
}

</style>

</head>

<body>

<header>
<h2>🚀 WebBoost</h2>
<p>Smart SEO Analyzer Tool</p>
</header>

<div class="card">

<h3>SEO Website Analyzer</h3>

<input type="text" id="url" placeholder="Enter Website URL">
<input type="text" id="keyword" placeholder="Enter Keyword">
<textarea id="content" placeholder="Paste website content"></textarea>

<br>

<button onclick="analyzeSEO()">Analyze</button>

<div id="result"></div>

<div class="progress">
<div id="bar" class="progress-bar"></div>
</div>

</div>

<script>

function analyzeSEO(){
document.getElementById("result").innerHTML="Analyzing...";
setTimeout(runSEO,1500);
}

function runSEO(){

let url=document.getElementById("url").value;
let keyword=document.getElementById("keyword").value;
let content=document.getElementById("content").value;

let score=0;
let report="";

// HTTPS Check
if(url.startsWith("https://")){
score+=20;
report+="✔ HTTPS enabled<br>";
}else{
report+="❌ Use HTTPS<br>";
}

// URL Length
if(url.length<60){
score+=15;
report+="✔ Short URL<br>";
}else{
report+="⚠ URL too long<br>";
}

// Keyword in URL
if(url.toLowerCase().includes(keyword.toLowerCase()) && keyword!=""){
score+=15;
report+="✔ Keyword in URL<br>";
}else{
report+="⚠ Add keyword in URL<br>";
}

// Content Length
if(content.length>300){
score+=20;
report+="✔ Good content length<br>";
}else{
report+="⚠ Content too short<br>";
}

// Keyword Density
let count=0;
if(keyword!=""){
count=content.toLowerCase().split(keyword.toLowerCase()).length-1;
}

let density=(count/content.split(" ").length)*100;

if(density>1 && density<3){
score+=20;
report+="✔ Good keyword usage<br>";
}else{
report+="⚠ Improve keyword usage<br>";
}

// Headings check (basic)
if(content.includes("<h1>") || content.includes("<h2>")){
score+=10;
report+="✔ Headings used<br>";
}else{
report+="⚠ Use headings (H1, H2)<br>";
}

document.getElementById("result").innerHTML=
"<div class='report'><b>SEO Score: "+score+"/100</b><br>"+report+
"<br><br>Keyword '"+keyword+"' found "+count+" times ("+density.toFixed(2)+"%)</div>";

document.getElementById("bar").style.width=score+"%";

}

</script>

</body>
</html>