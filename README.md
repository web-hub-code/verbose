<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Master OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #8b5cf6;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f87171;
            --bg: #030712;
            --glass: rgba(255, 255, 255, 0.03);
            --border: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at 0% 0%, #1e1b4b 0%, #030712 100%);
            color: #f1f5f9;
            min-height: 100vh;
            padding: 20px;
        }

        /* Modern Animated Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid var(--border);
            border-radius: 40px;
            padding: 60px 20px;
            text-align: center;
            margin-bottom: 40px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        header h1 {
            font-size: clamp(30px, 6vw, 60px);
            font-weight: 800; letter-spacing: 10px;
            background: linear-gradient(to right, #fff, #a78bfa, #f472b6);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .live-status {
            display: inline-flex; align-items: center; gap: 10px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 10px 30px; border-radius: 50px; font-size: 13px;
            font-weight: 700; border: 1px solid var(--success);
            margin-bottom: 25px;
        }

        /* Agent Control Hub */
        .control-hub {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px;
            margin-bottom: 40px; max-width: 1400px; margin-inline: auto;
        }

        .control-hub input {
            background: #020617; border: 1px solid var(--border);
            padding: 20px; color: white; border-radius: 18px;
            font-family: 'JetBrains Mono', monospace; outline: none;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.3);
        }

        .control-hub input:focus { border-color: var(--primary); box-shadow: 0 0 20px rgba(139, 92, 246, 0.3); }

        /* Main Workspace */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 35px;
            max-width: 1600px; margin: 0 auto;
        }

        @media (max-width: 1100px) { .workspace { grid-template-columns: 1fr; } }

        .script-panel {
            background: rgba(15, 23, 42, 0.8);
            border-radius: 50px; border: 1px solid var(--border);
            padding: clamp(20px, 5vw, 60px);
        }

        /* Casual Dialogue Bubbles */
        .chat-block {
            margin-bottom: 60px; padding: 35px;
            background: var(--glass); border-radius: 35px;
            border-left: 8px solid var(--primary);
            position: relative;
        }

        .chat-block:hover { background: rgba(255,255,255,0.05); transform: translateY(-5px); }

        .phase-tag {
            background: var(--primary); color: white;
            padding: 6px 18px; border-radius: 10px;
            font-size: 11px; font-weight: 900; text-transform: uppercase;
            margin-bottom: 25px; display: inline-block;
        }

        .dialogue { font-size: clamp(19px, 3vw, 26px); line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px dashed var(--warning); }
        .ghap-shup-tip { 
            color: var(--success); font-weight: 600; display: block; 
            margin-top: 25px; font-size: 16px; border-top: 1px solid var(--border);
            padding-top: 15px; font-style: italic;
        }

        /* Sidebar & Rebuttals */
        .sidebar { display: flex; flex-direction: column; gap: 30px; }

        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 35px; padding: 35px;
        }

        .rebuttal-pill {
            background: #020617; border-radius: 20px; padding: 25px;
            margin-bottom: 20px; border-left: 5px solid var(--danger);
            cursor: pointer;
        }

        .rebuttal-pill:hover { transform: scale(1.03); background: #1e1b4b; }
        .rebuttal-pill strong { color: var(--danger); font-size: 14px; display: block; margin-bottom: 10px; text-transform: uppercase; }
        .rebuttal-pill p { font-size: 15px; color: #94a3b8; line-height: 1.6; }

        .action-btn {
            background: linear-gradient(135deg, #10b981, #059669);
            color: white; border: none; width: 100%;
            padding: 28px; border-radius: 25px; font-weight: 900;
            font-size: 22px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 20px 40px rgba(16, 185, 129, 0.4);
        }

        .action-btn:hover { transform: translateY(-8px); box-shadow: 0 30px 60px rgba(16, 185, 129, 0.5); }

        footer { text-align: center; padding: 80px; opacity: 0.4; font-size: 12px; letter-spacing: 3px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="live-status">● LIVE: NATURAL CONVERSATION MODE</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="margin-top: 20px; font-weight: 600; opacity: 0.7; font-size: 14px; letter-spacing: 4px;">PREMIUM WINDOWS NETWORK</p>
    </header>

    <div class="control-hub">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="chat-block">
                <span class="phase-tag">Step 1-3: Friendly Vibe Check</span>
                <div class="dialogue">
                    "Hey <span class="hl cu">Customer</span>! How’s your day going over in <span class="hl ci">City</span>? <br><br>
                    Listen, I’m <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. I’m not calling to sell you anything right now—honestly, we’re just offering <strong>free estimates</strong> for <span class="hl">future</span> window upgrades. <br><br>
                    Just checking—are you the <strong>homeowner</strong> there?"
                </div>
                <span class="ghap-shup-tip">🗣️ Ghap Shup: Chill hokar baat karein, jaise kisi dost ko call kiya ho.</span>
            </div>

            <div class="chat-block" style="border-left-color: var(--warning);">
                <span class="phase-tag">Step 4-8: Baton Baton Mein Info</span>
                <div class="dialogue">
                    "That’s great! You know, most people aren't ready to change windows *today*, and that's totally cool. <br><br>
                    Whenever you *do* decide to fix 'em up—maybe in <strong>3 months, 6 months</strong>, or even <strong>next year</strong>—it’s better to have the <strong>best market price</strong> already locked in. <br><br>
                    Just curious, are we talking about <strong>5 to 10 windows</strong> or a bit more?"
                </div>
                <span class="ghap-shup-tip">🗣️ Ghap Shup: "Next year" bolne se customer relax ho jata hai aur details de deta hai.</span>
            </div>

            <div class="chat-block" style="border-left-color: var(--success);">
                <span class="phase-tag">Step 9-12: Locking The Value</span>
                <div class="dialogue">
                    "Perfect! Since we offer the <strong>best market discounts</strong> (especially for <span class="hl">Seniors and Veterans</span>), let me just verify your <strong>ZIP and DOB</strong> real quick. <br><br>
                    I’ll have my specialist drop off a <strong>Zero-Cost Price-Locked Guide</strong>. It’s free info—keep it in a drawer and use it when YOU are ready. <br><br>
                    Do <strong>mornings</strong> work for a 2-minute drop-off, or are afternoons better?"
                </div>
                <span class="ghap-shup-tip">🗣️ Ghap Shup: "Keep it in a drawer" bolne se pressure khatam ho jata hai.</span>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 25px; font-size: 14px; letter-spacing: 2px;">FRIENDLY COMEBACKS</h4>
                
                <div class="rebuttal-pill">
                    <strong>"I'm not interested."</strong>
                    <p>"Haha, I totally get it! Most homeowners say that. That's why I'm just giving you the <strong>free info for later</strong>. No biggie!"</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Is this a sales call?"</strong>
                    <p>"Honestly? No. It’s an <strong>informational call</strong>. We give you the price guarantee, and you're the boss of when to use it!"</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Just mail it to me."</strong>
                    <p>"I'd love to, but these discounts are <strong>zip-code specific</strong>. We just drop it off—takes 2 minutes, and it's 100% free."</p>
                </div>
            </div>

            <div class="tool-card" style="background: rgba(139, 92, 246, 0.05);">
                <h4 style="color: var(--primary); font-size: 12px; margin-bottom: 15px;">AGENT MASTER TIP</h4>
                <p style="font-size: 14px; color: #94a3b8; line-height: 1.8;">
                    <strong>Sweetie</strong>, yaad rakhna: Robot mat banna. Agar customer hansi mazaq kare, toh aap bhi karein. Sale khud ba khud mil jayegi!
                </p>
            </div>

            <button class="action-btn" onclick="alert('Natural Lead Successfully Saved!')">Finish Friendly Chat</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | The Art of Natural Sales © 2026<br>
        Everything Modern, Premium & Animated
    </footer>
</div>

<script>
    function sync() {
        let ag = document.getElementById('agN').value || "Agent";
        let cu = document.getElementById('cuN').value || "Customer";
        let ci = document.getElementById('ciN').value || "City";

        document.querySelectorAll('.ag').forEach(e => e.innerText = ag);
        document.querySelectorAll('.cu').forEach(e => e.innerText = cu);
        document.querySelectorAll('.ci').forEach(e => e.innerText = ci);
    }
</script>

</body>
</html>
