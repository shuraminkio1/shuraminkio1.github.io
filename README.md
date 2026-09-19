<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Minkio External - Key System Gateway</title>
  <meta name="description" content="Official Minkio External Key Gateway. Complete checkpoints via Linkvertise, Work.ink, or Lootlabs to generate your 12-Hour or 24-Hour activation key." />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet" />

  <style>
    :root {
      --bg-primary: #07090e;
      --bg-secondary: #0d111a;
      --card-bg: rgba(16, 22, 35, 0.75);
      --card-border: rgba(255, 255, 255, 0.12);
      --card-border-glow: rgba(230, 50, 68, 0.35);
      --accent: #e63244;
      --accent-glow: rgba(230, 50, 68, 0.45);
      --accent-gradient: linear-gradient(135deg, #ff334b 0%, #c4182b 100%);
      --emerald: #10b981;
      --emerald-glow: rgba(16, 185, 129, 0.35);
      --cyan: #38bdf8;
      --cyan-glow: rgba(56, 189, 248, 0.35);
      --amber: #f59e0b;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --text-dark: #64748b;
      --discord: #5865f2;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      -webkit-font-smoothing: antialiased;
    }

    body {
      min-height: 100vh;
      background-color: var(--bg-primary);
      color: var(--text-main);
      font-family: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 24px 16px;
      position: relative;
      overflow-x: hidden;
    }

    /* Ambient organic background glow & grid */
    .bg-grid {
      position: fixed;
      inset: 0;
      background-image: 
        linear-gradient(to right, rgba(255, 255, 255, 0.03) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    .bg-glow-top {
      position: fixed;
      top: -120px;
      left: 50%;
      transform: translateX(-50%);
      width: 650px;
      height: 400px;
      background: radial-gradient(circle, rgba(230, 50, 68, 0.18) 0%, rgba(7, 9, 14, 0) 70%);
      filter: blur(80px);
      pointer-events: none;
      z-index: 0;
    }

    .bg-glow-bottom {
      position: fixed;
      bottom: -150px;
      right: 10%;
      width: 500px;
      height: 350px;
      background: radial-gradient(circle, rgba(56, 189, 248, 0.10) 0%, rgba(7, 9, 14, 0) 70%);
      filter: blur(90px);
      pointer-events: none;
      z-index: 0;
    }

    /* Main Container */
    .app-container {
      width: 100%;
      max-width: 680px;
      position: relative;
      z-index: 10;
      margin: auto;
    }

    /* Header Brand */
    .brand-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 24px;
      padding: 0 8px;
    }

    .brand-left {
      display: flex;
      align-items: center;
      gap: 14px;
    }

    .brand-logo {
      width: 50px;
      height: 50px;
      border-radius: 14px;
      background: linear-gradient(135deg, #251216 0%, #151824 100%);
      border: 1px solid rgba(230, 50, 68, 0.45);
      box-shadow: 0 0 20px rgba(230, 50, 68, 0.25);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      font-weight: 800;
      color: #ff4757;
      position: relative;
    }

    .brand-logo::after {
      content: '';
      position: absolute;
      inset: 2px;
      border-radius: 12px;
      border: 1px solid rgba(255, 255, 255, 0.15);
      pointer-events: none;
    }

    .brand-title-wrap h1 {
      font-size: 22px;
      font-weight: 800;
      letter-spacing: 0.5px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .brand-title-wrap h1 span.highlight {
      color: var(--accent);
      text-shadow: 0 0 12px rgba(230, 50, 68, 0.5);
    }

    .brand-title-wrap p {
      font-size: 13px;
      color: var(--text-muted);
      margin-top: 2px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .status-dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: var(--emerald);
      box-shadow: 0 0 8px var(--emerald);
      display: inline-block;
      animation: pulse 2s infinite ease-in-out;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.4; transform: scale(0.85); }
    }

    .badge-v2 {
      font-size: 11px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      padding: 4px 10px;
      border-radius: 20px;
      background: rgba(230, 50, 68, 0.15);
      border: 1px solid rgba(230, 50, 68, 0.35);
      color: #ff6b7e;
    }

    /* Glass Card Standard */
    .glass-card {
      background: var(--card-bg);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      border: 1px solid var(--card-border);
      border-radius: 20px;
      padding: 24px;
      position: relative;
      overflow: hidden;
      box-shadow: 
        0 20px 40px rgba(0, 0, 0, 0.45),
        inset 0 1px 0 rgba(255, 255, 255, 0.12);
      margin-bottom: 18px;
    }

    /* Top Specular Lip */
    .glass-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 15%;
      right: 15%;
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
    }

    /* Section Title */
    .section-title {
      font-size: 13px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.8px;
      color: var(--text-muted);
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .section-title::before {
      content: '';
      width: 3px;
      height: 12px;
      background: var(--accent);
      border-radius: 2px;
      box-shadow: 0 0 8px var(--accent);
    }

    /* Two Big Tier Buttons */
    .tier-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
      margin-bottom: 20px;
    }

    @media (max-width: 540px) {
      .tier-grid {
        grid-template-columns: 1fr;
      }
    }

    .tier-btn {
      background: rgba(22, 28, 44, 0.6);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 16px;
      padding: 18px 16px;
      text-align: left;
      cursor: pointer;
      position: relative;
      transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .tier-btn:hover {
      background: rgba(30, 38, 58, 0.7);
      border-color: rgba(255, 255, 255, 0.2);
      transform: translateY(-2px);
    }

    .tier-btn.active {
      background: rgba(230, 50, 68, 0.12);
      border-color: rgba(230, 50, 68, 0.6);
      box-shadow: 0 8px 24px rgba(230, 50, 68, 0.2);
    }

    .tier-btn.active::after {
      content: 'SELECTED';
      position: absolute;
      top: 12px;
      right: 12px;
      font-size: 10px;
      font-weight: 800;
      color: #ff5266;
      background: rgba(230, 50, 68, 0.2);
      padding: 3px 8px;
      border-radius: 6px;
      border: 1px solid rgba(230, 50, 68, 0.4);
    }

    .tier-duration {
      font-size: 22px;
      font-weight: 800;
      color: #fff;
      display: flex;
      align-items: baseline;
      gap: 6px;
    }

    .tier-duration small {
      font-size: 13px;
      font-weight: 600;
      color: var(--text-muted);
    }

    .tier-checkpoints {
      font-size: 13px;
      color: var(--cyan);
      font-weight: 600;
      margin-top: 6px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .tier-desc {
      font-size: 12px;
      color: var(--text-dark);
      margin-top: 4px;
      line-height: 1.4;
    }

    /* Gateway Provider Buttons */
    .gateway-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin-bottom: 22px;
    }

    @media (max-width: 500px) {
      .gateway-grid {
        grid-template-columns: 1fr;
      }
    }

    .gw-btn {
      background: rgba(22, 28, 44, 0.5);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 12px;
      padding: 12px 10px;
      text-align: center;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 4px;
    }

    .gw-btn:hover {
      border-color: rgba(255, 255, 255, 0.25);
      background: rgba(30, 40, 62, 0.65);
    }

    .gw-btn.active {
      border-color: var(--cyan);
      background: rgba(56, 189, 248, 0.12);
      box-shadow: 0 0 16px rgba(56, 189, 248, 0.2);
    }

    .gw-name {
      font-size: 13px;
      font-weight: 700;
      color: #fff;
    }

    .gw-tag {
      font-size: 10px;
      font-weight: 600;
      color: var(--text-muted);
      text-transform: uppercase;
    }

    /* Checkpoint Progress Tracker */
    .progress-box {
      background: rgba(10, 14, 22, 0.8);
      border: 1px solid rgba(255, 255, 255, 0.07);
      border-radius: 14px;
      padding: 16px;
      margin-bottom: 20px;
    }

    .progress-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
      font-size: 13px;
    }

    .progress-status {
      font-weight: 700;
      color: var(--text-main);
    }

    .progress-counter {
      font-family: 'JetBrains Mono', monospace;
      font-weight: 700;
      color: var(--cyan);
    }

    .progress-track {
      width: 100%;
      height: 8px;
      background: rgba(255, 255, 255, 0.06);
      border-radius: 6px;
      overflow: hidden;
      position: relative;
    }

    .progress-bar {
      height: 100%;
      width: 0%;
      background: var(--accent-gradient);
      border-radius: 6px;
      box-shadow: 0 0 12px var(--accent-glow);
      transition: width 0.4s ease;
    }

    /* Step Checkpoint Pills */
    .steps-row {
      display: flex;
      gap: 6px;
      margin-top: 12px;
      justify-content: space-between;
    }

    .step-pill {
      flex: 1;
      text-align: center;
      padding: 6px 2px;
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.05);
      border-radius: 8px;
      font-size: 11px;
      font-weight: 600;
      color: var(--text-dark);
      transition: all 0.25s ease;
    }

    .step-pill.completed {
      background: rgba(16, 185, 129, 0.15);
      border-color: rgba(16, 185, 129, 0.4);
      color: #34d399;
    }

    .step-pill.current {
      background: rgba(230, 50, 68, 0.2);
      border-color: rgba(230, 50, 68, 0.6);
      color: #ff6b7e;
      box-shadow: 0 0 10px rgba(230, 50, 68, 0.3);
    }

    /* Primary Action Button */
    .btn-main {
      width: 100%;
      padding: 16px;
      border-radius: 14px;
      border: none;
      background: var(--accent-gradient);
      color: #fff;
      font-family: inherit;
      font-size: 15px;
      font-weight: 700;
      cursor: pointer;
      box-shadow: 0 10px 25px rgba(230, 50, 68, 0.35);
      transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }

    .btn-main:hover {
      transform: translateY(-2px);
      box-shadow: 0 14px 30px rgba(230, 50, 68, 0.5);
    }

    .btn-main:active {
      transform: translateY(1px);
    }

    .btn-main:disabled {
      opacity: 0.6;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }

    /* Key Generation Result Modal / Box */
    .key-result-box {
      display: none;
      background: rgba(16, 185, 129, 0.08);
      border: 1px solid rgba(16, 185, 129, 0.4);
      border-radius: 16px;
      padding: 20px;
      text-align: center;
      margin-top: 20px;
      animation: fadeIn 0.4s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .key-result-badge {
      display: inline-block;
      font-size: 11px;
      font-weight: 800;
      color: #34d399;
      background: rgba(16, 185, 129, 0.18);
      padding: 4px 12px;
      border-radius: 20px;
      margin-bottom: 10px;
      border: 1px solid rgba(16, 185, 129, 0.3);
    }

    .key-display {
      background: #090d15;
      border: 1px solid rgba(255, 255, 255, 0.12);
      border-radius: 10px;
      padding: 12px 14px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 16px;
      font-weight: 700;
      color: #fff;
      letter-spacing: 1px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 12px 0 14px 0;
    }

    .btn-copy {
      background: rgba(255, 255, 255, 0.1);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 6px;
      color: #fff;
      font-size: 12px;
      font-weight: 600;
      padding: 6px 14px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .btn-copy:hover {
      background: rgba(255, 255, 255, 0.2);
    }

    .btn-copy.copied {
      background: var(--emerald);
      border-color: var(--emerald);
      color: #fff;
    }

    /* Community Discord Card */
    .discord-card {
      background: linear-gradient(135deg, rgba(88, 101, 242, 0.18) 0%, rgba(20, 24, 45, 0.6) 100%);
      border: 1px solid rgba(88, 101, 242, 0.35);
      border-radius: 16px;
      padding: 16px 20px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      text-decoration: none;
      color: #fff;
      transition: all 0.25s ease;
      cursor: pointer;
    }

    .discord-card:hover {
      border-color: rgba(88, 101, 242, 0.7);
      transform: translateY(-2px);
      box-shadow: 0 10px 25px rgba(88, 101, 242, 0.25);
    }

    .discord-info {
      display: flex;
      align-items: center;
      gap: 14px;
    }

    .discord-icon {
      width: 42px;
      height: 42px;
      border-radius: 12px;
      background: #5865f2;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 20px;
      font-weight: 800;
    }

    .discord-texts h4 {
      font-size: 14px;
      font-weight: 700;
    }

    .discord-texts p {
      font-size: 12px;
      color: #a5b4fc;
      margin-top: 2px;
    }

    .discord-arrow {
      font-size: 12px;
      font-weight: 700;
      color: #c7d2fe;
      background: rgba(255, 255, 255, 0.08);
      padding: 6px 14px;
      border-radius: 20px;
      border: 1px solid rgba(255, 255, 255, 0.1);
    }

    /* Footer */
    footer {
      text-align: center;
      margin-top: 24px;
      font-size: 12px;
      color: var(--text-dark);
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    footer a {
      color: var(--text-muted);
      text-decoration: none;
      transition: color 0.2s;
    }

    footer a:hover {
      color: #fff;
    }

    /* Toast Notification */
    .toast {
      position: fixed;
      bottom: 24px;
      left: 50%;
      transform: translateX(-50%) translateY(100px);
      background: rgba(15, 23, 42, 0.95);
      border: 1px solid rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(16px);
      padding: 12px 20px;
      border-radius: 12px;
      font-size: 13px;
      font-weight: 600;
      color: #fff;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.6);
      transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
      z-index: 1000;
      pointer-events: none;
    }

    .toast.show {
      transform: translateX(-50%) translateY(0);
    }
  </style>
</head>
<body>
  <div class="bg-grid"></div>
  <div class="bg-glow-top"></div>
  <div class="bg-glow-bottom"></div>

  <div class="app-container">
    <!-- Header -->
    <header class="brand-header">
      <div class="brand-left">
        <div class="brand-logo">M</div>
        <div class="brand-title-wrap">
          <h1>MINKIO <span class="highlight">KEY SYSTEM</span></h1>
          <p><span class="status-dot"></span> Official Gateway &bull; v2.5.0 Premium</p>
        </div>
      </div>
      <div class="badge-v2">Fast Checkpoints</div>
    </header>

    <!-- Main Card -->
    <main class="glass-card">
      <!-- 1. Tier Selection -->
      <div class="section-title">1. Choose Key Duration & Checkpoints</div>
      <div class="tier-grid">
        <!-- 12 Hours Option -->
        <div class="tier-btn active" id="tier-12h" onclick="selectTier(3, 12, this)">
          <div class="tier-duration">12 Hours <small>Pass</small></div>
          <div class="tier-checkpoints">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M20 6L9 17l-5-5"/></svg>
            3 Fast Checkpoints
          </div>
          <div class="tier-desc">Quickest access. Complete 3 short verification links to claim a 12-hour session key.</div>
        </div>

        <!-- 24 Hours Option -->
        <div class="tier-btn" id="tier-24h" onclick="selectTier(6, 24, this)">
          <div class="tier-duration">24 Hours <small>Full Day</small></div>
          <div class="tier-checkpoints">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M20 6L9 17l-5-5"/></svg>
            6 Extended Checkpoints
          </div>
          <div class="tier-desc">Double validity. Complete 6 checkpoints to enjoy a full 24-hour uninterrupted key.</div>
        </div>
      </div>

      <!-- 2. Gateway Provider Selection -->
      <div class="section-title">2. Select Link Gateway Provider</div>
      <div class="gateway-grid">
        <div class="gw-btn active" id="gw-linkvertise" onclick="selectGateway('Linkvertise', this)">
          <div class="gw-name">Linkvertise</div>
          <div class="gw-tag">Direct &bull; High Speed</div>
        </div>
        <div class="gw-btn" id="gw-workink" onclick="selectGateway('Work.ink', this)">
          <div class="gw-name">Work.ink</div>
          <div class="gw-tag">Smooth &bull; Mobile Ready</div>
        </div>
        <div class="gw-btn" id="gw-lootlabs" onclick="selectGateway('Lootlabs', this)">
          <div class="gw-name">Lootlabs</div>
          <div class="gw-tag">Fast &bull; Low Ads</div>
        </div>
      </div>

      <!-- 3. Checkpoint Status Tracker -->
      <div class="progress-box">
        <div class="progress-header">
          <span class="progress-status" id="progress-text">Checkpoint 1 of 3 Pending</span>
          <span class="progress-counter" id="progress-pct">0%</span>
        </div>
        <div class="progress-track">
          <div class="progress-bar" id="progress-bar-fill"></div>
        </div>
        <div class="steps-row" id="steps-container">
          <!-- Dynamically populated step pills -->
        </div>
      </div>

      <!-- 4. Main Checkpoint Action Button -->
      <button class="btn-main" id="btn-checkpoint" onclick="handleCheckpointAction()">
        <span id="btn-text">Proceed to Checkpoint 1 &rarr;</span>
      </button>

      <!-- 5. Key Generation Result Box (Appears when all checkpoints are cleared) -->
      <div class="key-result-box" id="key-result-container">
        <div class="key-result-badge">&check; KEY GENERATED SUCCESSFULLY</div>
        <p style="font-size: 13px; color: var(--text-muted);">Copy your license key below and paste it into the Minkio menu:</p>
        <div class="key-display">
          <span id="generated-key-text">MINKIO-XXXX-XXXX-XXXX</span>
          <button class="btn-copy" id="copy-btn" onclick="copyGeneratedKey()">Copy Key</button>
        </div>
        <p style="font-size: 12px; color: #34d399;" id="key-duration-note">Valid for 12 Hours on your device HWID</p>
      </div>
    </main>

    <!-- Official Discord Banner -->
    <a href="https://discord.gg/UmH2kgajvK" target="_blank" rel="noopener noreferrer" class="discord-card">
      <div class="discord-info">
        <div class="discord-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057 19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028c.462-.63.874-1.295 1.226-1.994.021-.041.001-.09-.041-.106a13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.929 1.793 8.18 1.793 12.061 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.894.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.028zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/>
          </svg>
        </div>
        <div class="discord-texts">
          <h4>Join the Official Minkio Discord</h4>
          <p>Community updates, direct key support & announcements</p>
        </div>
      </div>
      <div class="discord-arrow">Join Server &rarr;</div>
    </a>

    <!-- Footer -->
    <footer>
      <p>&copy; 2026 Minkio External. All rights reserved.</p>
      <p>Protected by Minkio Anti-Bypass &bull; Hardware ID Cryptographic Binding</p>
    </footer>
  </div>

  <!-- Toast Element -->
  <div class="toast" id="toast-el">Key copied to clipboard!</div>

  <script>
    // =========================================================
    // MINKIO EXTERNAL KEY SYSTEM GATEWAY LOGIC
    // Easily hook up your API URLs or monetize links below
    // =========================================================

    const CONFIG = {
      // 1. Checkpoint API & URL endpoints (Replace with your actual monetize link APIs)
      gateways: {
        Linkvertise: {
          name: "Linkvertise",
          // Template URL: replace with your Linkvertise link or dynamic API generator
          getUrl: (tierHours, step) => `https://linkvertise.com?r=minkio_${tierHours}h_step${step}`
        },
        "Work.ink": {
          name: "Work.ink",
          getUrl: (tierHours, step) => `https://work.ink?r=minkio_${tierHours}h_step${step}`
        },
        Lootlabs: {
          name: "Lootlabs",
          getUrl: (tierHours, step) => `https://lootlabs.gg?r=minkio_${tierHours}h_step${step}`
        }
      },

      // Fallback Discord Invite
      discordUrl: "https://discord.gg/UmH2kgajvK"
    };

    // State
    let currentMaxSteps = 3;  // 3 for 12h, 6 for 24h
    let currentHours = 12;
    let currentStep = 1;
    let selectedGateway = "Linkvertise";
    let generatedKey = "";

    // Initialize UI on load
    window.addEventListener('DOMContentLoaded', () => {
      // Check query params (e.g. ?step=2&tier=12)
      const urlParams = new URLSearchParams(window.location.search);
      const tierParam = parseInt(urlParams.get('tier'));
      const stepParam = parseInt(urlParams.get('step'));

      if (tierParam === 24) {
        selectTier(6, 24, document.getElementById('tier-24h'));
      } else {
        selectTier(3, 12, document.getElementById('tier-12h'));
      }

      if (stepParam && stepParam >= 1 && stepParam <= currentMaxSteps) {
        currentStep = stepParam;
      }

      renderSteps();
      updateProgress();
    });

    // Tier Selection (3 Checkpoints = 12h, 6 Checkpoints = 24h)
    function selectTier(totalSteps, hours, el) {
      currentMaxSteps = totalSteps;
      currentHours = hours;
      currentStep = 1;

      document.querySelectorAll('.tier-btn').forEach(btn => btn.classList.remove('active'));
      el.classList.add('active');

      // Hide key box if visible
      document.getElementById('key-result-container').style.display = 'none';
      document.getElementById('btn-checkpoint').disabled = false;

      renderSteps();
      updateProgress();
    }

    // Gateway Selection (Linkvertise, Work.ink, Lootlabs)
    function selectGateway(gwName, el) {
      selectedGateway = gwName;
      document.querySelectorAll('.gw-btn').forEach(btn => btn.classList.remove('active'));
      el.classList.add('active');
      showToast(`Selected Gateway: ${gwName}`);
    }

    // Render Step Badges
    function renderSteps() {
      const container = document.getElementById('steps-container');
      container.innerHTML = '';

      for (let i = 1; i <= currentMaxSteps; i++) {
        const pill = document.createElement('div');
        pill.className = 'step-pill';
        pill.id = `step-pill-${i}`;
        pill.textContent = `CP ${i}`;
        if (i < currentStep) {
          pill.classList.add('completed');
          pill.innerHTML = `&check; ${i}`;
        } else if (i === currentStep) {
          pill.classList.add('current');
        }
        container.appendChild(pill);
      }
    }

    // Update Progress Bars and Counter
    function updateProgress() {
      const pct = Math.round(((currentStep - 1) / currentMaxSteps) * 100);
      document.getElementById('progress-bar-fill').style.width = `${pct}%`;
      document.getElementById('progress-pct').textContent = `${pct}%`;

      const progressText = document.getElementById('progress-text');
      const btnText = document.getElementById('btn-text');

      if (currentStep <= currentMaxSteps) {
        progressText.textContent = `Checkpoint ${currentStep} of ${currentMaxSteps} Pending`;
        btnText.innerHTML = `Complete Checkpoint ${currentStep} via ${selectedGateway} &rarr;`;
      } else {
        progressText.textContent = `All Checkpoints Cleared! (${currentHours}h Key Ready)`;
        document.getElementById('progress-bar-fill').style.width = '100%';
        document.getElementById('progress-pct').textContent = '100%';
        btnText.innerHTML = `&check; Checkpoints Completed`;
        document.getElementById('btn-checkpoint').disabled = true;
      }
    }

    // Handle Checkpoint Button Click
    function handleCheckpointAction() {
      if (currentStep <= currentMaxSteps) {
        const gwConfig = CONFIG.gateways[selectedGateway];
        const targetUrl = gwConfig ? gwConfig.getUrl(currentHours, currentStep) : `https://linkvertise.com`;

        // Open monetized gateway link in new tab
        window.open(targetUrl, '_blank');
        showToast(`Opening Checkpoint ${currentStep} (${selectedGateway})...`);

        // Advance checkpoint step simulation (once you add your backend API, pass token via URL or webhook)
        currentStep++;
        renderSteps();
        updateProgress();

        // If completed all checkpoints, generate key!
        if (currentStep > currentMaxSteps) {
          generateFinalKey();
        }
      }
    }

    // Cryptographic-style Key Generator matching Minkio format
    function generateFinalKey() {
      const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
      const makeSeg = (len) => {
        let seg = '';
        for (let i = 0; i < len; i++) seg += chars.charAt(Math.floor(Math.random() * chars.length));
        return seg;
      };

      const prefix = currentHours === 24 ? "MINKIO-24H" : "MINKIO-12H";
      generatedKey = `${prefix}-${makeSeg(4)}-${makeSeg(4)}`;

      document.getElementById('generated-key-text').textContent = generatedKey;
      document.getElementById('key-duration-note').textContent = `Valid for ${currentHours} Hours on your Roblox HWID`;
      document.getElementById('key-result-container').style.display = 'block';

      // Smooth scroll to key
      document.getElementById('key-result-container').scrollIntoView({ behavior: 'smooth' });
    }

    // Copy to Clipboard
    function copyGeneratedKey() {
      if (!generatedKey) return;
      navigator.clipboard.writeText(generatedKey).then(() => {
        const copyBtn = document.getElementById('copy-btn');
        copyBtn.textContent = 'Copied!';
        copyBtn.classList.add('copied');
        showToast('License Key copied to clipboard!');

        setTimeout(() => {
          copyBtn.textContent = 'Copy Key';
          copyBtn.classList.remove('copied');
        }, 2500);
      });
    }

    // Toast Notification helper
    function showToast(msg) {
      const t = document.getElementById('toast-el');
      t.textContent = msg;
      t.classList.add('show');
      setTimeout(() => {
        t.classList.remove('show');
      }, 3000);
    }
  </script>
</body>
</html>
