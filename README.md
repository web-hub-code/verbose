<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Professional Appointment System | USA Windows</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #0a0a0a;
            --card: #171717;
            --primary: #2563eb;
            --accent: #fbbf24;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg);
            color: var(--text-main);
            margin: 0;
            padding: 30px 15px;
        }

        .main-container {
            max-width: 1100px;
            margin: 0 auto;
            background: var(--card);
            border: 1px solid #262626;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 40px 80px rgba(0,0,0,0.7);
        }

        .header-section {
            background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
            padding: 40px;
            text-align: center;
            border-bottom: 3px solid var(--accent);
        }

        .header-section h1 { margin: 0; font-size: 26px; text-transform: uppercase; letter-spacing: 3px; }
        .header-section p { margin-top: 10px; font-weight: 600; color: var(--accent); }

        .dashboard-body {
            display: grid;
            grid-template-columns: 1.6fr 1fr;
            gap: 2px;
            background: #262626;
        }

        .script-area, .sidebar-area {
            background: var(--card);
            padding: 35px;
        }

        .phase-box {
            background: rgba(255,255,255,0.03);
            border-left: 5px solid var(--primary);
            padding: 20px;
            border-radius: 0 12px 12px 0;
            margin-bottom: 25px;
        }

        .phase-label {
            font-size: 11px;
            font-weight: 800;
            color: var(--primary);
            text-transform: uppercase;
            margin-bottom: 10px;
            display: block;
        }

        .dialogue-text {
            font-size: 18px;
            line-height: 1.7;
            color: #e2e8f0;
        }

        .highlight { color: var(--accent); font-weight: 700; }

        .info-card {
            background: rgba(37, 99, 235, 0.1);
            border: 1px solid rgba(37, 99, 235, 0.2);
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
        }

        .info-card h4 { margin: 0 0 10px 0; color: var(--accent); font-size: 14px; text-transform: uppercase; }

        .tag-list {
            list-style: none;
            padding: 0;
            font-size: 13px;
            color: var(--text-muted);
        }

        .tag-list li { margin-bottom: 8px; display: flex; align-items: center; }
        .tag-list li::before { content: "✓"; color: #10b981; margin-right: 10px; font-weight: bold; }

        .btn-action {
            width: 100%;
            background: #10b981;
            color: white;
            border: none;
            padding: 18px;
            border-radius: 10px;
            font-weight: 800;
            text-transform: uppercase;
            cursor: pointer;
            margin-top: 10px;
        }

        @media (max-width: 850px) {
            .dashboard-body { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

<div class="main-container">
    <div class="header-section">
        <h1>Window Solutions USA</h1>
        <p>Premium Appointment Setting & Lead Generation Dashboard</p>
    </div>

    <div class="dashboard-body">
        <div class="script-area">
            
            <div class="phase-box">
                <span class="phase-label">Phase 1: Professional Opening</span>
                <div class="dialogue-text">
                    "Hi, is this <strong>[Customer Name]</strong>? <br><br>
                    This is [Your Name] calling from the <span class="highlight">Project Design Office</span>. We are reaching out to a few homeowners in <strong>[City]</strong> to provide a no-cost <span class="highlight">2026 Energy-Efficiency Assessment</span> for your windows and doors. Have you noticed any increase in your utility bills lately?"
                </div>
            </div>

            <div class="step-box" style="margin-bottom: 25px;">
                <span class="phase-label" style="color: var(--accent);">Phase 2: The Future-Proof Value</span>
                <div class="dialogue-text" style="background: rgba(255,255,255,0.02); padding: 20px; border-radius: 12px;">
                    "The reason for my call is to help you lock in <span class="highlight">Current Material Rates</span>. We are sending out a Senior Field Contractor to provide <strong>Free Written Estimates</strong> that are guaranteed for a full year. This allows you to have a precise budget in hand, protected against any future inflation, with absolutely no obligation."
                </div>
            </div>

            <div class="phase-box" style="border-left-color: #10b981;">
                <span class="phase-label" style="color: #10b981;">Phase 3: Appointment Confirmation</span>
                <div class="dialogue-text">
                    "Our Specialist will be on your street this <strong>[Day]</strong>. He’ll take exact measurements and leave you with a price-lock quote. Would <strong>[Time 1]</strong> work for you and your spouse, or is <strong>[Time 2]</strong> more convenient?"
                </div>
            </div>

        </div>

        <div class="sidebar-area">
            <div class="info-card">
                <h4>🎯 Grab the Customer</h4>
                <ul class="tag-list">
                    <li>Mention 1-Year Price Guarantee</li>
                    <li>Focus on "Energy Independence"</li>
                    <li>Transferable Lifetime Warranty</li>
                </ul>
            </div>

            <div class="info-card">
                <h4>🛡️ Build Instant Trust</h4>
                <p style="font-size: 13px; line-height: 1.5; color: var(--text-muted);">
                    Avoid sounding like a salesperson. Use terms like <strong>"Field Consultant"</strong> and <strong>"Structural Audit"</strong> to establish professional authority.
                </p>
            </div>

            <div class="info-card" style="background: rgba(251, 191, 36, 0.05); border-color: var(--accent);">
                <h4>📋 Verification Checklist</h4>
                <p style="font-size: 12px; margin-bottom: 5px;">1. Confirm Full Name & Address</p>
                <p style="font-size: 12px; margin-bottom: 5px;">2. Confirm Spouse Presence</p>
                <p style="font-size: 12px; margin-bottom: 5px;">3. Set Expectations (15-20 Mins)</p>
            </div>

            <button class="btn-action">Lock Appointment</button>
        </div>
    </div>
</div>

</body>
</html>
