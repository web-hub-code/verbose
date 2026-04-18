<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Master OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg: #030712;
            --card: #0f172a;
            --glass: rgba(255, 255, 255, 0.03);
            --border: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; transition: 0.3s ease; }
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at 0% 0%, #1e1b4b 0%, #030712 100%);
            color: #f1f5f9;
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        /* Premium Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid var(--border);
            border-radius: 40px;
            padding: 50px 20px;
            text-align: center;
            margin-bottom: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
            position: relative;
        }

        header h1 {
            font-size: clamp(30px, 5vw, 55px);
            font-weight: 800; letter-spacing: 8px;
            background: linear-gradient(to right, #fff, var(--primary), #a855f7);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .live-badge {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 8px 25px; border-radius: 50px; font-size: 12px;
            font-weight: 700; border: 1px solid var(--success);
            margin-bottom: 20px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.5; } 100% { opacity: 1; } }

        /* Variable Input Hub */
        .control-hub {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;
            margin-bottom: 30px; max-width: 1400px; margin-inline: auto;
        }

        .control-hub input {
            background: #020617; border: 1px solid var(--border);
            padding: 18px; color: white; border-radius: 15px;
            font-family: 'JetBrains Mono', monospace; outline: none;
            font-size: 14px;
        }

        .control-hub input:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(99, 102, 241, 0.2); }

        /* Main Grid */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 30px;
            max-width: 1600px; margin: 0 auto;
        }

        @media (max-width: 1024px) { .workspace { grid-template-columns: 1fr; } }

        .script-panel {
            background: var(--card); border-radius: 40px;
            border: 1px solid var(--border); padding: clamp(20px, 5vw, 50px);
        }

        /* Script Step Styling */
        .step-block {
            margin-bottom: 50px; padding-left: 30px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-tag {
            background: var(--primary); color: white;
            padding: 6px 16px; border-radius: 8px;
            font-size: 11px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 20px; display: inline-block;
        }

        .dialogue { font-size: clamp(18px, 3vw, 24px); line-height: 1.8; color: #cbd5e1; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px solid var(--warning); }
        .soft-hook { color: var(--success); font-weight: 600; display: block; margin-top: 20px; font-size: 16px; }

        /* Sidebar & Rebuttals */
        .sidebar { display: flex; flex-direction: column; gap: 25px; }

        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 30px; padding: 30px;
        }

        .rebuttal-pill {
            background: #020617; border-radius: 20px; padding: 25px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            cursor: pointer;
        }

        .rebuttal-pill:hover { transform: translateX(10px); background: #1e1b4b; }
        .rebuttal-pill strong { color: #f87171; font-size: 13px; display: block; margin-bottom: 8px; text-transform: uppercase; }
        .rebuttal-pill p { font-size: 15px; color: #94a3b8; line-height: 1.6; }

        /* Timeline Selector */
        .time-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-top: 20px; }
        .time-btn {
            background: rgba(255,255,255,0.05); border: 1px solid var(--border);
            color: #fff; padding: 12px; border-radius: 12px; font-size: 12px;
            font-weight: 600; cursor: pointer; text-align: center;
        }
        .time-btn:hover, .time-btn.active { background: var(--primary); border-color: white; }

        .submit-lead {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white; border: none; width: 100%;
            padding: 25px; border-radius: 22px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.3);
        }

        .submit-lead:hover { transform: translateY(-5px); box-shadow: 0 20px 50px rgba(16, 185, 129, 0.4); }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; letter-spacing: 2px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="live-badge">● SECURE MASTER PORTAL | FUTURE PLANNING 2026</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="margin-top: 15px; font-weight: 600; opacity: 0.8; letter-spacing: 2px;">ELITE HOME IMPROVEMENT NETWORK</p>
    </header>

    <div class="control-hub">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City/Location..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-block">
                <span class="step-tag">Phase 1: The Informational Hook</span>
                <div class="dialogue">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. We're reaching out to homeowners in <span class="hl ci">City</span>—not for a sales or sign-up call, but to offer <strong>Free Estimates</strong> for your <span class="hl">future home improvements</span>. <br><br>
                    Our company offers the <strong>best prices and discounts</strong> in the market, so we want to provide this free info for whenever you might need it. Are you the <strong>homeowner</strong>?"
                </div>
                <span class="soft-hook">💡 CX Grab: This is a 100% free informational call for your future records.</span>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-tag">Phase 2: Qualification (The "When")</span>
                <div class="dialogue">
                    "We understand you’re not looking to do this right now, and that's perfectly fine! <br><br>
                    Just so I can mark the right <strong>seasonal discount</strong> for you—<strong>how soon do you think you'll be ready for windows or improvements?</strong> <br><br>
                    Maybe in a <span class="hl">couple of months</span>, <strong>3 to 6 months</strong>, or perhaps <strong>8 months to a year</strong>?"
                </div>
                <div class="time-grid">
                    <div class="time-btn" onclick="this.classList.toggle('active')">ASAP</div>
                    <div class="time-btn" onclick="this.classList.toggle('active')">2-3 Months</div>
                    <div class="time-btn" onclick="this.classList.toggle('active')">6 Months</div>
                    <div class="time-btn" onclick="this.classList.toggle('active')">1 Year+</div>
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-tag">Phase 3: Security & Savings</span>
                <div class="dialogue">
                    "Perfect, <span class="hl cu">Customer</span>. To ensure you get the <strong>highest discount compared to the market</strong>, may I verify your <strong>ZIP code</strong> and <strong>DOB</strong>? <br><br>
                    This is strictly to apply any <span class="hl">Senior, Veteran, or Homeowner incentives</span> available. Our specialist will just drop off a <strong>Free Price-Locked Guide</strong> for your future thinking. <br><br>
                    Does a morning or afternoon work for a quick drop-off?"
                </div>
                <span class="soft-hook">💡 CX Grab: Lock the best price today; decide whenever you are ready.</span>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 25px; font-size: 14px; letter-spacing: 1px;">🎯 ELITE CX REBUTTALS</h4>
                
                <div class="rebuttal-pill">
                    <strong>"I'm not interested right now."</strong>
                    <p>"I completely understand! That's why we're here—not for today, but for your <strong>future</strong> project. We just want you to have the best market numbers on hand."</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Is this a sales call?"</strong>
                    <p>"Not at all. This is a <strong>free informational call</strong>. There is no sign-up required. It’s just to show you what benefits our company offers homeowners."</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Why should I choose you?"</strong>
                    <p>"Because we guarantee the <strong>best price and highest discounts</strong> in the market. It costs nothing to check and think about it."</p>
                </div>
            </div>

            <div class="tool-card" style="background: rgba(99, 102, 241, 0.05); border-color: var(--primary);">
                <h4 style="color: var(--primary); font-size: 12px; margin-bottom: 15px;">AGENT GUIDELINES</h4>
                <p style="font-size: 13px; color: #94a3b8; line-height: 2;">
                    • Stick to <strong>"Future Improvement"</strong>.<br>
                    • Mention <strong>"No Sign-Up"</strong> twice.<br>
                    • Focus on <strong>Market Discounts</strong>.<br>
                    • Keep the tone <strong>Helpful & Relaxed</strong>.
                </p>
            </div>

            <button class="submit-lead" onclick="alert('Future Lead Successfully Logged!')">Submit Future Lead</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Lead OS V12.0 FINAL<br>
        Proprietary Scripting Architecture © 2026
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
