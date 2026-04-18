<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Lead OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg: #020617;
            --card: #0f172a;
            --border: rgba(255,255,255,0.1);
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--bg);
            color: #f1f5f9;
            margin: 0;
            padding: 20px;
        }

        .master-wrapper {
            max-width: 1400px;
            margin: 0 auto;
            background: var(--card);
            border-radius: 40px;
            border: 1px solid var(--border);
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.9);
        }

        /* Agency Branding Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4338ca 100%);
            padding: 40px;
            text-align: center;
            border-bottom: 5px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 42px; font-weight: 800; letter-spacing: 4px; }
        .links { margin-top: 15px; }
        .links a { 
            color: var(--warning); text-decoration: none; font-size: 13px; font-weight: 600; 
            padding: 8px 20px; border: 1px solid var(--warning); border-radius: 50px; margin: 0 5px;
            transition: 0.3s;
        }
        .links a:hover { background: var(--warning); color: #000; }

        /* Dynamic Input Bar */
        .var-bar {
            background: rgba(99, 102, 241, 0.1);
            padding: 20px 40px;
            display: flex;
            gap: 15px;
            border-bottom: 1px solid var(--border);
        }

        .var-bar input {
            background: #020617;
            border: 1px solid #334155;
            padding: 12px;
            color: white;
            border-radius: 10px;
            flex: 1;
            outline: none;
        }

        .var-bar input:focus { border-color: var(--primary); }

        .main-grid {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: var(--border);
        }

        .panel { background: var(--card); padding: 40px; }

        /* Step Styling */
        .step-block {
            margin-bottom: 45px;
            border-left: 5px solid var(--primary);
            padding-left: 25px;
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

        .dialogue { font-size: 21px; line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; }

        /* Action Buttons */
        .copy-btn {
            margin-top: 15px;
            background: var(--glass);
            border: 1px solid var(--primary);
            color: var(--primary);
            padding: 8px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 700;
        }

        .copy-btn:hover { background: var(--primary); color: white; }

        /* Sidebar Rebuttals (Clickable) */
        .rebuttal-card {
            background: #020617;
            border: 1px solid #1e293b;
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 15px;
            cursor: pointer;
            transition: 0.3s;
        }

        .rebuttal-card:hover { border-color: var(--danger); }
        .rebuttal-card strong { color: var(--danger); font-size: 13px; display: block; margin-bottom: 5px; }
        .rebuttal-card p { font-size: 14px; color: #94a3b8; margin: 0; line-height: 1.5; }

        .submit-btn {
            background: var(--success);
            color: white;
            width: 100%;
            padding: 25px;
            border: none;
            border-radius: 20px;
            font-weight: 900;
            font-size: 18px;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.2);
            margin-top: 20px;
        }

        footer {
            text-align: center;
            padding: 40px;
            background: #020617;
            font-size: 13px;
            color: #475569;
        }
    </style>
</head>
<body>

<div class="master-wrapper">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <div class="links">
            <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" target="_blank">Agency Portfolio</a>
            <a href="https://web-hub-code.github.io/script/" target="_blank">User Script Hub</a>
        </div>
    </header>

    <div class="var-bar">
        <input type="text" id="custName" placeholder="Customer Name..." onkeyup="updateVars()">
        <input type="text" id="cityName" placeholder="City Name..." onkeyup="updateVars()">
        <input type="text" id="agentName" placeholder="Your Name..." onkeyup="updateVars()">
    </div>

    <div class="main-grid">
        <div class="panel">
            
            <div class="step-block">
                <span class="step-badge">Step 1-3: Intro & Verification</span>
                <div class="dialogue" id="s1">
                    "Hi, this is <span class="hl agent">Agent</span> from <strong>Prime Solutions</strong>. How are you today? <br><br>
                    We’re verifying homeowners in <span class="hl city">Your City</span> for the <span class="hl">2026 Home Energy Credits</span>. Are you the <strong>homeowner</strong>? <br><br>
                    Great! How many windows are we looking at—<strong>5 to 10</strong> or more?"
                </div>
                <button class="copy-btn" onclick="copyText('s1')">CLICK TO COPY DIALOGUE</button>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-badge">Step 4-6: Rebate Data</span>
                <div class="dialogue" id="s2">
                    "To check the exact rebate for your street, what is your <strong>ZIP code</strong>? <br><br>
                    And for the record, what is your <strong>Date of Birth</strong>? This is strictly to apply <span class="hl">Senior or Military discounts</span> to your estimate."
                </div>
                <button class="copy-btn" onclick="copyText('s2')">CLICK TO COPY DIALOGUE</button>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-badge">Step 7-10: Credit & Financing</span>
                <div class="dialogue" id="s3">
                    "For our <span class="hl">0% interest plans</span>, what range is your credit score in? Most people check their banking app—I'll wait. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
                <button class="copy-btn" onclick="copyText('s3')">CLICK TO COPY DIALOGUE</button>
            </div>

            <div class="step-block" style="border-left-color: var(--danger);">
                <span class="step-badge">Step 11-12: The 12-Month Lock</span>
                <div class="dialogue" id="s4">
                    "Perfect, <span class="hl name">Customer</span>. Confirm your address. <br><br>
                    Our expert will visit for a <span class="hl">Free 12-Month Price-Locked Report</span>. Do mornings or evenings work for you and your spouse?"
                </div>
                <button class="copy-btn" onclick="copyText('s4')">CLICK TO COPY DIALOGUE</button>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid var(--border);">
            <h4 style="color: var(--success); margin-top: 0; font-size: 14px;">LIVE REBUTTAL ENGINE</h4>
            
            <div class="rebuttal-card">
                <strong>"Why do you need my ZIP?"</strong>
                <p>"Rebates are county-specific. Your ZIP ensures we find the exact local credits for your area."</p>
            </div>

            <div class="rebuttal-card">
                <strong>"Why both spouses?"</strong>
                <p>"The quote is a legal 12-month price-lock. We need both owners to receive the data together."</p>
            </div>

            <div class="rebuttal-card">
                <strong>"Is this a sales call?"</strong>
                <p>"This is a technical assessment for the rebate. We provide the price-locked data, you decide when to use it."</p>
            </div>

            <div style="background: rgba(99, 102, 241, 0.1); padding: 20px; border-radius: 15px; margin-top: 20px;">
                <h4 style="margin:0; font-size:12px; color: var(--primary);">PRO TIPS:</h4>
                <ul style="font-size: 13px; color: #94a3b8; padding-left: 20px; line-height: 1.8;">
                    <li>Call it a <b>"Technical Audit."</b></li>
                    <li>Always confirm <b>Homeowner</b> status.</li>
                    <li>Maintain high energy!</li>
                </ul>
            </div>

            <button class="submit-btn">Lock Certified Lead</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Branding & Lead Generation OS © 2026<br>
        Proprietary System for Call Centers & High-Ticket Sales
    </footer>
</div>

<script>
    function updateVars() {
        let name = document.getElementById('custName').value || "Customer";
        let city = document.getElementById('cityName').value || "Your City";
        let agent = document.getElementById('agentName').value || "Agent";

        document.querySelectorAll('.name').forEach(el => el.innerText = name);
        document.querySelectorAll('.city').forEach(el => el.innerText = city);
        document.querySelectorAll('.agent').forEach(el => el.innerText = agent);
    }

    function copyText(id) {
        let text = document.getElementById(id).innerText;
        navigator.clipboard.writeText(text);
        alert("Dialogue Copied to Clipboard!");
    }
</script>

</body>
</html>
