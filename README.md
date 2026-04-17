<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Master Script Dashboard | Prime Solutions</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4f46e5;
            --secondary: #10b981;
            --accent: #f59e0b;
            --dark: #0f172a;
            --card: #1e293b;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--dark);
            color: #f8fafc;
            margin: 0;
            padding: 20px;
        }

        .dashboard {
            max-width: 1200px;
            margin: 0 auto;
            background: var(--card);
            border-radius: 24px;
            overflow: hidden;
            border: 1px solid #334155;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.5);
        }

        header {
            background: linear-gradient(135deg, #312e81 0%, #4f46e5 100%);
            padding: 40px;
            text-align: center;
            border-bottom: 4px solid var(--accent);
        }

        header h1 { margin: 0; font-size: 28px; text-transform: uppercase; letter-spacing: 2px; }
        header p { color: var(--accent); margin-top: 5px; font-weight: 600; }

        .content-grid {
            display: grid;
            grid-template-columns: 1.6fr 1fr;
            gap: 2px;
            background: #334155;
        }

        .main-column, .side-column { background: var(--card); padding: 30px; }

        .step-box {
            margin-bottom: 35px;
            padding-left: 20px;
            border-left: 4px solid var(--primary);
        }

        .step-num {
            background: var(--primary);
            color: white;
            padding: 4px 10px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 800;
            display: inline-block;
            margin-bottom: 10px;
        }

        .dialogue {
            font-size: 18px;
            line-height: 1.6;
            color: #e2e8f0;
        }

        .highlight { color: var(--accent); font-weight: 700; }

        /* Sidebar Tools */
        .tool-card {
            background: rgba(15, 23, 42, 0.5);
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
            border: 1px solid #334155;
        }

        .tool-card h4 { color: var(--secondary); margin-top: 0; font-size: 14px; text-transform: uppercase; }

        .btn-confirm {
            background: var(--secondary);
            color: white;
            width: 100%;
            border: none;
            padding: 15px;
            border-radius: 10px;
            font-weight: 800;
            cursor: pointer;
            margin-top: 20px;
        }

        .disclaimer {
            font-size: 12px;
            color: #94a3b8;
            font-style: italic;
            margin-top: 15px;
        }
    </style>
</head>
<body>

<div class="dashboard">
    <header>
        <h1>USA Home Improvement Master Script</h1>
        <p>12-Step Complete Customer Acquisition System</p>
    </header>

    <div class="content-grid">
        <div class="main-column">
            
            <div class="step-box">
                <span class="step-num">STEP 1 - 2</span>
                <div class="dialogue">
                    "Hi, this is [Name] calling regarding home improvement services in your area. How are you today? <br><br>
                    We're offering <span class="highlight">free window estimates</span> for homeowners looking to upgrade. Just to make sure—are you the <strong>homeowner</strong> of this property?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--secondary);">
                <span class="step-num">STEP 3 - 5</span>
                <div class="dialogue">
                    "Great! To give you an accurate estimate, roughly <strong>how many windows</strong> are you looking at? Around 5 to 10, or more than that? <br><br>
                    And for the report, do you prefer <span class="highlight">Sliding, Casement, or Aluminum</span> windows? <br><br>
                    Perfect. To verify local rates, may I have your <strong>ZIP code</strong> and confirm you are <strong>over 21</strong> for financing options?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--accent);">
                <span class="step-num">STEP 6 - 9</span>
                <div class="dialogue">
                    "To match you with the 2026 incentives, what is your <strong>Date of Birth</strong>? <br><br>
                    Are you looking to start this project <span class="highlight">this month or in 90 days</span>? And have you received any other estimates lately? <br><br>
                    For our <strong>0% down financing</strong>, where does your credit sit? Most people check their banking app real quick—I’ll stay on the line for a second while you grab that range."
                </div>
            </div>

            <div class="step-box" style="border-left-color: #ef4444;">
                <span class="step-num">STEP 10 - 12</span>
                <div class="dialogue">
                    "Last thing—have you had any <strong>mortgage modifications</strong> recently? <br><br>
                    Perfect. Let’s get your <strong>Full Name and Address</strong>. You’re all set! Our specialist will visit to provide that <span class="highlight">free, no-obligation estimate</span>. Do mornings or evenings work best for you?"
                </div>
            </div>

        </div>

        <div class="side-column">
            <div class="tool-card">
                <h4>🎯 The "Grab" Logic</h4>
                <ul style="padding-left: 20px; font-size: 14px; color: #cbd5e1;">
                    <li><strong>No Cost:</strong> Free future planning.</li>
                    <li><strong>No Obligation:</strong> Zero pressure.</li>
                    <li><strong>Inflation Protection:</strong> Lock today's price.</li>
                </ul>
            </div>

            <div class="tool-card" style="border-color: var(--primary);">
                <h4>📋 Disclaimer (Official)</h4>
                <div class="disclaimer">
                    "One of our specialists will call you back shortly to finalize. By confirming, you agree to this call even if you are on a <strong>Do Not Call List</strong>."
                </div>
            </div>

            <div class="tool-card">
                <h4>🛠️ Quick Handling</h4>
                <p style="font-size: 13px;">If they say <strong>"I'm busy"</strong>:<br>
                <em>"I understand! That's why it's just a 15-min price-lock report for your future records."</em></p>
            </div>

            <button class="btn-confirm">SUBMIT LEAD</button>
        </div>
    </div>
</div>

</body>
</html>
