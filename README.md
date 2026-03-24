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

  /* HEADER */
  header { text-align: center; padding: 50px 20px 20px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 14px; text-shadow: 0 0 30px var(--neon); color: #fff; }
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.5s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  /* DASHBOARD CARDS */
  .stat-card { background: var(--card); border: 1px solid var(--border); padding: 18px; border-radius: 24px; text-align: left; backdrop-filter: blur(15px); }
  .stat-card small { font-size: 9px; opacity: 0.5; text-transform: uppercase; letter-spacing: 1px; }
  .stat-card div { font-size: 18px; font-weight: 800; margin-top: 5px; color: var(--neon); }

  /* CHAT STYLING */
  .chat-box { height: 350px; overflow-y: auto; background: rgba(255,255,255,0.02); border: 1px solid var(--border); border-radius: 25px; padding: 15px; margin-bottom: 10px; }
  .chat-msg { margin-bottom: 12px; padding: 10px 15px; border-radius: 18px; background: rgba(255,255,255,0.04); font-size: 12px; position: relative; }
  .chat-msg b { color: var(--neon); display: block; font-size: 10px; margin-bottom: 3px; }
  .admin-msg { border: 1px solid var(--gold); background: rgba(255,204,0,0.05); }
  .admin-msg b { color: var(--gold) !important; text-shadow: 0 0 5px var(--gold); }
  .admin-badge { background: var(--gold); color: #000; padding: 2px 6px; border-radius: 5px; font-size: 8px; font-weight: 800; margin-left: 5px; }

  /* CLOUD NODES */
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center; border-left: 4px solid var(--accent); }
  .node-info h4 { margin: 0; font-size: 14px; color: #fff; }
  .node-info p { margin: 5px 0 0; font-size: 10px; opacity: 0.6; }
  .btn-buy { background: var(--neon); color: #000; border: none; padding: 10px 18px; border-radius: 15px; font-weight: 800; font-size: 10px; cursor: pointer; }

  /* NAV */
  .nav { position: fixed; bottom: 30px; left: 20px; right: 20px; background: rgba(10,10,10,0.85); backdrop-filter: blur(20px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  /* ADMIN UI */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 20px; overflow-y: auto; }
</style>
</head>
<body>

<header id="adminTrigger">
    <div class="logo-text">VERBOSE</div>
    <div style="font-size:8px; opacity:0.5; margin-top:8px; letter-spacing:4px;">QUANTUM CLOUD INFRASTRUCTURE</div>
</header>

<div id="dash" class="page">
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 25px;">
        <div class="stat-card" style="grid-column: span 2; background: linear-gradient(135deg, #0a0a0a, #000); border-color: var(--neon);">
            <small>Active Net Balance</small>
            <div style="font-size:32px;">PKR <span id="uBal">0.00</span></div>
        </div>
        <div class="stat-card"><small>Daily Yield</small><div id="uDaily">0.00</div></div>
        <div class="stat-card"><small>Total Mining</small><div id="uTotal">0.00</div></div>
    </div>
    <div class="stat-card" style="margin-bottom: 25px; border-style: dashed;">
        <small>Share & Earn (10%)</small>
        <div id="refLink" style="font-size: 10px; color: var(--accent); margin-top: 5px; word-break: break-all;">---</div>
    </div>
    <h3 style="letter-spacing:2px; font-size:12px; margin-bottom:15px;">CLOUD NODES (ONLINE)</h3>
    <div id="plansList"></div>
</div>

<div id="chatPage" class="page">
    <h3 style="letter-spacing:2px; font-size:14px; margin-bottom:15px;">OPERATOR NETWORK CHAT</h3>
    <div class="chat-box" id="chatContainer"></div>
    <div style="display:flex; gap:10px;">
        <input id="chatInput" placeholder="Type a transmission..." style="flex:1; background:rgba(255,255,255,0.05); border:1px solid var(--border); border-radius:15px; padding:15px; color:#fff;">
        <button class="btn-buy" style="height:50px;" onclick="sendChatMessage()">SEND</button>
    </div>
</div>

<div id="finance" class="page">
    <div class="stat-card" style="margin-bottom:20px;">
        <h3>DEPOSIT</h3>
        <p style="font-size:10px; opacity:0.6;">JazzCash/SadaPay: 03705519562</p>
        <input id="dAmt" type="number" placeholder="PKR Amount">
        <input id="dTID" placeholder="TID Number">
        <input type="file" id="dFile" style="font-size:10px; margin-top:10px;">
        <button class="btn-buy" style="width:100%; margin-top:15px;" onclick="userDeposit()">SUBMIT ASSETS</button>
    </div>
    <div class="stat-card">
        <h3>WITHDRAW</h3>
        <input id="wAmt" type="number" placeholder="PKR Amount">
        <input id="wNum" placeholder="Account Number">
        <select id="wMethod"><option>JazzCash</option><option>EasyPaisa</option></select>
        <button class="btn-quantum" style="background:var(--error); margin-top:15px;" onclick="userWithdraw()">REQUEST PAYOUT</button>
    </div>
</div>

<div id="adminDash">
    <div style="display:flex; justify-content:space-between; margin-bottom:25px;">
        <h2 style="color:var(--neon); font-size:16px;">VERBOSE_ROOT_ACCESS</h2>
        <button onclick="document.getElementById('adminDash').style.display='none'" style="color:var(--error); border:1px solid var(--error); background:none; padding:10px; border-radius:12px;">EXIT</button>
    </div>
    <div id="admContent">
        </div>
</div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Nodes</div>
    <div class="nav-item" onclick="tab('chatPage', this)">Chat</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="logout()">Exit</div>
</div>

<script type="module">
  // FIREBASE CONFIG (verbose-6c008 active)
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get, remove, push } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    storageBucket: "verbose-6c008.appspot.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  let user = localStorage.getItem('v_user');
  let isAdmin = (user === "nazim786");

  // --- RENDER 25 PLANS ---
  const pList = document.getElementById('plansList');
  for(let i=1; i<=25; i++){
      let price = 500 * i;
      let profit = 50 * i;
      pList.innerHTML += `
        <div class="node-card">
            <div class="node-info">
                <h4>Quantum Node v.${i}</h4>
                <p>Cost: PKR ${price} | Daily Yield: PKR ${profit}</p>
            </div>
            <button class="btn-buy" onclick="buyPlan(${price}, ${profit})">ACTIVATE</button>
        </div>`;
  }

  // --- LIVE CHAT SYSTEM ---
  window.sendChatMessage = () => {
    const input = document.getElementById('chatInput');
    if(!input.value) return;
    push(ref(db, 'chat'), {
        sender: user,
        msg: input.value,
        role: isAdmin ? 'admin' : 'user',
        time: Date.now()
    });
    input.value = '';
  };

  onValue(ref(db, 'chat'), s => {
    const container = document.getElementById('chatContainer');
    container.innerHTML = '';
    s.forEach(child => {
        const d = child.val();
        const isAdminMsg = d.role === 'admin';
        container.innerHTML += `
            <div class="chat-msg ${isAdminMsg ? 'admin-msg' : ''}">
                <b>@${d.sender} ${isAdminMsg ? '<span class="admin-badge">ADMIN</span>' : ''}</b>
                ${d.msg}
            </div>`;
    });
    container.scrollTop = container.scrollHeight;
  });

  // --- ADMIN TRIGGER ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    if(++clicks >= 7) {
        let key = prompt("ENTER ROOT KEY:");
        if(key === "nazim786") {
            document.getElementById('adminDash').style.display = 'block';
            // loadAdminPanel(); // Function to load lists
        }
        clicks = 0;
    }
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };

  // Main Auth Check
  if(user) {
    document.getElementById('dash').classList.add('active');
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('refLink').innerText = window.location.origin + "?ref=" + user;
  }
</script>
</body>
</html>
