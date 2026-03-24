<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Prime Sovereign Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #020202; --card: rgba(255,255,255,0.06); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* NAVIGATION & LAYOUT */
  header { display: flex; align-items: center; padding: 65px 25px 20px; position: sticky; top: 0; background: rgba(2,2,2,0.85); backdrop-filter: blur(20px); z-index: 1000; justify-content: space-between; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 18px; font-weight: 800; letter-spacing: 6px; text-shadow: 0 0 15px var(--neon); cursor: pointer; color: #fff; text-decoration: none; }
  
  .page { max-width: 480px; margin: 0 auto; padding: 25px 20px 160px; display: none; }
  .active { display: block !important; animation: slideUp 0.5s ease; }
  @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  /* CARDS */
  .prime-card { background: linear-gradient(145deg, rgba(20,20,20,0.9), rgba(5,5,5,0.95)); border: 1px solid var(--border); border-radius: 40px; padding: 35px 25px; position: relative; overflow: hidden; margin-bottom: 25px; box-shadow: 0 25px 50px rgba(0,0,0,0.5); border-top: 1px solid rgba(255,255,255,0.1); }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; backdrop-filter: blur(10px); }
  
  /* BUTTONS */
  .btn-prime { width: 100%; padding: 20px; border-radius: 25px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; text-transform: uppercase; letter-spacing: 2px; box-shadow: 0 10px 25px rgba(0,247,255,0.2); }
  .btn-outline { width: 100%; padding: 12px; border-radius: 15px; border: 1px solid var(--border); background: transparent; color: #fff; font-size: 10px; font-weight: 700; margin-top: 10px; cursor: pointer; }

  /* NOTIFICATIONS */
  #liveToast { position: fixed; bottom: 125px; left: 20px; background: rgba(10,10,10,0.95); border: 1px solid var(--neon); padding: 12px 20px; border-radius: 20px; display: none; align-items: center; gap: 12px; z-index: 10000; box-shadow: 0 10px 30px rgba(0,247,255,0.2); backdrop-filter: blur(10px); }
  
  /* ADMIN HUD */
  .adm-log { max-height: 120px; overflow-y: auto; background: #000; padding: 10px; font-size: 10px; border-radius: 12px; border: 1px solid var(--gold); color: var(--gold); margin-bottom: 15px; }
  input { width: 100%; padding: 20px; margin-top: 15px; border-radius: 22px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; font-size: 14px; }

  .nav-bar { position: fixed; bottom: 35px; left: 25px; right: 25px; background: rgba(15,15,15,0.9); backdrop-filter: blur(30px); border-radius: 50px; display: flex; justify-content: space-around; padding: 20px; border: 1px solid var(--border); z-index: 1000; }
  .nav-link { font-size: 10px; font-weight: 800; opacity: 0.4; color: #fff; cursor: pointer; text-transform: uppercase; }
  .nav-link.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div id="liveToast">
    <div style="width:8px; height:8px; background:var(--success); border-radius:50%; box-shadow: 0 0 8px var(--success);"></div>
    <span id="toastMsg" style="font-size:11px; font-weight:600;">Processing...</span>
</div>

<header>
    <div style="font-size:22px; cursor:pointer;" onclick="tab('info')">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
    <div style="width:24px;"></div>
</header>

<div id="dash" class="page active">
    <div class="prime-card" style="text-align:center;">
        <small style="opacity:0.5; letter-spacing:3px;">TOTAL EQUITY</small>
        <h1 style="font-size:48px; margin:10px 0; font-weight:800;">PKR <span id="uBal">0.00</span></h1>
        <div id="uNameDisplay" style="font-size:11px; font-weight:800; color:var(--neon);">
            AGENT: --- <span style="background:var(--neon); color:#000; padding:2px 6px; border-radius:6px; font-size:9px; margin-left:5px;">VERIFIED ✓</span>
        </div>
    </div>

    <div style="display:flex; gap:10px; margin-bottom:20px;">
        <div class="node-card" style="flex:1; margin-bottom:0; text-align:center;"><small style="opacity:0.5;">Active Nodes</small><br><b id="activeNodes">0</b></div>
        <div class="node-card" style="flex:1; margin-bottom:0; text-align:center;"><small style="opacity:0.5;">Team Size</small><br><b id="teamCount">0</b></div>
    </div>

    <div class="node-card" style="border-left:4px solid var(--success);">
        <h4 style="margin:0 0 10px;">Network Security</h4>
        <p style="font-size:12px; opacity:0.6; line-height:1.6;">Your wallet is secured with end-to-end encryption. All mining yields are audited by Prime Solutions protocols.</p>
    </div>
</div>

<div id="mining" class="page">
    <h2 style="text-align:center; letter-spacing:3px;">MINING NODES</h2>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-top:3px solid var(--success);">
        <h3>DEPOSIT CAPITAL</h3>
        <p style="font-size:12px; opacity:0.6;">JazzCash/EasyPaisa: <b style="color:#fff;">03705519562</b></p>
        <input id="dAmt" type="number" placeholder="Enter Amount (PKR)">
        <input id="dTID" placeholder="Enter Transaction ID (TID)">
        <button class="btn-prime" style="margin-top:20px;" onclick="sendReq('Deposit')">Confirm Investment</button>
    </div>

    <div class="node-card" style="border-top:3px solid var(--error); margin-top:30px;">
        <h3>WITHDRAW ASSETS</h3>
        <input id="wAmt" type="number" placeholder="Amount">
        <input id="wNum" placeholder="Account Number">
        <button class="btn-prime" style="background:var(--error);" onclick="sendReq('Withdraw')">Request Payout</button>
    </div>
</div>

<div id="history" class="page">
    <h3>TRANSACTION LEDGER</h3>
    <div id="histList"></div>
</div>

<div id="admin" class="page">
    <h2 style="color:var(--gold); text-align:center; letter-spacing:4px;">ADMIN SUPREME HUD</h2>
    <div class="node-card">
        <h4 style="margin:0 0 10px; color:var(--gold);">LIVE ACTIVITY LOGS</h4>
        <div id="admLogs" class="adm-log"></div>
    </div>
    
    <h4 style="color:var(--gold);">PENDING AUDITS</h4>
    <div id="admReqs"></div>

    <h4 style="color:var(--gold); margin-top:30px;">USER DIRECTORY</h4>
    <input id="uSearch" oninput="filterUsers()" placeholder="Search User Phone...">
    <div id="admUsers"></div>
</div>

<nav class="nav-bar">
    <div class="nav-link active" onclick="tab('dash', this)">Home</div>
    <div class="nav-link" onclick="tab('mining', this)">Mining</div>
    <div class="nav-link" onclick="tab('finance', this)">Finance</div>
    <div class="nav-link" onclick="tab('history', this)">History</div>
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

  // --- AUTH ---
  const doAuth = async () => {
    let p = prompt("Phone:"), pin = prompt("PIN:"), n = prompt("Full Name:");
    if(!p || !pin) return;
    const s = await get(ref(db, `users/${p}`));
    if(s.exists()){
        if(s.val().pass === pin) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("WRONG PIN");
    } else {
        const refCode = prompt("Referral Phone (Optional):") || "NONE";
        await set(ref(db, `users/${p}`), { name:n||"Investor", balance:0, pass:pin, isBanned:false, referredBy:refCode, team:[] });
        if(refCode !== "NONE") {
            const upS = await get(ref(db, `users/${refCode}/team`));
            let team = upS.val() || []; team.push(p);
            await update(ref(db, `users/${refCode}`), { team });
        }
        localStorage.setItem('v_user', p); location.reload();
    }
  };
  if(!user) doAuth();

  // --- CORE SYNC ---
  if(user) {
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        if(!d) return;
        if(d.isBanned) document.body.innerHTML = "<h1 style='color:red; text-align:center; margin-top:100px;'>ACCOUNT SUSPENDED</h1>";
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uNameDisplay').innerHTML = `AGENT: ${d.name.toUpperCase()} <span style="background:var(--neon); color:#000; padding:2px 6px; border-radius:6px; font-size:9px; margin-left:5px;">VERIFIED ✓</span>`;
        document.getElementById('teamCount').innerText = (d.team || []).length;
        document.getElementById('activeNodes').innerText = d.hasActive ? "1" : "0";
        
        const hList = document.getElementById('histList'); hList.innerHTML = "";
        if(d.history) Object.values(d.history).reverse().forEach(x => {
            hList.innerHTML += `<div class="node-card" style="font-size:11px; border-left:4px solid ${x.status.includes('Approved')?'var(--success)':'var(--gold)'}">
                <b>${x.type}</b>: ${x.amt} PKR<br>Status: ${x.status}<br><small>${x.time}</small></div>`;
        });
        renderNodes(d.hasActive);
    });
  }

  const renderNodes = (active) => {
    const g = document.getElementById('nodeGrid'); g.innerHTML = "";
    [{n:"Titan",p:1000,d:125},{n:"Aura",p:2500,d:320},{n:"Zenith",p:5000,d:700}].forEach(x => {
        g.innerHTML += `<div class="node-card"><b>${x.n} Cluster</b><br><small>Yield: ${x.d} PKR / Day</small>
        <button class="btn-prime" ${active?'disabled':''} onclick="buyNode(${x.p})">${active?'ACTIVE':'INITIALIZE '+x.p}</button></div>`;
    });
  };

  window.buyNode = async (p) => {
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < p) return alert("Insufficient Balance");
    await update(ref(db, `users/${user}`), { balance: s.val().balance - p, hasActive:true });
    alert("Node Successfully Initialized!");
  };

  window.sendReq = (type) => {
    const amt = document.getElementById(type==='Deposit'?'dAmt':'wAmt').value;
    const info = document.getElementById(type==='Deposit'?'dTID':'wNum').value;
    if(!amt || !info) return alert("Missing Info");
    const id = push(ref(db, `admin/requests`)).key;
    const data = { user, type, amt, info, status: "Pending", time: new Date().toLocaleString() };
    update(ref(db, `admin/requests/${id}`), data);
    update(ref(db, `users/${user}/history/${id}`), data);
    alert("Request Transmitted to Server.");
  };

  // --- ADMIN SUPREME HUD ---
  let clickCount = 0; document.getElementById('adminTrigger').onclick = () => { if(++clickCount >= 7) { if(prompt("ACCESS KEY?")==="nazim786") { tab('admin'); loadAdmin(); } clickCount=0; } };

  const loadAdmin = () => {
    onValue(ref(db, `admin/requests`), s => {
        const div = document.getElementById('admReqs'); div.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).forEach(([id, r]) => {
            div.innerHTML += `<div class="node-card" style="font-size:11px; border-color:var(--gold);">
                <b>${r.type}</b> | User: ${r.user} | PKR ${r.amt}<br>Info: ${r.info}
                <div style="margin-top:10px;">
                    <button class="btn-outline" style="background:var(--success); color:#000; border:none;" onclick="approveAudit('${id}','${r.user}',${r.amt},'${r.type}')">APPROVE</button>
                    <button class="btn-outline" style="background:var(--error); border:none;" onclick="rejectAudit('${id}','${r.user}')">REJECT</button>
                </div></div>`;
        });
    });
    onValue(ref(db, `users`), s => { window.allUsers = s.val(); filterUsers(); });
    onValue(ref(db, `admin/logs`), s => {
        const lBox = document.getElementById('admLogs'); lBox.innerHTML = "";
        if(s.exists()) Object.values(s.val()).reverse().forEach(l => lBox.innerHTML += `<div>${l}</div>`);
    });
  };

  window.filterUsers = () => {
    const q = document.getElementById('uSearch').value;
    const div = document.getElementById('admUsers'); div.innerHTML = "";
    Object.entries(window.allUsers).forEach(([p, u]) => {
        if(p.includes(q)) div.innerHTML += `<div class="node-card" style="font-size:10px;">
            <b>${u.name}</b> (${p})<br>Balance: ${u.balance} | Team: ${(u.team||[]).length}
            <button class="btn-outline" onclick="toggleBan('${p}',${u.isBanned})">${u.isBanned?'UNBAN':'BAN'}</button>
            <button class="btn-outline" style="color:var(--error);" onclick="delUser('${p}')">DELETE</button>
        </div>`;
    });
  };

  window.approveAudit = async (id, target, amt, type) => {
    const s = await get(ref(db, `users/${target}`));
    const u = s.val();
    let newBal = (u.balance || 0) + (type==='Deposit'?Number(amt):-Number(amt));
    await update(ref(db, `users/${target}`), { balance: newBal });
    await update(ref(db, `users/${target}/history/${id}`), { status: "Approved" });
    
    // Auto Commission 5%
    if(type==='Deposit' && u.referredBy !== "NONE") {
        const upS = await get(ref(db, `users/${u.referredBy}`));
        if(upS.exists()) await update(ref(db, `users/${u.referredBy}`), { balance: (upS.val().balance||0)+(amt*0.05) });
    }
    push(ref(db, `admin/logs`), `${new Date().toLocaleTimeString()}: Approved ${type} for ${target}`);
    await remove(ref(db, `admin/requests/${id}`));
  };

  window.rejectAudit = async (id, target) => {
    const r = prompt("Reason for rejection?");
    await update(ref(db, `users/${target}/history/${id}`), { status: "Rejected: "+r });
    await remove(ref(db, `admin/requests/${id}`));
    push(ref(db, `admin/logs`), `${new Date().toLocaleTimeString()}: Rejected ${target} (${r})`);
  };

  // --- UI UTILS ---
  window.tab = (id, el) => { document.querySelectorAll('.page').forEach(p => p.classList.remove('active')); document.getElementById(id).classList.add('active'); if(el) { document.querySelectorAll('.nav-link').forEach(n => n.classList.remove('active')); el.classList.add('active'); } };
  window.logout = () => { localStorage.clear(); location.reload(); };
  
  // Fake Notifications for Social Proof
  const msgs = ["User 0321*** just withdrew 5,000 PKR", "New Zenith Node active in Islamabad", "Referral commission of 250 PKR paid", "Audit Success: Deposit of 10,000 PKR"];
  setInterval(() => {
    const t = document.getElementById('liveToast');
    document.getElementById('toastMsg').innerText = msgs[Math.floor(Math.random()*msgs.length)];
    t.style.display = 'flex'; setTimeout(() => t.style.display='none', 4000);
  }, 12000);
</script>
</body>
</html>
