<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Autonomous Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.05); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* AUTH SCREEN */
  #authOverlay { position: fixed; inset: 0; background: var(--bg); z-index: 100000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); border-radius: 40px; padding: 40px; text-align: center; backdrop-filter: blur(20px); box-shadow: 0 20px 50px rgba(0,0,0,0.5); }

  /* HEADER */
  header { display: flex; align-items: center; padding: 65px 20px 15px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }

  /* PAGES */
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* UI CARDS */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 35px; border-radius: 40px; text-align: center; margin-bottom: 25px; }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 25px; margin-bottom: 15px; border-left: 4px solid var(--neon); position: relative; }
  
  /* INPUTS & BUTTONS */
  input { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; letter-spacing: 1px; }
  .btn-action:disabled { background: #222; cursor: not-allowed; opacity: 0.4; }

  /* PROGRESS BAR */
  .progress-container { background: rgba(255,255,255,0.05); height: 6px; border-radius: 10px; margin-top: 15px; overflow: hidden; }
  .progress-fill { height: 100%; background: var(--success); width: 0%; transition: 1s linear; box-shadow: 0 0 10px var(--success); }

  /* NAVIGATION */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div id="authOverlay">
    <div class="auth-card">
        <div class="logo-text" style="font-size:18px; margin-bottom:25px;">SECURE LOGIN</div>
        <input id="authPhone" type="number" placeholder="Phone Number">
        <input id="authPass" type="password" placeholder="Access PIN">
        <button class="btn-action" onclick="handleAuth()">INITIALIZE ACCESS</button>
        <p style="font-size:9px; opacity:0.5; margin-top:15px; letter-spacing:1px;">NEW USERS WILL BE REGISTERED AUTOMATICALLY</p>
    </div>
</div>

<header><div class="logo-text" id="adminTrigger">VERBOSE</div></header>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="uID" style="font-size:10px; opacity:0.6; letter-spacing:2px;">UID: ---</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>

    <div id="statusBox" style="background:rgba(0,255,136,0.05); border:1px solid var(--success); padding:25px; border-radius:30px; display:none;">
        <div style="display:flex; justify-content:space-between; align-items:center;">
            <div>
                <small style="color:var(--success); font-weight:800; letter-spacing:1px;">ACTIVE NODE</small>
                <div id="activeNameDisplay" style="font-size:18px; font-weight:800;">NONE</div>
            </div>
            <div id="timerDisplay" style="font-size:22px; font-weight:800; color:var(--success); font-variant-numeric: tabular-nums;">24:00:00</div>
        </div>
        <div class="progress-container"><div id="pFill" class="progress-fill"></div></div>
        <small style="font-size:9px; opacity:0.5; display:block; margin-top:10px;">NEXT PROFIT DISTRIBUTION IN PROGRESS</small>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">INVESTMENT NODES</h3>
    <div id="nodeGrid"></div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center;">ADMIN COMMAND HUD</h2>
    <div class="node-card" style="border-color:var(--gold);">
        <input id="admT" placeholder="User Phone Number">
        <input id="admV" type="number" placeholder="Adjustment Amount (+/-)">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="adminSync()">UPDATE DATABASE</button>
    </div>
</div>

<nav class="nav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="logout()">Logout</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, update, onValue, get, set } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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

  const nodeData = [
    {n:"Starter Core", p:500, d:55},
    {n:"Advanced Pulse", p:1000, d:125},
    {n:"Enterprise Link", p:2500, d:320},
    {n:"Quantum Node", p:5000, d:700}
  ];

  // --- AUTH SYSTEM ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value, s = document.getElementById('authPass').value;
    if(!p || !s) return alert("Required fields missing");
    const snap = await get(ref(db, `users/${p}`));
    if(snap.exists()) {
        if(snap.val().pass === s) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("Incorrect Access PIN");
    } else {
        await set(ref(db, `users/${p}`), { name:"User", pass:s, balance:0, daily:0, hasActive:false });
        localStorage.setItem('v_user', p); location.reload();
    }
  };

  // --- ENGINE LOGIC ---
  const runEngine = (data) => {
    if(!data.hasActive) {
        document.getElementById('statusBox').style.display = 'none';
        return;
    }
    document.getElementById('statusBox').style.display = 'block';
    document.getElementById('activeNameDisplay').innerText = data.activeName;

    const now = Date.now();
    const lastProfit = data.lastProfitTime || data.startTime;
    const nextProfit = lastProfit + (24 * 60 * 60 * 1000); // 24 Hours cycle
    const timeLeft = nextProfit - now;

    if(timeLeft <= 0) {
        // AUTO PROFIT TRIGGER
        update(ref(db, `users/${user}`), { 
            balance: (data.balance || 0) + data.daily, 
            lastProfitTime: now 
        });
    } else {
        // UI UPDATE
        let h = Math.floor(timeLeft/3600000).toString().padStart(2,'0');
        let m = Math.floor((timeLeft%3600000)/60000).toString().padStart(2,'0');
        let s = Math.floor((timeLeft%60000)/1000).toString().padStart(2,'0');
        document.getElementById('timerDisplay').innerText = `${h}:${m}:${s}`;
        document.getElementById('pFill').style.width = `${((86400000 - timeLeft)/86400000)*100}%`;
    }
  };

  const renderNodes = (hasActive) => {
    const grid = document.getElementById('nodeGrid');
    grid.innerHTML = "";
    nodeData.forEach(x => {
        grid.innerHTML += `<div class="node-card">
            <b>${x.n}</b><br><small>Daily Yield: PKR ${x.d}</small><br>
            <button class="btn-action" ${hasActive ? 'disabled' : ''} onclick="buyNode(${x.p}, ${x.d}, '${x.n}')">
                ${hasActive ? 'ACTIVE PLAN LIMIT' : 'ACTIVATE PKR ' + x.p}
            </button>
        </div>`;
    });
  };

  window.buyNode = async (price, daily, name) => {
    const snap = await get(ref(db, `users/${user}`));
    if(snap.val().balance < price) return alert("Insufficient Balance");
    const startTime = Date.now();
    await update(ref(db, `users/${user}`), {
        balance: snap.val().balance - price,
        daily: daily,
        hasActive: true,
        activeName: name,
        startTime: startTime,
        lastProfitTime: startTime
    });
    alert("Node Activated Successfully");
  };

  // --- ADMIN SYSTEM ---
  let cCount = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++cCount >= 7) { if(prompt("Passcode?")==="nazim786") tab('adminPage'); cCount=0; } };
  window.adminSync = async () => {
    const t = document.getElementById('admT').value, v = Number(document.getElementById('admV').value);
    const s = await get(ref(db, `users/${t}`));
    if(s.exists()) await update(ref(db, `users/${t}`), { balance: (s.val().balance || 0) + v });
    alert("User data synchronized");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authOverlay').style.display = 'none';
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uID').innerText = "UID: " + user;
        renderNodes(d.hasActive);
        runEngine(d);
    });
    // Engine Tick
    setInterval(() => { get(ref(db, `users/${user}`)).then(s => runEngine(s.val())); }, 1000);
  }
</script>
</body>
</html>
