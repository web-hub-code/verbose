<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Master Script Dashboard | USA Home Improvement</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;800&family=Roboto+Mono&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #2563eb;
            --success: #10b981;
            --accent: #fbbf24;
            --dark-bg: #0f172a;
            --card-bg: #1e293b;
            --text: #f8fafc;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--dark-bg);
            color: var(--text);
            margin: 0;
            padding: 20px;
        }

        .dashboard {
            max-width: 1200px;
            margin: 0 auto;
            background: var(--card-bg);
            border-radius: 20px;
            border: 1px solid #334155;
            overflow: hidden;
            box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5);
        }

        header {
            background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
            padding: 40px;
            text-align: center;
            border-bottom: 4px solid var(--accent);
        }

        header h1 { margin: 0; font-size: 28px; text-transform: uppercase; letter-spacing: 3px; }
        header p { color: var(--accent); font-weight: 600; margin-top: 10px; }

        .main-container {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: #334155;
        }

        .script-panel, .info-panel { background: var(--card-bg); padding: 40px; }

        .step-block {
            margin-bottom: 40px;
            padding-left: 20px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-header {
            display: inline-block;
            background: var(--primary);
            color: white;
            padding: 4px 12px;
            border-radius: 6px;
            font-size: 12px;
            font-weight: 800;
            margin-bottom: 15px;
            text-transform: uppercase;
        }

        .dialogue {
            font-size: 19px;
            line-height: 1.7;
            color: #e2e8f0;
        }

        .highlight { color: var(--accent); font-weight: 700; border-bottom: 1px dashed var(--accent); }

        /* Training Tools */
        .tool-card {
            background: rgba(15, 23, 42, 0.5);
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 25px;
            border: 1px solid #334155;
        }

        .tool-card h4 { color: var(--success); margin: 0 0 10px 0; text-transform: uppercase; font-size: 14px; }

        .status-badge {
            background: var(--success);
            color: white;
            text-align: center;
            padding: 15px;
            border-radius: 10px;
            font-weight: 800;
            font-size: 18px;
            margin-top: 20px;
        }

        .disclaimer-box {
            background: #0f172a;
            padding: 20px;
            border-radius: 10px;
            font-size: 12px;
            line-height: 1.5;
            color: #94a3b8;
            border: 1px solid #1e293b;
        }

        .logic-note {
            font-family: 'Roboto Mono', monospace;
            font-size: 13px;
            color: #38bdf8;
            margin-top: 10px;
            display: block;
        }
    </style>
</head>
<body>

<div class="dashboard">
    <header>
        <h1>HI APPOINTMENT MASTER SCRIPT</h1>
        <p>12-Step Conversion Protocol | Professional Agent Edition</p>
    </header>

    <div class="main-container">
        <div class="script-panel">
            
            <div class="step-block">
                <span class="step-header">Phase 1: Opening & Verification</span>
                <div class="dialogue">
                    "Hi, this is [Your Name] calling regarding the <span class="highlight">Home Improvement Project</span> in your area. How are you today? <br><br>
                    We’re currently providing free window estimates for homeowners looking to upgrade. Just to verify—are you the <strong>homeowner</strong>? <br><br>
                    Great! Roughly how many windows are we looking at—around <strong>5 to 10</strong>, or a full house of 30? And do you prefer <strong>Sliding, Casement, or Aluminum</strong> styles?"
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--accent);">
                <span class="step-header">Phase 2: Qualification & Incentives</span>
                <div class="dialogue">
                    "Perfect. To check the local rebate rates, what is your <strong>ZIP code</strong> please? <br><br>
                    And to match you with the <span class="highlight">proper government financing</span> incentives, may I ask for your <strong>Date of Birth</strong> for the file?"
                </div>
                <span class="logic-note">// Logic: DOB is required to verify 21+ and Senior rebates.</span>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-header">Phase 3: Financial Suitability</span>
                <div class="dialogue">
                    "How soon are you looking to start—this month or next? And have you received other estimates yet? <br><br>
                    To qualify for <strong>0% interest options</strong>, what is your credit score range? Most homeowners check their banking app real quick—I'll stay on the line while you grab that. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
                <span class="logic-note">// Logic: Banking app check keeps customer engaged on the phone.</span>
            </div>

            <div class="step-block" style="border-left-color: #ef4444;">
                <span class="step-header">Phase 4: The Final Lock</span>
                <div class="dialogue">
                    "Perfect. Can I get your <strong>Full Name and Full Property Address</strong> for the specialist? <br><br>
                    You’re all set! One of our experts will visit to provide that <strong>12-month price-locked estimate</strong>. Do mornings or evenings work best for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="info-panel">
            <div class="tool-card">
                <h4>🎯 Psychological Grab</h4>
                <p style="font-size: 14px; color: #cbd5e1;">
                    <strong>Price Lock:</strong> Tell the customer the quote is valid for 1 year. This stops them from feeling pressured to buy <em>today</em>.
                </p>
            </div>

            <div class="tool-card" style="border-color: var(--primary);">
                <h4>📋 Legal Compliance</h4>
                <div class="disclaimer-box">
                    "Today is [Date]. A specialist will call you shortly. By confirming, you agree to receive this call even if you are on a <strong>Do Not Call (DNC) List</strong>."
                </div>
            </div>

            <div class="tool-card">
                <h4>🛠️ Objection Handling</h4>
                <p style="font-size: 13px;">
                    <strong>If "I'm not ready":</strong> <br>
                    <em>"That’s exactly why we’re here! We provide the budget now so you can use it whenever you're ready in the future."</em>
                </p>
            </div>

            <div class="status-badge">
                READY TO CONVERT
            </div>
            
            <p style="text-align: center; font-size: 11px; margin-top: 20px; color: #64748b;">
                © 2026 PRIME SOLUTIONS USA
            </p>
        </div>
    </div>
</div>

</body>
</html>
