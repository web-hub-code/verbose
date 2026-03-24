<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Cloud Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.04); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* OVERLAYS */
  .overlay { position: fixed; inset: 0; background: var(--bg); z-index: 20000; padding: 20px; display: flex; flex-direction: column; justify-content: center; align-items: center; }
  .glass-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 35px; border-radius: 40px; backdrop-filter: blur(25px); text-align: center; }
  
  /* HEADER & NAVIGATION */
  header { text-align: center; padding: 40px 20px 10px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 10px; text-shadow: 0 0 20px var(--neon); color: #fff; }
  .page { max-width: 450px; margin: 0 auto; padding: 10px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* HOME WALLET DESIGN */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 30px; border-radius: 35px; margin-bottom: 25px; box-shadow: 0 15px 35px rgba(0,247,255,0.1); position: relative; overflow: hidden; }
  .u-name { font-size: 14px; font-weight: 600; color: var(--neon); margin-bottom: 5px; display: block; letter-spacing: 1px; }
  .u-bal { font-size: 38px; font-weight: 800; color: #fff; }

  /* STATS & CARDS */
  .stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 25px; }
  .stat-card { background: var(--card); border: 1px solid var(--border); padding: 18px; border-radius: 25px; }
  .stat-card small { font-size: 9px; opacity: 0.5; text-transform: uppercase; }
  .stat-card div { font-size: 18px; font-weight: 700; margin-top: 5px; }

  /* NODES LISTING */
  .node-item { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 18px; display: flex; align-items: center; gap: 15px; margin-bottom: 12px; border-left: 4px solid var(--accent); }
  .node-icon { width: 50px; height: 50px; background: rgba(0,247,255,0.05); border: 1px solid var(--neon); border-radius: 18px; display: flex; align-items: center; justify-content: center; font-size: 22px; }
  .buy-btn { margin-left: auto; background: var(--neon); color: #000; border: none; padding: 10px 18px; border-radius: 14px; font-weight: 800; font-size: 10px; cursor: pointer; }

  /* INPUTS & BUTTONS */
  input { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; box-shadow: 0 5px 15px rgba(0,247,255,0.2); }

  /* BOTTOM NAV */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(25px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div id="authPage" class="overlay">
    <div class="glass-card">
        <div class="logo-text" style="font-size:24px;">VERBOSE</div>
        <p style="font-size:9px; opacity:0.4; letter-spacing:3px; margin: 10px 0 20px;">NYC CLOUD INFRASTRUCTURE</p>
        <input id="authName" placeholder="Full Name">
        <input id="authPhone" type="number" placeholder="Phone (Node ID)">
        <input id="authPass" type="password" placeholder="Access Key">
        <button class="btn-action" onclick="handleAuth()">INITIALIZE SYSTEM</button>
        <a href="https://wa.me/923705519562" style="display:block; margin-top:20px; font-size:10px; color:var(--success); text-decoration:none; font-weight:800;">⚡ FORGOT KEY? CHAT SUPPORT</a>
    </div>
</div>

<div id="adminModal" class="overlay" style="display:none; z-index:40000;">
    <div class="glass-card" style="border-color:var(--gold);">
        <h3 style="color:var(--gold);">ROOT ACCESS REQUIRED</h3>
        <input id="adminKey" type="password" placeholder="Enter Admin Key">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="verifyAdmin()">VERIFY ROOT</button>
        <button onclick="document.getElementById('adminModal').style.display='none'" style="background:none; border:none; color:var(--error); margin-top:15px; font-size:10px;">CANCEL</button>
    </div>
</div>

<header id="adminTrigger"><div class="logo-text">VERBOSE</div></header>

<div id="dash" class="page">
    <div class="wallet-box">
        <span class="u-name" id="dispUser">CONNECTING...</span>
        <div class="u-bal">PKR <span id="uBal">0.00</span></div>
    </div>
    <div class="stat-grid">
        <div class="stat-card"><small>Daily Yield</small><div id="uDaily">0.00</div></div>
        <div class="stat-card"><small>Total Mining</small><div id="uTotal">0.00</div></div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">CLOUD NODES (25 ONLINE)</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="stat-card" style="margin-bottom:20px; border-color:var(--success);">
        <h4>DEPOSIT</h4>
        <p style="font-size:10px; opacity:0.6;">JazzCash/SadaPay: 03705519562</p>
        <input id="dAmt" type="number" placeholder="Amount PKR">
        <input id="dTID" placeholder="TID Number">
        <button class="btn-action" onclick="alert('Transaction sent for verification!')">SUBMIT TID</button>
    </div>
    <div class="stat-card" style="border-color:var(--error);">
        <h4>WITHDRAWAL</h4>
        <input id="wAmt" type="number" placeholder="Amount PKR">
        <input id="wNum" placeholder="Account Number">
        <button class="btn-action" style="background:var(--error);" onclick="alert('Withdrawal Request Sent!')">REQUEST PAYOUT</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold);">ADMIN HUB</h2>
    <div class="stat-card" style="border-color:var(--gold);">
        <input id="tUser" placeholder="User Phone">
        <input id="nBal" type="number" placeholder="New Balance">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="adminUpdateBal()">SYNC BALANCE</button>
    </div>
    <button class="btn-action" style="background:var(--error);" onclick="location.reload()">EXIT ROOT</button>
</div>

<nav class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="logout()" style="color:var(--error);">Exit</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  let user = localStorage.getItem('v_user');

  // --- RENDER NODES ---
  const icons = ["📡", "🛰️", "🚀", "🧬", "💎", "⚡", "🌀"];
  const grid = document.getElementById('nodeGrid');
  for(let i=1; i<=25; i++) {
    grid.innerHTML += `
      <div class="node-item">
        <div class="node-icon">${icons[i % icons.length]}</div>
        <div class="node-info"><h4>Node v.${i}</h4><p>PKR ${500*i} | Yield ${50*i}/D</p></div>
        <button class="buy-btn" onclick="alert('Order queued!')">BUY</button>
      </div>`;
  }

  // --- AUTH ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value;
    const s = document.getElementById('authPass').value;
    const n = document.getElementById('authName').value;
    if(!p || !s) return alert("Fill credentials, sweetie!");

    const r = ref(db, `users/${p}`);
    const snap = await get(r);
    if(snap.exists()) {
        if(snap.val().pass === s) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("Wrong Key!");
    } else {
        if(!n) return alert("Enter name to register!");
        await set(r, { name: n, pass: s, balance: 0, daily: 0, total: 0 });
        localStorage.setItem('v_user', p); location.reload();
    }
  };

  // --- ADMIN LOGIC ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    if(++clicks >= 7) { document.getElementById('adminModal').style.display='flex'; clicks=0; }
  };
  window.verifyAdmin = () => {
    if(document.getElementById('adminKey').value === "nazim786") {
        document.getElementById('adminModal').style.display='none';
        tab('adminPage', null);
    } else alert("Invalid Root Key!");
  };
  window.adminUpdateBal = () => {
    update(ref(db, `users/${document.getElementById('tUser').value}`), { balance: Number(document.getElementById('nBal').value) });
    alert("Database Synced!");
  };

  // --- UI ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) {
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        el.classList.add('active');
    }
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

  // --- DATA SYNC ---
  if(user) {
    document.getElementById('authPage').style.display = 'none';
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        if(d) {
            document.getElementById('uBal').innerText = d.balance.toLocaleString();
            document.getElementById('uDaily').innerText = (d.daily || 0).toLocaleString();
            document.getElementById('uTotal').innerText = (d.total || 0).toLocaleString();
            document.getElementById('dispUser').innerText = "WELCOME, " + d.name.toUpperCase();
        }
    });
  }
</script>
</body>
</html>
