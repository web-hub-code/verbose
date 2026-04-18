<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Official 12-Step Master Script</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #22c55e;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --dark-bg: #020617;
            --panel-bg: #0f172a;
            --text-light: #f8fafc;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--dark-bg);
            color: var(--text-light);
            margin: 0;
            padding: 20px;
            scroll-behavior: smooth;
        }

        .master-container {
            max-width: 1450px;
            margin: 0 auto;
            background: var(--panel-bg);
            border-radius: 35px;
            border: 1px solid #1e293b;
            overflow: hidden;
            box-shadow: 0 50px 100px -30px rgba(0,0,0,0.9);
        }

        /* Animated Branding Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #6366f1 100%);
            padding: 50px 30px;
            text-align: center;
            border-bottom: 5px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 42px; font-weight: 800; text-transform: uppercase; letter-spacing: 4px; }
        header .website-link { 
            display: inline-block; margin-top: 15px; padding: 10px 25px; 
            background: rgba(255,255,255,0.1); border-radius: 50px; 
            color: var(--warning); text-decoration: none; font-size: 14px; font-weight: 600;
            border: 1px solid rgba(245, 158, 11, 0.3);
            transition: 0.3s;
        }
        header .website-link:hover { background: var(--warning); color: #000; }

        .content-grid {
            display: grid;
            grid-template-columns: 1.7fr 1fr;
            gap: 2px;
            background: #1e293b;
        }

        .panel { background: var(--panel-bg); padding: 45px; }

        /* Script Flow Steps */
        .step-box {
            margin-bottom: 45px;
            padding-left: 25px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-id {
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

        .dialogue { font-size: 21px; line-height: 1.8; color: #f1f5f9; }
        .hl { color: var(--warning); font-weight: 800; }

        /* Side Tools & Rebuttal Engine */
        .card {
            background: rgba(2, 6, 23, 0.4);
            border: 1px solid #334155;
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 30px;
        }

        .card h4 { margin: 0 0 20px 0; color: var(--success); text-transform: uppercase; font-size: 15px; letter-spacing: 1px; }

        .rebuttal {
            background: #020617;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 15px;
            border-left: 4px solid var(--danger);
        }

        .rebuttal strong { color: var(--danger); font-size: 13px; display: block; margin-bottom: 5px; }
        .rebuttal p { font-size: 14px; color: #94a3b8; margin: 0; line-height: 1.5; }

        .cta-btn {
            background: var(--success);
            color: white;
            width: 100%;
            border: none;
            padding: 22px;
            border-radius: 18px;
            font-weight: 900;
            font-size: 18px;
            cursor: pointer;
            text-transform: uppercase;
            transition: 0.3s;
        }
        .cta-btn:hover { transform: translateY(-3px); box-shadow: 0 10px 30px rgba(34, 197, 94, 0.4); }

        footer {
            background: #020617;
            padding: 40px;
            text-align: center;
            border-top: 1px solid #1e293b;
        }

        .footer-brand { font-size: 14px; color: #64748b; }
        .footer-brand strong { color: var(--primary); }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <a href="https://web-hub-code.github.io/script/" target="_blank" class="website-link">Official Portal: web-hub-code.github.io/script/</a>
        <p style="margin-top: 15px; opacity: 0.8; font-weight: 600;">USA Home Performance & Energy Systems Master Script</p>
    </header>

    <div class="content-grid">
        <div class="panel">
            
            <div class="step-box">
                <span class="step-id">Steps 1 - 3: Opening & Verification</span>
                <div class="dialogue">
                    "Hi, this is [Name] calling from <strong>Prime Solutions</strong>. How are you today? <br><br>
                    We're currently reaching out to verify homeowners for the <span class="hl">2026 Home Efficiency Rebates</span>. Just to confirm—are you the <strong>homeowner</strong>? <br><br>
                    Excellent! Are we looking at <strong>5 to 10 windows</strong> or the full house? And do you prefer <strong>Sliding or Casement</strong> styles?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--warning);">
                <span class="step-id">Steps 4 - 6: Local Qualification</span>
                <div class="dialogue">
                    "To check the specific tax credits for your area, may I have your <strong>ZIP code</strong>? <br><br>
                    And for the state record eligibility, what is your <strong>Date of Birth</strong>? This helps us apply any <span class="hl">Senior, Veteran, or Homeowner discounts</span> to your estimate."
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--success);">
                <span class="step-id">Steps 7 - 10: Financing & Trust</span>
                <div class="dialogue">
                    "Are you planning this <strong>this month</strong> or just budgeting? Have you seen other quotes? <br><br>
                    To qualify for our <span class="hl">0% Interest Financing</span>, what range does your credit score sit in? Most people check their banking app—I’ll hold for a second while you look. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--danger);">
                <span class="step-id">Steps 11 - 12: The Professional Lock</span>
                <div class="dialogue">
                    "Perfect! Just confirm your <strong>Name and Property Address</strong>. <br><br>
                    Our specialist will visit to drop off your <strong>12-Month Price-Locked Report</strong>. It’s 100% free. Do <span class="hl">mornings or evenings</span> work best for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid #1e293b;">
            
            <div class="card">
                <h4>🎯 Advanced Rebuttals (The "Why")</h4>
                <div class="rebuttal">
                    <strong>"Why do you need my ZIP code?"</strong>
                    <p>"Local rebates vary by county. Your ZIP ensures we calculate the exact incentives for your specific street."</p>
                </div>
                <div class="rebuttal">
                    <strong>"Why do you need my DOB?"</strong>
                    <p>"It's strictly for Senior and Military discount eligibility. We want to ensure you get every dollar you're entitled to."</p>
                </div>
                <div class="rebuttal">
                    <strong>"Why should my spouse be there?"</strong>
                    <p>"Since the quote is a legal 12-month price guarantee, we need both homeowners to receive the data together to answer all questions."</p>
                </div>
            </div>

            <div class="card" style="border-color: var(--primary);">
                <h4>🚀 Agent Strategy</h4>
                <ul style="font-size: 13px; color: #94a3b8; line-height: 2; padding-left: 20px;">
                    <li>Keep the tone <strong>Consultative</strong>, not pushy.</li>
                    <li>Always use the phrase <strong>"12-Month Price Lock."</strong></li>
                    <li>Refer to the visit as a <strong>"Technical Report."</strong></li>
                </ul>
            </div>

            <button class="cta-btn">Submit Certified Lead</button>
        </div>
    </div>

    <footer>
        <div class="footer-brand">
            PROPRIETARY SYSTEM OF <strong>PRIME SOLUTIONS</strong> © 2026<br>
            Official Portal: <a href="https://web-hub-code.github.io/script/" style="color:var(--primary); text-decoration:none;">web-hub-code.github.io/script/</a>
        </div>
        <p style="font-size: 11px; color: #475569; margin-top: 20px; font-style: italic;">
            DNC Disclaimer: Homeowner agrees to a callback even if on the DNC list for this requested free service estimate.
        </p>
    </footer>
</div>

</body>
</html>
