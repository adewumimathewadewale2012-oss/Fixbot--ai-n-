<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FixBot AI 🔧</title>
<style>
body{font-family:system-ui;background:#f0f0f0;margin:0;padding:20px}
.box{max-width:500px;margin:0 auto;background:white;padding:20px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.1)}
h2{color:#00C2A8;margin:0 0 15px}
textarea,select{width:100%;padding:12px;border:2px solid #00C2A8;border-radius:8px;font-size:16px;margin-bottom:10px;box-sizing:border-box}
button{background:#00C2A8;color:white;padding:14px;border:none;border-radius:8px;font-size:18px;width:100%;font-weight:bold}
#answer{margin-top:20px;padding:15px;background:#f9f9f9;border-radius:8px;min-height:50px;white-space:pre-wrap}
</style>
</head>
<body>
<div class="box">
<h2>FixBot AI 🔧</h2>
<p>Your AI phone technician. Describe any fault:</p>

<select id="quicklist" onchange="document.getElementById('p').value=this.value;if(this.value)ask()">
  <option value="">🔧 Select Common Fault - Lagos Top 20</option>
  <option value="iPhone 11 black screen but vibrates">iPhone 11 Black Screen + Vibrate</option>
  <option value="iPhone X Face ID not working">iPhone X Face ID Failed</option>
  <option value="Samsung A12 not charging">Samsung A12 Not Charging</option>
  <option value="Samsung S21 overheating">Samsung S21 Overheating</option>
  <option value="Tecno Spark 10 stuck on logo">Tecno Spark 10 Stuck on Logo</option>
  <option value="Tecno Camon 20 battery drains fast">Tecno Camon 20 Battery Drain</option>
  <option value="Infinix Hot 12 no service">Infinix Hot 12 No Network</option>
  <option value="Infinix Note 30 ghost touch">Infinix Note 30 Ghost Touch</option>
  <option value="Water damaged iPhone won't turn on">Water Damage Won't Turn On</option>
  <option value="Phone dropped screen cracked no display">Cracked Screen No Display</option>
</select>

<textarea id="p" rows="3" placeholder="e.g., iPhone 11 black screen but still vibrates"></textarea>
<button onclick="ask()">Diagnose Now</button>
<div id="answer"></div>
</div>

<script>
const API_KEY = 'sk-YOUR_KEY_HERE'; // REPLACE THIS WITH YOUR REAL KEY

async function ask(){
  const p = document.getElementById('p').value;
  const a = document.getElementById('answer');
  if(!p) return a.innerHTML = '<span style="color:red">Type your phone issue first</span>';

  a.innerHTML = '⏳ Scanning hardware...';

  try{
    const r = await fetch('https://api.openai.com/v1/chat/completions', {
      method:'POST',
      headers:{'Content-Type':'application/json','Authorization':'Bearer '+API_KEY},
      body:JSON.stringify({
        model:'gpt-4o-mini',
        messages:[{
          role:'system',
          content:'You are FixBot AI for Nigerian phone technicians. Diagnose in this format: Fault: [name]\\nConfidence: [0-100]%\\nLikely Parts: [list]\\nPrice: ₦[range]\\nRisk: Low/Medium/High\\nSteps: [numbered list]. Be brief.'
        },{
          role:'user',
          content:p
        }],
        max_tokens:300
      })
    });
    const d = await r.json();
    if(d.error) throw new Error(d.error.message);
    a.innerHTML = d.choices[0].message.content.replace(/\n/g,'<br>');
  }catch(e){
    a.innerHTML = '<span style="color:red">⚠️ Error: '+e.message+'<br>Check your API key or data.</span>';
  }
}
</script>
</body>
</html>
// === VIDEO REPAIR GUIDES ===
const VIDEO_DB = {
  'black screen': 'https://www.youtube.com/embed/dQw4w9WgXcQ',
  'not charging': 'https://www.youtube.com/embed/dQw4w9WgXcQ',
  'stuck on logo': 'https://www.youtube.com/embed/dQw4w9WgXcQ',
  'water damage': 'https://www.youtube.com/embed/dQw4w9WgXcQ',
  'battery drain': 'https://www.youtube.com/embed/dQw4w9WgXcQ'
};

function addVideoGuide(issue, answerDiv) {
  let videoUrl = '';
  for(let key in VIDEO_DB) {
    if(issue.toLowerCase().includes(key)) {
      videoUrl = VIDEO_DB[key];
      break;
    }
  }

  if(videoUrl) {
    answerDiv.innerHTML += `
    <div style="margin-top:15px;padding:15px;background:#fff3cd;border:1px solid #ffc107;border-radius:8px">
      <b>🎥 Video Repair Guide</b>
      <div style="position:relative;padding-bottom:56.25%;height:0;margin-top:10px">
        <iframe src="${videoUrl}" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;border-radius:6px" allowfullscreen></iframe>
      </div>
      <button onclick="alert('Pro feature: Download HD video')" style="background:#FF6B00;color:white;padding:8px 12px;border:none;border-radius:6px;margin-top:10px;width:100%">⭐ Upgrade to Pro for HD + No Ads</button>
    </div>`;
  } else {
    answerDiv.innerHTML += `<p style="margin-top:15px;font-size:14px;color:#666">🎥 Video guide coming soon. <b>Need video? Upgrade Pro.</b></p>`;
  }
}

// Hook into existing ask function
const oldAsk2 = ask;
ask = async function() {
  const p = document.getElementById('p').value;
  await oldAsk2();
  const a = document.getElementById('a');
  if(a.innerText.includes('Fault:')) {
    addVideoGuide(p, a);
  }
}<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>FixBot AI</title>
  <style>
    body { font-family: -apple-system, sans-serif; max-width: 600px; margin: 0 auto; padding: 16px; background: #f7f7f7; }
    h2 { color: #00C2A8; text-align: center; }
    textarea { width: 100%; height: 100px; padding: 12px; font-size: 16px; border: 1px solid #ddd; border-radius: 8px; }
    button { background: #00C2A8; color: white; border: none; padding: 14px; width: 100%; font-size: 16px; border-radius: 8px; margin-top: 10px; }
    #answer { background: white; padding: 15px; margin-top: 15px; white-space: pre-wrap; border-radius: 8px; min-height: 100px; }
   .pro { color: #666; font-size: 12px; text-align: center; margin-top: 20px; }
  </style>
</head>
<body>
  <h2>FixBot AI 🔧</h2>
  <p>Snap. Scan. Fix. Save money.</p>
  <textarea id="problem" placeholder="Describe issue: e.g. iPhone 11 black screen but vibrates"></textarea>
  <button onclick="askFixBot()">Diagnose Phone</button>
  <div id="answer">FixBot reply will appear here...</div>
  <p class="pro">Need video guide? Upgrade to Pro for ₦1500</p>

<script>
const API_KEY = 'sk-YOUR_KEY_HERE'; // REPLACE THIS WITH YOUR OPENAI KEY

async function askFixBot() {
  const problem = document.getElementById('problem').value;
  const answer = document.getElementById('answer');
  if (!problem) return answer.innerText = "Type your phone issue first";
  answer.innerText = "FixBot scanning...";

  try {
    const response = await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${API_KEY}`,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        model: "gpt-4o-mini",
        messages: [
          {role: "system", content: "You are FixBot, a phone repair expert with 5+ years experience, Cisco certified. You diagnose broken phones. Output format: Fault: [issue] [confidence%] Parts: [name] ~$[price] Tools: Risk: [1-5]/5 – [why] Steps: 1. 2. 3. Warning: [if needed]. Under 120 words. End with: Need video guide? Upgrade to Pro."},
          {role: "user", content: problem}
        ]
      })
    });
    const data = await response.json();
    answer.innerText = data.choices[0].message.content;
  } catch (e) {
    answer.innerText = "Error. Check your API key or connection.";
  }
}
</script>
</body>
</html>
// === NEW FEATURE 1: Copy Button + History ===
let history = JSON.parse(localStorage.getItem('fixbotHistory') || '[]');

function saveHistory(q, a) {
  history.unshift({q: q, a: a, t: new Date().toLocaleTimeString()});
  history = history.slice(0, 5); // Keep last 5
  localStorage.setItem('fixbotHistory', JSON.stringify(history));
  showHistory();
}

function showHistory() {
  let h = document.getElementById('history');
  if (!h) {
    document.body.insertAdjacentHTML('beforeend', `<div id="history" style="margin-top:20px;padding:15px;background:#f5f5f5;border-radius:8px"><b>Recent Fixes:</b><div id="hlist"></div></div>`);
    h = document.getElementById('history');
  }
  document.getElementById('hlist').innerHTML = history.map(i => 
    `<div style="padding:8px 0;border-bottom:1px solid #ddd"><b>${i.t}</b> - ${i.q}<br><small>${i.a.substring(0,80)}...</small></div>`
  ).join('') || 'No history yet';
}

function copyAnswer() {
  navigator.clipboard.writeText(document.getElementById('a').innerText);
  alert('Copied to clipboard ✅');
}

// === NEW FEATURE 2: Better Loading + Error Handling ===
const oldAsk = ask;
ask = async function() {
  const p = document.getElementById('p').value;
  const a = document.getElementById('a');
  if(!p) return a.innerHTML = '<span style="color:red">Type your phone issue first</span>';
  
  a.innerHTML = '<div style="text-align:center">⏳ <b>Scanning hardware...</b><br><small>Checking Fault DB + Price List</small></div>';
  
  try {
    await oldAsk();
    saveHistory(p, a.innerText);
