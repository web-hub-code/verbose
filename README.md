<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions Ultimate</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { 
    --neon: #00f7ff; --accent: #ff5cff; --dark: #050505; --glass: rgba(255,255,255,0.05); --text: #fff; 
  }
  .light-mode {
    --dark: #f0f2f5; --glass: rgba(0,0,0,0.05); --text: #222; 
  }
  
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Poppins', sans-serif; -webkit-tap-highlight-color: transparent; }
  body { margin:0; background: var(--dark); color: var(--text); overflow-x: hidden; }
  
  header { text-align: center; padding: 30px 20px; font-size: 32px; font-weight: 800; background: linear-gradient(90deg, var(--neon), var(--accent)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; letter-spacing: 5px; cursor: pointer; }
  
  .page { max-width: 420px; margin: 10px auto 100px; background: var(--glass); padding: 25px; border-radius: 30px; border: 1px solid rgba(0,255,240,0.1); backdrop-filter: blur(15px); min-height: 500px; }
  
  .user-card { background: linear-gradient(135deg, rgba(0,247,255,0.1), rgba(255,92,255,0.05)); padding: 20px; border-radius: 20px; margin-bottom: 15px; border-left: 5px solid var(--neon); box-shadow: 0 10px 20px rgba(0,0,0,0.2); }
  
  input, select { width: 100%; padding: 14px; margin-top: 10px; border-radius: 12px; border: 1px solid rgba(255,255,255,0.1); background: rgba(0,0,0,0.4); color: #fff; font-size: 14px; }
  .light-mode input { background: #fff; color: #000; border: 1px solid #ddd; }
  
  button { width: 100%; padding: 15px; margin-top: 15px; border-radius: 12px; border: none; background: linear-gradient(90deg, var(--neon), var(--accent)); color: #000; font-weight: 800; cursor: pointer; box-shadow: 0 5px 15px rgba(0,247,255,0.3); }
  
  .nav { position: fixed; bottom: 0; left: 0; right: 0; background: rgba(10,10,12,0.95); display: flex; justify-content: space-around; padding: 15px; z-index: 1000; border-top: 1px solid rgba(255,255,255,0.05); }
  .nav-item { text-align: center; font-size: 10px; cursor: pointer; opacity: 0.5; color: #fff; flex:1; }
  .nav-item.active { opacity: 1; color: var(--neon); transform: translateY(-5px); }

  #newsTicker { background: rgba(255, 68, 68, 0.15); color: #ff8888; padding: 10px; font-size: 12px; border-radius: 10px; margin-bottom: 15px; border: 1px solid rgba(255,68,68,0.2); }
  .status-tag { font-size: 10px; padding: 2px 8px; border-radius: 10px; float: right; font-weight: bold; text-transform: uppercase; }
  .approved { background: #00ff88; color: #000; } .pending { background: #ffa500; color: #000; } .rejected { background: #ff4444; color: #fff; }
  
  .theme-toggle { position: absolute; top: 20px; right: 20px; cursor: pointer; font-size: 20px; }
  .hidden { display: none; }
  .btn-sm { padding: 8px; font-size: 10px; margin-top: 5px; }
</style>
</head>
<body>

<div class="theme-toggle" onclick="toggleTheme()">🌓</div>
<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center;">Elite Access</h2>
  <input id="u_name" type="text" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn">SIGN IN / JOIN</button>
</div>

<div id="dashboard" class="page hidden">
  <div id="newsTicker" class="hidden"><marquee id="newsText">Welcome to Verbose Prime Solutions!</marquee></div>
  <div class="user-card">
    <div id="welcomeMsg" style="opacity:0.7; font-size:12px;">Welcome back</div>
    <div style="font-size:32px; font-weight:900; margin:10px 0;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:10px; color:var(--neon); letter-spacing:1px; font-weight:bold;">AVAILABLE BALANCE</div>
  </div>
  <div class="user-card" style="border-left-color: #fff;">
    <p style="font-size:11px; margin:0;">Daily Rewards Code:</p>
    <div style="display:flex; gap:8px;">
      <input id="promoInput" placeholder="Code" style="margin:0; flex:2;">
      <button onclick="applyPromo()" style="margin:0; flex:1; padding:10px; font-size:10px;">APPLY</button>
    </div>
  </div>
</div>

<div id="plansPage" class="page hidden">
  <h3 style="color:var(--neon); margin:0;">Investment Plans</h3>
  <p style="font-size:10px; opacity:0.6; margin-bottom:15px;">Profit credited every 24 hours.</p>
  <div id="plansList"></div>
</div>

<div id="historyPage" class="page hidden">
  <h3 style="color:var(--neon); margin:0;">Transaction History</h3>
  <div id="userHistoryList" style="margin-top:15px;"></div>
</div>

<div id="walletPage" class="page hidden">
  <div class="user-card" style="font-size:12px; background:rgba(0,0,0,0.5);">
    <b>JazzCash/SadaPay:</b> 03705519562<br>
    <b>EasyPaisa:</b> 03379827882<br>
    <small>Owner: Muhammad Nazim</small>
  </div>
  <input id="d_amount" type="number" placeholder="Deposit Amount">
  <input id="d_tid" placeholder="TID (Transaction ID)">
  <input id="d_proof" placeholder="Proof (Link/Detail)">
  <button onclick="submitReq('Deposit')">DEPOSIT FUNDS</button>
  <hr style="opacity:0.1; margin:25px 0;">
  <input id="w_amount" type="number" placeholder="Withdraw Amount">
  <input id="w_phone" placeholder="Account Number">
  <button onclick="submitReq('Withdraw')" style="background:var(--accent)">REQUEST PAYOUT</button>
</div>

<div id="adminPage" class="page hidden" style="border: 2px dashed var(--accent);">
  <h2 style="text-align:center; color:var(--accent);">👑 EMPEROR MODE</h2>
  <div class="user-card" style="background:#111;">
    <input id="adminMsg" placeholder="Global Announcement">
    <button onclick="sendBroadcast()" class="btn-sm">SEND NEWS</button>
  </div>
  <div class="user-card" style="background:#111; border-left-color: var(--neon);">
    <input id="searchUser" placeholder="Spy Username">
    <button onclick="inspectUser()" style="margin-top:5px;">INSPECT & SPY</button>
    <div id="userControlPanel" class="hidden" style="margin-top:10px; font-size:11px;">
       <p id="targetInfo"></p>
       <input id="newBalVal" type="number" placeholder="Set Balance">
       <button onclick="forceUpdateBal()" class="btn-sm">UPDATE BALANCE</button>
       <button onclick="banUser()" class="btn-sm" style="background:#ff4444;">BAN USER</button>
       <div id="spyHistory" style="margin-top:10px; max-height:100px; overflow:auto;"></div>
    </div>
  </div>
  <div id="adminRequests"></div>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">🏠<br>Home</div>
  <div class="nav-item" onclick="tab('plansPage', this)">📦<br>Plans</div>
  <div class="nav-item" onclick="tab('historyPage', this)">📜<br>History</div>
  <div class="nav-item" onclick="tab('walletPage', this)">💰<br>Wallet</div>
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

  // AUTH SYSTEM
  document.getElementById('entryBtn').onclick = async () => {
    const u = document.getElementById('u_name').value.trim().toLowerCase();
    const p = document.getElementById('u_pass').value.trim();
    if(!u || !p) return alert("Fill all details!");
    const userRef = ref(db, 'users/' + u);
    const snap = await get(userRef);
    if(snap.exists()){
      if(snap.val().isBanned) return alert("Account BANNED!");
      if(snap.val().password === p) initApp(u); else alert("Wrong Pass!");
    } else {
      await set(userRef, { username:u, password:p, balance:0, isBanned: false });
      initApp(u);
    }
  };

  function initApp(u) {
    localStorage.setItem('v_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    tab('dashboard');
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    
    onValue(ref(db, 'users/' + u), s => {
      document.getElementById('mainBal').innerText = parseFloat(s.val().balance).toFixed(2);
    });
    
    renderPlans();
    loadNews();
    listenAdmin();
  }

  // PLANS SYSTEM
  function renderPlans() {
    const cont = document.getElementById('plansList'); cont.innerHTML = "";
    for(let i=1; i<=25; i++) {
      let cost = (i<=20) ? 200 + (i-1)*1000 : 25000 + (i-21)*15000;
      let daily = (i<=20) ? Math.round(cost*0.1) : Math.round(cost*0.18);
      cont.innerHTML += `<div class="user-card" style="border-left-color:${i>20?'var(--accent)':'var(--neon)'}">
        <b>Level ${i} Plan</b><br>Cost: Rs ${cost} | Daily: Rs ${daily}<br>
        <button class="btn-sm" onclick="alert('Contact Admin to Activate or Deposit First!')">Activate</button>
      </div>`;
    }
  }

  // HISTORY & SPY
  function loadHistory(u) {
    onValue(ref(db, 'history/' + u), snap => {
      const cont = document.getElementById('userHistoryList'); cont.innerHTML = "";
      const data = snap.val();
      for(let id in data) {
        cont.innerHTML += `<div class="user-card" style="font-size:11px;">
          <span class="status-tag ${data[id].status}">${data[id].status}</span>
          <b>${data[id].type}</b>: Rs ${data[id].amount}<br><small>${data[id].time}</small>
        </div>`;
      }
    });
  }

  // ADMIN POWERS
  window.inspectUser = async () => {
    const target = document.getElementById('searchUser').value.trim().toLowerCase();
    const s = await get(ref(db, 'users/' + target));
    if(s.exists()){
      document.getElementById('userControlPanel').classList.remove('hidden');
      document.getElementById('targetInfo').innerText = target + " | Balance: " + s.val().balance;
      const hSnap = await get(ref(db, 'history/' + target));
      document.getElementById('spyHistory').innerHTML = hSnap.exists() ? "History Loaded Below" : "No history";
    }
  };

  window.forceUpdateBal = async () => {
    const target = document.getElementById('searchUser').value.trim().toLowerCase();
    const val = document.getElementById('newBalVal').value;
    await update(ref(db, 'users/' + target), { balance: parseFloat(val) });
    alert("Updated!");
  };

  window.sendBroadcast = () => {
    const m = document.getElementById('adminMsg').value;
    set(ref(db, 'broadcast'), { msg: m });
    alert("News Sent!");
  };

  function loadNews() {
    onValue(ref(db, 'broadcast'), s => {
      if(s.exists()){
        document.getElementById('newsTicker').classList.remove('hidden');
        document.getElementById('newsText').innerText = s.val().msg;
      }
    });
  }

  // FINANCE
  window.submitReq = (type) => {
    const u = localStorage.getItem('v_user');
    const amt = (type=='Deposit')? document.getElementById('d_amount').value : document.getElementById('w_amount').value;
    if(!amt) return alert("Enter Amount!");
    const key = Date.now();
    const r = { user:u, amount:amt, type:type, status:'pending', time:new Date().toLocaleString(), tid: document.getElementById('d_tid').value || 'N/A' };
    set(ref(db, 'requests/' + key), r);
    set(ref(db, 'history/' + u + '/' + key), r);
    alert("Request Sent!");
  };

  function listenAdmin() {
    onValue(ref(db, 'requests'), s => {
      const cont = document.getElementById('adminRequests'); cont.innerHTML = "<h3>Pending</h3>";
      const data = s.val();
      for(let id in data){
        const r = data[id];
        cont.innerHTML += `<div class="user-card" style="font-size:11px;">
          ${r.user} | ${r.type}: ${r.amount}<br>
          <button onclick="manage('${id}','${r.user}',${r.amount},'${r.type}','approved')">Approve</button>
          <button onclick="manage('${id}','${r.user}',${r.amount},'${r.type}','rejected')" style="background:red; color:white;">Reject</button>
        </div>`;
      }
    });
  }

  window.manage = async (id, u, amt, type, status) => {
    if(status == 'approved'){
      const s = await get(ref(db, 'users/' + u));
      let nb = (type=='Deposit')? parseFloat(s.val().balance) + parseFloat(amt) : parseFloat(s.val().balance) - parseFloat(amt);
      await update(ref(db, 'users/' + u), { balance: nb });
    }
    await update(ref(db, 'history/' + u + '/' + id), { status: status });
    await remove(ref(db, 'requests/' + id));
    alert("Done!");
  };

  // HELPERS
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById(id).classList.remove('hidden');
    if(el) el.classList.add('active');
    if(id === 'historyPage') loadHistory(localStorage.getItem('v_user'));
  };

  window.toggleTheme = () => document.body.classList.toggle('light-mode');
  window.doLogout = () => { localStorage.clear(); location.reload(); };

  let t = 0; document.getElementById('mainHeader').onclick = () => { if(++t===7){ document.getElementById('adminNav').classList.remove('hidden'); tab('adminPage'); t=0; } };
</script>
</body>
</html>
