<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.06); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* UI COMPONENTS */
  .page { max-width: 480px; margin: 0 auto; padding: 25px 20px 150px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  header { display: flex; align-items: center; padding: 60px 25px 15px; position: sticky; top: 0; background: rgba(3,3,3,0.9); backdrop-filter: blur(15px); z-index: 1000; justify-content: space-between; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 18px; font-weight: 800; letter-spacing: 5px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }

  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 25px; margin-bottom: 20px; position: relative; backdrop-filter: blur(10px); }
  .btn-action { width: 100%; padding: 18px; border-radius: 22px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; text-transform: uppercase; margin-top: 15px; box-shadow: 0 10px 20px rgba(0,247,255,0.15); }
  
  /* LIVE NOTIFICATION POPUP */
  #payoutPopup { position: fixed; bottom: 120px; left: 20px; background: rgba(20,20,20,0.95); border: 1px solid var(--neon); padding: 12px 18px; border-radius: 18px; display: none; align-items: center; gap: 10px; z-index: 9999; box-shadow: 0 10px 30px rgba(0,247,255,0.3); backdrop-filter: blur(10px); font-size: 11px; font-weight: 600; }

  /* NAVIGATION */
  .nav-bar { position: fixed; bottom: 30px; left: 20px; right: 20px; background: rgba(15,15,15,0.95); backdrop-filter: blur(25px); border-radius: 50px; display: flex; justify-content: space-around; padding: 18px; border: 1px solid var(--border); z-index: 1000; }
  .nav-link { font-size: 10px; font-weight: 800; opacity: 0.4; color: #fff; cursor: pointer; text-transform: uppercase; }
  .nav-link.active { opacity: 1; color: var(--neon); }

  /* ADMIN HUD STYLES */
  .admin-log-box { max-height: 150px; overflow-y: auto; background: #000; border-radius: 15px; padding: 10px; font-size: 10px; border: 1px solid var(--gold); margin-bottom: 20px; }
  .admin-btn { padding: 8px 12px; border-radius: 10px; font-size: 10px; font-weight: 800; border: none; cursor: pointer; margin: 4px; }
  input { width: 100%; padding: 18px; margin-top: 12px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; font-size: 14px; }
</style>
</head>
<body>

<div id="payoutPopup">
    <div style="width:8px; height:8px; background:var(--success); border-radius:50%; box-shadow: 0 0 10px var(--success);"></div>
    <span id="popupText">Processing Payout...</span>
</div>

<div id="banOverlay" style="position:fixed; inset:0; background:rgba(0,0,0,0.98); z-index:1000000; display:none; flex-direction:column; align-items:center; justify-content:center; text-align:center; padding:30px;">
    <div style="border:1px solid var(--error); padding:40px; border-radius:40px; background:rgba(255,70,70,0.05);">
        <h1 style="color:var(--error); letter-spacing:5px;">ACCESS REVOKED</h1>
        <p style="opacity:0.7;">Your account has been blacklisted for security violations.</p>
        <button class="btn-action" style="background:var(--error);" onclick="logout()">LOGOUT</button>
    </div>
</div>

<header>
    <div style="font-size:22px; cursor:pointer;" onclick="tab('infoPage')">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
    <div style="width:24px;"></div>
</header>

<div id="dash" class="page active">
    <div class="node-card" style="text-align:center; border-color:var(--neon); background: radial-gradient(circle at top, rgba(0,247,255,0.05), transparent);">
        <small style="opacity:0.5; letter-spacing:3px;">PORTFOLIO VALUE</small>
        <h1 style="font-size:45px; margin:10px 0; font-weight:800;">PKR <span id="uBal">0.00</span></h1>
        <div id="uNameDisplay" style="font-size:11px; color:var(--neon); font-weight:800;">SECURE AGENT <span style="background:var(--neon); color:#000; font-size:8px; padding:2px 5px; border-radius:5px; margin-left:5px;">✓</span></div>
    </div>
    
    <div style="display:flex; gap:10px; margin-bottom:20px;">
        <div class="node-card" style="flex:1; margin-bottom:0; padding:15px; text-align:center;"><small style="opacity:0.5;">Active Nodes</small><br><b>1,248+</b></div>
        <div class="node-card" style="flex:1; margin-bottom:0; padding:15px; text-align:center;"><small style="opacity:0.5;">Health</small><br><b style="color:var(--success);">Optimal</b></div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="text-align:center; letter-spacing:3px;">MINING CLUSTERS</h3>
    <div id="nodeGrid"></div>
</div>

<div id="financePage" class="page">
    <div class="node-card" style="border-top:3px solid var(--success);">
        <h3>INJECT CAPITAL</h3>
        <p style="font-size:12px; opacity:0.6;">Admin: 03705519562 (JazzCash/EP)</p>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="Transaction ID (TID)">
        <button class="btn-action" onclick="sendReq('Deposit')">Confirm Deposit</button>
    </div>
    <div class="node-card" style="border-top:3px solid var(--error); margin-top:30px;">
        <h3>WITHDRAWAL</h3>
        <input id="wAmt" type="number" placeholder="Withdrawal Amount">
        <input id="wNum" placeholder="Account Number">
        <button class="btn-action" style="background:var(--error);" onclick="sendReq('Withdraw')">Submit Withdrawal</button>
    </div>
</div>

<div id="historyPage" class="page">
    <h3>AUDIT HISTORY</h3>
    <div id="userHistoryList"></div>
</div>

<div id="infoPage" class="page">
    <h3>COMPANY PROTOCOLS</h3>
    <div class="node-card" style="font-size:12px; line-height:1.7;">
        <b>ABOUT:</b> Verbose is a Rawalpindi-based decentralized infrastructure for cloud computing.<br><br>
        <b>PRIVACY:</b> All investor data is encrypted. No third-party logs are maintained.<br><br>
        <b>SUPPORT:</b> Contact 03705519562 for direct assistance.
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center; letter-spacing:4px;">OVERLORD HUD</h2>
    <div class="node-card">
        <h4 style="color:var(--neon); margin:0 0 10px;">SYSTEM LOGS</h4>
        <div id="adminLogs" class="admin-log-box"></div>
    </div>
    <h4 style="color:var(--gold);">ACTIVE AUDITS</h4>
    <div id="admReqs"></div>
    <h4 style="color:var(--gold);">USER DIRECTORY</h4>
    <input id="userSearch" oninput="filterUsers()" placeholder="Search by Phone..." style="background:#000;">
    <div id="admUsers"></div>
</div>

<nav class="nav-bar">
    <div class="nav-link active" onclick="tab('dash', this)">Home</div>
    <div class="nav-link" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-link" onclick="tab('financePage', this)">Finance</div>
    <div class="nav-link" onclick="tab('historyPage', this)">History</div>
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

  // --- AUTH SYSTEM ---
  const handleAuth = async () => {
    let p = prompt("Phone (03xx...):"), pin = prompt("Access PIN:"), n = prompt("Full Name (New Users Only):");
    if(!p || !pin) return;
    const s = await get(ref(db, `users/${p}`));
    if(s.exists()) {
        if(s.val().pass === pin) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("ACCESS DENIED");
    } else {
        const refCode = prompt("Referral Phone (Optional):") || "NONE";
        await set(ref(db, `users/${p}`), { name:n, balance:0, pass:pin, isBanned:false, referredBy:refCode });
        localStorage.setItem('v_user', p); location.reload();
    }
  };
  if(!user) handleAuth();

  // --- CORE UI & POPUPS ---
  const notifications = ["User 0321*** withdrew 2,500 PKR", "New Titan Node initialized", "Payout of 1,200 PKR processed", "System hash-rate optimal", "User 0300*** earned 5% commission"];
  setInterval(() => {
    const p = document.getElementById('payoutPopup');
    document.getElementById('popupText').innerText = notifications[Math.floor(Math.random()*notifications.length)];
    p.style.display = 'flex';
    setTimeout(() => p.style.display = 'none', 4000);
  }, 12000);

  if(user) {
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        if(!d) return;
        if(d.isBanned) document.getElementById('banOverlay').style.display = 'flex';
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uNameDisplay').innerHTML = `AGENT: ${d.name.toUpperCase()} <span style="background:var(--neon); color:#000; font-size:8px; padding:2px 5px; border-radius:5px; margin-left:5px;">✓</span>`;
        
        const hDiv = document.getElementById('userHistoryList'); hDiv.innerHTML = "";
        if(d.history) Object.values(d.history).reverse().forEach(x => {
            hDiv.innerHTML += `<div class="node-card" style="font-size:11px; border-left:4px solid ${x.status.includes('Approved')?'var(--success)':'var(--gold)'}">
                <b>${x.type}</b>: ${x.amt} PKR<br>Status: ${x.status}<br><small>${x.time}</small></div>`;
        });
        renderNodes(d.hasActive);
    });
  }

  const renderNodes = (active) => {
    const g = document.getElementById('nodeGrid'); g.innerHTML = "";
    [{n:"Titan",p:1000,d:125},{n:"Aura",p:2500,d:320},{n:"Zenith",p:5000,d:700}].forEach(x => {
        g.innerHTML += `<div class="node-card"><b>${x.n} Cluster</b><br><small>Daily Yield: ${x.d} PKR</small>
        <button class="btn-action" ${active?'disabled':''} onclick="buyNode(${x.p},'${x.n}')">${active?'ACTIVE':'INITIALIZE '+x.p}</button></div>`;
    });
  };

  window.buyNode = async (p, name) => {
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < p) return alert("Insufficient Capital");
    await update(ref(db, `users/${user}`), { balance: s.val().balance - p, hasActive:true });
    alert(name + " Cluster Initialized!");
  };

  window.sendReq = (type) => {
    const amt = document.getElementById(type === 'Deposit'?'dAmt':'wAmt').value;
    const info = document.getElementById(type === 'Deposit'?'dTID':'wNum').value;
    if(!amt || !info) return alert("Fill all fields");
    const id = push(ref(db, `admin/requests`)).key;
    const data = { user, type, amt, info, status: "Pending", time: new Date().toLocaleString() };
    update(ref(db, `admin/requests/${id}`), data);
    update(ref(db, `users/${user}/history/${id}`), data);
    alert("Request Transmitted to Audit.");
  };

  // --- ADMIN SUPREME ---
  let c = 0; document.getElementById('adminTrigger').onclick = () => { if(++c >= 7) { if(prompt("HUD KEY?")==="nazim786") { tab('adminPage'); loadAdmin(); } c=0; } };

  const loadAdmin = () => {
    onValue(ref(db, `admin/requests`), s => {
        const div = document.getElementById('admReqs'); div.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).forEach(([id, r]) => {
            div.innerHTML += `<div class="node-card" style="font-size:11px; border-color:var(--gold);">
                <b>${r.type}</b> | ${r.user} | PKR ${r.amt}<br>TID/Num: ${r.info}
                <div style="margin-top:10px;">
                    <button class="admin-btn" style="background:var(--success);" onclick="approveGod('${id}','${r.user}',${r.amt},'${r.type}')">APPROVE</button>
                    <button class="admin-btn" style="background:var(--error); color:#fff;" onclick="rejectGod('${id}','${r.user}')">REJECT</button>
                </div></div>`;
        });
    });
    onValue(ref(db, `users`), s => { window.allU = s.val(); filterUsers(); });
    onValue(ref(db, `admin/logs`), s => {
        const div = document.getElementById('adminLogs'); div.innerHTML = "";
        if(s.exists()) Object.values(s.val()).reverse().forEach(l => div.innerHTML += `<div>${l}</div>`);
    });
  };

  window.filterUsers = () => {
    const q = document.getElementById('userSearch').value;
    const div = document.getElementById('admUsers'); div.innerHTML = "";
    Object.entries(window.allU).forEach(([p, u]) => {
        if(p.includes(q)) div.innerHTML += `<div class="node-card" style="font-size:10px;">
            <b>${u.name}</b> (${p}) | BAL: ${u.balance}<br>
            <button class="admin-btn" style="background:#444; color:#fff;" onclick="toggleBan('${p}', ${u.isBanned})">${u.isBanned?'UNBAN':'BAN'}</button>
            <button class="admin-btn" style="background:var(--error); color:#fff;" onclick="deleteUser('${p}')">DELETE</button>
        </div>`;
    });
  };

  window.approveGod = async (id, target, amt, type) => {
    const s = await get(ref(db, `users/${target}`));
    const uData = s.val();
    let b = (uData.balance || 0) + (type==='Deposit'?Number(amt):-Number(amt));
    await update(ref(db, `users/${target}`), { balance: b });
    await update(ref(db, `users/${target}/history/${id}`), { status: "Approved" });
    if(type==='Deposit' && uData.referredBy !== "NONE") {
        const upS = await get(ref(db, `users/${uData.referredBy}`));
        if(upS.exists()) await update(ref(db, `users/${uData.referredBy}`), { balance: (upS.val().balance||0)+(amt*0.05) });
    }
    push(ref(db, `admin/logs`), `${new Date().toLocaleTimeString()}: Approved ${type} for ${target}`);
    await remove(ref(db, `admin/requests/${id}`));
  };

  window.rejectGod = async (id, target) => {
    const res = prompt("Reason?");
    await update(ref(db, `users/${target}/history/${id}`), { status: "Rejected: "+res });
    await remove(ref(db, `admin/requests/${id}`));
    push(ref(db, `admin/logs`), `${new Date().toLocaleTimeString()}: Rejected ${target} (${res})`);
  };

  window.toggleBan = (p, curr) => update(ref(db, `users/${p}`), { isBanned: !curr });
  window.deleteUser = (p) => { if(confirm("Delete user?")) remove(ref(db, `users/${p}`)); };
  window.tab = (id, el) => { document.querySelectorAll('.page').forEach(p => p.classList.remove('active')); document.getElementById(id).classList.add('active'); if(el) { document.querySelectorAll('.nav-link').forEach(n => n.classList.remove('active')); el.classList.add('active'); } };
  window.logout = () => { localStorage.clear(); location.reload(); };
</script>
</body>
</html>
