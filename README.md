<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Enterprise Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.05); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* AUTH MODAL */
  #authOverlay { position: fixed; inset: 0; background: var(--bg); z-index: 100000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); border-radius: 40px; padding: 40px; backdrop-filter: blur(20px); text-align: center; }
  .auth-toggle { display: flex; background: rgba(255,255,255,0.05); border-radius: 20px; margin-bottom: 25px; padding: 5px; }
  .auth-btn { flex: 1; padding: 12px; border-radius: 15px; cursor: pointer; font-size: 12px; font-weight: 800; border: none; background: transparent; color: #fff; opacity: 0.5; }
  .auth-btn.active { background: var(--neon); color: #000; opacity: 1; }

  /* HEADER & DRAWER */
  header { display: flex; align-items: center; padding: 65px 20px 15px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .menu-btn { position: absolute; left: 20px; font-size: 24px; cursor: pointer; color: var(--neon); top: 68px; }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }

  .drawer { position: fixed; top: 0; left: -100%; width: 280px; height: 100%; background: rgba(10,10,10,0.98); backdrop-filter: blur(25px); z-index: 50000; border-right: 1px solid var(--border); padding: 40px 20px; }
  .drawer.open { left: 0; }
  .drawer-item { padding: 18px; border-radius: 15px; margin-bottom: 10px; background: var(--card); font-size: 11px; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 15px; text-transform: uppercase; }

  /* PAGES */
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* CARDS */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 35px; border-radius: 40px; text-align: center; margin-bottom: 25px; }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; border-left: 4px solid var(--neon); }
  
  /* INPUTS */
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; }

  /* ADMIN HUD EXCLUSIVE */
  .admin-req-card { background: #111; border: 1px solid var(--gold); border-radius: 20px; padding: 15px; margin-bottom: 10px; font-size: 11px; }

  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div id="authOverlay">
    <div class="auth-card">
        <div class="logo-text" style="font-size:20px; margin-bottom:30px;">VERBOSE</div>
        <div class="auth-toggle">
            <div id="tglLog" class="auth-btn active" onclick="setAuthMode('login')">LOGIN</div>
            <div id="tglSign" class="auth-btn" onclick="setAuthMode('signup')">SIGNUP</div>
        </div>
        <input id="authPhone" type="number" placeholder="Mobile Number">
        <input id="authName" placeholder="Full Name (Signup Only)" style="display:none;">
        <input id="authPass" type="password" placeholder="Cloud Security Pin">
        <button class="btn-action" onclick="handleAuth()">CONTINUE ACCESS</button>
    </div>
</div>

<header>
    <div class="menu-btn" onclick="toggleMenu()">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
</header>

<div class="drawer" id="drawer">
    <div class="logo-text" style="font-size:16px; margin-bottom:40px; text-align:center;">MENU</div>
    <div class="drawer-item" onclick="tab('dash'); toggleMenu()">Dashboard</div>
    <div class="drawer-item" onclick="tab('teamPage'); toggleMenu()">My Team</div>
    <div class="drawer-item" onclick="tab('promoPage'); toggleMenu()">Promo Code</div>
    <div class="drawer-item" style="margin-top:50px; color:var(--error);" onclick="logout()">Logout</div>
</div>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="dispUser" style="font-size:10px; letter-spacing:2px; opacity:0.6;">LOADING...</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div style="background:rgba(112,0,255,0.08); border:1px dashed var(--accent); padding:20px; border-radius:25px; text-align:center;">
        <div id="timer" style="font-size:26px; font-weight:800; color:var(--accent);">23:59:59</div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px;">MINING NODES</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3>DEPOSIT</h3>
        <p style="font-size:11px;">JazzCash: 03705519562 | EasyPaisa: 03379827882</p>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="TID">
        <button class="btn-action" onclick="submitDeposit()">Submit Deposit</button>
    </div>
</div>

<div id="withdrawPage" class="page">
    <div class="node-card" style="border-color:var(--error);">
        <h3>WITHDRAW</h3>
        <input id="wNum" type="number" placeholder="Account Number">
        <input id="wAmt" type="number" placeholder="Amount (Min 500)">
        <button class="btn-action" style="background:var(--error);" onclick="submitWithdraw()">Withdraw Now</button>
    </div>
</div>

<div id="promoPage" class="page">
    <div class="node-card" style="border-color:var(--gold);">
        <h3>PROMO CODE</h3>
        <input id="pCode" placeholder="Enter Code">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="submitPromo()">Claim Bonus</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center;">ADMIN CONTROL HUD</h2>
    <div id="adminDataList">
        <p style="font-size:10px; opacity:0.5;">Fetching live data requests...</p>
    </div>
    <hr style="opacity:0.1; margin:20px 0;">
    <div class="node-card">
        <small>QUICK UPDATE USER</small>
        <input id="admTarg" placeholder="User Phone">
        <input id="admBal" type="number" placeholder="Add Amount">
        <button class="btn-action" onclick="godUpdate()">SYNC DATA</button>
    </div>
</div>

<nav class="nav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Deposit</div>
    <div class="nav-item" onclick="tab('withdrawPage', this)">Payout</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, update, onValue, push, get, set } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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
  let authMode = 'login';

  // --- AUTH LOGIC ---
  window.setAuthMode = (m) => {
    authMode = m;
    document.getElementById('authName').style.display = m === 'signup' ? 'block' : 'none';
    document.getElementById('tglLog').classList.toggle('active', m === 'login');
    document.getElementById('tglSign').classList.toggle('active', m === 'signup');
  };

  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value, s = document.getElementById('authPass').value, n = document.getElementById('authName').value;
    if(!p || !s) return alert("Fill all fields");
    const uRef = ref(db, `users/${p}`);
    const snap = await get(uRef);
    if(authMode === 'login') {
        if(snap.exists() && snap.val().pass === s) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("Invalid Credentials");
    } else {
        if(snap.exists()) return alert("User already exists");
        await set(uRef, { name: n, pass: s, balance: 0, daily: 0, total: 0 });
        localStorage.setItem('v_user', p); location.reload();
    }
  };

  // --- NODES ---
  const nodeArr = [{n:"Alpha", p:500, d:50}, {n:"Beta", p:1000, d:110}, {n:"Gamma", p:2500, d:300}, {n:"Delta", p:5000, d:650}];
  nodeArr.forEach(x => {
    document.getElementById('nodeGrid').innerHTML += `<div class="node-card"><b>${x.n} Node</b> | PKR ${x.p}<br><button class="btn-action" style="padding:10px; font-size:10px;" onclick="buyNode(${x.p}, ${x.d})">Activate</button></div>`;
  });

  window.buyNode = async (p, d) => {
    const snap = await get(ref(db, `users/${user}`));
    if(snap.val().balance < p) return alert("Low balance");
    await update(ref(db, `users/${user}`), { balance: snap.val().balance - p, daily: d });
    alert("Node Active");
  };

  // --- ADMIN LIVE SYNC ---
  window.loadAdminData = () => {
    onValue(ref(db, `admin/requests`), s => {
        const list = document.getElementById('adminDataList');
        list.innerHTML = "";
        if(s.exists()) {
            Object.entries(s.val()).reverse().forEach(([key, val]) => {
                list.innerHTML += `<div class="admin-req-card">
                    <b>TYPE: ${val.type}</b> | ID: ${val.user}<br>
                    AMT: ${val.amt} | TID/ACC: ${val.tid || val.acc}<br>
                    <small>${val.status}</small>
                </div>`;
            });
        }
    });
  };

  window.submitDeposit = () => push(ref(db, `admin/requests`), { user, type:"Deposit", amt: document.getElementById('dAmt').value, tid: document.getElementById('dTID').value, status: "Pending" });
  window.submitWithdraw = () => push(ref(db, `admin/requests`), { user, type:"Withdraw", amt: document.getElementById('wAmt').value, acc: document.getElementById('wNum').value, status: "Pending" });
  window.submitPromo = () => push(ref(db, `admin/requests`), { user, type:"Promo", code: document.getElementById('pCode').value, status: "Pending" });

  // --- ADMIN ACCESS ---
  let clks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clks >= 7) { if(prompt("Key?")==="nazim786") { tab('adminPage'); loadAdminData(); } clks=0; } };
  window.godUpdate = async () => {
    const t = document.getElementById('admTarg').value, v = Number(document.getElementById('admBal').value);
    const snap = await get(ref(db, `users/${t}`));
    if(snap.exists()) await update(ref(db, `users/${t}`), { balance: (snap.val().balance || 0) + v });
    alert("Database Updated");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authOverlay').style.display = 'none';
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('dispUser').innerText = "ID: " + user + " | " + d.name.toUpperCase();
    });
  }
</script>
</body>
</html>
