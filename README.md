<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Lead OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg: #030712;
            --panel: #0f172a;
            --glass: rgba(255, 255, 255, 0.03);
            --border: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at 0% 0%, #1e1b4b 0%, #030712 100%);
            color: #f1f5f9;
            min-height: 100vh;
            padding: 20px;
            line-height: 1.6;
        }

        /* Premium Animations */
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes pulseGlow { 0% { box-shadow: 0 0 0 0 rgba(99, 102, 241, 0.4); } 70% { box-shadow: 0 0 0 15px rgba(99, 102, 241, 0); } 100% { box-shadow: 0 0 0 0 rgba(99, 102, 241, 0); } }

        .container {
            max-width: 1600px;
            margin: 0 auto;
            animation: slideUp 0.8s ease-out;
        }

        /* Glass Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid var(--border);
            border-radius: 40px;
            padding: 60px 20px;
            text-align: center;
            margin-bottom: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
        }

        header h1 {
            font-size: 55px; font-weight: 800; letter-spacing: 8px;
            background: linear-gradient(to right, #fff, #6366f1, #a855f7);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase; margin-bottom: 10px;
        }

        .live-status {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 8px 20px; border-radius: 50px; font-size: 12px;
            font-weight: 700; border: 1px solid var(--success);
        }

        .dot { width: 8px; height: 8px; background: var(--success); border-radius: 50%; animation: pulseGlow 2s infinite; }

        /* Variable Inputs */
        .input-center {
            display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px;
            margin-bottom: 30px;
        }

        .input-center input {
            background: #020617; border: 1px solid var(--border);
            padding: 18px; color: white; border-radius: 15px;
            font-family: 'JetBrains Mono', monospace; outline: none;
            transition: 0.3s;
        }

        .input-center input:focus { border-color: var(--primary); background: #0f172a; }

        /* 12-Step Master Flow */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 30px;
        }

        .script-panel {
            background: var(--panel); border-radius: 40px;
            border: 1px solid var(--border); padding: 50px;
        }

        .step-block {
            margin-bottom: 60px; padding-left: 35px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-tag {
            background: var(--primary); color: white;
            padding: 5px 15px; border-radius: 8px;
            font-size: 11px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 20px; display: inline-block;
        }

        .dialogue { font-size: 24px; font-weight: 400; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px solid var(--warning); }
        .cx-hook { color: var(--success); font-weight: 600; display: block; margin-top: 15px; font-size: 16px; }

        /* Tools & Rebuttals */
        .sidebar { display: flex; flex-direction: column; gap: 25px; }

        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 30px; padding: 35px;
        }

        .rebuttal-box {
            background: #020617; border-radius: 20px; padding: 25px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            cursor: pointer; transition: 0.3s;
        }

        .rebuttal-box:hover { transform: translateX(10px); background: #1e1b4b; }
        .rebuttal-box strong { color: var(--danger); font-size: 13px; text-transform: uppercase; display: block; margin-bottom: 8px; }
        .rebuttal-box p { font-size: 15px; color: #94a3b8; margin: 0; }

        .action-btn {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white; border: none; width: 100%;
            padding: 25px; border-radius: 22px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.3);
            transition: 0.3s;
        }

        .action-btn:hover { transform: translateY(-5px); box-shadow: 0 20px 50px rgba(16, 185, 129, 0.4); }

        /* Copy Button */
        .copy-trigger {
            margin-top: 20px; background: rgba(255,255,255,0.05);
            border: 1px solid var(--primary); color: var(--primary);
            padding: 10px 20px; border-radius: 12px; cursor: pointer;
            font-weight: 700; font-size: 12px;
        }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; letter-spacing: 2px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="live-status"><span class="dot"></span> SECURE AGENT PORTAL ACTIVE</div>
        <h1>PRIME SOLUTIONS</h1>
        <div style="margin-top: 25px;">
            <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" style="color:var(--warning); text-decoration:none; font-weight:800; font-size:13px; border: 1px solid var(--warning); padding: 10px 25px; border-radius: 50px;">VISIT AGENCY PORTFOLIO</a>
        </div>
    </header>

    <div class="input-center">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-block">
                <span class="step-tag">Step 1-3: Intro & Interest</span>
                <div class="dialogue" id="d1">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. How's your afternoon going in <span class="hl ci">City</span>? <br><br>
                    I'm calling because you're eligible for a <strong>No-Cost Technical Audit</strong> under the <span class="hl">2026 Home Efficiency Program</span>. To confirm—are you the <strong>homeowner</strong>? <br><br>
                    Excellent! Are we looking at <strong>5 to 10 windows</strong> or more? And do you prefer <strong>Sliding or Casement</strong>?"
                </div>
                <span class="cx-hook">💡 Hook: We are currently in your neighborhood verifying local tax credits.</span>
                <button class="copy-trigger" onclick="copy('d1')">COPY DIALOGUE</button>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-tag">Step 4-6: Data Validation</span>
                <div class="dialogue" id="d2">
                    "To see the exact rebates for your street, what is your <strong>ZIP code</strong>? <br><br>
                    And for the record, what is your <strong>Date of Birth</strong>? This ensures you get the <span class="hl">Senior, Veteran, or Homeowner discounts</span> available on our database."
                </div>
                <span class="cx-hook">💡 Hook: Your DOB is required for the Federal Age-Based Incentive check.</span>
                <button class="copy-trigger" onclick="copy('d2')">COPY DIALOGUE</button>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-tag">Step 7-9: Credit & Plan</span>
                <div class="dialogue" id="d3">
                    "Are you planning this <strong>this month</strong>? For our <span class="hl">0% Interest & No-Money-Down</span> programs, what's your estimated credit range? <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
                <span class="cx-hook">💡 Hook: We match the interest rate to your score to ensure zero out-of-pocket costs.</span>
                <button class="copy-trigger" onclick="copy('d3')">COPY DIALOGUE</button>
            </div>

            <div class="step-block" style="border-left-color: var(--danger);">
                <span class="step-badge">Step 10-12: The 1-Year Lock</span>
                <div class="dialogue" id="d4">
                    "Perfect, <span class="hl cu">Customer</span>. Confirm your <strong>Full Address</strong> for the report. <br><br>
                    Our specialist will visit to drop off your <strong>Free 12-Month Price-Locked Estimate</strong>. Do <strong>mornings or evenings</strong> work best for you and your spouse?"
                </div>
                <span class="cx-hook">💡 Hook: Even if you're not ready now, the price is locked for 365 days.</span>
                <button class="copy-trigger" onclick="copy('d4')">COPY DIALOGUE</button>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 25px; font-size: 14px; letter-spacing: 1px;">🎯 CX GRAB REBUTTALS</h4>
                
                <div class="rebuttal-box">
                    <strong>"Why do you need my DOB?"</strong>
                    <p>"State incentives are higher for Seniors and Veterans. Your DOB validates you for the maximum possible credit."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Why both spouses?"</strong>
                    <p>"The report is a legal 12-month price-lock. We need both owners present to finalize the technical specs together."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Is this a sales call?"</strong>
                    <p>"This is a Technical Assessment. We provide the data and the price lock; you decide when or if you want to use it."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"I'm busy right now."</strong>
                    <p>"I understand! This takes only 60 seconds to lock your rebate spot. Let's finish the last 2 questions."</p>
                </div>
            </div>

            <div class="tool-card" style="background: rgba(99, 102, 241, 0.05); border-color: var(--primary);">
                <h4 style="color: var(--primary); font-size: 12px; margin-bottom: 15px;">PRO AGENT STATS</h4>
                <p style="font-size: 13px; color: #94a3b8; line-height: 2;">
                    • Current Lead Conv: <span style="color:white;">8.4%</span><br>
                    • Top State: <span style="color:white;">Florida / Texas</span><br>
                    • Best Hook: <span style="color:white;">"12-Month Price Lock"</span>
                </p>
            </div>

            <button class="action-btn" onclick="alert('Lead Logged into Prime Solutions CRM!')">Submit Final Lead</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Web Development & Lead Systems © 2026<br>
        Proprietary Script Architecture V6.0 | Engineered for High Conversions
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

    function copy(id) {
        let text = document.getElementById(id).innerText;
        navigator.clipboard.writeText(text);
        alert("Dialogue Copied to Clipboard!");
    }
</script>

</body>
</html>
