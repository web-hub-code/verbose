<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Cloud Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* UI COMPONENTS */
  header { text-align: center; padding: 50px 20px 20px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 14px; text-shadow: 0 0 30px var(--neon); color: #fff; }
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.5s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; backdrop-filter: blur(20px); margin-bottom: 20px; position: relative; }
  .stat-card { background: var(--card); border: 1px solid var(--border); padding: 18px; border-radius: 24px; text-align: left; }
  .stat-card small { font-size: 9px; opacity: 0.5; text-transform: uppercase; letter-spacing: 1px; }
  .stat-card div { font-size: 18px; font-weight: 800; margin-top: 5px; color: var(--neon); }

  .trusted-alert { background: rgba(0, 247, 255, 0.05); border: 1px solid var(--neon); padding: 15px; border-radius: 20px; display: flex; align-items: center; gap: 12px; font-size: 11px; margin-bottom: 20px; border-left: 5px solid var(--neon); }
  
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; outline: none; font-size: 12px; }
  .btn-quantum { width: 100%; padding: 18px; border-radius: 22px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; box-shadow: 0 10px 20px rgba(112,0,255,0.2); }

  /* ADMIN UI */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 20px; overflow-y: auto; }
  .admin-card { background: #0a0a0a; border: 1px solid #1a1a1a; padding: 20px; border-radius: 25px; margin-bottom: 15px; }
  .proof-img { width: 100%; border-radius: 15px; margin: 10px 0; border: 1px solid #333; cursor: zoom-in; }

  /* NAV BAR */
  .nav { position: fixed; bottom: 30px; left: 20px; right: 20px; background: rgba(10,10,10,0.85); backdrop-filter: blur(20px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<header id="adminTrigger">
    <div class="logo-text">VERBOSE</div>
    <div style="font-size:8px; opacity:0.5; margin-top:8px; letter-spacing:4px;">QUANTUM CLOUD INFRASTRUCTURE</div>
</header>

<div id="dash" class="page">
    <div class="trusted-alert">
        <span style="font-size:22px;">🛡️</span>
        <div><b>SECURE CLOUD ACTIVE</b><br>New York City, USA | ID: 03705519562</div>
    </div>

    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 25px;">
        <div class="stat-card" style="grid-column: span 2; background: linear-gradient(135deg, #0a0a0a, #000);">
            <small>Active Balance</small>
            <div style="font-size:32px;">PKR <span id="uBal">0.00</span></div>
        </div>
        <div class="stat-card"><small>Daily Profit</small><div id="uDaily">0.00</div></div>
        <div class="stat-card"><small>Total Mining</small><div id="uTotal">0.00</div></div>
    </div>

    <div class="glass-card" style="padding: 15px;">
        <small style="opacity:0.5; font-size:9px;">REFERRAL LINK</small>
        <div id="refLink" style="font-size:11px; color:var(--neon); margin-top:5px; word-break: break-all;">Loading...</div>
    </div>

    <h3 style="letter-spacing:2px; font-size:13px; margin: 25px 0 15px 5px;">CLOUD MINING NODES</h3>
    <div id="plansList"></div>

    <div style="text-align: center; font-size: 10px; opacity: 0.3; margin-top: 50px; line-height: 1.8;">
        VERBOSE TECHNOLOGY LLC<br>
        244 Madison Ave, New York, NY 10016<br>
        Support: webhub262@gmail.com
    </div>
</div>

<div id="finance" class="page">
    <div class="glass-card">
        <h3>DEPOSIT ASSETS</h3>
        <p style="font-size:10px; opacity:0.6;">JazzCash/SadaPay: 03705519562</p>
        <input id="dAmt" type="number" placeholder="Enter Amount">
        <input id="dTID" placeholder="TID Number">
        <input type="file" id="dFile" accept="image/*" style="margin-top:10px; font-size:10px;">
        <button class="btn-quantum" id="dBtn" onclick="userDeposit()">SUBMIT DEPOSIT</button>
    </div>
    <div class="glass-card">
        <h3>WITHDRAWAL</h3>
        <input id="wAmt" type="number" placeholder="Amount">
        <input id="wNum" placeholder="Account Number">
        <select id="wMethod"><option>JazzCash</option><option>EasyPaisa</option></select>
        <button class="btn-quantum" style="background:var(--error);" onclick="userWithdraw()">REQUEST PAYOUT</button>
    </div>
</div>

<div id="adminDash">
    <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:25px;">
        <h2 style="color:var(--neon); font-size:16px;">VERBOSE_ROOT_v10</h2>
        <button onclick="document.getElementById('adminDash').style.display='none'" style="color:var(--error); background:none; border:1px solid var(--error); padding:6px 12px; border-radius:12px; font-size:10px;">EXIT</button>
    </div>
    <div class="admin-card"><small style="color:var(--gold);">PENDING DEPOSITS</small><div id="admDepList"></div></div>
    <div class="admin-card"><small style="color:var(--error);">WITHDRAW REQUESTS</small><div id="admWitList"></div></div>
    <div class="admin-card">
        <small style="color:var(--success);">NODE ARCHITECT</small>
        <input id="pName" placeholder="Node Name">
        <input id="pPrice" type="number" placeholder="Price">
        <input id="pProfit" type="number" placeholder="Daily Profit">
        <input type="file" id="pFile" accept="image/*">
        <button class="btn-quantum" onclick="admAddPlan()">DEPLOY</button>
        <div id="admPlanList"></div>
    </div>
    <div class="admin-card"><small>USER DATABASE</small><div id="admUsers"></div></div>
</div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Cloud</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="logout()">Logout</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
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

  // --- ADMIN SECRET KEY: nazim786 ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    if(++clicks >= 7) {
        if(prompt("VERBOSE ROOT KEY:") === "nazim786") {
            document.getElementById('adminDash').style.display = 'block';
            loadAdminTerminal();
        }
        clicks = 0;
    }
  };

  // --- LOGIC: USER DEPOSIT & WITHDRAW ---
  window.userDeposit = async () => {
    const file = document.getElementById('dFile').files[0];
    const amt = document.getElementById('dAmt').value;
    const tid = document.getElementById('dTID').value;
    if(!file || !amt) return alert("All fields required, sweetie!");
    
    const dBtn = document.getElementById('dBtn'); dBtn.disabled = true; dBtn.innerText = "UPLOADING...";
    try {
        const path = sRef(storage, `proofs/${user}_${Date.now()}`);
        await uploadBytes(path, file);
        const url = await getDownloadURL(path);
        await set(ref(db, `admin/deposits/${Date.now()}`), { user, amt, tid, url, status:'Pending' });
        alert("Success! Admin is verifying."); location.reload();
    } catch(e) { alert("Error!"); dBtn.disabled = false; }
  };

  window.userWithdraw = async () => {
    const amt = document.getElementById('wAmt').value;
    const num = document.getElementById('wNum').value;
    const method = document.getElementById('wMethod').value;
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < amt) return alert("Insufficient Balance!");
    
    await update(ref(db, `users/${user}`), { balance: s.val().balance - amt });
    await set(ref(db, `admin/withdraws/${Date.now()}`), { user, amt, num, method, status:'Pending' });
    alert("Withdrawal Requested!");
  };

  // --- ADMIN LOGIC ---
  function loadAdminTerminal() {
    onValue(ref(db, 'admin/deposits'), s => {
        const div = document.getElementById('admDepList'); div.innerHTML = '';
        s.forEach(c => {
            const d = c.val();
            div.innerHTML += `<div class="admin-card" style="font-size:11px;">
                ${d.user} | PKR ${d.amt} | TID: ${d.tid}<br>
                <img src="${d.url}" class="proof-img" onclick="window.open(this.src)">
                <button onclick="approveDep('${c.key}','${d.user}',${d.amt})">APPROVE</button>
            </div>`;
        });
    });
    // Add logic for Withdrawals and User management here similarly
  }

  window.approveDep = async (id, target, amt) => {
    const s = await get(ref(db, `users/${target}`));
    await update(ref(db, `users/${target}`), { balance: (s.val().balance||0) + parseFloat(amt) });
    await remove(ref(db, `admin/deposits/${id}`));
    alert("Approved!");
  };

  // --- CORE UI LOGIC ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };

  if(user) {
    document.getElementById('dash').classList.add('active');
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('refLink').innerText = window.location.origin + "?ref=" + user;
    onValue(ref(db, `users/${user}`), s => {
        const u = s.val();
        document.getElementById('uBal').innerText = (u.balance || 0).toLocaleString();
        document.getElementById('uDaily').innerText = (u.dailyProfit || 0).toLocaleString();
        document.getElementById('uTotal').innerText = (u.totalMining || 0).toLocaleString();
        if(u.status === 'Banned') { localStorage.clear(); location.reload(); }
    });
  } else {
    // Show auth logic (not shown for brevity but same as v9)
  }
</script>
</body>
</html>
