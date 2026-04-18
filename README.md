<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Prime Solutions | Elite Lead OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --glass: rgba(255, 255, 255, 0.05);
            --primary: #6366f1;
            --success: #10b981;
            --accent: #f59e0b;
            --bg: #030712;
        }

        body {
            font-family: 'Outfit', sans-serif;
            background: var(--bg);
            color: #f8fafc;
            margin: 0;
            overflow-x: hidden;
        }

        /* Hero Animation */
        .glass-header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4338ca 100%);
            padding: 60px 20px;
            text-align: center;
            border-bottom: 2px solid var(--accent);
        }

        .live-status {
            display: inline-block;
            background: rgba(16, 185, 129, 0.2);
            color: var(--success);
            padding: 5px 15px;
            border-radius: 50px;
            font-size: 12px;
            font-weight: 700;
            margin-bottom: 20px;
            border: 1px solid var(--success);
        }

        .main-grid {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 20px;
            padding: 30px;
            max-width: 1500px;
            margin: 0 auto;
        }

        .script-card {
            background: var(--glass);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 30px;
            padding: 40px;
        }

        .step {
            margin-bottom: 40px;
            border-left: 4px solid var(--primary);
            padding-left: 20px;
        }

        .step-num { color: var(--primary); font-weight: 900; font-size: 14px; text-transform: uppercase; }
        .dialogue { font-size: 20px; line-height: 1.6; color: #e2e8f0; }
        .hl { color: var(--accent); font-weight: 700; }

        /* Sidebar Tools */
        .tool-box {
            background: rgba(15, 23, 42, 0.8);
            border-radius: 25px;
            padding: 25px;
            position: sticky;
            top: 20px;
        }

        .rebuttal-btn {
            background: rgba(239, 68, 68, 0.1);
            border: 1px solid #ef4444;
            color: #ef4444;
            padding: 10px;
            width: 100%;
            border-radius: 10px;
            margin-bottom: 10px;
            cursor: pointer;
            text-align: left;
            font-size: 13px;
            transition: 0.3s;
        }

        .rebuttal-btn:hover { background: #ef4444; color: white; }

        .zip-checker {
            background: #1e1b4b;
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 20px;
        }

        input {
            background: transparent;
            border: 1px solid #334155;
            padding: 10px;
            color: white;
            border-radius: 8px;
            width: 70%;
        }

        footer {
            text-align: center;
            padding: 40px;
            opacity: 0.6;
            font-size: 13px;
        }

        .btn-submit {
            background: var(--success);
            color: white;
            width: 100%;
            padding: 20px;
            border-radius: 15px;
            border: none;
            font-weight: 900;
            font-size: 18px;
            cursor: pointer;
            box-shadow: 0 10px 20px rgba(16, 185, 129, 0.2);
        }
    </style>
</head>
<body>

<div class="glass-header">
    <div class="live-status">● LIVE LEAD COUNTER: 47 QUALIFIED TODAY</div>
    <h1>PRIME SOLUTIONS LEAD OS</h1>
    <p>web-hub-code.github.io/PRIMESOLUTIONS/</p>
</div>

<div class="main-grid">
    <div class="script-card">
        <div class="step">
            <span class="step-num">Steps 1-3: Intro Hook</span>
            <div class="dialogue">"Hi, calling from <span class="hl">Prime Solutions</span> regarding the 2026 Energy Project. Are you the homeowner? How many windows do you have—5 or 10?"</div>
        </div>

        <div class="step">
            <span class="step-num">Steps 4-6: The Why</span>
            <div class="dialogue">"What's your <span class="hl">ZIP Code</span> so I can verify local rebates? And your DOB ensures you get the <span class="hl">Senior/Homeowner discounts</span>."</div>
        </div>

        <div class="step">
            <span class="step-num">Steps 7-10: Financing</span>
            <div class="dialogue">"Looking to start this month? For <span class="hl">0% Interest</span>, what's your credit range? I'll hold while you check your banking app."</div>
        </div>

        <div class="step">
            <span class="step-num">Steps 11-12: Closing</span>
            <div class="dialogue">"Great, just confirm your address. Will mornings or evenings work for the <span class="hl">Price-Locked Visit</span> with your spouse?"</div>
        </div>
    </div>

    <div class="tool-box">
        <div class="zip-checker">
            <h4 style="margin:0 0 10px 0; font-size: 12px; color: var(--accent);">AREA VALIDATOR</h4>
            <input type="text" placeholder="Enter ZIP Code...">
            <button style="background: var(--primary); border:none; color:white; padding:10px; border-radius:8px;">Check</button>
        </div>

        <h4 style="color: var(--success); font-size: 12px;">LIVE REBUTTALS</h4>
        <button class="rebuttal-btn">"Why do you need ZIP Code?"</button>
        <button class="rebuttal-btn">"I'm not interested right now."</button>
        <button class="rebuttal-btn">"Why should my spouse be there?"</button>
        <button class="rebuttal-btn">"Is this a sales call?"</button>

        <button class="btn-submit">SUBMIT LEAD TO CRM</button>
    </div>
</div>

<footer>
    PRIME SOLUTIONS © 2026 | MODERN LEAD GENERATION SYSTEMS<br>
    <a href="https://web-hub-code.github.io/script/" style="color:var(--primary); text-decoration: none;">Explore Official Script Portal</a>
</footer>

</body>
</html>
