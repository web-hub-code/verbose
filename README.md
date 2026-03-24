<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Nexus Fixed v4.0</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.4s; font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* GHOST ADMIN */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 20px; overflow-y: auto; }
  .ghost-card { background: #0a0a0a; border: 1px solid #1a1a1a; padding: 20px; border-radius: 25px; margin-bottom: 15px; }
  
  /* UI */
  header { text-align: center; padding: 40px 20px 10px; font-size: 24px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; }
  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; backdrop-filter: blur(40px); margin-bottom: 20px; position: relative; }
  
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; outline: none; font-size: 13px; }
  .btn-quantum { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; }
  
  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); display: none; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; color: #fff; font-weight: 800; text-transform: uppercase; cursor: pointer; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<header id="adminTrigger">VERBOSE</header>

<div id="authPage" style="position:fixed; top:0; left:0; width:100%; height:100%; background:#000; z-index:10000; display:flex; align-items:center; justify-content:center; padding:20px;">
    <div class="glass-card" style="width:100%; max-width:400px; text-align:center;">
        <h1 id="authTitle" style="letter-spacing:5px;">AUTHORIZE</h1>
        <div id="loginForm">
            <input id="logUser" placeholder="Username">
            <input id="logPass" type="password" placeholder="Password">
            <button class="btn-quantum" onclick="handleLogin()">ACCESS NEXUS</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('reg')">Create New Identity</p>
        </div>
        <div id="regForm" class="hidden" style="display:none;">
            <input id="regUser" placeholder="Username">
            <input id="regPass" type="password" placeholder="Password">
            <button class="btn-quantum" onclick="handleReg()">INITIALIZE</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('login')">Back to Login</p>
        </div>
    </div>
</div>

<div id="dash" class="page">
    <div class="glass-card" style="background: linear-gradient(135deg, #0a0a0a, #000); border-color: var(--neon);">
        <h2 id="hiUser" style="margin:0;">Operator</h2>
        <div style="font-size:42px; font-weight:800; margin:10px 0; color:var(--neon);">PKR <span id="uBal">0.00</span></div>
    </div>
    <div id="plansContainer"></div>
</div>

<div id="finance" class="page">
    <div class="glass-card">
        <h3>DEPOSIT PROOF</h3>
        <select id="depMethod">
            <option>JazzCash (03705519562)</option>
            <option>EasyPaisa (03379827882)</option>
        </select>
        <input id="depAmt" type="number" placeholder="Amount">
        <input id="depTID" placeholder="TID Number">
        <p style="font-size:10px; opacity:0.6; margin-top:15px;">Choose Screenshot:</p>
        <input type="file" id="depProof" accept="image/*" style="font-size:10px;">
        <button class="btn-quantum" id="depBtn" onclick="submitDeposit()">UPLOAD & SUBMIT</button>
    </div>
</div>

<div id="adminDash">
    <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;">
        <h2 style="color:var(--neon);">ROOT_TERMINAL</h2>
        <button onclick="document.getElementById('adminDash').style.display='none'" style="color:var(--error); background:none; border:none;">[EXIT]</button>
    </div>

    <div class="ghost-card">
        <small>CREATE NEW PLAN</small>
        <input id="pName" placeholder="Node Name">
        <input id="pPrice" type="number" placeholder="Cost">
        <input id="pProfit" type="number" placeholder="Daily Profit">
        <input type="file" id="pImage" accept="image/*">
        <button class="btn-quantum" id="planBtn" onclick="admCreatePlan()">DEPLOY PLAN</button>
    </div>

    <div class="ghost-card">
        <small>PLAN MANAGEMENT</small>
        <div id="admPlanList"></div>
    </div>
</div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
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

  // --- IMAGE UPLOAD LOGIC (FIXED) ---
  window.submitDeposit = async () => {
    const file = document.getElementById('depProof').files[0];
    const amt = document.getElementById('depAmt').value;
    const tid = document.getElementById('depTID').value;
    const btn = document.getElementById('depBtn');

    if(!file || !amt) return alert("Please fill all details and select image!");
    
    btn.innerText = "UPLOADING...";
    btn.disabled = true;

    try {
        const storagePath = sRef(storage, `deposits/${user}_${Date.now()}`);
        const snapshot = await uploadBytes(storagePath, file);
        const downloadURL = await getDownloadURL(snapshot.ref);

        const reqRef = push(ref(db, 'admin/deposits'));
        await set(reqRef, { user, amt, tid, url: downloadURL, status: 'Pending', date: new Date().toLocaleString() });
        
        alert("Deposit submitted successfully, sweetie!");
        location.reload();
    } catch (error) {
        console.error(error);
        alert("Upload Failed! Check Firebase Rules.");
        btn.innerText = "SUBMIT AGAIN";
        btn.disabled = false;
    }
  };

  // --- ADMIN: CREATE PLAN (FIXED) ---
  window.admCreatePlan = async () => {
    const file = document.getElementById('pImage').files[0];
    const name = document.getElementById('pName').value;
    const price = document.getElementById('pPrice').value;
    const profit = document.getElementById('pProfit').value;
    const btn = document.getElementById('planBtn');

    if(!file || !name) return alert("Fill Plan Details!");
    btn.innerText = "DEPLOYING...";

    try {
        const storagePath = sRef(storage, `plans/${Date.now()}_${name}`);
        const snapshot = await uploadBytes(storagePath, file);
        const downloadURL = await getDownloadURL(snapshot.ref);

        await set(ref(db, `plans/${name}`), { name, price, profit, url: downloadURL });
        alert("Plan Deployed!");
        location.reload();
    } catch (e) { alert("Admin Upload Failed!"); btn.innerText = "DEPLOY PLAN"; }
  };

  // --- ADMIN TRIGGER ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clicks >= 7) { if(prompt("KEY:")==="NAZIM786") { document.getElementById('adminDash').style.display='block'; loadPlans(); } clicks=0; } };

  function loadPlans() {
    onValue(ref(db, 'plans'), s => {
        const list = document.getElementById('admPlanList'); list.innerHTML = '';
        if(s.exists()) Object.values(s.val()).forEach(p => {
            list.innerHTML += `<div style="display:flex; justify-content:space-between; padding:10px; border-bottom:1px solid #222;">
                <span>${p.name}</span>
                <button onclick="admDelPlan('${p.name}')" style="color:red; background:none; border:none;">DELETE</button>
            </div>`;
        });
    });
  }
  window.admDelPlan = (name) => { if(confirm("Delete this plan?")) remove(ref(db, `plans/${name}`)); };

  // --- AUTH & USER SYNC ---
  window.toggleAuth = (t) => {
    document.getElementById('loginForm').style.display = t === 'reg' ? 'none' : 'block';
    document.getElementById('regForm').style.display = t === 'reg' ? 'block' : 'none';
  };
  window.handleLogin = async () => {
    const u = document.getElementById('logUser').value.trim().toLowerCase();
    const p = document.getElementById('logPass').value;
    const s = await get(ref(db, `users/${u}`));
    if(s.exists() && s.val().pass === p) { localStorage.setItem('v_user', u); location.reload(); } else alert("Failed!");
  };
  window.handleReg = async () => {
    const u = document.getElementById('regUser').value.trim().toLowerCase();
    const p = document.getElementById('regPass').value;
    await set(ref(db, `users/${u}`), { username: u, pass: p, balance: 0 });
    alert("Success!"); toggleAuth('login');
  };
  window.logout = () => { localStorage.removeItem('v_user'); location.reload(); };

  if(user) {
    document.getElementById('authPage').style.display='none';
    document.getElementById('mainNav').style.display='flex';
    document.getElementById('dash').classList.add('active');
    onValue(ref(db, `users/${user}`), s => document.getElementById('uBal').innerText = s.val().balance.toLocaleString());
    onValue(ref(db, 'plans'), s => {
        const cont = document.getElementById('plansContainer'); cont.innerHTML = '';
        if(s.exists()) Object.values(s.val()).forEach(p => {
            cont.innerHTML += `<div class="glass-card" style="padding:0; overflow:hidden;">
                <img src="${p.url}" style="width:100%; height:160px; object-fit:cover;">
                <div style="padding:15px;">
                    <h3>${p.name}</h3>
                    <div style="display:flex; justify-content:space-between; font-size:12px; opacity:0.8;">
                        <span>Price: PKR ${p.price}</span>
                        <span>Daily: PKR ${p.profit}</span>
                    </div>
                    <button class="btn-quantum" style="font-size:11px; padding:12px;">Activate Now</button>
                </div>
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
