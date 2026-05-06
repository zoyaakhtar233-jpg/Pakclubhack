<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PakClub App</title>

<style>
body {
    margin: 0;
    background: #0f172a;
    font-family: Arial;
}

/* WebView */
iframe {
    width: 100%;
    height: 100vh;
    border: none;
}

/* Floating Buttons */
.floating {
    position: fixed;
    bottom: 20px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: #22c55e;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 0 10px rgba(0,0,0,0.5);
}

/* Left (Prediction) */
#predictionBtn {
    left: 20px;
    background: #3b82f6;
}

/* Right (WhatsApp) */
#whatsappBtn {
    right: 20px;
}

/* Prediction Box */
#predictionBox {
    position: fixed;
    bottom: 100px;
    left: 20px;
    background: #1e293b;
    padding: 10px 15px;
    border-radius: 10px;
    color: white;
    display: none;
}
</style>
</head>

<body>

<!-- WebView -->
<iframe src="https://pakclub.email/register?inviteCode=33MDH5W&from=app"></iframe>

<!-- Prediction Button -->
<div id="predictionBtn" class="floating" onclick="togglePrediction()">P</div>

<!-- WhatsApp Button -->
<div id="whatsappBtn" class="floating" onclick="openWhatsApp()">W</div>

<!-- Prediction Box -->
<div id="predictionBox">Prediction: <span id="result">---</span></div>

<script>

// ================= VOICE =================

// First Auto Voice
window.onload = function () {
    speak("Game main welcome, sabse pehle new account banao. Agar login kiya to account band kar diya jayega.");

    // Random second voice after few seconds
    setTimeout(randomVoice, 8000);
};

function speak(text) {
    let msg = new SpeechSynthesisUtterance(text);
    msg.rate = 0.9;
    msg.pitch = 1;
    speechSynthesis.speak(msg);
}

function randomVoice() {
    let messages = [
        "Agar aap strategy samajhna chahte hain ya VIP session follow karna chahte hain to abhi WhatsApp channel join karein. WhatsApp button par click karein."
    ];

    let random = messages[Math.floor(Math.random() * messages.length)];
    speak(random);
}

// ================= WHATSAPP =================
function openWhatsApp() {
    window.open("https://whatsapp.com/channel/yourlinkiy", "_blank");
}

// ================= PREDICTION =================
let active = false;

function togglePrediction() {
    let box = document.getElementById("predictionBox");

    active = !active;
    box.style.display = active ? "block" : "none";

    if (active) startPrediction();
}

function startPrediction() {
    if (!active) return;

    let result = Math.random() > 0.5 ? "BIG" : "SMALL";
    document.getElementById("result").innerText = result;

    setTimeout(startPrediction, 3000); // every 3 sec change
}

// ================= DRAG (MOVE BUTTONS) =================
dragElement(document.getElementById("predictionBtn"));
dragElement(document.getElementById("whatsappBtn"));

function dragElement(elmnt) {
    let pos1=0, pos2=0, pos3=0, pos4=0;

    elmnt.onmousedown = dragMouseDown;

    function dragMouseDown(e) {
        e.preventDefault();
        pos3 = e.clientX;
        pos4 = e.clientY;
        document.onmouseup = closeDrag;
        document.onmousemove = elementDrag;
    }

    function elementDrag(e) {
        e.preventDefault();
        pos1 = pos3 - e.clientX;
        pos2 = pos4 - e.clientY;
        pos3 = e.clientX;
        pos4 = e.clientY;

        elmnt.style.top = (elmnt.offsetTop - pos2) + "px";
        elmnt.style.left = (elmnt.offsetLeft - pos1) + "px";
    }

    function closeDrag() {
        document.onmouseup = null;
        document.onmousemove = null;
    }
}

</script>

</body>
</html>
