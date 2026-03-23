<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VERBOSE — Premium Earning</title>

<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-firestore.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-storage.js"></script>

<style>
body{background:#0d1117;color:white;font-family:sans-serif;padding:10px}
.box{border:1px solid cyan;padding:10px;margin-top:10px;border-radius:8px}
.btn{background:cyan;color:black;padding:8px;border:none;border-radius:6px;margin-top:5px}
input{width:100%;padding:6px;margin-top:5px}
</style>
</head>

<body>

<h2>💰 Balance: <span id="balance">0</span> PKR</h2>
<button onclick="logout()" class="btn">Logout</button>

<div class="box">
<h3>👥 Referral</h3>
<input id="refLink" readonly>
<p>Invite → 50 PKR</p>
</div>

<div class="box">
<h3>💼 Plans</h3>
<div onclick="buyPlan(200,10)" class="btn">200 PKR → 10 Daily</div>
<div onclick="buyPlan(500,30)" class="btn">500 PKR → 30 Daily</div>
<div onclick="buyPlan(1000,80)" class="btn">1000 PKR → 80 Daily</div>
</div>

<div class="box">
<h3>Deposit</h3>
<input id="amount" placeholder="Amount">
<input id="tid" placeholder="TID">
<input type="file" id="proof">
<button onclick="submitDeposit()" class="btn">Submit</button>
</div>

<div class="box">
<h3>History</h3>
<div id="history"></div>
</div>

<div class="box">
<h3>Withdraw</h3>
<input id="withdrawAmount" placeholder="Amount">
<input id="account" placeholder="Account">
<button onclick="withdraw()" class="btn">Withdraw</button>
</div>

<hr>

<div id="adminPanel" style="display:none">
<h3>👑 GOD ADMIN PANEL</h3>
<div id="adminData"></div>
<div id="withdrawAdmin"></div>
<div id="allUsers"></div>
</div>

<script>

// 🔥 Firebase Config (same)
const firebaseConfig = {
  apiKey: "AIzaSyCMG6KG_oD8cjEk4YpbxXik-C5q8K5MDHk",
  authDomain: "dark-web-9.firebaseapp.com",
  projectId: "dark-web-9",
  storageBucket: "dark-web-9.firebasestorage.app",
  messagingSenderId: "564328425161",
  appId: "1:564328425161:web:eb109ab77356dafe7f4f18"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

// 🔐 ADMIN EMAIL
const ADMIN_EMAILS = ["youradmin@gmail.com"];

function isAdmin(user){
  return user && ADMIN_EMAILS.includes(user.email);
}

// 🔓 Logout
function logout(){
  firebase.auth().signOut().then(()=>location.reload());
}

// 🔗 Referral
firebase.auth().onAuthStateChanged(user=>{
if(user){
document.getElementById("refLink").value = location.origin+"?ref="+user.uid;
if(isAdmin(user)) document.getElementById("adminPanel").style.display="block";
}
});

// 💰 Daily Profit
firebase.auth().onAuthStateChanged(user=>{
if(user){
let today=new Date().toDateString();
let ref=db.collection("users").doc(user.uid);

ref.get().then(doc=>{
let d=doc.data()||{};
if(d.lastClaim!==today){
ref.set({balance:(d.balance||0)+20,lastClaim:today},{merge:true});
}
});
}
});

// 💼 Plan Buy (deposit required)
function buyPlan(price,daily){
let user=firebase.auth().currentUser;

db.collection("deposits")
.where("user","==",user.uid)
.where("status","==","approved")
.get().then(snap=>{

if(snap.empty){
alert("Deposit required ❌");
return;
}

db.collection("users").doc(user.uid).get().then(doc=>{
let bal=doc.data()?.balance||0;

if(bal<price){
alert("Low balance ❌");
return;
}

db.collection("users").doc(user.uid).update({
balance:bal-price,
plan:{price:price,daily:daily}
});

alert("Plan Activated ✅");
});

});
}

// 💸 Deposit
function submitDeposit(){
let file=document.getElementById("proof").files[0];
let user=firebase.auth().currentUser;

let ref=firebase.storage().ref("proofs/"+Date.now()+"_"+file.name);

ref.put(file).then(()=>{
ref.getDownloadURL().then(url=>{
db.collection("deposits").add({
user:user.uid,
amount:document.getElementById("amount").value,
tid:document.getElementById("tid").value,
proof:url,
status:"pending"
});
alert("Submitted");
});
});
}

// 📊 Balance + History
firebase.auth().onAuthStateChanged(user=>{
if(user){
db.collection("users").doc(user.uid)
.onSnapshot(doc=>{
document.getElementById("balance").innerText=doc.data()?.balance||0;
});

db.collection("deposits").where("user","==",user.uid)
.onSnapshot(snap=>{
let html="";
snap.forEach(doc=>{
let d=doc.data();
html+=`<div class="box">${d.amount} PKR - ${d.status}</div>`;
});
document.getElementById("history").innerHTML=html;
});
}
});

// 👨‍💼 Admin Deposits
db.collection("deposits").onSnapshot(snap=>{
let html="";
snap.forEach(doc=>{
let d=doc.data();
html+=`
<div class="box">
${d.amount} PKR<br>
${d.tid}<br>
<img src="${d.proof}" width="80"><br>
${d.status}
<button onclick="approveDeposit('${doc.id}','${d.user}',${d.amount})">Approve</button>
</div>`;
});
document.getElementById("adminData").innerHTML=html;
});

// ✅ Approve Deposit
function approveDeposit(id,uid,amount){
db.collection("deposits").doc(id).update({status:"approved"});
db.collection("users").doc(uid).get().then(doc=>{
let bal=doc.data()?.balance||0;
db.collection("users").doc(uid).update({balance:bal+Number(amount)});
});
}

// 💸 Withdraw
function withdraw(){
let user=firebase.auth().currentUser;
db.collection("withdraws").add({
user:user.uid,
amount:document.getElementById("withdrawAmount").value,
account:document.getElementById("account").value,
status:"pending"
});
}

// 👨‍💼 Withdraw Admin
db.collection("withdraws").onSnapshot(snap=>{
let html="";
snap.forEach(doc=>{
let d=doc.data();
html+=`
<div class="box">
${d.amount} PKR - ${d.account}
<button onclick="approveWithdraw('${doc.id}','${d.user}',${d.amount})">Approve</button>
</div>`;
});
document.getElementById("withdrawAdmin").innerHTML=html;
});

// ✅ Approve Withdraw
function approveWithdraw(id,uid,amount){
db.collection("withdraws").doc(id).update({status:"approved"});
db.collection("users").doc(uid).get().then(doc=>{
let bal=doc.data()?.balance||0;
db.collection("users").doc(uid).update({balance:bal-Number(amount)});
});
}

// 👑 Admin All Users
db.collection("users").onSnapshot(snap=>{
let html="";
snap.forEach(doc=>{
let d=doc.data();
html+=`<div class="box">UID: ${doc.id} - ${d.balance||0}
<button onclick="addBalance('${doc.id}',100)">+100</button>
</div>`;
});
document.getElementById("allUsers").innerHTML=html;
});

function addBalance(uid,amt){
db.collection("users").doc(uid).get().then(doc=>{
let bal=doc.data()?.balance||0;
db.collection("users").doc(uid).update({balance:bal+amt});
});
}

</script>

</body>
</html>
