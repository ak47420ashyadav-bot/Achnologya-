<!DOCTYPE html>
<html>
<head>
<title>Achnologya</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-storage.js"></script>

<style>
body{font-family:Arial;background:#0f2027;color:white;text-align:center}
input,button{padding:10px;margin:10px;border-radius:5px;border:none}
button{background:#00c6ff}
#adminPanel{display:none;margin-top:20px}
</style>
</head>
<body>

<h1>Achnologya</h1>

<div id="loginDiv">
<h3>Admin Login</h3>
<input type="email" id="email" placeholder="Email"><br>
<input type="password" id="password" placeholder="Password"><br>
<button onclick="login()">Login</button>
</div>

<div id="adminPanel">
<h2>Admin Panel</h2>
<input type="file" id="pdfFile"><br>
<button onclick="uploadPDF()">Upload PDF</button>
<button onclick="logout()">Logout</button>
<div id="pdfList"></div>
</div>

<script>
// 🔥 Replace with your Firebase config
const firebaseConfig = {
apiKey: "YOUR_API_KEY",
authDomain: "YOUR_DOMAIN",
projectId: "YOUR_PROJECT_ID",
storageBucket: "YOUR_BUCKET",
messagingSenderId: "YOUR_ID",
appId: "YOUR_APP_ID"
};

firebase.initializeApp(firebaseConfig);

const auth = firebase.auth();
const db = firebase.firestore();
const storage = firebase.storage();

function login(){
let email = document.getElementById("email").value;
let password = document.getElementById("password").value;

auth.signInWithEmailAndPassword(email,password)
.then(()=>{
document.getElementById("loginDiv").style.display="none";
document.getElementById("adminPanel").style.display="block";
loadPDFs();
})
.catch(error=>alert(error.message));
}

function logout(){
auth.signOut();
location.reload();
}

function uploadPDF(){
let file = document.getElementById("pdfFile").files[0];
let storageRef = storage.ref("pdfs/"+file.name);

storageRef.put(file).then(()=>{
storageRef.getDownloadURL().then(url=>{
db.collection("notes").add({
name:file.name,
url:url
});
loadPDFs();
});
});
}

function loadPDFs(){
document.getElementById("pdfList").innerHTML="";
db.collection("notes").get().then(snapshot=>{
snapshot.forEach(doc=>{
let data=doc.data();
document.getElementById("pdfList").innerHTML+=
`<p><a href="${data.url}" target="_blank">${data.name}</a></p>`;
});
});
}
</script>

</body>
</html> 
