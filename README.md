
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="robots" content="noindex">
<title>SYSTEM COMPROMISED</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html, body {
    background: #000;
    color: #0f0;
    font-family: 'Courier New', monospace;
    overflow: hidden;
    height: 100vh;
    width: 100vw;
  }
  canvas#matrix {
    position: fixed;
    top: 0; left: 0;
    z-index: 0;
    opacity: 0.35;
  }
  #terminal {
    position: fixed;
    top: 0; left: 0;
    width: 100%;
    height: 100%;
    padding: 20px;
    z-index: 1;
    overflow: hidden;
    font-size: 14px;
    line-height: 1.4;
    white-space: pre-wrap;
    text-shadow: 0 0 4px #0f0;
  }
  .glitch {
    animation: glitch 0.15s infinite;
  }
  @keyframes glitch {
    0% { transform: translate(0); }
    20% { transform: translate(-2px, 2px); }
    40% { transform: translate(-2px, -2px); }
    60% { transform: translate(2px, 2px); }
    80% { transform: translate(2px, -2px); }
    100% { transform: translate(0); }
  }
  #alertBox {
    position: fixed;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    background: #900;
    color: #fff;
    border: 4px solid #f00;
    padding: 30px 50px;
    font-size: 22px;
    font-weight: bold;
    z-index: 5;
    display: none;
    text-align: center;
    box-shadow: 0 0 40px #f00;
    animation: pulse 0.5s infinite;
  }
  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 40px #f00; }
    50% { box-shadow: 0 0 80px #f00; }
  }
  #finalScreen {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: #000;
    color: #f00;
    z-index: 10;
    display: none;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: 'Courier New', monospace;
    text-shadow: 0 0 10px #f00;
  }
  #finalScreen .skull {
    font-size: 120px;
    animation: flicker 1s infinite;
  }
  #finalScreen h1 {
    font-size: 42px;
    margin-top: 20px;
    letter-spacing: 4px;
  }
  #finalScreen p {
    margin-top: 15px;
    color: #0f0;
    font-size: 16px;
  }
  @keyframes flicker {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }
</style>
</head>
<body>

<canvas id="matrix"></canvas>
<div id="terminal"></div>

<div id="alertBox">
  ⚠ CRITICAL SECURITY BREACH ⚠<br>
  UNAUTHORIZED ACCESS DETECTED<br>
  DO NOT POWER OFF
</div>

<div id="finalScreen">
  <div class="skull">💀</div>
  <h1>WALLET SUCCESSFULLY EXTRACTED</h1>
  <p>connection terminated — session closed</p>
</div>

<script>
// Matrix rain — toned down
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const chars = "01アイウエオカキクケコｱｲｳｴｵ".split("");
const fontSize = 16;
const columns = Math.floor(canvas.width / fontSize / 2); // half density
const drops = Array(columns).fill(1);

function drawMatrix() {
  ctx.fillStyle = "rgba(0,0,0,0.08)";
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = "#0f0";
  ctx.font = fontSize + "px monospace";
  for (let i = 0; i < drops.length; i++) {
    const text = chars[Math.floor(Math.random() * chars.length)];
    ctx.fillText(text, i * fontSize * 2, drops[i] * fontSize);
    if (drops[i] * fontSize > canvas.height && Math.random() > 0.98) {
      drops[i] = 0;
    }
    drops[i]++;
  }
}
setInterval(drawMatrix, 60);

// Terminal spam
const terminal = document.getElementById('terminal');
const lines = [
  "[root@victim ~]# initializing intrusion protocol...",
  "[+] bypassing firewall............... OK",
  "[+] escalating privileges............ OK",
  "[+] dumping /etc/shadow.............. OK",
  "[+] hooking browser processes........ OK",
  "[+] scanning local storage for wallet.dat",
  "[!] found: MetaMask vault (encrypted)",
  "[!] found: Phantom keystore",
  "[!] found: Trust Wallet mnemonic cache",
  "[+] extracting seed phrases..........",
  "  > word[1]: ██████",
  "  > word[2]: ██████",
  "  > word[3]: ██████",
  "  > word[4]: ██████",
  "  > word[5]: ██████",
  "  > word[6]: ██████",
  "[+] decrypting private keys..........",
  "  > 0x8f...c3a4 [BTC]  --> OK",
  "  > 0x7d...9e2b [ETH]  --> OK",
  "  > 0x4a...11f9 [SOL]  --> OK",
  "[+] broadcasting transactions to relay nodes...",
  "[+] laundering through mixer.............",
  "[+] wiping local traces..................",
  "[+] disabling antivirus..................",
  "[+] injecting persistence into registry..",
  "[!] webcam access granted",
  "[!] microphone access granted",
  "[!] keylogger active",
  "[+] uploading data to remote C2..........",
  "[+] TOR circuit established..............",
  "[+] finalizing exfiltration..............",
];

let lineIndex = 0;
function typeLine() {
  if (lineIndex < lines.length) {
    terminal.innerHTML += lines[lineIndex] + "\n";
    lineIndex++;
    terminal.scrollTop = terminal.scrollHeight;
    setTimeout(typeLine, 500 + Math.random() * 400);
  } else {
    setTimeout(() => {
      document.body.classList.add('glitch');
      document.getElementById('alertBox').style.display = 'block';
      setTimeout(showFinal, 4000);
    }, 800);
  }
}

function showFinal() {
  document.getElementById('finalScreen').style.display = 'flex';
}

typeLine();

window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});
</script>
</body>
</html>
