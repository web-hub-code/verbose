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
            --bg: #020617;
            --card: #0f172a;
            --glass: rgba(255, 255, 255, 0.03);
            --border: rgba(255, 255, 255, 0.08);
        }

        * { box-sizing: border-box; transition: all 0.3s ease; }
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at top right, #1e1b4b, #020617);
            color: #f1f5f9;
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }

        /* Premium Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(20px);
            border: 1px solid var(--border);
            border-radius: 35px;
            padding: 50px 20px;
            text-align: center;
            margin-bottom: 30px;
            position: relative;
            overflow: hidden;
        }

        header h1 { 
            font-size: 52px; font-weight: 800; letter-spacing: 5px; margin: 0;
            background: linear-gradient(to right, #fff, var(--primary));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .status-pill {
            background: rgba(16, 185, 129, 0.1);
            color: var(--success);
            padding: 6px 20px;
            border-radius: 50px;
            font-size: 12px;
            font-weight: 700;
            border: 1px solid var(--success);
            display: inline-block;
            margin-bottom: 15px;
            letter-spacing: 1px;
        }

        /* Variable Input Bar */
        .control-hub {
            background: var(--card);
            border: 1px solid var(--border);
            padding: 25px;
            border-radius: 25px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 30px;
        }

        .control-hub input {
            background: #020617;
            border: 1px solid #1e293b;
            padding: 15px;
            color: white;
            border-radius: 12px;
            outline: none;
            font-family: 'JetBrains Mono', monospace;
        }

        .control-hub input:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(99, 102, 241, 0.2); }

        /* Main Workspace */
        .workspace {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 25px;
            max-width: 1550px;
            margin: 0 auto;
        }

        /* Script Panel */
        .script-panel {
            background: var(--card);
            border-radius: 40px;
            border: 1px solid var(--border);
            padding: 50px;
        }

        .step-container {
            margin-bottom: 50px;
            padding-left: 30px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-badge {
            background: var(--primary);
            color: white;
            padding: 5px 15px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 800;
            text-transform: uppercase;
            margin-bottom: 15px;
            display: inline-block;
        }

        .dialogue { font-size: 23px; line-height: 1.8; color: #cbd5e1; }
        .hl { color: var(--warning); font-weight: 800; text-decoration: underline; }
        .trust-hook { color: var(--success); font-weight: 600; font-style: italic; }

        /* Functional Buttons */
        .btn-group { margin-top: 20px; display: flex; gap: 10px; }
        .copy-btn {
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--primary);
            color: var(--primary);
            padding: 10px 20px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 700;
        }
        .copy-btn:hover { background: var(--primary); color: white; }

        /* Sidebar Tools */
        .sidebar { display: flex; flex-direction: column; gap: 20px; }
        
        .tool-card {
            background: var(--glass);
            border: 1px solid var(--border);
            border-radius: 30px;
            padding: 30px;
        }

        .rebuttal-box {
            background: #020617;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            border-left: 4px solid var(--danger);
            cursor: help;
        }

        .rebuttal-box strong { color: var(--danger); font-size: 13px; display: block; margin-bottom: 5px; text-transform: uppercase; }
        .rebuttal-box p { font-size: 14px; color: #94a3b8; margin: 0; line-height: 1.6; }

        .trust-meter {
            text-align: center;
            padding: 20px;
            background: rgba(16, 185, 129, 0.05);
            border-radius: 20px;
            border: 1px dashed var(--success);
        }

        .final-btn {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white;
            padding: 25px;
            border-radius: 20px;
            border: none;
            font-weight: 900;
            font-size: 20px;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 15px 35px rgba(16, 185, 129, 0.3);
        }

        .final-btn:hover { transform: translateY(-5px); box-shadow: 0 20px 45px rgba(16, 185, 129, 0.4); }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; }

        /* Animations */
        @keyframes slideIn { from { opacity: 0; transform: translateX(-20px); } to { opacity: 1; transform: translateX(0); } }
        .step-container { animation: slideIn 0.5s ease-out forwards; }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <div class="status-pill">● SECURE & TRUSTED 2026 NETWORK</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="margin-top: 15px; opacity: 0.8; font-weight: 600;">USA Home Efficiency & Lead Validation System</p>
    </header>

    <div class="control-hub">
        <input type="text" id="agInput" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuInput" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciInput" placeholder="City/Location..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-container">
                <span class="step-badge">Phase 1: Verification (Steps 1-3)</span>
                <div class="dialogue" id="d1">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. How are you doing today in <span class="hl ci">City</span>? <br><br>
                    We’re reaching out regarding the <span class="hl">2026 Federal Energy-Efficiency Rebates</span>. To ensure accuracy—are you the <strong>homeowner</strong>? <br><br>
                    <span class="trust-hook">(Trust Hook: We are currently verifying street-level eligibility for your county.)</span> <br><br>
                    Great! Are we looking at <strong>5 to 10 windows</strong> or more? And do you prefer <strong>Sliding or Casement</strong>?"
                </div>
                <div class="btn-group">
                    <button class="copy-btn" onclick="copy('d1')">COPY DIALOGUE</button>
                </div>
            </div>

            <div class="step-container" style="border-left-color: var(--warning);">
                <span class="step-badge">Phase 2: Data Validation (Steps 4-6)</span>
                <div class="dialogue" id="d2">
                    "To access the precise tax incentives for your specific ZIP, may I have your <strong>ZIP code</strong>? <br><br>
                    And for the official record, what is your <strong>Date of Birth</strong>? This is strictly to verify <span class="hl">Senior, Veteran, or Homeowner discounts</span> available on our system."
                </div>
                <div class="btn-group">
                    <button class="copy-btn" onclick="copy('d2')">COPY DIALOGUE</button>
                </div>
            </div>

            <div class="step-container" style="border-left-color: var(--success);">
                <span class="step-badge">Phase 3: The Price Lock (Steps 7-12)</span>
                <div class="dialogue" id="d3">
                    "Are you planning this <strong>this month</strong>? For our <span class="hl">0% interest / No-Money-Down</span> programs, what is your credit range? <br><br>
                    Lastly, <span class="hl cu">Customer</span>, we'll have a specialist visit to drop off a <strong>Free 12-Month Price-Locked Technical Report</strong>. <br><br>
                    Do <strong>mornings or evenings</strong> work best for you and your spouse?"
                </div>
                <div class="btn-group">
                    <button class="copy-btn" onclick="copy('d3')">COPY DIALOGUE</button>
                </div>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin: 0 0 20px 0; font-size: 14px;">🎯 CX GRAB REBUTTALS</h4>
                
                <div class="rebuttal-box">
                    <strong>"Why do you need my ZIP?"</strong>
                    <p>"State rebates vary by county. Your ZIP allows us to see exactly which federal funds are reserved for your street."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Why both spouses?"</strong>
                    <p>"The report is a legal 12-month price guarantee. We need both owners present to finalize the technical data together."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"I'm not buying today."</strong>
                    <p>"That’s the best part! Our report is valid for a full year. We lock the lowest price today, and you decide when you're ready."</p>
                </div>
            </div>

            <div class="tool-card">
                <div class="trust-meter">
                    <p style="margin:0; font-size:12px; color: var(--success); font-weight:800;">CX TRUST METER: HIGH</p>
                    <div style="height:8px; background:var(--success); width:95%; border-radius:10px; margin-top:10px;"></div>
                </div>
                <p style="font-size: 13px; color: #94a3b8; margin-top: 20px; line-height: 1.6;">
                    • Use "Technical Audit" instead of "Sales Call".<br>
                    • Mention "12-Month Price Lock" 3 times.<br>
                    • Refer to the specialist as a "Field Auditor".
                </p>
            </div>

            <button class="final-btn" onclick="alert('Appointment Logged & Locked!')">Lock Certified Appointment</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Branding & Lead Generation Systems © 2026<br>
        Proprietary OS V5.0 | High-Conversion Script Architecture
    </footer>
</div>

<script>
    function sync() {
        let ag = document.getElementById('agInput').value || "Agent";
        let cu = document.getElementById('cuInput').value || "Customer";
        let ci = document.getElementById('ciInput').value || "City";

        document.querySelectorAll('.ag').forEach(e => e.innerText = ag);
        document.querySelectorAll('.cu').forEach(e => e.innerText = cu);
        document.querySelectorAll('.ci').forEach(e => e.innerText = ci);
    }

    function copy(id) {
        let text = document.getElementById(id).innerText;
        navigator.clipboard.writeText(text);
        alert("Dialogue Copied!");
    }
</script>

</body>
</html>
