<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contractor Appointment Script | Prime Solutions</title>
    <style>
        :root {
            --glass: rgba(255, 255, 255, 0.2);
            --primary: #2563eb;
            --accent: #f59e0b;
            --success: #10b981;
            --dark: #1e293b;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            color: #f1f5f9;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }

        .dashboard {
            width: 100%;
            max-width: 1000px;
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5);
        }

        .header {
            text-align: center;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            padding-bottom: 20px;
            margin-bottom: 30px;
        }

        .header h1 {
            color: var(--accent);
            margin: 0;
            font-size: 28px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .badge {
            background: var(--success);
            color: white;
            padding: 5px 15px;
            border-radius: 50px;
            font-size: 12px;
            font-weight: bold;
        }

        .grid-layout {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 20px;
        }

        .script-card {
            background: rgba(255,255,255,0.05);
            padding: 25px;
            border-radius: 15px;
            border-left: 6px solid var(--primary);
        }

        .section-title {
            color: var(--primary);
            font-weight: 800;
            font-size: 14px;
            margin-bottom: 15px;
            display: block;
        }

        .dialogue-box {
            font-size: 17px;
            line-height: 1.6;
            margin-bottom: 25px;
        }

        .highlight-yellow {
            color: #fde047;
            font-weight: 600;
        }

        .action-btn {
            background: var(--primary);
            color: white;
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }

        .action-btn:hover {
            background: #1d4ed8;
            transform: translateY(-2px);
        }

        .side-panel {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .info-card {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 12px;
            font-size: 14px;
        }

        .info-card h4 {
            margin: 0 0 10px 0;
            color: var(--accent);
        }

        .status-tag {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 4px;
            background: #475569;
            font-size: 11px;
            margin-top: 5px;
        }

        .pro-tip {
            border: 1px dashed var(--accent);
            padding: 10px;
            font-style: italic;
            color: #cbd5e1;
        }
    </style>
</head>
<body>

<div class="dashboard">
    <div class="header">
        <span class="badge">LIVE CAMPAIGN: WINDOWS USA 2026</span>
        <h1>Contractor Booking System</h1>
    </div>

    <div class="grid-layout">
        <div class="main-content">
            <div class="script-card">
                <span class="section-title">PHASE 1: THE DISCOVERY</span>
                <div class="dialogue-box">
                    "Hi, this is <strong>[Your Name]</strong> calling from the <strong>Project Design Team</strong>. We’re reaching out because we have a Senior Windows Contractor in <strong>[City Name]</strong> doing energy audits this week. <br><br>
                    Quick question, sweetie—are your current windows the original ones that came with the house, or have you upgraded them to <span class="highlight-yellow">High-Efficiency glass</span> yet?"
                </div>

                <span class="section-title">PHASE 2: THE HOOK (Why Meet the Contractor?)</span>
                <div class="dialogue-box">
                    "The reason I ask is that our contractor is showing homeowners how to lock in <span class="highlight-yellow">2026 Tax Credits</span>. He’s not a salesman—he’s the technical expert who actually does the measurements and checks for seal failure. He’ll show you exactly how to stop your money from flying out of the window!"
                </div>

                <span class="section-title">PHASE 3: THE APPOINTMENT SET (The Close)</span>
                <div class="dialogue-box">
                    "He’s going to be on your street this <strong>Thursday</strong>. It takes him exactly 15 minutes to give you a 'Price-Locked' estimate. <br><br>
                    Should I put you down for the <strong>[Time 1]</strong> slot, or would <strong>[Time 2]</strong> be more convenient for you and your spouse?"
                </div>
                
                <button class="action-btn">CONFIRM APPOINTMENT</button>
            </div>
        </div>

        <div class="side-panel">
            <div class="info-card">
                <h4>🎯 Key Selling Points</h4>
                <ul>
                    <li>Lifetime Warranty</li>
                    <li>0% Down Financing</li>
                    <li>Energy Star Certified</li>
                </ul>
            </div>

            <div class="info-card pro-tip">
                <strong>💡 Pro-Tip:</strong> Use the word "Expert" instead of "Salesman". People love experts but hate being sold to.
            </div>

            <div class="info-card">
                <h4>🛡️ Handling No's</h4>
                <p>"I understand! That's why the contractor gives you a <strong>Written Estimate</strong> that stays valid for 1 full year. No pressure to buy today."</p>
                <span class="status-tag">Trust Builder</span>
            </div>
        </div>
    </div>
</div>

</body>
</html>
