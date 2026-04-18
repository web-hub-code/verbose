<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Master Lead OS</title>
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
        }

        /* Premium Header */
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
            font-size: 50px; font-weight: 800; letter-spacing: 8px;
            background: linear-gradient(to right, #fff, var(--primary), #a855f7);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .portal-badge {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 8px 25px; border-radius: 50px; font-size: 12px;
            font-weight: 700; border: 1px solid var(--success);
            margin-bottom: 20px;
        }

        /* Agent Input Hub */
        .input-hub {
            display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px;
            margin-bottom: 30px; max-width: 1500px; margin-inline: auto;
        }

        .input-hub input {
            background: #020617; border: 1px solid var(--border);
            padding: 18px; color: white; border-radius: 15px;
            font-family: 'JetBrains Mono', monospace; outline: none;
        }

        .input-hub input:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(99, 102, 241, 0.2); }

        /* Main Grid Layout */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 30px;
            max-width: 1600px; margin: 0 auto;
        }

        .script-panel {
            background: var(--card); border-radius: 40px;
            border: 1px solid var(--border); padding: 50px;
        }

        /* Step Logic Styling */
        .step-block {
            margin-bottom: 60px; padding-left: 35px;
            border-left: 5px solid var(--primary);
            position: relative;
            animation: fadeIn 0.6s ease-out;
        }

        .step-tag {
            background: var(--primary); color: white;
            padding: 6px 16px; border-radius: 8px;
            font-size: 11px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 20px; display: inline-block;
        }

        .dialogue { font-size: 24px; line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px solid var(--warning); }
        .benefit-hook { color: var(--success); font-weight: 600; display: block; margin-top: 20px; font-size: 16px; }

        /* Rebuttals & Sidebar */
        .sidebar { display: flex; flex-direction: column; gap: 25px; }

        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 30px; padding: 35px;
        }

        .rebuttal-pill {
            background: #020617; border-radius: 20px; padding: 25px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            cursor: pointer;
        }

        .rebuttal-pill:hover { transform: translateX(10px); background: #1e1b4b; }
        .rebuttal-pill strong { color: var(--danger); font-size: 13px; text-transform: uppercase; display: block; margin-bottom: 8px; }
        .rebuttal-pill p { font-size: 15px; color: #94a3b8; margin: 0; line-height: 1.6; }

        /* Timeline Selector */
        .time-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 20px; }
        .time-btn {
            background: rgba(255,255,255,0.05); border: 1px solid var(--border);
            color: #fff; padding: 12px; border-radius: 12px; font-size: 12px;
            font-weight: 600; cursor: pointer; text-align: center;
        }
        .time-btn:hover { background: var(--primary); }

        .submit-lead {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white; border: none; width: 100%;
            padding: 25px; border-radius: 22px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.3);
        }

        .submit-lead:hover { transform: translateY(-5px); box-shadow: 0 20px 50px rgba(16, 185, 129, 0.4); }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; letter-spacing: 2px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="portal-badge">● ELITE AGENT PORTAL | ACTIVE 2026</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="margin-top: 15px; font-weight: 600; opacity: 0.8; font-size: 14px; letter-spacing: 2px;">FUTURE HOME IMPROVEMENT NETWORK</p>
    </header>

    <div class="input-hub">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-block">
                <span class="step-tag">Phase 1: The Informational Hook</span>
                <div class="dialogue">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. We're reaching out to homeowners in <span class="hl ci">City</span>—not for a sales call, but to offer <strong>Free Estimates</strong> for your <span class="hl">future home improvements</span>. <br><br>
                    Whether it's windows or roofing, we want to provide you with the <strong>best market rates and discounts</strong> so you have them on file whenever you're ready. Are you the <strong>homeowner</strong>?"
                </div>
                <span class="benefit-hook">✅ CX GRAB: No sign-up, no cost—just market information for the future.</span>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-tag">Phase 2: Qualification (Timeline)</span>
                <div class="dialogue">
                    "We understand you're not looking to do this right now, and that's perfectly fine! <br><br>
                    Just so I can mark the right <strong>seasonal discount</strong> for you—<strong>how soon do you think you'll be ready to look into your windows?</strong> <br><br>
                    Maybe in a <span class="hl">couple of months</span>, <strong>3 to 6 months</strong>, or perhaps <strong>8 months to a year</strong>?"
                </div>
                <div class="time-grid">
                    <div class="time-btn">As Soon As Possible</div>
                    <div class="time-btn">2-3 Months (Planning)</div>
                    <div class="time-btn">6 Months (Future)</div>
                    <div class="time-btn">1 Year (Long Term)</div>
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-tag">Phase 3: Market Discount Lock</span>
                <div class="dialogue">
                    "Our company offers the <strong>best market-beating prices</strong>. To ensure we have the correct data for your report, what is your <strong>ZIP code</strong> and <strong>Date of Birth</strong>? <br><br>
                    This is strictly so we can apply the <span class="hl">Senior or Veteran incentives</span> to your future quote, keeping it 100% free of cost for you, <span class="hl cu">Customer</span>."
                </div>
                <span class="benefit-hook">✅ CX GRAB: Market-best pricing locked in for 12 months.</span>
            </div>

            <div class="step-block" style="border-left-color: var(--danger);">
                <span class="step-tag">Phase 4: The Drop-Off</span>
                <div class="dialogue">
                    "I’ll have our specialist visit for just a moment to drop off this <strong>Free Informational Price-Guide</strong>. <br><br>
                    This way, when you ARE ready, you’ll have the <strong>best discount already in your hands</strong>. Do mornings or afternoons work better for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 25px; font-size: 14px; letter-spacing: 1px;">🎯 CX TRUST REBUTTALS</h4>
                
                <div class="rebuttal-pill">
                    <strong>"I'm not buying anything today."</strong>
                    <p>"We're not selling anything today! This is strictly a <strong>Future Resource</strong> so you know the best market prices whenever you decide to move forward."</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Is this a sales or sign-up call?"</strong>
                    <p>"Not at all. There is <strong>no sign-up</strong> and no obligation. This is just a free informational service for homeowners in <span class="ci">City</span>."</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Why should I check your company?"</strong>
                    <p>"We offer <strong>maximum discounts</strong> and the best market price. Checking us now saves you thousands in the future."</p>
                </div>
            </div>

            <div class="tool-card" style="background: rgba(99, 102, 241, 0.05); border-color: var(--primary);">
                <h4 style="color: var(--primary); font-size: 12px; margin-bottom: 15px;">PRO AGENT TIPS</h4>
                <p style="font-size: 13px; color: #94a3b8; line-height: 2;">
                    • Emphasize <strong>"Free Informational Call"</strong>.<br>
                    • Use <strong>"Future Planning"</strong> to relax CX.<br>
                    • No pressure—focus on <strong>Market Benefits</strong>.
                </p>
            </div>

            <button class="submit-lead" onclick="alert('Future Lead Logged for Prime Solutions!')">Submit Future Lead</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Lead Generation Systems © 2026<br>
        Proprietary Script Architecture V10.0 | High-Conversion Informational Flow
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
