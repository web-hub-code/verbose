<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Master Appointment Setter | Prime Solutions</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0f172a;
            --card-color: #1e293b;
            --primary: #3b82f6;
            --accent: #fbbf24;
            --success: #22c55e;
            --text-p: #cbd5e1;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-color);
            color: #f8fafc;
            margin: 0;
            padding: 20px;
        }

        .dashboard {
            max-width: 1100px;
            margin: 0 auto;
            background: var(--card-color);
            border: 1px solid #334155;
            border-radius: 25px;
            overflow: hidden;
            box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5);
        }

        .hero-banner {
            background: linear-gradient(90deg, #1e40af, #3b82f6);
            padding: 40px;
            text-align: center;
            border-bottom: 4px solid var(--accent);
        }

        .hero-banner h1 { margin: 0; font-size: 30px; letter-spacing: 2px; }
        .hero-banner p { color: var(--accent); font-weight: 600; font-size: 18px; margin-top: 10px; }

        .main-grid {
            display: grid;
            grid-template-columns: 1.5fr 1fr;
            gap: 20px;
            padding: 30px;
        }

        .script-section {
            background: rgba(255, 255, 255, 0.02);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .step-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
        }

        .step-num {
            background: var(--primary);
            color: white;
            padding: 5px 12px;
            border-radius: 50%;
            font-weight: 800;
        }

        .step-title {
            color: var(--primary);
            font-weight: 800;
            text-transform: uppercase;
            font-size: 14px;
        }

        .dialogue-box {
            font-size: 19px;
            line-height: 1.7;
            color: #e2e8f0;
            margin-bottom: 30px;
            padding: 10px;
        }

        .highlight {
            color: var(--accent);
            font-weight: 700;
            text-decoration: underline;
        }

        /* Sidebar Tools */
        .sidebar { display: flex; flex-direction: column; gap: 20px; }

        .card-info {
            background: #0f172a;
            padding: 20px;
            border-radius: 15px;
            border: 1px solid #334155;
        }

        .card-info h4 { color: var(--accent); margin-top: 0; font-size: 14px; text-transform: uppercase; }

        .feature-list { list-style: none; padding: 0; font-size: 14px; color: var(--text-p); }
        .feature-list li { margin-bottom: 10px; display: flex; align-items: flex-start; gap: 10px; }
        .feature-list li::before { content: "✔"; color: var(--success); font-weight: 900; }

        .price-lock-badge {
            background: var(--success);
            color: white;
            text-align: center;
            padding: 15px;
            border-radius: 12px;
            font-weight: 800;
            font-size: 18px;
            margin-top: 10px;
        }

        .footer-note {
            text-align: center;
            padding: 20px;
            font-size: 12px;
            color: #64748b;
            background: #1e293b;
        }
    </style>
</head>
<body>

<div class="dashboard">
    <div class="hero-banner">
        <h1>WINDOW ESTIMATE COMMAND CENTER</h1>
        <p>MAXIMUM CONVERSION • ZERO-COST QUOTES • USA MARKET</p>
    </div>

    <div class="main-grid">
        <div class="script-section">
            
            <div class="step-header">
                <span class="step-num">1</span>
                <span class="step-title">The Value-First Opening</span>
            </div>
            <div class="dialogue-box">
                "Hi, is this <strong>[Customer Name]</strong>? <br><br>
                Hi <strong>[Customer Name]</strong>, I'm calling from the <span class="highlight">Project Assessment Team</span>. We are currently helping homeowners in your zip code secure <strong>Price-Locked Estimates</strong> for their windows. <br><br>
                Most residents are seeing a sharp rise in energy costs, so we are providing <strong>completely free, no-obligation audits</strong> to show you exactly how much your home is leaking in energy. Have you had your windows inspected lately?"
            </div>

            <div class="step-header">
                <span class="step-num">2</span>
                <span class="step-title">The "Future" Strategy</span>
            </div>
            <div class="dialogue-box">
                "The best part is, we are providing a <span class="highlight">Written Labor & Material Quote</span> that is valid for an <strong>entire year</strong>. <br><br>
                Even if you aren't ready to upgrade today, this protects you against next year's material price hikes. You get the expert information for free, and you can keep it in your files until you're ready. It's truly a win-win for your home's value."
            </div>

            <div class="step-header">
                <span class="step-num">3</span>
                <span class="step-title">The Soft Appointment Lock</span>
            </div>
            <div class="dialogue-box">
                "Our Senior Consultant will be right in your neighborhood this <strong>[Day]</strong>. He’ll take the measurements, show you some modern energy-efficient samples, and hand you that 12-month guaranteed quote. <br><br>
                Would <strong>[Time 1]</strong> work for you and your spouse, or is <strong>[Time 2]</strong> a better time to grab that info?"
            </div>
        </div>

        <div class="sidebar">
            <div class="card-info">
                <h4>🎯 Why Customers Say Yes</h4>
                <ul class="feature-list">
                    <li><strong>No-Cost:</strong> Absolutely zero fees for the visit.</li>
                    <li><strong>No-Obligation:</strong> They don't have to buy anything.</li>
                    <li><strong>Price Protection:</strong> Quote is valid for 12 months.</li>
                    <li><strong>Expert Advice:</strong> Thermal leak detection included.</li>
                </ul>
            </div>

            <div class="card-info">
                <h4>🛡️ Trusted Power Words</h4>
                <p style="font-size: 13px; color: var(--text-p);">
                    Use these instead of sales words: <br><br>
                    • <span class="highlight">"Energy Audit"</span> (Not Sales Call) <br>
                    • <span class="highlight">"Senior Consultant"</span> (Not Salesman) <br>
                    • <span class="highlight">"Price Protection"</span> (Not Quote)
                </p>
            </div>

            <div class="price-lock-badge">
                12-MONTH PRICE LOCK GUARANTEE
            </div>

            <div class="card-info" style="border-color: var(--success);">
                <h4>📋 Quality Control</h4>
                <p style="font-size: 12px; margin-bottom: 5px;">1. Confirm Home Ownership</p>
                <p style="font-size: 12px; margin-bottom: 5px;">2. Confirm Spouse Presence (Crucial)</p>
                <p style="font-size: 12px; margin-bottom: 5px;">3. Set 20-Minute Expectation</p>
            </div>
        </div>
    </div>

    <div class="footer-note">
        CONFIDENTIAL: FOR INTERNAL USE ONLY | PRIME SOLUTIONS USA 2026
    </div>
</div>

</body>
</html>
