<!DOCTYPE html>
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
