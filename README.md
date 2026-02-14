<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Achnologya</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}

body{
background:linear-gradient(135deg,#0f2027,#203a43,#2c5364);
color:white;
}

/* Navbar */
nav{
display:flex;
justify-content:space-between;
align-items:center;
padding:15px 8%;
background:rgba(0,0,0,0.4);
backdrop-filter:blur(10px);
position:sticky;
top:0;
}

nav h2{
font-weight:700;
}

nav input{
padding:8px;
border-radius:20px;
border:none;
outline:none;
}

/* Hero */
.hero{
text-align:center;
padding:50px 20px;
}

.hero h1{
font-size:40px;
}

.hero p{
opacity:0.8;
margin-top:10px;
}

/* Cards */
.container{
padding:40px 8%;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:25px;
}

.card{
background:rgba(255,255,255,0.1);
padding:25px;
border-radius:15px;
backdrop-filter:blur(8px);
transition:0.3s;
}

.card:hover{
transform:translateY(-10px);
background:rgba(255,255,255,0.2);
}

.card h3{
margin-bottom:10px;
}

button{
padding:8px 15px;
border:none;
border-radius:20px;
cursor:pointer;
background:#00c6ff;
color:black;
font-weight:500;
margin-top:10px;
}

/* Upload Section */
.upload{
margin-top:40px;
text-align:center;
}

.upload input{
margin-top:15px;
}

/* Login Modal */
.modal{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.6);
justify-content:center;
align-items:center;
}

.modal-content{
background:white;
color:black;
padding:30px;
border-radius:10px;
width:300px;
text-align:center;
}

.modal-content input{
width:100%;
padding:8px;
margin:10px 0;
}

footer{
text-align:center;
padding:20px;
margin-top:50px;
opacity:0.8;
}
</style>
</head>

<body>

<nav>
<h2>Achnologya</h2>
<input type="text" id="search" placeholder="Search subject...">
<button onclick="openLogin()">Login</button>
</nav>

<section class="hero">
<h1>Welcome to Achnologya</h1>
<p>Your Smart Study Partner 📚</p>
</section>

<section class="container">
<div class="grid" id="subjectGrid">

<div class="card">
<h3>Mathematics</h3>
<p>Formulas, solved examples & practice sets.</p>
<button>View Notes</button>
</div>

<div class="card">
<h3>Science</h3>
<p>Physics, Chemistry & Biology notes.</p>
<button>View Notes</button>
</div>

<div class="card">
<h3>English</h3>
<p>Grammar, writing skills & literature.</p>
<button>View Notes</button>
</div>

<div class="card">
<h3>Social Science</h3>
<p>History, Civics & Geography.</p>
<button>View Notes</button>
</div>

</div>

<div class="upload">
<h2>Upload PDF Notes</h2>
<input type="file" accept="application/pdf">
<p style="opacity:0.7;margin-top:10px;">(Frontend demo only)</p>
</div>
</section>

<footer>
© 2026 Achnologya | Made by Akash 🚀
</footer>

<!-- Login Modal -->
<div class="modal" id="loginModal">
<div class="modal-content">
<h3>Login</h3>
<input type="text" placeholder="Username">
<input type="password" placeholder="Password">
<button onclick="closeLogin()">Login</button>
</div>
</div>

<script>
function openLogin(){
document.getElementById("loginModal").style.display="flex";
}

function closeLogin(){
document.getElementById("loginModal").style.display="none";
}

/* Search Function */
document.getElementById("search").addEventListener("keyup", function(){
let filter = this.value.toLowerCase();
let cards = document.querySelectorAll(".card");
cards.forEach(card=>{
let text = card.innerText.toLowerCase();
card.style.display = text.includes(filter) ? "block" : "none";
});
});
</script>

</body>
</html>
