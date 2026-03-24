<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Cloud Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* AUTH SCREEN */
  #authPage { position: fixed; inset: 0; background: var(--bg); z-index: 20000; padding: 20px; display: flex; flex-direction: column; justify-content: center; align-items: center; }
  .auth-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 45px 30px; border-radius: 40px; backdrop-filter: blur(30px); text-align: center; box-shadow: 0 20px 50px rgba(0,0,0,0.5); }
  .auth-logo { font-size: 36px; font-weight: 800; letter-spacing: 15px; text-shadow: 0 0 25px var(--neon); margin-bottom: 5px; }
  
  /* INPUTS & BUTTONS */
  input, select { width: 100%; padding: 18px; margin-top: 15px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 14px; }
  .btn-primary { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 25px; box-shadow: 0 10px 25px rgba(112,0,255,0.3); }
  .wa-help { display: block; margin-top: 25px; font-size: 11px; color: var(--success); text-decoration: none; font-weight: 700; letter-spacing: 0.5px; }

  /* HOME PAGE UI */
  header { text-align: center; padding: 45px 20px 10px; cursor: pointer; }
  .page { max-width: 450px; margin: 0 auto; padding: 10px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease-out; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

  .balance-card { background: linear-gradient(160deg, #0a0a0a, #000); border: 1px solid var(--border); padding: 35px; border-radius: 40px; margin-bottom: 30px; border-top: 1px solid var(--neon); }
  
  /* NODE LISTING */
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 35px; padding: 20px; display: flex; align-items: center; gap: 18px; margin-bottom: 15px; border-left: 5px solid var(--accent); }
  .node-icon { width: 55px; height: 55px; background: rgba(0,247,255,0.03); border: 1px solid var(--neon); border-radius: 20px; display: flex; align-items: center; justify-content: center; font-size: 24px; box-shadow: 0 0 15px rgba(0,247,255,0.1); }
  .node-info h4 { margin: 0; font-size: 14px; font-weight: 800; }
  .node-info p { margin: 3px 0 0; font-size: 10px; opacity: 0.5; }
  .buy-btn { margin-left: auto; background: var(--neon); color: #000; border: none; padding: 10px 16px; border-radius: 14px; font-weight: 800; font-size: 10px; cursor: pointer; }

  /* LIVE CHAT */
  .chat-box { height: 380px; overflow-y: auto; background: rgba(255,255,255,0.01); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; }
  .msg { margin-bottom: 12px; padding: 12px 18px; border-radius: 20px; background: rgba(255,255,255,0.04); font-size: 12px; position: relative; }
  .msg b { color: var(--neon); display: block; font-size: 9px; margin-bottom: 4px; text-transform: uppercase; }
  .adm-msg { border: 1px solid var(--gold); background: rgba(255,204,0,0.05); }
  .adm-msg b { color: var(--gold) !important; text-shadow: 0 0 8px var(--gold); }

  /* NAV */
  .nav { position: fixed; bottom: 30px; left: 20px; right: 20px; background: rgba(10,10,10,0.92); backdrop-filter: blur(20px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; letter-spacing: 1px; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  /* TOAST */
  #toast { position: fixed; top: 20px; right: 20px; left: 20px; background: rgba(0,0,0,0.85); border: 1px solid var(--success); padding: 15px; border-radius: 20px; font-size: 11px; z-index: 30000; display: none; backdrop-filter: blur(10px); text-align: center; }
</style>
</head>
<body>

<div id="toast"></div>

<div id="authPage">
    <div class="auth-card">
        <div class="auth-logo">VERBOSE</div>
        <p style="font-size:9px; opacity:0.4; letter-spacing:4px; margin-bottom:30px;">QUANTUM DATA INFRASTRUCTURE</p>
        <div id="authBox">
            <input id="authPhone" type="number" placeholder="Mobile Node ID">
            <input id="authPass" type="password" placeholder="Access Key (Password)">
            <button class="btn-primary" onclick="handleAuth()">INITIALIZE SYSTEM</button>
            <p id="authSwitch" style="font-size:11px; margin-top:20px; cursor:pointer; color:var(--neon);" onclick="toggleAuth()">New User? Register Node</p>
            <a href="https://wa.me/923705519562?text=Hello%20Admin,%20I%20need%20help%20recovering%20my%20VERBOSE%20account." class="wa-help">
                💬 FORGOT KEY? CONTACT WHATSAPP SUPPORT
            </a>
        </div>
    </div>
</div>

<header id="adminTrigger">
    <div class="logo-text">VERBOSE</div>
    <div style="font-size:8px; opacity:0.5; margin-top:8px; letter-spacing:4px;">NEW YORK DATA CENTER v16.0</div>
</header>

<div id="dash" class="page">
    <div class="balance-card">
        <small style="opacity:0.5; text-transform:uppercase; letter-spacing:1.5px; font-size:9px;">Active Cloud Balance</small>
        <div style="font-size:36px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <h3 style="letter-spacing:2px; font-size:11px; margin: 0 0 20px 5px; opacity:0.8;">MINING SERVERS ONLINE</h3>
    <div id="nodeGrid"></div>
</div>

<div id="chatPage" class="page">
    <h3 style="letter-spacing:2px; font-size:13px; margin-bottom:20px;">OPERATOR GLOBAL NETWORK</h3>
    <div class="chat-box" id="chatBox"></div>
    <div style="display:flex; gap:10px;">
        <input id="cInput" placeholder="Secure transmission..." style="margin-top:0; flex:1;">
        <button class="btn-primary" style="margin-top:0; width:80px; border-radius:18px;" onclick="sendMsg()">SEND</button>
    </div>
</div>

<div id="finance" class="page">
    <div class="balance-card" style="padding:25px; margin-bottom:15px;">
        <h3 style="margin:0 0 10px 0; font-size:16px;">DEPOSIT ASSETS</h3>
        <p style="font-size:10px; opacity:0.6;">JazzCash/SadaPay: 03705519562</p>
        <input id="dAmt" type="number" placeholder="Enter Amount">
        <input id="dTID" placeholder="Transaction ID (TID)">
        <input type="file" id="dFile" style="font-size:10px;">
        <button class="btn-primary" onclick="userDeposit()">SUBMIT DEPOSIT</button>
    </div>
</div>

<nav class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Nodes</div>
    <div class="nav-item" onclick="tab('chatPage', this)">Chat</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="logout()">Exit</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get, push } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  let isLogin = true;
  let user = localStorage.getItem('v_user');

  // --- RENDER 25 NODES ---
  const icons = ["📡", "🛰️", "🚀", "🧬", "💎", "⚡", "🌀", "🛰️", "🛸"];
  const grid = document.getElementById('nodeGrid');
  for(let i=1; i<=25; i++) {
    let price = 500 * i;
    let icon = icons[i % icons.length];
    grid.innerHTML += `
      <div class="node-card">
        <div class="node-icon">${icon}</div>
        <div class="node-info">
            <h4>Server Alpha v.${i}</h4>
            <p>Cost: PKR ${price} | Daily: PKR ${50*i}</p>
        </div>
        <button class="buy-btn" onclick="buyNode(${price})">BUY</button>
      </div>`;
  }

  // --- AUTH LOGIC ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value;
    const s = document.getElementById('authPass').value;
    if(!p || !s) return alert("Fill all credentials, sweetie!");

    const r = ref(db, `users/${p}`);
    const snap = await get(r);

    if(isLogin) {
        if(snap.exists() && snap.val().pass === s) {
            localStorage.setItem('v_user', p);
            location.reload();
        } else alert("Invalid Node ID or Key!");
    } else {
        if(snap.exists()) return alert("Node ID already active!");
        await set(r, { pass: s, balance: 0, status: 'Active' });
        localStorage.setItem('v_user', p);
        location.reload();
    }
  };

  window.toggleAuth = () => {
    isLogin = !isLogin;
    document.getElementById('authSwitch').innerText = isLogin ? "New User? Register Node" : "Existing Operator? Access ID";
  };

  // --- FAKE PAYOUT SYSTEM ---
  setInterval(() => {
    const t = document.getElementById('toast');
    const u = ["Ali", "Sara", "Khan", "Deep", "Zain"][Math.floor(Math.random()*5)];
    const a = [1000, 5000, 12000, 800][Math.floor(Math.random()*4)];
    t.innerHTML = `💸 <b>Transmission:</b> ${u} withdrawn <b>PKR ${a}</b> via JazzCash`;
    t.style.display = 'block';
    setTimeout(() => t.style.display = 'none', 4000);
  }, 18000);

  // --- GLOBAL UI ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };

  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authPage').style.display = 'none';
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');
    onValue(ref(db, `users/${user}`), s => {
        document.getElementById('uBal').innerText = (s.val().balance || 0).toLocaleString();
    });
  }
</script>
</body>
</html>
