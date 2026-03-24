<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Nexus v5.0</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.4s cubic-bezier(0.1, 1, 0.1, 1); font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* GHOST ADMIN LAYER */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 20px; overflow-y: auto; }
  .ghost-card { background: #0a0a0a; border: 1px solid #1a1a1a; padding: 20px; border-radius: 25px; margin-bottom: 15px; }
  .stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 20px; }
  .stat-box { background: var(--card); border: 1px solid var(--border); padding: 15px; border-radius: 20px; text-align: center; }

  /* UI COMPONENTS */
  header { text-align: center; padding: 40px 20px 10px; font-size: 24px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.5s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; backdrop-filter: blur(40px); margin-bottom: 20px; position: relative; }
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; outline: none; font-size: 13px; }
  .btn-quantum { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 8px 25px rgba(112,0,255,0.25); margin-top: 15px; }
  
  /* NAV */
  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); display: none; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; color: #fff; font-weight: 800; text-transform: uppercase; cursor: pointer; text-align: center; }
  .nav-item.active { opacity: 1; color: var(--neon); }
  
  .hidden { display: none !important; }
</style>
</head>
<body>

<div id="authPage" style="position:fixed; top:0; left:0; width:100%; height:100%; background:#000; z-index:10000; display:flex; align-items:center; justify-content:center; padding:20px;">
    <div class="glass-card" style="width:100%; max-width:400px; text-align:center;">
        <h1 id="authTitle" style="letter-spacing:5px;">AUTHORIZE</h1>
        <div id="loginForm">
            <input id="logUser" placeholder="Username">
            <input id="logPass" type="password" placeholder="Password">
            <button class="btn-quantum" onclick="handleLogin()">ACCESS NEXUS</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('reg')">Create New Identity</p>
        </div>
        <div id="regForm" class="hidden">
            <input id="regUser" placeholder="Choose Username">
            <input id="regPass" type="password" placeholder="Choose Password">
            <button class="btn-quantum" onclick="handleReg()">INITIALIZE</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('login')">Back to Login</p>
        </div>
    </div>
</div>

<header id="adminTrigger">VERBOSE</header>

<div id="dash" class="page">
    <div class="glass-card" style="background: linear-gradient(135deg, #0a0a0a, #000); border-color: var(--neon);">
        <h2 id="hiUser" style="margin:0;">Operator</h2>
        <div style="font-size:42px; font-weight:800; margin:10px 0; color:var(--neon);">PKR <span id="uBal">0.00</span></div>
        <p style="font-size:10px; color:var(--success); font-weight:800;">STATUS: ENCRYPTED & SECURE</p>
    </div>
    <div id="plansContainer"></div>
</div>

<div id="finance" class="page">
    <div class="glass-card">
        <h3 style="color:var(--success); margin:0;">DEPOSIT ASSETS</h3>
        <p style="font-size:10px; margin-bottom:15px; opacity:0.6;">JazzCash/SadaPay: 03705519562<br>EasyPaisa: 03379827882</p>
        <input id="depAmt" type="number" placeholder="Amount (PKR)">
        <input id="depTID" placeholder="TID Number">
        <div onclick="document.getElementById('depProof').click()" style="margin-top:15px; border:2px dashed #333; padding:20px; border-radius:20px; text-align:center; cursor:pointer;">
            <input type="file" id="depProof" accept="image/*" style="display:none;" onchange="handlePreview(this, 'pImg')">
            <img id="pImg" src="#" style="display:none; width:100%; max-height:100px; object-fit:contain; margin-bottom:10px;">
            <span id="pTxt" style="font-size:11px; opacity:0.5;">📸 Tap to Upload Proof</span>
        </div>
        <button class="btn-quantum" id="depBtn" onclick="submitDeposit()">SUBMIT REQUEST</button>
    </div>

    <div class="glass-card" style="border-color:var(--error);">
        <h3 style="color:var(--error); margin:0;">WITHDRAWAL</h3>
        <input id="witName" placeholder="Account Name">
        <input id="witNum" placeholder="Account Number">
        <select id="witMethod"><option>JazzCash</option><option>EasyPaisa</option><option>SadaPay</option></select>
        <input id="witAmt" type="number" placeholder="Withdraw Amount">
        <button class="btn-quantum" style="background:var(--error);" onclick="submitWithdraw()">REQUEST PAYOUT</button>
    </div>
</div>

<div id="history" class="page">
    <h3 style="letter-spacing:3px; padding-left:10px;">TRANSACTION LOGS</h3>
    <div id="historyList"></div>
</div>

<div id="adminDash">
    <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;">
        <h2 style="color:var(--neon);">ROOT_TERMINAL</h2>
        <button onclick="document.getElementById('adminDash').style.display='none'" style="color:var(--error); background:none; border:none; font-weight:800;">[EXIT]</button>
    </div>

    <div class="stat-grid">
        <div class="stat-box"><small>TOTAL USERS</small><div id="statUsers" style="font-size:18px; font-weight:800;">0</div></div>
        <div class="stat-box"><small>TOTAL DEPOSITS</small><div id="statInvest" style="font-size:18px; font-weight:800; color:var(--success);">0</div></div>
    </div>

    <div class="ghost-card">
        <small>PLAN ARCHITECT</small>
        <input id="admPName" placeholder="Node Name">
        <input id="admPPrice" type="number" placeholder="Price">
        <input id="admPProfit" type="number" placeholder="Daily Profit">
        <input type="file" id="admPImg" accept="image/*" onchange="handlePreview(this, 'admPImgPrev')">
        <img id="admPImgPrev" src="#" style="display:none; width:50px; margin-top:10px;">
        <button class="btn-quantum" onclick="admCreatePlan()">DEPLOY PLAN</button>
    </div>

    <div class="ghost-card"><small>PENDING REQUESTS</small><div id="admReqs" style="font-size:11px; margin-top:10px;"></div></div>
    <div class="ghost-card"><small>USER DATABASE</small><div id="admUserList" style="margin-top:10px;"></div></div>
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

  // --- BASE64 PREVIEW HELPER ---
  window.handlePreview = (input, imgId) => {
    if (input.files && input.files[0]) {
        const reader = new FileReader();
        reader.onload = (e) => {
            document.getElementById(imgId).src = e.target.result;
            document.getElementById(imgId).style.display = 'block';
            if(imgId === 'pImg') document.getElementById('pTxt').style.display = 'none';
        }
        reader.readAsDataURL(input.files[0]);
    }
  };

  // --- AUTH ---
  window.toggleAuth = (t) => { document.getElementById('loginForm').classList.toggle('hidden', t==='reg'); document.getElementById('regForm').classList.toggle('hidden', t==='login'); };
  window.handleReg = async () => {
    const u = document.getElementById('regUser').value.trim().toLowerCase();
    const p = document.getElementById('regPass').value;
    if(!u || !p) return alert("Fill all!");
    const s = await get(ref(db, 'users/'+u));
    if(s.exists()) return alert("Username taken!");
    await set(ref(db, 'users/'+u), { username: u, pass: p, balance: 0, status: 'Active' });
    alert("Success! Login now."); toggleAuth('login');
  };
  window.handleLogin = async () => {
    const u = document.getElementById('logUser').value.trim().toLowerCase();
    const p = document.getElementById('logPass').value;
    const s = await get(ref(db, 'users/'+u));
    if(s.exists() && s.val().pass === p) {
        if(s.val().status === 'Banned') return alert("You are banned!");
        localStorage.setItem('v_user', u); location.reload();
    } else alert("Invalid Login!");
  };
  window.logout = () => { localStorage.removeItem('v_user'); location.reload(); };

  // --- FINANCE (BASE64 DIRECT) ---
  window.submitDeposit = async () => {
    const amt = document.getElementById('depAmt').value;
    const tid = document.getElementById('depTID').value;
    const base64 = document.getElementById('pImg').src;
    if(!amt || !tid || base64.length < 100) return alert("Fill all details & Proof!");

    const reqRef = push(ref(db, 'admin/deposits'));
    await set(reqRef, { user, amt, tid, proof: base64, status: 'Pending', date: new Date().toLocaleString() });
    
    const hRef = push(ref(db, `history/${user}`));
    await set(hRef, { type: 'Deposit', amount: amt, status: 'Pending', date: new Date().toLocaleString() });
    alert("Proof Uploaded via Base64! Admin will verify, sweetie.");
    location.reload();
  };

  window.submitWithdraw = async () => {
    const amt = document.getElementById('witAmt').value;
    const name = document.getElementById('witName').value;
    const num = document.getElementById('witNum').value;
    const method = document.getElementById('witMethod').value;
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < amt) return alert("Insufficient Balance!");
    
    await update(ref(db, `users/${user}`), { balance: s.val().balance - amt });
    const reqRef = push(ref(db, 'admin/withdraws'));
    await set(reqRef, { user, amt, name, num, method, status: 'Pending' });
    const hRef = push(ref(db, `history/${user}`));
    await set(hRef, { type: 'Withdraw', amount: amt, status: 'Pending', date: new Date().toLocaleString() });
    alert("Withdrawal request sent!");
  };

  // --- ADMIN CORE ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clicks >= 7) { if(prompt("KEY:")==="NAZIM786") { document.getElementById('adminDash').style.display='block'; loadAdmin(); } clicks=0; } };

  function loadAdmin() {
    onValue(ref(db, 'users'), s => {
        document.getElementById('statUsers').innerText = s.exists() ? Object.keys(s.val()).length : 0;
        const list = document.getElementById('admUserList'); list.innerHTML = '';
        if(s.exists()) Object.values(s.val()).forEach(u => {
            list.innerHTML += `<div style="padding:10px; border-bottom:1px solid #222; display:flex; justify-content:space-between; font-size:11px;">
                <span>${u.username} (PKR ${u.balance})</span>
                <button onclick="admBan('${u.username}')" style="color:var(--error); background:none; border:none;">BAN</button>
            </div>`;
        });
    });

    onValue(ref(db, 'admin/deposits'), s => {
        const cont = document.getElementById('admReqs'); cont.innerHTML = '';
        if(s.exists()) Object.entries(s.val()).forEach(([id, r]) => {
            if(r.status === 'Pending') {
                cont.innerHTML += `<div class="stat-box" style="margin-bottom:10px; font-size:10px;">
                    User: ${r.user} | PKR ${r.amt} <br><img src="${r.proof}" style="width:100px; cursor:pointer;" onclick="window.open(this.src)"><br>
                    <button onclick="admApproveDep('${id}', '${r.user}', ${r.amt})" style="color:var(--success); border:none; background:none; font-weight:800; margin-top:5px;">APPROVE</button>
                </div>`;
            }
        });
    });
  }

  window.admApproveDep = async (id, target, amt) => {
    const s = await get(ref(db, `users/${target}`));
    await update(ref(db, `users/${target}`), { balance: (s.val().balance||0) + parseFloat(amt) });
    await update(ref(db, `admin/deposits/${id}`), { status: 'Approved' });
    alert("Approved!");
  };

  window.admCreatePlan = async () => {
    const n = document.getElementById('admPName').value;
    const p = document.getElementById('admPPrice').value;
    const pr = document.getElementById('admPProfit').value;
    const img = document.getElementById('admPImgPrev').src;
    if(!n || !img) return alert("Fill Plan!");
    await set(ref(db, `plans/${n}`), { name: n, price: p, profit: pr, url: img });
    alert("Plan Deployed!");
  };

  // --- APP INIT ---
  if(user) {
    document.getElementById('authPage').style.display='none';
    document.getElementById('mainNav').style.display='flex';
    document.getElementById('dash').classList.add('active');
    onValue(ref(db, `users/${user}`), s => {
        if(s.val().status === 'Banned') logout();
        document.getElementById('uBal').innerText = s.val().balance.toLocaleString();
        document.getElementById('hiUser').innerText = `Hi, ${user}!`;
    });
    onValue(ref(db, 'plans'), s => {
        const cont = document.getElementById('plansContainer'); cont.innerHTML = '';
        if(s.exists()) Object.values(s.val()).forEach(p => {
            cont.innerHTML += `<div class="glass-card" style="padding:0; overflow:hidden;">
                <img src="${p.url}" style="width:100%; height:150px; object-fit:cover;">
                <div style="padding:15px;">
                    <h3>${p.name}</h3>
                    <div style="display:flex; justify-content:space-between; font-size:12px; opacity:0.8;">
                        <span>Price: PKR ${p.price}</span>
                        <span>Daily: PKR ${p.profit}</span>
                    </div>
                    <button class="btn-quantum" style="font-size:11px; padding:12px;">Activate Node</button>
                </div>
            </div>`;
        });
    });
    onValue(ref(db, `history/${user}`), s => {
        const list = document.getElementById('historyList'); list.innerHTML = '';
        if(s.exists()) Object.values(s.val()).reverse().forEach(h => {
            list.innerHTML += `<div class="glass-card" style="padding:15px; display:flex; justify-content:space-between; font-size:12px;">
                <div><b>${h.type}</b><br><small>${h.date}</small></div>
                <div style="text-align:right;">PKR ${h.amount}<br><small style="color:${h.status==='Pending'?'var(--gold)':'var(--success)'}">${h.status}</small></div>
            </div>`;
        });
    });
  }

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };
</script>
</body>
</html>
