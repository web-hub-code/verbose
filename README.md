<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; }
  *{box-sizing:border-box}
  body { margin:0; font-family:Inter, sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
  
  /* Header */
  header { text-align:center; padding:30px; font-size:32px; font-weight:900; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; letter-spacing:2px; }

  /* Layout */
  .page { max-width:420px; margin:20px auto; background:rgba(255,255,255,0.03); padding:25px; border-radius:15px; border:1px solid rgba(0,255,240,0.1); box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
  input { width:100%; padding:14px; margin-top:12px; border-radius:10px; border:1px solid rgba(255,255,255,0.1); background:rgba(0,0,0,0.2); color:#fff; outline:none; }
  button { width:100%; padding:14px; margin-top:15px; border-radius:10px; border:none; background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:800; cursor:pointer; font-size:16px; }
  
  /* Nav */
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(15,17,20,0.95); display:flex; justify-content:space-around; padding:15px; border-top:1px solid rgba(0,255,240,0.1); backdrop-filter: blur(10px); }
  .nav-item { text-align:center; font-size:12px; cursor:pointer; opacity:0.7; }
  .hidden { display:none; }

  /* Dashboard Details */
  .user-card { background:linear-gradient(135deg, rgba(0,247,255,0.1), rgba(255,92,255,0.05)); padding:20px; border-radius:15px; border-left:4px solid var(--neon); margin-bottom:15px; }
  .plan-card { background:rgba(255,255,255,0.02); padding:15px; border-radius:12px; margin:10px 0; display:flex; justify-content:space-between; align-items:center; border:1px solid rgba(255,255,255,0.05); }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center; margin-bottom:10px;">Portal Access</h2>
  <p style="font-size:12px; text-align:center; color:rgba(255,255,255,0.5);">Enter details to Login or Create Account</p>
  
  <input id="u_name" type="text" placeholder="Username" autocomplete="off">
  <input id="u_pass" type="password" placeholder="Password">
  
  <button id="entryBtn">ENTER DASHBOARD</button>
  
  <div style="margin-top:20px; font-size:11px; color:rgba(255,255,255,0.4); text-align:center;">
    Securely encrypted by Prime Solutions Cloud
  </div>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-card">
    <div id="welcomeMsg" style="font-size:18px; font-weight:bold;">Welcome!</div>
    <div style="margin-top:10px; font-size:26px; font-weight:900;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:11px; color:var(--neon); text-transform:uppercase;">Available Balance</div>
  </div>
  
  <div class="user-card" style="background:rgba(0,0,0,0.2); border:none;">
    <p style="font-size:11px; margin:0 0 5px 0;">Your Referral Link:</p>
    <input id="refUrl" readonly style="font-size:10px; padding:8px; background:#000;">
    <button onclick="copyLink()" style="padding:8px; font-size:12px; margin-top:10px;">Copy Link</button>
  </div>
</div>

<div id="plansPage" class="page hidden">
  <h3 style="color:var(--neon); margin-top:0;">Available Plans (1-25)</h3>
  <div id="plansContainer"></div>
</div>

<div id="adminPage" class="page hidden" style="border: 2px dashed var(--accent);">
  <h2 style="text-align:center; color:var(--accent);">⚡ GOD MODE ⚡</h2>
  <input id="searchUser" placeholder="Enter Target Username">
  <button id="findBtn">Search User</button>
  
  <div id="editBox" class="hidden">
    <p id="targetDisplay" style="text-align:center; font-weight:bold;"></p>
    <input id="setBal" type="number" placeholder="New Balance Amount">
    <button id="saveBtn" style="background:var(--accent)">Update Balance</button>
  </div>
  
  <button onclick="changeTab('dashboard')" style="background:#333; color:#fff; margin-top:15px;">Exit Admin</button>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item" onclick="changeTab('dashboard')">🏠<br>Home</div>
  <div class="nav-item" onclick="changeTab('plansPage')">📦<br>Plans</div>
  <div class="nav-item" onclick="doLogout()">🚪<br>Logout</div>
  <div id="adminNav" class="nav-item hidden" onclick="changeTab('adminPage')">⚡<br>Admin</div>
</div>

<script type="module">
  // Firebase Modules
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  // Your Firebase Config
  const firebaseConfig = {
    apiKey: "AIzaSyCMG6KG_oD8cjEk4YpbxXik-C5q8K5MDHk",
    authDomain: "dark-web-9.firebaseapp.com",
    projectId: "dark-web-9",
    databaseURL: "https://dark-web-9-default-rtdb.firebaseio.com",
    appId: "1:564328425161:web:eb109ab77356dafe7f4f18"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // --- LOGIN / SIGNUP SYSTEM ---
  document.getElementById('entryBtn').onclick = async () => {
    const user = document.getElementById('u_name').value.trim().toLowerCase();
    const pass = document.getElementById('u_pass').value.trim();

    if(!user || !pass) { alert("Username aur Password dono zaroori hain!"); return; }

    const userRef = ref(db, 'users/' + user);
    
    try {
      const snap = await get(userRef);
      if(snap.exists()) {
        // Login Logic
        const data = snap.val();
        if(data.password === pass) {
          startSession(user, data);
        } else {
          alert("Password ghalat hai, sweetie!");
        }
      } else {
        // Signup Logic
        const newData = {
          username: user,
          password: pass,
          balance: 0,
          refCode: Math.random().toString(36).substring(7)
        };
        await set(userRef, newData);
        startApp(user, newData);
      }
    } catch(e) { alert("Error: " + e.message); }
  };

  function startSession(u, data) {
    localStorage.setItem('v_active_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    document.getElementById('mainBal').innerText = parseFloat(data.balance).toFixed(2);
    document.getElementById('refUrl').value = "https://gtv140.github.io/verbose/?ref=" + data.refCode;
    
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    renderPlans();
  }

  // --- PLANS GENERATOR ---
  function renderPlans() {
    const cont = document.getElementById('plansContainer');
    cont.innerHTML = "";
    for(let i=1; i<=25; i++) {
      const cost = Math.round(200 + (i-1)*(30000-200)/24);
      cont.innerHTML += `
        <div class="plan-card">
          <div><b>Plan ${i}</b><br><small style="color:var(--neon)">Investment: Rs ${cost}</small></div>
          <button style="width:70px; margin:0; font-size:11px;" onclick="alert('Contact 03705519562 to Activate')">BUY</button>
        </div>`;
    }
  }

  // --- GOD MODE (7 Taps) ---
  let taps = 0;
  document.getElementById('mainHeader').onclick = () => {
    taps++;
    if(taps === 7) {
      if(prompt("Admin Secret Key:") === "prime786") {
        document.getElementById('adminNav').classList.remove('hidden');
        changeTab('adminPage');
      }
      taps = 0;
    }
  };

  document.getElementById('findBtn').onclick = async () => {
    const target = document.getElementById('searchUser').value.trim().toLowerCase();
    const s = await get(ref(db, 'users/' + target));
    if(s.exists()) {
      document.getElementById('targetDisplay').innerText = "Editing: " + target;
      document.getElementById('setBal').value = s.val().balance;
      document.getElementById('editBox').classList.remove('hidden');
    } else { alert("User nahi mila!"); }
  };

  document.getElementById('saveBtn').onclick = async () => {
    const target = document.getElementById('searchUser').value.trim().toLowerCase();
    const newAmt = parseFloat(document.getElementById('setBal').value);
    await update(ref(db, 'users/' + target), { balance: newAmt });
    alert("Balance Update Ho Gaya!");
    if(localStorage.getItem('v_active_user') === target) {
        document.getElementById('mainBal').innerText = newAmt.toFixed(2);
    }
  };

  // --- NAVIGATION HELPERS ---
  window.changeTab = (id) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.getElementById(id).classList.remove('hidden');
  };
  
  window.doLogout = () => { localStorage.clear(); location.reload(); };
  
  window.copyLink = () => {
    const el = document.getElementById("refUrl");
    el.select();
    document.execCommand("copy");
    alert("Referral Link Copied!");
  };
</script>
</body>
</html>
