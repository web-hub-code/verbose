<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions Elite</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; --glass:rgba(255,255,255,0.04); }
  *{box-sizing:border-box; transition: 0.3s; -webkit-tap-highlight-color: transparent;}
  body { margin:0; font-family:'Segoe UI', sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
  header { text-align:center; padding:35px 20px; font-size:35px; font-weight:900; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; text-transform:uppercase; letter-spacing:5px; }
  
  .page { max-width:420px; margin:15px auto 100px; background:var(--glass); padding:25px; border-radius:25px; border:1px solid rgba(0,255,240,0.1); backdrop-filter: blur(15px); }
  .user-card { background:linear-gradient(135deg, rgba(0,247,255,0.1), rgba(255,92,255,0.05)); padding:18px; border-radius:18px; margin-bottom:15px; border-left:5px solid var(--neon); }
  
  /* Broadcast News Style */
  #newsTicker { background: rgba(255, 68, 68, 0.2); color: #ff8888; padding: 10px; font-size: 12px; font-weight: bold; border-radius: 10px; margin-bottom: 15px; border: 1px solid #ff4444; }

  input, select { width:100%; padding:14px; margin-top:12px; border-radius:12px; border:1px solid rgba(255,255,255,0.1); background:rgba(0,0,0,0.5); color:#fff; font-size:14px; }
  button { width:100%; padding:15px; margin-top:18px; border-radius:12px; border:none; background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:800; cursor:pointer; }
  
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(10,10,12,0.98); display:flex; justify-content:space-around; padding:18px; border-top:1px solid rgba(0,255,240,0.15); z-index:1000; }
  .nav-item { text-align:center; font-size:10px; cursor:pointer; opacity:0.6; color:#fff; flex:1; }
  .nav-item.active { opacity:1; color:var(--neon); font-weight:bold; }
  
  .status-tag { font-size:10px; padding:2px 8px; border-radius:10px; float:right; font-weight:bold; }
  .pending { background: #ffa500; color: #000; }
  .approved { background: #00ff88; color: #000; }
  .rejected { background: #ff4444; color: #fff; }
  .hidden { display:none; }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center;">Secure Portal</h2>
  <input id="u_name" type="text" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn">ACCESS ACCOUNT</button>
</div>

<div id="dashboard" class="page hidden">
  <div id="newsTicker" class="hidden"><marquee id="newsText">Welcome to Verbose Prime!</marquee></div>

  <div class="user-card">
    <div id="welcomeMsg" style="opacity:0.8;">Hello, User</div>
    <div style="font-size:32px; font-weight:900; margin:10px 0;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:11px; color:var(--neon);">WITHDRAWABLE BALANCE</div>
  </div>

  <div class="user-card" style="border-left-color: #fff;">
    <p style="font-size:11px; margin:0;">Have a Promo Code?</p>
    <div style="display:flex; gap:10px;">
      <input id="promoInput" placeholder="Enter Code" style="margin-top:8px; flex:2;">
      <button onclick="applyPromo()" style="margin-top:8px; flex:1; padding:10px; font-size:10px;">APPLY</button>
    </div>
  </div>

  <h3 style="margin:20px 0 10px 0; font-size:16px;">Transaction History</h3>
  <div id="historyList"></div>
</div>

<div id="walletPage" class="page hidden">
  <div class="user-card" style="font-size:12px; background:rgba(0,0,0,0.4);">
    <b>JazzCash/SadaPay:</b> 03705519562<br>
    <b>EasyPaisa:</b> 03379827882<br>
    <small>Owner: Muhammad Nazim</small>
  </div>
  <input id="d_amount" type="number" placeholder="Amount">
  <input id="d_tid" placeholder="TID Number">
  <input id="d_proof" placeholder="Proof (Screenshot link or Detail)">
  <button onclick="submitReq('Deposit')">DEPOSIT FUNDS</button>
  <hr style="opacity:0.1; margin:25px 0;">
  <input id="w_amount" type="number" placeholder="Withdraw Amount">
  <input id="w_phone" placeholder="Account Number">
  <button onclick="submitReq('Withdraw')" style="background:var(--accent)">REQUEST WITHDRAW</button>
</div>

<div id="adminPage" class="page hidden" style="border: 2px dashed var(--accent);">
  <h2 style="text-align:center; color:var(--accent);">⚡ GOD MODE ⚡</h2>
  
  <div class="user-card" style="background:#111;">
    <p style="font-size:11px;">Broadcast Message to All:</p>
    <input id="adminMsg" placeholder="Type News Here...">
    <button onclick="sendBroadcast()" class="btn-sm" style="padding:10px;">SEND BROADCAST</button>
  </div>

  <div id="adminRequests"></div>
  
  <hr style="opacity:0.1; margin:20px 0;">
  <input id="searchUser" placeholder="Username">
  <button id="findBtn">Search User</button>
  <div id="editBox" class="hidden">
    <input id="setBal" type="number">
    <button id="saveBtn">Update Balance</button>
  </div>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">🏠<br>Home</div>
  <div class="nav-item" onclick="tab('walletPage', this)">💰<br>Wallet</div>
  <div class="nav-item" onclick="doLogout()">🚪<br>Exit</div>
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
    if(!user || !pass) return alert("Fill fields!");

    const userRef = ref(db, 'users/' + user);
    const snap = await get(userRef);
    if(snap.exists()){
      if(snap.val().password === pass) init(user, snap.val());
      else alert("Wrong pass!");
    } else {
      const d = { username:user, password:pass, balance:0 };
      await set(userRef, d);
      init(user, d);
    }
  };

  function init(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');

    onValue(ref(db, 'users/' + u), snap => {
      document.getElementById('mainBal').innerText = parseFloat(snap.val().balance).toFixed(2);
    });

    // Load History & Broadcast
    loadHistory(u);
    loadBroadcast();
    listenAdmin();
  }

  // --- BROADCAST SYSTEM ---
  function loadBroadcast() {
    onValue(ref(db, 'broadcast'), snap => {
      if(snap.exists()) {
        document.getElementById('newsTicker').classList.remove('hidden');
        document.getElementById('newsText').innerText = snap.val().msg;
      }
    });
  }
  window.sendBroadcast = () => {
    const msg = document.getElementById('adminMsg').value;
    set(ref(db, 'broadcast'), { msg: msg });
    alert("News Sent!");
  };

  // --- HISTORY & PROMO ---
  function loadHistory(u) {
    onValue(ref(db, 'history/' + u), snap => {
      const cont = document.getElementById('historyList');
      cont.innerHTML = "";
      const data = snap.val();
      for(let id in data) {
        const h = data[id];
        cont.innerHTML += `<div class="user-card" style="font-size:12px; border-left-color:${h.type==='Deposit'?'var(--neon)':'var(--accent)'}">
          <span class="status-tag ${h.status}">${h.status}</span>
          <b>${h.type}</b>: Rs ${h.amount}<br><small>${h.time}</small>
        </div>`;
      }
    });
  }

  window.applyPromo = async () => {
    const code = document.getElementById('promoInput').value.trim();
    const u = localStorage.getItem('v_user');
    const s = await get(ref(db, 'promos/' + code));
    if(s.exists() && !s.val().usedBy?.[u]) {
      const reward = parseFloat(s.val().amount);
      const userRef = ref(db, 'users/' + u);
      const userSnap = await get(userRef);
      await update(userRef, { balance: parseFloat(userSnap.val().balance) + reward });
      await update(ref(db, 'promos/' + code + '/usedBy'), { [u]: true });
      alert("Promo Applied! Rs " + reward + " added.");
    } else { alert("Invalid or already used code!"); }
  };

  // --- FINANCE REQUESTS ---
  window.submitReq = (type) => {
    const u = localStorage.getItem('v_user');
    const amt = (type === 'Deposit') ? document.getElementById('d_amount').value : document.getElementById('w_amount').value;
    const tid = document.getElementById('d_tid').value || 'N/A';
    if(!amt) return alert("Enter amount!");

    const key = Date.now();
    const req = { user:u, amount:amt, tid:tid, type:type, status:'pending', time:new Date().toLocaleString() };
    set(ref(db, 'requests/' + key), req);
    set(ref(db, 'history/' + u + '/' + key), req);
    alert("Request Submitted!");
  };

  // --- ADMIN GOD ---
  let tap = 0;
  document.getElementById('mainHeader').onclick = () => {
    if(++tap === 7) {
      if(prompt("Admin Key:") === "prime786") {
        document.getElementById('adminNav').classList.remove('hidden');
        tab('adminPage');
      }
      tap = 0;
    }
  };

  function listenAdmin() {
    onValue(ref(db, 'requests'), snap => {
      const cont = document.getElementById('adminRequests');
      cont.innerHTML = "<h3>Pending</h3>";
      const data = snap.val();
      for(let id in data) {
        const r = data[id];
        cont.innerHTML += `<div class="user-card" style="font-size:11px;">
          ${r.user} | ${r.type}: ${r.amount}<br>TID: ${r.tid}<br>
          <button onclick="manage('${id}','${r.user}',${r.amount},'${r.type}','approved')" style="width:45%; font-size:10px;">Approve</button>
          <button onclick="manage('${id}','${r.user}',${r.amount},'${r.type}','rejected')" style="width:45%; font-size:10px; background:#ff4444;">Reject</button>
        </div>`;
      }
    });
  }

  window.manage = async (id, u, amt, type, status) => {
    if(status === 'approved') {
      const s = await get(ref(db, 'users/' + u));
      let nb = parseFloat(s.val().balance);
      nb = (type === 'Deposit') ? nb + parseFloat(amt) : nb - parseFloat(amt);
      await update(ref(db, 'users/' + u), { balance: nb });
    }
    await update(ref(db, 'history/' + u + '/' + id), { status: status });
    await remove(ref(db, 'requests/' + id));
    alert("Updated!");
  };

  // HELPERS
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
