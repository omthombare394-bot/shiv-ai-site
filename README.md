
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#101329">
<title>SHIV AI - Your Smart Assistant</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#101329;color:#fff;
 font-family:Arial,sans-serif;transition:.2s;
}
header{
 background:#191e3b;padding:16px;
 display:flex;justify-content:space-between;
 align-items:center;position:sticky;top:0;
 border-bottom:1px solid #353958;
}
.logo{font-size:24px;font-weight:bold;color:#a78bfa}
button{cursor:pointer;border:0;border-radius:10px;
 padding:11px 15px;background:#7959e9;color:white}
main{max-width:850px;margin:auto;padding:18px}
.hero{text-align:center;padding:30px 5px}
.hero h1{font-size:34px;margin:10px}
.hero p{color:#b9bfdc}
.tools{
 display:grid;grid-template-columns:repeat(2,1fr);
 gap:12px;margin:20px 0;
}
.tool{
 padding:17px;background:#1c2343;
 border:1px solid #394264;border-radius:14px;
 cursor:pointer;
}
.tool:active{transform:scale(.97)}
.tool h3{margin:5px 0}
.tool p{font-size:12px;color:#bdc5e0;margin:5px 0}
.chat{
 background:#1c2343;border:1px solid #394264;
 padding:15px;border-radius:16px;
}
#messages{height:260px;overflow-y:auto;padding:8px}
.msg{padding:11px;margin:9px 0;border-radius:12px;
 background:#2a3458;overflow-wrap:anywhere}
.user{background:#493a80}
.small{font-size:12px;color:#c0c8e2}
.inputrow{display:flex;gap:7px}
input{
 flex:1;min-width:0;padding:14px;
 background:#101329;border:1px solid #515b7e;
 border-radius:10px;color:white;
}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
.secondary{background:#394264}
footer{text-align:center;padding:25px;color:#9da7c9}
body.light{background:#f2f3fa;color:#17182b}
body.light header,body.light .tool,body.light .chat{
 background:white;color:#17182b;border-color:#ddd;
}
body.light input{background:white;color:#17182b}
body.light .msg{background:#e7e8f5;color:#17182b}
body.light .user{background:#ded4ff}
@media(min-width:600px){
 .tools{grid-template-columns:repeat(3,1fr)}
}
</style>
</head>
<body>
<header>
 <div class="logo">✦ SHIV AI</div>
 <div>
  <button class="secondary" onclick="toggleTheme()">◐</button>
  <button onclick="toggleLanguage()" id="lang">मराठी</button>
 </div>
</header>

<main>
<section class="hero">
 <div style="font-size:40px">✦</div>
 <h1 id="heading">Welcome to SHIV AI</h1>
 <p id="sub">One Platform. Many Possibilities.</p>
</section>

<h2 id="toolsTitle">Explore AI Tools</h2>
<section class="tools">
 <div class="tool" onclick="selectTool('AI Chat')">
  <h3>💬 AI Chat</h3><p>Ask anything</p>
 </div>
 <div class="tool" onclick="selectTool('Writing Assistant')">
  <h3>✍️ Writing AI</h3><p>Writing help</p>
 </div>
 <div class="tool" onclick="selectTool('Study Assistant')">
  <h3>📚 Study AI</h3><p>Study support</p>
 </div>
 <div class="tool" onclick="selectTool('Translator')">
  <h3>🌐 Translator</h3><p>Language help</p>
 </div>
 <div class="tool" onclick="selectTool('Ideas Assistant')">
  <h3>💡 Ideas AI</h3><p>Creative ideas</p>
 </div>
 <div class="tool" onclick="selectTool('Marathi Assistant')">
  <h3>📝 Marathi AI</h3><p>Marathi writing</p>
 </div>
</section>

<section class="chat">
 <h2 id="chatTitle">Chat with SHIV AI</h2>
 <p class="small" id="status">
  Offline demo mode – AI connection not added yet.
 </p>
 <div id="messages" aria-live="polite">
  <div class="msg">Welcome to SHIV AI! Select a tool or type a message.</div>
 </div>
 <input id="question" placeholder="Type your message..."
 onkeydown="if(event.key==='Enter')sendMessage()">
 <div class="actions">
  <button onclick="sendMessage()" id="send">Send</button>
  <button class="secondary" onclick="clearChat()" id="clear">Clear Chat</button>
  <button class="secondary" onclick="copyLast()" id="copy">Copy Last</button>
 </div>
</section>
</main>

<footer>© 2026 SHIV AI | Built with creativity</footer>

<script>
let marathi=false;
let lastAnswer="";
let selectedTool="AI Chat";

function toggleTheme(){
 document.body.classList.toggle("light");
}

function toggleLanguage(){
 marathi=!marathi;
 document.getElementById("lang").innerText=
 marathi?"English":"मराठी";
 document.getElementById("heading").innerText=
 marathi?"SHIV AI मध्ये स्वागत आहे":"Welcome to SHIV AI";
 document.getElementById("sub").innerText=
 marathi?"एक व्यासपीठ, अनेक शक्यता":"One Platform. Many Possibilities.";
 document.getElementById("toolsTitle").innerText=
 marathi?"AI सुविधा":"Explore AI Tools";
 document.getElementById("chatTitle").innerText=
 marathi?"SHIV AI सोबत चॅट":"Chat with SHIV AI";
 document.getElementById("question").placeholder=
 marathi?"तुमचा संदेश लिहा...":"Type your message...";
 document.getElementById("send").innerText=
 marathi?"पाठवा":"Send";
 document.getElementById("clear").innerText=
 marathi?"चॅट साफ करा":"Clear Chat";
 document.getElementById("copy").innerText=
 marathi?"शेवटचे उत्तर कॉपी":"Copy Last";
}

function addMessage(text,type){
 const box=document.getElementById("messages");
 const div=document.createElement("div");
 div.className="msg "+type;
 div.textContent=text;
 box.appendChild(div);
 box.scrollTop=box.scrollHeight;
}

function selectTool(tool){
 selectedTool=tool;
 document.getElementById("question").value=
 marathi?tool+" साठी मला मदत करा.": "Help me with "+tool+".";
 document.getElementById("question").focus();
}

function sendMessage(){
 const input=document.getElementById("question");
 const q=input.value.trim();
 if(!q)return;

 addMessage((marathi?"तुम्ही: ":"You: ")+q,"user");

 const answer=marathi?
 "तुमचा संदेश SHIV AI डेमोमध्ये नोंदवला आहे. खरे AI उत्तर देण्यासाठी सुरक्षित AI सेवा जोडणे बाकी आहे. सध्या हा मोफत ऑफलाइन डेमो आहे.":
 "Your message has been added to the SHIV AI demo. A secure AI service is still needed for real AI answers. This is currently a free offline demo.";

 addMessage("SHIV AI: "+answer,"");
 lastAnswer=answer;

 try{
  let history=JSON.parse(localStorage.getItem("shivHistory")||"[]");
  history.push({question:q,answer:answer});
  localStorage.setItem("shivHistory",JSON.stringify(history.slice(-30)));
 }catch(e){}

 input.value="";
}

function clearChat(){
 document.getElementById("messages").innerHTML="";
 lastAnswer="";
}

async function copyLast(){
 if(!lastAnswer){
  alert(marathi?"कॉपी करण्यासाठी उत्तर नाही":"No answer to copy");
  return;
 }
 try{
  await navigator.clipboard.writeText(lastAnswer);
  alert(marathi?"कॉपी झाले!":"Copied!");
 }catch(e){
  alert(marathi?"कॉपी करता आले नाही":"Copy unavailable");
 }
}
</script>
</body>
</html>
# shiv-ai-site
