<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Pro Appointment Setter</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4f46e5;
            --accent: #f59e0b;
            --success: #10b981;
            --dark-bg: #09090b;
            --card-bg: #18181b;
            --text-main: #f4f4f5;
            --text-dim: #a1a1aa;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--dark-bg);
            color: var(--text-main);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 1100px;
            background: var(--card-bg);
            border: 1px solid #27272a;
            border-radius: 24px;
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.5);
        }

        /* Header Section */
        header {
            background: linear-gradient(90deg, var(--primary), #818cf8);
            padding: 30px;
            text-align: center;
        }

        header h1 { margin: 0; font-size: 28px; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; }
        header p { margin: 10px 0 0; opacity: 0.9; font-weight: 500; }

        /* Main Content */
        .content { display: grid; grid-template-columns: 1.5fr 1fr; gap: 2px; background: #27272a; }
        .section { background: var(--card-bg); padding: 30px; }

        /* Script UI */
        .step { margin-bottom: 30px; position: relative; }
        .step-label { 
            background: var(--primary); color: white; padding: 4px 12px; 
            border-radius: 6px; font-size: 11px; font-weight: 800; display: inline-block; margin-bottom: 12px;
        }

        .dialogue-card {
            background: rgba(255,255,255,0.03);
            border: 1px solid rgba(255,255,255,0.05);
            padding: 20px;
            border-radius: 12px;
            font-size: 17px;
            line-height: 1.6;
            color: #d4d4d8;
        }

        .highlight { color: var(--accent); font-weight: 700; }
        .success-text { color: var(--success); font-weight: 600; }

        /* Sidebar Tools */
        .tool-box { margin-bottom: 25px; }
        .tool-title { font-size: 14px; color: var(--accent); font-weight: 700; text-transform: uppercase; margin-bottom: 15px; display: block; }
        
        .trust-badge {
            background: rgba(16, 185, 129, 0.1);
            border: 1px solid var(--success);
            padding: 10px;
            border-radius: 8px;
            font-size: 13px;
            margin-bottom: 10px;
        }

        .objection-pill {
            background: #27272a;
            border: 1px solid #3f3f46;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 10px;
            font-size: 13px;
            cursor: pointer;
            transition: 0.2s;
        }

        .objection-pill:hover { border-color: var(--primary); background: #323238; }

        /* Footer */
        .footer-banner {
            background: #27272a;
            padding: 15px;
            text-align: center;
            font-size: 12px;
            color: var(--text-dim);
        }

        .flex { display: flex; gap: 10px; }
        .btn-confirm {
            background: var(--success);
            color: white;
            border: none;
            padding: 15px;
            border-radius: 12px;
            width: 100%;
            font-weight: 800;
            cursor: pointer;
            margin-top: 20px;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Prime Solutions Appointment Pro</h1>
        <p>Premium Windows & Doors - USA Market Specialist</p>
    </header>

    <div class="content">
        <div class="section">
            <div class="step">
                <span class="step-label">PHASE 1: THE DISCOVERY (THE GRAB)</span>
                <div class="dialogue-card">
                    "Hi, am I speaking with <strong>[Customer Name]</strong>? <br><br>
                    Hi <strong>[Customer Name]</strong>, I'm [Your Name] with the <span class="highlight">Project Design Team</span> here at Prime Solutions. I’m reaching out because we’ve been authorized to provide <span class="highlight">2026 Energy-Efficiency Audits</span> for a few select homes on <strong>[Street Name]</strong>. <br><br>
                    Just a quick question—are you still using your original windows, or have you already upgraded to the new <span class="success-text">Energy-Star Rated</span> glass?"
                </div>
            </div>

            <div class="step">
                <span class="step-label">PHASE 2: BUILDING THE FUTURE (THE TRUST)</span>
                <div class="dialogue-card">
                    "The reason I ask, sweetie, is that we aren't just selling windows; we’re helping your neighbors <strong>lock in their home value</strong>. <br><br>
                    Our <span class="highlight">Senior Field Contractor</span> is in your area this week. He’s an expert who uses thermal technology to show you exactly where you're losing money on electricity. He’ll leave you with a <strong>'Price-Locked' quote</strong> that's guaranteed for a full year—no matter how much inflation goes up."
                </div>
            </div>

            <div class="step">
                <span class="step-label">PHASE 3: THE APPOINTMENT LOCK</span>
                <div class="dialogue-card">
                    "Since he's already right down the street on <strong>[Day]</strong>, it only takes 15 minutes for him to give you the roadmap for your home’s efficiency. <br><br>
                    I have a slot open at <strong>[Time 1]</strong> or <strong>[Time 2]</strong>. Which one works better for you and your spouse to get that free information?"
                </div>
            </div>
        </div>

        <div class="section">
            <div class="tool-box">
                <span class="tool-title">🛡️ Trust Boosters</span>
                <div class="trust-badge">✅ BBB A+ Rated Company</div>
                <div class="trust-badge">✅ Transferable Lifetime Warranty</div>
                <div class="trust-badge">✅ 0% Interest Financing Available</div>
            </div>

            <div class="tool-box">
                <span class="tool-title">⚡ Objection Killers</span>
                <div class="objection-pill">
                    <strong>"I'm too busy"</strong><br>
                    "I hear you! That's why he's only there for 15 mins. Information is power—even if you don't use it today."
                </div>
                <div class="objection-pill">
                    <strong>"I need to talk to my spouse"</strong><br>
                    "Perfect! We actually require both homeowners to be present so everyone gets the same expert info at once."
                </div>
            </div>

            <div class="tool-box">
                <span class="tool-title">📝 Required Details</span>
                <p style="font-size: 13px; color: var(--text-dim);">
                    1. Confirm Address <br>
                    2. Confirm Both Spouses <br>
                    3. Mobile Number for SMS Alert
                </p>
                <button class="btn-confirm">Book Appointment</button>
            </div>
        </div>
    </div>

    <div class="footer-banner">
        &copy; 2026 Prime Solutions | Developed for Premium Conversion & CX Excellence
    </div>
</div>

</body>
</html>
