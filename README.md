<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | High-Conversion Window Script</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #2563eb;
            --secondary: #10b981;
            --accent: #f59e0b;
            --danger: #ef4444;
            --dark-navy: #0f172a;
            --glass-bg: rgba(255, 255, 255, 0.03);
        }

        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #020617 0%, #0f172a 100%);
            color: #e2e8f0;
            margin: 0;
            display: flex;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
        }

        .dashboard {
            width: 100%;
            max-width: 1100px;
            background: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 24px;
            overflow: hidden;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        /* Top Header */
        .top-bar {
            background: var(--primary);
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .top-bar h2 {
            margin: 0;
            font-size: 18px;
            letter-spacing: 1px;
            font-weight: 800;
        }

        .status-dot {
            height: 10px;
            width: 10px;
            background-color: var(--secondary);
            border-radius: 50%;
            display: inline-block;
            margin-right: 5px;
            box-shadow: 0 0 10px var(--secondary);
        }

        /* Main Content Grid */
        .content-grid {
            display: grid;
            grid-template-columns: 1.6fr 1fr;
            gap: 2px; /* For border effect */
            background: rgba(255, 255, 255, 0.1);
        }

        .main-script, .sidebar {
            background: #0f172a;
            padding: 30px;
        }

        /* Script Blocks */
        .script-block {
            background: var(--glass-bg);
            border-left: 4px solid var(--primary);
            padding: 20px;
            border-radius: 0 12px 12px 0;
            margin-bottom: 25px;
            transition: 0.3s;
        }

        .script-block:hover {
            background: rgba(255, 255, 255, 0.07);
            border-left: 4px solid var(--accent);
        }

        .tag {
            font-size: 11px;
            font-weight: 800;
            text-transform: uppercase;
            color: var(--primary);
            margin-bottom: 8px;
            display: block;
        }

        .text {
            font-size: 16px;
            line-height: 1.7;
            color: #cbd5e1;
        }

        .highlight {
            color: var(--accent);
            font-weight: 600;
        }

        /* Sidebar Elements */
        .info-box {
            background: rgba(37, 99, 235, 0.1);
            border: 1px solid rgba(37, 99, 235, 0.2);
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
        }

        .info-box h4 {
            margin: 0 0 10px 0;
            color: var(--accent);
            font-size: 14px;
        }

        .objection-btn {
            background: rgba(239, 68, 68, 0.1);
            border: 1px solid var(--danger);
            color: white;
            padding: 10px;
            border-radius: 8px;
            width: 100%;
            text-align: left;
            margin-bottom: 10px;
            cursor: pointer;
            font-size: 13px;
        }

        .appointment-form {
            background: var(--secondary);
            color: white;
            padding: 20px;
            border-radius: 12px;
            margin-top: 20px;
            text-align: center;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .content-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

<div class="dashboard">
    <div class="top-bar">
        <h2>PRIME SOLUTIONS | USA WINDOWS 2026</h2>
        <div><span class="status-dot"></span> AGENT ACTIVE</div>
    </div>

    <div class="content-grid">
        <div class="main-script">
            
            <div class="script-block">
                <span class="tag">01. The Trust Opener</span>
                <div class="text">
                    "Hi, is this <strong>[Customer Name]</strong>? Hi, this is <strong>[Your Name]</strong> from <span class="highlight">Prime Solutions</span>. We are currently working on a neighborhood energy-saving project right near <strong>[Street/Landmark]</strong>. <br><br>
                    I’m calling to see if you’ve already been approved for the <span class="highlight">2026 Window Rebate Program</span>, or if you're still using the original builder-grade windows?"
                </div>
            </div>

            <div class="script-block">
                <span class="tag">02. The "Expert" Solution</span>
                <div class="text">
                    "The reason I ask, sweetie, is that we have our <strong>Senior Field Contractor</strong> in your zip code. Unlike a salesman, he’s a structural expert. He’s doing free <span class="highlight">Thermal Leak Tests</span> to show exactly where your AC is leaking out. <br><br>
                    He gives you a written labor-and-material quote that’s <strong>price-locked for 1 year</strong>. It’s a great way to protect yourself against inflation."
                </div>
            </div>

            <div class="script-block" style="border-left-color: var(--secondary);">
                <span class="tag">03. Setting The Appointment</span>
                <div class="text">
                    "He’ll be on your street this <strong>[Day]</strong>. He only needs about 15-20 minutes to take measurements and show you the energy-efficient samples. <br><br>
                    I have a <strong>[Time 1, e.g. 5:15 PM]</strong> or a <strong>[Time 2, e.g. 10:00 AM]</strong>. Which one works best for you and your spouse to take a quick look?"
                </div>
            </div>

        </div>

        <div class="sidebar">
            <div class="info-box">
                <h4>🎯 Grab the Customer (Triggers)</h4>
                <ul style="padding-left: 18px; font-size: 13px; line-height: 1.8;">
                    <li><strong>Social Proof:</strong> "We just helped the [Last Name] family nearby."</li>
                    <li><strong>Warranty:</strong> "Transferable Lifetime Warranty."</li>
                    <li><strong>Saving:</strong> "Save up to 30% on electric bills."</li>
                </ul>
            </div>

            <div class="info-box" style="background: rgba(245, 158, 11, 0.1); border-color: var(--accent);">
                <h4>🛡️ Objection Handling</h4>
                <button class="objection-btn">"I'm Not Interested"</button>
                <p style="font-size: 12px; margin-top: -5px; color: #94a3b8;">"I understand! Most people aren't looking until they see the savings. Why not get the price while it's locked?"</p>
                
                <button class="objection-btn">"I Need to Talk to My Spouse"</button>
                <p style="font-size: 12px; margin-top: -5px; color: #94a3b8;">"Exactly! That's why we invite both of you to be there so we can answer all questions at once. How's [Time]?"</p>
            </div>

            <div class="appointment-form">
                <strong>BOOK NOW</strong><br>
                <small>Lock in the 2026 Rate</small>
            </div>
        </div>
    </div>
</div>

</body>
</html>
