<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.05); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* UI COMPONENTS */
  header { display: flex; align-items: center; padding: 65px 20px 15px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; }

  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 25px; padding: 20px; margin-bottom: 15px; position: relative; }
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 35px; border-radius: 40px; text-align: center; margin-bottom: 25px; }

  /* ADMIN STYLES */
  .admin-list { max-height: 250px; overflow-y: auto; background: #000; border: 1px solid var(--border); border-radius: 20px; padding: 10px; margin-top: 10px; }
  .admin-item { background: #111; padding: 12px; border-radius: 15px; margin-bottom: 8px; font-size: 10px; border-left: 3px solid var(--gold); }
  .status-badge { font-size: 8px; padding: 2px 6px; border-radius: 5px; text-transform: uppercase; margin-left: 5px; }
  
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; }

  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  /* MAINTENANCE */
  #maintenance { position: fixed; inset: 0; background: #000; z-index: 999999; display: none; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
</style>
</head>
<body>

<div id="maintenance">
    <h1 style="color:var(--neon); letter-spacing:10px;">MAINTENANCE</h1>
    <p style="opacity:0.6;">SYSTEM UPGRADE IN PROGRESS. CHECK BACK LATER.</p>
</div>

<header><div class="logo-text" id="adminTrigger">VERBOSE</div></header>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="uNameDisplay" style="font-size:10px; opacity:0.6; letter-spacing:2px;">---</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div id="profitHUD" class="node-card" style="display:none; border-color:var(--success);">
        <div id="countdown" style="font-size:24px; font-weight:800; text-align:center;">24:00:00</div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="letter-spacing:1px;">MINING NODES</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3>DEPOSIT</h3>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="TID (Transaction ID)">
        <button class="btn-action" onclick="submitReq('Deposit')">Submit</button>
    </div>
    <div class="node-card" style="border-color:var(--error);">
        <h3>WITHDRAW</h3>
        <input id="wNum" type="number" placeholder="Account Number">
        <input id="wAmt" type="number" placeholder="Min 500">
        <button class="btn-action" style="background:var(--error);" onclick="submitReq('Withdraw')">Request</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center;">GOD MODE HUD</h2>
    
    <button class="btn-action" style="background:var(--error); margin-bottom:20px;" onclick="toggleMaintenance()">TOGGLE MAINTENANCE</button>

    <small style="color:var(--gold);">ALL REGISTERED USERS</small>
    <div class="admin-list" id="fullUserList"></div>

    <small style="color:var(--gold);">PENDING REQUESTS</small>
    <div class="admin-list" id="pendingReqList"></div>

    <div class="node-card" style="border-color:var(--gold);">
        <small>CREATE PROMO CODE</small>
        <input id="newPCode" placeholder="CODE123">
        <input id="newPVal" type="number" placeholder="Value (PKR)">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="createPromo()">GENERATE CODE</button>
    </div>
</div>

<nav class="nav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Finance</div>
    <div class="nav-item" onclick="logout()">Logout</div>
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

  // --- GOD MODE CORE ---
  let c = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++c >= 7) { if(prompt("Key?")==="nazim786") { tab('adminPage'); loadAdminData(); } c=0; } };

  const loadAdminData = () => {
    // Users List
    onValue(ref(db, `users`), s => {
        const div = document.getElementById('fullUserList'); div.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).forEach(([num, d]) => {
            div.innerHTML += `<div class="admin-item"><b>${d.name}</b> (${num})<br>PIN: ${d.pass} | BAL: ${d.balance}</div>`;
        });
    });
    // Requests List
    onValue(ref(db, `admin/requests`), s => {
        const div = document.getElementById('pendingReqList'); div.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).forEach(([id, r]) => {
            div.innerHTML += `<div class="admin-item">
                <b>${r.type}</b>: ${r.amt} PKR<br>User: ${r.user} | TID: ${r.info}<br>
                <button onclick="approveReq('${id}', '${r.user}', ${r.amt}, '${r.type}')" style="color:var(--success); background:none; border:none; font-weight:800;">APPROVE</button>
                <button onclick="rejectReq('${id}')" style="color:var(--error); background:none; border:none; font-weight:800; margin-left:10px;">REJECT</button>
            </div>`;
        });
    });
  };

  window.approveReq = async (id, target, amt, type) => {
    const s = await get(ref(db, `users/${target}`));
    if(type === 'Deposit') await update(ref(db, `users/${target}`), { balance: (s.val().balance || 0) + Number(amt) });
    await remove(ref(db, `admin/requests/${id}`));
    alert("Approved & Balance Updated!");
  };

  window.rejectReq = async (id) => { await remove(ref(db, `admin/requests/${id}`)); alert("Request Rejected"); };

  window.toggleMaintenance = async () => {
    const s = await get(ref(db, `admin/settings/maintenance`));
    await set(ref(db, `admin/settings/maintenance`), !s.val());
    alert("Maintenance Toggled!");
  };

  window.createPromo = async () => {
    const code = document.getElementById('newPCode').value;
    const val = document.getElementById('newPVal').value;
    if(code && val) { await set(ref(db, `admin/promos/${code}`), Number(val)); alert("Promo Code Active!"); }
  };

  // --- USER CORE ---
  window.submitReq = (type) => {
    const amt = document.getElementById(type === 'Deposit' ? 'dAmt' : 'wAmt').value;
    const info = document.getElementById(type === 'Deposit' ? 'dTID' : 'wNum').value;
    push(ref(db, `admin/requests`), { user, type, amt, info, time: new Date().toLocaleString() });
    alert("Request Sent!");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  };

  if(user) {
    onValue(ref(db, `admin/settings/maintenance`), s => { if(s.val() && !document.getElementById('adminPage').classList.contains('active')) document.getElementById('maintenance').style.display='flex'; });
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uNameDisplay').innerText = d.name.toUpperCase();
    });
  } else {
    let n = prompt("Full Name:"); let p = prompt("Phone:"); let pin = prompt("PIN:");
    if(n && p && pin) { set(ref(db, `users/${p}`), { name:n, balance:0, hasActive:false, pass:pin }); localStorage.setItem('v_user', p); location.reload(); }
  }
</script>
</body>
</html>
