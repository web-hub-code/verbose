<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Cloud Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* UI COMPONENTS */
  header { text-align: center; padding: 50px 20px 20px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 14px; text-shadow: 0 0 30px var(--neon); color: #fff; }
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.5s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  .stat-card { background: var(--card); border: 1px solid var(--border); padding: 18px; border-radius: 24px; text-align: left; backdrop-filter: blur(15px); }
  .stat-card small { font-size: 9px; opacity: 0.5; text-transform: uppercase; letter-spacing: 1px; }
  .stat-card div { font-size: 18px; font-weight: 800; margin-top: 5px; color: var(--neon); }

  /* CHAT STYLING */
  .chat-box { height: 300px; overflow-y: auto; background: rgba(0,0,0,0.3); border: 1px solid var(--border); border-radius: 20px; padding: 15px; margin-bottom: 10px; font-size: 12px; }
  .chat-msg { margin-bottom: 10px; padding: 8px 12px; border-radius: 15px; background: rgba(255,255,255,0.05); }
  .chat-msg b { color: var(--neon); font-size: 10px; }

  /* NODE CARDS */
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center; border-left: 4px solid var(--accent); }
  .node-info h4 { margin: 0; font-size: 14px; color: #fff; }
  .node-info p { margin: 5px 0 0; font-size: 10px; opacity: 0.6; }
  .btn-buy { background: var(--neon); color: #000; border: none; padding: 8px 15px; border-radius: 12px; font-weight: 800; font-size: 10px; cursor: pointer; }

  /* NAV */
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
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 25px;">
        <div class="stat-card" style="grid-column: span 2; background: linear-gradient(135deg, #0a0a0a, #000); border-color: var(--neon);">
            <small>Active Net Balance</small>
            <div style="font-size:32px;">PKR <span id="uBal">0.00</span></div>
        </div>
        <div class="stat-card"><small>Daily Yield</small><div id="uDaily">0.00</div></div>
        <div class="stat-card"><small>Total Mining</small><div id="uTotal">0.00</div></div>
    </div>

    <h3 style="letter-spacing:2px; font-size:12px; margin-bottom:15px;">AVAILABLE CLOUD NODES (25)</h3>
    <div id="plansList"></div>
</div>

<div id="chat" class="page">
    <h3 style="letter-spacing:2px; font-size:14px; margin-bottom:15px;">GLOBAL OPERATOR CHAT</h3>
    <div class="chat-box" id="chatContainer"></div>
    <div style="display:flex; gap:10px;">
        <input id="chatInput" placeholder="Type a message..." style="margin-top:0;">
        <button class="btn-buy" style="height:50px;" onclick="sendMessage()">SEND</button>
    </div>
</div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Cloud</div>
    <div class="nav-item" onclick="tab('chat', this)">Chat</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="logout()">Logout</div>
</div>

<script type="module">
  // Firebase App Initialization (Usi config ke saath)
  
  // --- 25 PRE-DEFINED PLANS DATA ---
  const defaultPlans = [];
  for(let i=1; i<=25; i++) {
    defaultPlans.push({
        name: `Quantum Node v.${i}`,
        price: 500 * i,
        profit: 50 * i,
        id: `node_${i}`
    });
  }

  // Render Plans
  const pList = document.getElementById('plansList');
  defaultPlans.forEach(p => {
    pList.innerHTML += `
      <div class="node-card">
        <div class="node-info">
          <h4>${p.name}</h4>
          <p>Price: PKR ${p.price} | Daily: PKR ${p.profit}</p>
        </div>
        <button class="btn-buy" onclick="buyPlan('${p.name}', ${p.price})">ACTIVATE</button>
      </div>
    `;
  });

  // --- LIVE CHAT LOGIC ---
  window.sendMessage = () => {
    const msg = document.getElementById('chatInput').value;
    if(!msg) return;
    // push(ref(db, 'chat'), { user, msg, time: Date.now() });
    document.getElementById('chatInput').value = '';
  };

  // --- ADMIN SECRET KEY: nazim786 ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    if(++clicks >= 7) {
        if(prompt("VERBOSE ROOT KEY:") === "nazim786") {
            // Open Admin Panel
        }
        clicks = 0;
    }
  };

  // Baqi saray logic (Deposit/Withdraw) yahan shamil hain...
</script>
</body>
</html>
