<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Elite 12-Step Master Script | Prime Solutions</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4f46e5;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --dark-navy: #0f172a;
            --card-bg: #1e293b;
            --text-main: #f8fafc;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--dark-navy);
            color: var(--text-main);
            margin: 0;
            padding: 20px;
        }

        .master-container {
            max-width: 1400px;
            margin: 0 auto;
            background: var(--card-bg);
            border-radius: 30px;
            border: 1px solid #334155;
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.6);
        }

        /* Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4f46e5 100%);
            padding: 40px;
            text-align: center;
            border-bottom: 5px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 32px; font-weight: 800; letter-spacing: 2px; }
        header p { color: var(--warning); font-weight: 600; margin-top: 10px; }

        .dashboard-grid {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: #334155;
        }

        .panel { background: var(--card-bg); padding: 40px; }

        /* Step Logic */
        .step-block {
            margin-bottom: 40px;
            padding-left: 20px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-label {
            background: var(--primary);
            color: white;
            padding: 4px 12px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 800;
            text-transform: uppercase;
            margin-bottom: 12px;
            display: inline-block;
        }

        .dialogue {
            font-size: 20px;
            line-height: 1.7;
            color: #e2e8f0;
        }

        .highlight { color: var(--warning); font-weight: 700; border-bottom: 1px dashed var(--warning); }

        /* Sidebar Tools */
        .tool-card {
            background: rgba(15, 23, 42, 0.5);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 1px solid #334155;
        }

        .tool-card h4 { margin: 0 0 15px 0; color: var(--success); text-transform: uppercase; font-size: 14px; }

        .rebuttal-box {
            background: #0f172a;
            border-radius: 10px;
            padding: 15px;
            margin-top: 10px;
            border: 1px solid #1e293b;
        }

        .rebuttal-q { color: var(--danger); font-weight: 800; font-size: 13px; display: block; margin-bottom: 5px; }
        .rebuttal-a { color: #94a3b8; font-size: 14px; display: block; line-height: 1.4; border-left: 2px solid var(--success); padding-left: 10px; }

        .disclaimer-area {
            background: #020617;
            padding: 25px;
            font-size: 13px;
            color: #64748b;
            border-top: 1px solid #334155;
            text-align: justify;
        }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <h1>ULTIMATE 12-STEP CONVERSION MACHINE</h1>
        <p>USA HOME IMPROVEMENT | PROFESSIONAL AGENT DASHBOARD 2026</p>
    </header>

    <div class="dashboard-grid">
        <div class="panel">
            
            <div class="step-block">
                <span class="step-label">Step 1-3: The Hook & Ownership</span>
                <div class="dialogue">
                    "Hi, this is [Name] regarding the <span class="highlight">Energy-Efficient Project</span> in your area. How are you today? <br><br>
                    We’re offering free window estimates to help lower utility bills. Just to verify—are you the <strong>homeowner</strong>? <br><br>
                    Perfect. Roughly how many windows are we looking at—around <strong>5 to 10</strong> or more? And do you prefer <strong>Sliding, Casement, or Aluminum</strong> styles?"
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-label">Step 4-6: Rebate Qualification</span>
                <div class="dialogue">
                    "To check the 2026 local rebate rates, what is your <strong>ZIP code</strong>? <br><br>
                    And for the state eligibility record, may I have your <strong>Date of Birth</strong>? This ensures you receive the <span class="highlight">Senior or First-Time Buyer discounts</span>."
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-label">Step 7-10: Financing & Credit Lock</span>
                <div class="dialogue">
                    "Are you planning this project <strong>this month</strong> or just budgeting? Have you received other estimates? <br><br>
                    To qualify for our <span class="highlight">0% Down-Payment programs</span>, what is your credit score range? Most homeowners check their banking app—I’ll hold for a second while you grab that. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--danger);">
                <span class="step-label">Step 11-12: The Final Closing</span>
                <div class="dialogue">
                    "Great! Can I get your <strong>Full Name and Full Address</strong> for the specialist? <br><br>
                    Our expert will visit to drop off your <strong>12-Month Price-Locked Technical Report</strong>. It's 100% free. Do <span class="highlight">mornings or evenings</span> work best for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid #334155;">
            
            <div class="tool-card">
                <h4>🚀 Professional Rebuttals (The "Why")</h4>
                
                <div class="rebuttal-box">
                    <span class="rebuttal-q">Why ZIP Code?</span>
                    <span class="rebuttal-a">"Utility incentives vary by county; your ZIP ensures we calculate the exact credits for your street."</span>
                </div>

                <div class="rebuttal-box">
                    <span class="rebuttal-q">Why Credit Score?</span>
                    <span class="rebuttal-a">"We use it to match you with 0% interest lenders so you pay nothing out of pocket today."</span>
                </div>

                <div class="rebuttal-box">
                    <span class="rebuttal-q">Why DOB?</span>
                    <span class="rebuttal-a">"To verify eligibility for state-specific Senior (65+) or Military discounts."</span>
                </div>

                <div class="rebuttal-box">
                    <span class="rebuttal-q">Why both spouses?</span>
                    <span class="rebuttal-a">"The estimate is a legal 12-month price guarantee; we need both owners to receive the data together."</span>
                </div>
            </div>

            <div class="tool-card" style="border-color: var(--primary);">
                <h4>💎 Why This Grabs the CX</h4>
                <p style="font-size: 13px; line-height: 1.6; color: #cbd5e1;">
                    • <strong>12-Month Price Lock:</strong> Inflation protection hook.<br>
                    • <strong>Banking App Engagement:</strong> Prevents call drops.<br>
                    • <strong>Consultative Tone:</strong> Technician, not salesman.
                </p>
            </div>

            <button style="background:var(--success); color:white; width:100%; border:none; padding:18px; border-radius:12px; font-weight:800; cursor:pointer; text-transform:uppercase;">
                Submit Certified Lead
            </button>
        </div>
    </div>

    <div class="disclaimer-area">
        <strong>FINAL LEGAL DISCLAIMER:</strong> "Today’s date is [Date]. A specialist will call you shortly to finalize. By confirming, you agree to this call even if you are on a <strong>Do Not Call List</strong>. This is for your requested free technical estimate."
    </div>
</div>

</body>
</html>
