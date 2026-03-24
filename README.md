<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Nexus v7.0</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.1, 1, 0.1, 1); font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* GHOST ADMIN */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 20px; overflow-y: auto; }
  .ghost-card { background: #0a0a0a; border: 1px solid #1a1a1a; padding: 20px; border-radius: 25px; margin-bottom: 15px; }
  
  /* UI COMPONENTS */
  header { text-align: center; padding: 40px 20px 10px; font-size: 24px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; backdrop-filter: blur(40px); margin-bottom: 20px; }
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; outline: none; font-size: 13px; }
  .btn-quantum { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; }
  .btn-quantum:disabled { opacity: 0.5; cursor: not-allowed; }

  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); display: none; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; color: #fff; font-weight: 800; text-transform: uppercase; cursor: pointer; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div id="authPage" style="position:fixed; top:0; left:0; width:100%; height:100%; background:#000; z-index:10000; display:flex; align-items:center; justify-content:center; padding:20px;">
    <div class="glass-card" style="width:100%; max-width:400px; text-align:center;">
        <h1 style="letter-spacing:5px;">AUTHORIZE</h1>
        <div id="loginForm">
            <input id="logUser" placeholder="Username">
            <input id="logPass" type="password" placeholder="Password">
            <button class="btn-quantum" onclick="handleLogin()">ACCESS NEXUS</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('reg')">Create New Identity</p>
        </div>
        <div id="regForm" style="display:none;">
            <input id="regUser" placeholder="Username">
            <input id="regPass" type="password" placeholder="Password">
            <button class="btn-quantum" onclick="handleReg()">INITIALIZE</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('login')">Back to Login</p>
        </div>
    </div>
</div>

<header id="adminTrigger">VERBOSE</header>

<div id="dash" class="page">
    <div class="glass-card" style="background: linear-gradient(135deg, #0a0a0a, #000); border-color: var(--neon);">
        <h2 id="hiUser" style="margin:0;">Operator</h2>
        <div style="font-size:42px; font-weight:800; color:var(--neon);">PKR <span id="uBal">0.00</span></div>
    </div>
    <div id="plansContainer"></div>
</div>

<div id="finance" class="page">
    <div class="glass-card">
        <h3>DEPOSIT ASSETS</h3>
        <select id="depMethod">
            <option>JazzCash/SadaPay (03705519562)</option>
            <option>EasyPaisa (03379827882)</option>
        </select>
        <input id="depAmt" type="number" placeholder="Amount">
        <input id="depTID" placeholder="TID Number">
        <input type="file" id="depFile" accept="image/*" style="margin-top:15px; font-size:10px;">
        <button class="btn-quantum" id="depBtn" onclick="submitDeposit()">SUBMIT PROOF</button>
    </div>
    <div class="glass-card">
        <h3>WITHDRAW</h3>
        <input id="witAmt" type="number" placeholder="Amount">
        <input id="witNum" placeholder="Account Number">
        <button class="btn-quantum" style="background:var(--error);" onclick="submitWithdraw()">REQUEST PAYOUT</button>
    </div>
</div>

<div id="history" class="page">
    <h3 style="margin-left:10px;">LOGS</h3>
    <div id="historyList"></div>
</div>

<div id="adminDash">
    <div style="display:flex; justify-content:space-between; align-items:center;">
        <h2 style="color:var(--neon);">ROOT</h2>
        <button onclick="document.getElementById('adminDash').style.display='none'" style="color:red; background:none; border:none;">[EXIT]</button>
    </div>
    <div class="ghost-card">
        <small>PLAN ARCHITECT</small>
        <input id="pName" placeholder="Name">
        <input id="pPrice" type="number" placeholder="Price">
        <input id="pProfit" type="number" placeholder="Daily Profit">
        <input type="file" id="pFile" accept="image/*">
        <button class="btn-quantum" id="pBtn" onclick="admCreatePlan()">DEPLOY PLAN</button>
    </div>
    <div class="ghost-card"><small>DEPOSIT REQUESTS</small><div id="admReqs"></div></div>
    <div class="ghost-card"><small>USERS</small><div id="admUsers"></div></div>
</div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="tab('history', this)">Logs</div>
    <div class="nav-item" onclick="logout()">Logout</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get, push, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
  import { getStorage, ref as sRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    storageBucket: "verbose-6c008.appspot.com",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  const storage = getStorage(app);
  let user = localStorage.getItem('v_user');

  // --- AUTH ---
  window.toggleAuth = (t) => {
    document.getElementById('loginForm').style.display = t === 'reg' ? 'none' : 'block';
    document.getElementById('regForm').style.display = t === 'reg' ? 'block' : 'none';
  };
  window.handleReg = async () => {
    const u = document.getElementById('regUser').value.trim().toLowerCase();
    const p = document.getElementById('regPass').value;
    if(!u || !p) return alert("Fill all!");
    await set(ref(db, `users/${u}`), { username: u, pass: p, balance: 0, status: 'Active' });
    alert("Success!"); toggleAuth('login');
  };
  window.handleLogin = async () => {
    const u = document.getElementById('logUser').value.trim().toLowerCase();
    const p = document.getElementById('logPass').value;
    const s = await get(ref(db, `users/${u}`));
    if(s.exists() && s.val().pass === p) {
        if(s.val().status === 'Banned') return alert("Banned!");
        localStorage.setItem('v_user', u); location.reload();
    } else alert("Invalid!");
  };
  window.logout = () => { localStorage.removeItem('v_user'); location.reload(); };

  // --- DEPOSIT WITH STORAGE ---
  window.submitDeposit = async () => {
    const file = document.getElementById('depFile').files[0];
    const amt = document.getElementById('depAmt').value;
    const tid = document.getElementById('depTID').value;
    const btn = document.getElementById('depBtn');

    if(!file || !amt) return alert("Select image and enter amount!");
    btn.disabled = true; btn.innerText = "UPLOADING...";

    try {
        const path = sRef(storage, `proofs/${user}_${Date.now()}`);
        await uploadBytes(path, file);
        const url = await getDownloadURL(path);
        
        const id = Date.now();
        await set(ref(db, `admin/deposits/${id}`), { user, amt, tid, url, status: 'Pending' });
        await set(ref(db, `history/${user}/${id}`), { type: 'Deposit', amount: amt, status: 'Pending', date: new Date().toLocaleString() });
        alert("Submitted, sweetie!"); location.reload();
    } catch(e) { alert("Upload Failed! Check Rules."); btn.disabled = false; btn.innerText = "RETRY"; }
  };

  // --- ADMIN: CREATE PLAN ---
  window.admCreatePlan = async () => {
    const file = document.getElementById('pFile').files[0];
    const name = document.getElementById('pName').value;
    const price = document.getElementById('pPrice').value;
    const profit = document.getElementById('pProfit').value;
    const btn = document.getElementById('pBtn');

    if(!file || !name) return alert("Fill all!");
    btn.disabled = true; btn.innerText = "DEPLOYING...";

    try {
        const path = sRef(storage, `plans/${Date.now()}`);
        await uploadBytes(path, file);
        const url = await getDownloadURL(path);
        await set(ref(db, `plans/${name}`), { name, price, profit, url });
        alert("Plan Deployed!"); location.reload();
    } catch(e) { alert("Admin Error!"); btn.disabled = false; }
  };

  // --- DATA SYNC ---
  if(user) {
    document.getElementById('authPage').style.display='none';
    document.getElementById('mainNav').style.display='flex';
    document.getElementById('dash').classList.add('active');

    onValue(ref(db, `users/${user}`), s => {
        if(s.val().status === 'Banned') logout();
        document.getElementById('uBal').innerText = (s.val().balance || 0).toLocaleString();
        document.getElementById('hiUser').innerText = `Hi, ${user}!`;
    });

    onValue(ref(db, 'plans'), s => {
        const cont = document.getElementById('plansContainer'); cont.innerHTML = '';
        if(s.exists()) Object.values(s.val()).forEach(p => {
            cont.innerHTML += `<div class="glass-card" style="padding:0; overflow:hidden;">
                <img src="${p.url}" style="width:100%; height:160px; object-fit:cover;">
                <div style="padding:20px;">
                    <h3 style="margin:0;">${p.name}</h3>
                    <p style="opacity:0.6; font-size:12px;">Price: PKR ${p.price} | Daily: PKR ${p.profit}</p>
                    <button class="btn-quantum" style="font-size:11px; padding:12px;">ACTIVATE</button>
                </div>
            </div>`;
        });
    });

    onValue(ref(db, `history/${user}`), s => {
        const list = document.getElementById('historyList'); list.innerHTML = '';
        if(s.exists()) Object.values(s.val()).reverse().forEach(h => {
            list.innerHTML += `<div class="glass-card" style="padding:15px; display:flex; justify-content:space-between; font-size:12px;">
                <span>${h.type}<br><small>${h.date}</small></span>
                <span style="text-align:right;">PKR ${h.amount}<br><small style="color:var(--success)">${h.status}</small></span>
            </div>`;
        });
    });
  }

  // --- ADMIN TRIGGER ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clicks >= 7) { if(prompt("KEY:")==="NAZIM786") { 
    document.getElementById('adminDash').style.display='block';
    loadAdmin();
  } clicks=0; } };

  function loadAdmin() {
    onValue(ref(db, 'admin/deposits'), s => {
        const cont = document.getElementById('admReqs'); cont.innerHTML = '';
        if(s.exists()) Object.entries(s.val()).forEach(([id, r]) => {
            if(r.status === 'Pending') {
                cont.innerHTML += `<div class="ghost-card" style="font-size:11px;">
                    ${r.user} - PKR ${r.amt}<br><img src="${r.url}" style="width:60px; margin:5px 0;"><br>
                    <button onclick="approveDep('${id}','${r.user}',${r.amt})" style="color:var(--success); background:none; border:none; font-weight:800;">APPROVE</button>
                </div>`;
            }
        });
    });
    onValue(ref(db, 'users'), s => {
        const cont = document.getElementById('admUsers'); cont.innerHTML = '';
        if(s.exists()) Object.values(s.val()).forEach(u => {
            cont.innerHTML += `<div style="font-size:10px; border-bottom:1px solid #222; padding:5px; display:flex; justify-content:space-between;">
                <span>${u.username} (${u.balance})</span>
                <button onclick="banUser('${u.username}')" style="color:red; background:none; border:none;">BAN</button>
            </div>`;
        });
    });
  }

  window.approveDep = async (id, target, amt) => {
    const s = await get(ref(db, `users/${target}`));
    await update(ref(db, `users/${target}`), { balance: (s.val().balance||0) + parseFloat(amt) });
    await update(ref(db, `admin/deposits/${id}`), { status: 'Approved' });
    await update(ref(db, `history/${target}/${id}`), { status: 'Approved' });
    alert("Approved!");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };
</script>
</body>
</html>
