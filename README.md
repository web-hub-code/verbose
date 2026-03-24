<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions Pro</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#050505; --glass:rgba(255,255,255,0.05); }
  *{box-sizing:border-box; transition: 0.3s; -webkit-tap-highlight-color: transparent;}
  body { margin:0; font-family:'Poppins', sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
  header { text-align:center; padding:35px 20px; font-size:35px; font-weight:900; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; text-transform:uppercase; letter-spacing:5px; }
  
  .page { max-width:420px; margin:15px auto 100px; background:var(--glass); padding:25px; border-radius:30px; border:1px solid rgba(0,255,240,0.1); backdrop-filter: blur(20px); box-shadow: 0 25px 50px rgba(0,0,0,0.8); }
  .user-card { background:linear-gradient(135deg, rgba(0,247,255,0.12), rgba(255,92,255,0.06)); padding:20px; border-radius:22px; margin-bottom:15px; border-left:5px solid var(--neon); }
  
  #newsTicker { background: rgba(255, 68, 68, 0.15); color: #ff8888; padding: 12px; font-size: 13px; font-weight: 600; border-radius: 12px; margin-bottom: 15px; border: 1px solid rgba(255, 68, 68, 0.3); overflow: hidden; }

  input, select { width:100%; padding:15px; margin-top:12px; border-radius:15px; border:1px solid rgba(255,255,255,0.1); background:rgba(0,0,0,0.6); color:#fff; font-size:14px; outline:none; }
  input:focus { border-color: var(--neon); }
  button { width:100%; padding:16px; margin-top:18px; border-radius:15px; border:none; background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:800; cursor:pointer; font-size:15px; box-shadow: 0 8px 20px rgba(0,247,255,0.2); }
  button:active { transform: scale(0.97); }
  
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(5,5,5,0.95); display:flex; justify-content:space-around; padding:20px; border-top:1px solid rgba(255,255,255,0.05); backdrop-filter: blur(10px); z-index:1000; }
  .nav-item { text-align:center; font-size:10px; cursor:pointer; opacity:0.5; color:#fff; flex:1; }
  .nav-item.active { opacity:1; color:var(--neon); text-shadow: 0 0 10px var(--neon); }
  
  .status-tag { font-size:10px; padding:3px 10px; border-radius:20px; float:right; text-transform:uppercase; font-weight:bold; }
  .pending { background: #ffa500; color: #000; }
  .approved { background: #00ff88; color: #000; }
  .rejected { background: #ff4444; color: #fff; }
  .hidden { display:none; }
  .btn-sm { padding:8px 12px; font-size:10px; margin-top:5px; width:auto; }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center;">Elite Access</h2>
  <input id="u_name" type="text" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn">SIGN IN / JOIN</button>
</div>

<div id="dashboard" class="page hidden">
  <div id="newsTicker" class="hidden"><marquee id="newsText"></marquee></div>
  <div class="user-card">
    <div id="welcomeMsg" style="font-size:14px; opacity:0.7;">Welcome</div>
    <div style="font-size:35px; font-weight:900; margin:10px 0;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:11px; color:var(--neon); letter-spacing:1px; font-weight:bold;">WALLET BALANCE</div>
  </div>
  <div class="user-card" style="border-left-color:#fff;">
    <p style="font-size:11px; margin-bottom:5px;">Promo Reward:</p>
    <div style="display:flex; gap:8px;">
      <input id="promoInput" placeholder="Enter Code" style="margin:0; flex:2;">
      <button onclick="applyPromo()" style="margin:0; flex:1; padding:12px; font-size:11px;">APPLY</button>
    </div>
  </div>
  <h3 style="font-size:16px; margin:25px 0 12px 0;">Activity History</h3>
  <div id="historyList"></div>
</div>

<div id="walletPage" class="page hidden">
  <div class="user-card" style="font-size:13px; background:rgba(0,0,0,0.5);">
    <div style="margin-bottom:8px;"><b>JazzCash / SadaPay:</b> <span style="color:var(--neon)">03705519562</span></div>
    <div><b>EasyPaisa:</b> <span style="color:var(--neon)">03379827882</span></div>
    <div style="font-size:10px; opacity:0.6; margin-top:5px;">Beneficiary: Muhammad Nazim</div>
  </div>
  <input id="d_amount" type="number" placeholder="Deposit Amount">
  <input id="d_tid" placeholder="TID (Transaction ID)">
  <input id="d_proof" placeholder="Proof Info / Screenshot Link">
  <button onclick="submitReq('Deposit')">CONFIRM DEPOSIT</button>
  <hr style="opacity:0.1; margin:30px 0;">
  <input id="w_amount" type="number" placeholder="Withdraw Amount">
  <input id="w_phone" placeholder="Account Number">
  <button onclick="submitReq('Withdraw')" style="background:var(--accent)">REQUEST PAYOUT</button>
</div>

<div id="adminPage" class="page hidden" style="border: 2px dashed var(--accent);">
  <h2 style="text-align:center; color:var(--accent); margin-top:0;">⚡ GOD MODE ⚡</h2>
  
  <div class="user-card" style="background:#111;">
    <b>Broadcast News:</b>
    <input id="adminMsg" placeholder="News message...">
    <button onclick="sendBroadcast()" class="btn-sm">UPDATE NEWS</button>
  </div>

  <div class="user-card" style="background:#111;">
    <b>Create Promo Code:</b>
    <input id="newPromoCode" placeholder="Code (e.g. GIFT500)">
    <input id="newPromoAmt" type="number" placeholder="Amount (Rs)">
    <button onclick="createPromo()" class="btn-sm">CREATE PROMO</button>
  </div>

  <div id="adminRequests"></div>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">🏠<br>Home</div>
  <div class="nav-item" onclick="tab('walletPage', this)">💰<br>Wallet</div>
  <div class="nav-item" onclick="doLogout()">🚪<br>Logout</div>
  <div id="adminNav" class="nav-item hidden" onclick="tab('adminPage', this)">⚡<br>God</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // AUTH
  document.getElementById('entryBtn').onclick = async () => {
    const user = document.getElementById('u_name').value.trim().toLowerCase();
    const pass = document.getElementById('u_pass').value.trim();
    if(!user || !pass) return alert("All fields are required!");

    const userRef = ref(db, 'users/' + user);
    const snap = await get(userRef);
    if(snap.exists()){
      if(snap.val().password === pass) start(user, snap.val());
      else alert("Wrong password!");
    } else {
      const d = { username:user, password:pass, balance:0 };
      await set(userRef, d);
      start(user, d);
    }
  };

  function start(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');

    onValue(ref(db, 'users/' + u), s => {
      document.getElementById('mainBal').innerText = parseFloat(s.val().balance).toFixed(2);
    });

    loadHistory(u);
    loadNews();
    if(u === 'nazim_admin') document.getElementById('adminNav').classList.remove('hidden'); // Shortcut for you
    listenAdmin();
  }

  // BROADCAST & PROMO CREATOR
  function loadNews() {
    onValue(ref(db, 'broadcast'), s => {
      if(s.exists()){
        document.getElementById('newsTicker').classList.remove('hidden');
        document.getElementById('newsText').innerText = s.val().msg;
      }
    });
  }
  window.sendBroadcast = () => {
    const m = document.getElementById('adminMsg').value;
    set(ref(db, 'broadcast'), { msg: m });
    alert("News updated!");
  };
  window.createPromo = () => {
    const code = document.getElementById('newPromoCode').value.trim();
    const amt = document.getElementById('newPromoAmt').value;
    if(!code || !amt) return alert("Fill details!");
    set(ref(db, 'promos/' + code), { amount: amt });
    alert("Promo Code " + code + " is Live!");
  };

  // APPLY PROMO
  window.applyPromo = async () => {
    const code = document.getElementById('promoInput').value.trim();
    const u = localStorage.getItem('v_user');
    const s = await get(ref(db, 'promos/' + code));
    if(s.exists() && !s.val().usedBy?.[u]) {
      const reward = parseFloat(s.val().amount);
      const userRef = ref(db, 'users/' + u);
      const uSnap = await get(userRef);
      await update(userRef, { balance: parseFloat(uSnap.val().balance) + reward });
      await update(ref(db, 'promos/' + code + '/usedBy'), { [u]: true });
      alert("Success! Rs " + reward + " added.");
    } else { alert("Invalid or already used promo!"); }
  };

  // FINANCE & HISTORY
  function loadHistory(u) {
    onValue(ref(db, 'history/' + u), s => {
      const cont = document.getElementById('historyList');
      cont.innerHTML = "";
      const data = s.val();
      for(let id in data){
        const h = data[id];
        cont.innerHTML += `<div class="user-card" style="font-size:12px; border-left-color:${h.type=='Deposit'?'var(--neon)':'var(--accent)'}">
          <span class="status-tag ${h.status}">${h.status}</span>
          <b>${h.type}</b>: Rs ${h.amount}<br><small>${h.time}</small>
        </div>`;
      }
    });
  }

  window.submitReq = (type) => {
    const u = localStorage.getItem('v_user');
    const amt = (type=='Deposit')? document.getElementById('d_amount').value : document.getElementById('w_amount').value;
    const tid = document.getElementById('d_tid').value || 'N/A';
    const proof = document.getElementById('d_proof').value || 'N/A';
    if(!amt) return alert("Enter amount!");
    const key = Date.now();
    const r = { user:u, amount:amt, tid:tid, proof:proof, type:type, status:'pending', time:new Date().toLocaleString() };
    set(ref(db, 'requests/' + key), r);
    set(ref(db, 'history/' + u + '/' + key), r);
    alert("Request Sent!");
  };

  // ADMIN SYSTEM
  let taps = 0;
  document.getElementById('mainHeader').onclick = () => {
    if(++taps === 7) {
      if(prompt("God Key:") === "prime786") {
        document.getElementById('adminNav').classList.remove('hidden');
        tab('adminPage');
      }
      taps = 0;
    }
  };

  function listenAdmin() {
    onValue(ref(db, 'requests'), s => {
      const cont = document.getElementById('adminRequests');
      cont.innerHTML = "<h3>Pending List</h3>";
      const data = s.val();
      for(let id in data){
        const r = data[id];
        cont.innerHTML += `<div class="user-card" style="font-size:11px;">
          <b>${r.user}</b> | ${r.type}: ${r.amount}<br>TID: ${r.tid} | Proof: ${r.proof}<br>
          <button onclick="manage('${id}','${r.user}',${r.amount},'${r.type}','approved')" style="width:45%; margin-top:10px;">APPROVE</button>
          <button onclick="manage('${id}','${r.user}',${r.amount},'${r.type}','rejected')" style="width:45%; background:#ff4444; margin-top:10px;">REJECT</button>
        </div>`;
      }
    });
  }

  window.manage = async (id, u, amt, type, status) => {
    if(status == 'approved'){
      const s = await get(ref(db, 'users/' + u));
      let nb = parseFloat(s.val().balance);
      nb = (type=='Deposit')? nb + parseFloat(amt) : nb - parseFloat(amt);
      await update(ref(db, 'users/' + u), { balance: nb });
    }
    await update(ref(db, 'history/' + u + '/' + id), { status: status });
    await remove(ref(db, 'requests/' + id));
    alert("Action Completed!");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById(id).classList.remove('hidden');
    if(el) el.classList.add('active');
  };
  window.doLogout = () => { localStorage.clear(); location.reload(); };
</script>
</body>
</html>
