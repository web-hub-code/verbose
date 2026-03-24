<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Financial Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.04); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* UI COMPONENTS */
  header { text-align: center; padding: 75px 20px 10px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 10px; text-shadow: 0 0 20px var(--neon); }
  .page { max-width: 450px; margin: 0 auto; padding: 10px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* MODERN NODE CARD */
  .node-box { background: var(--card); border: 1px solid var(--border); border-radius: 35px; padding: 25px; margin-bottom: 20px; position: relative; overflow: hidden; border-left: 5px solid var(--neon); }
  .node-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 15px; }
  .node-title { font-size: 18px; font-weight: 800; color: #fff; }
  .node-price { font-size: 14px; color: var(--neon); font-weight: 600; }
  
  .node-stats { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; margin: 15px 0; border-top: 1px solid var(--border); padding-top: 15px; }
  .n-stat { text-align: center; }
  .n-stat small { font-size: 8px; opacity: 0.5; text-transform: uppercase; display: block; }
  .n-stat b { font-size: 12px; color: #fff; }

  /* BUTTONS & INPUTS */
  .btn-buy { width: 100%; padding: 15px; border-radius: 18px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 5px 15px rgba(0,247,255,0.2); }
  .btn-buy:disabled { background: #333; cursor: not-allowed; opacity: 0.5; box-shadow: none; }
  
  /* NAV & TICKER */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(25px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<header id="adminTrigger"><div class="logo-text">VERBOSE</div></header>

<div id="dash" class="page">
    <div style="background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 30px; border-radius: 35px; margin-bottom: 20px; text-align: center;">
        <span style="font-size:10px; color:var(--neon); letter-spacing:2px;" id="dispUser">OPERATOR</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div style="background: rgba(112,0,255,0.1); border: 1px dashed var(--accent); padding: 15px; border-radius: 20px; text-align: center;">
        <small style="font-size:9px; opacity:0.6;">NEXT PROFIT IN</small>
        <div id="timer" style="font-size:24px; font-weight:800; color:var(--accent);">23:59:59</div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">INVESTMENT MARKET</h3>
    <div id="nodeGrid"></div>
</div>

<div id="historyPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">LOGS</h3>
    <div id="histGrid"></div>
</div>

<nav class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('historyPage', this)">Logs</div>
    <div class="nav-item" onclick="logout()" style="color:var(--error);">Exit</div>
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
  let user = localStorage.getItem('v_user');
  let currentBalance = 0;

  // --- RENDER NODES ---
  const grid = document.getElementById('nodeGrid');
  const nodeData = [
    { name: "Alpha Core", price: 500, daily: 50, days: 30 },
    { name: "Beta Node", price: 1000, daily: 110, days: 30 },
    { name: "Gamma Pulse", price: 2500, daily: 280, days: 30 },
    { name: "Delta Link", price: 5000, daily: 600, days: 30 },
    { name: "Omega Prime", price: 10000, daily: 1300, days: 30 }
  ];

  nodeData.forEach((node, i) => {
    grid.innerHTML += `
      <div class="node-box">
        <div class="node-header">
            <div class="node-title">${node.name}</div>
            <div class="node-price">PKR ${node.price}</div>
        </div>
        <div class="node-stats">
            <div class="n-stat"><small>Daily</small><b>PKR ${node.daily}</b></div>
            <div class="n-stat"><small>Period</small><b>${node.days} Days</b></div>
            <div class="n-stat"><small>Total</small><b>PKR ${node.daily * node.days}</b></div>
        </div>
        <button class="btn-buy" id="btn-${i}" onclick="buyNode(${node.price}, '${node.name}', ${node.daily})">ACTIVATE SERVER</button>
      </div>`;
  });

  // --- BUY LOGIC ---
  window.buyNode = async (price, name, daily) => {
    if(currentBalance < price) {
        alert("Sweetie, balance kam hai! Please deposit first. 😘");
        return;
    }

    const newBal = currentBalance - price;
    const userRef = ref(db, `users/${user}`);
    
    // Deduct Balance & Update Income
    await update(userRef, { 
        balance: newBal,
        daily: daily // Node income set ho jayega
    });

    // Add to History
    push(ref(db, `users/${user}/history`), {
        type: "Node Purchase: " + name,
        amt: "-" + price,
        date: new Date().toLocaleDateString()
    });

    alert(`Successfully Activated ${name}! Your mining has started, sweetie! 😘`);
  };

  // --- UI SYNC ---
  if(user) {
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');
    
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        currentBalance = d.balance || 0;
        document.getElementById('uBal').innerText = currentBalance.toLocaleString();
        document.getElementById('dispUser').innerText = "OPERATOR: " + d.name.toUpperCase();
        
        // History Render
        const hGrid = document.getElementById('histGrid');
        hGrid.innerHTML = '';
        if(d.history) {
            Object.values(d.history).reverse().forEach(h => {
                hGrid.innerHTML += `<div style="background:var(--card); padding:15px; border-radius:15px; margin-bottom:10px; display:flex; justify-content:space-between; font-size:11px;">
                    <span>${h.type}</span><b style="color:var(--neon)">${h.amt}</b></div>`;
            });
        }
    });
  }

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };
</script>
</body>
</html>
