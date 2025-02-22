<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blinking REAL Text with Glitch Effect</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #222;
            font-family: Arial, sans-serif;
            overflow: hidden;
            position: relative;
        }
        
        .background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(0, 0, 0, 0.8) 10%, transparent 90%),
                        repeating-conic-gradient(black, transparent 10%, black 20%);
            mask-image: radial-gradient(circle, transparent 20%, black 70%);
            -webkit-mask-image: radial-gradient(circle, transparent 20%, black 70%);
        }
        
        .text {
            font-size: 80px;
            font-weight: bold;
            letter-spacing: 5px;
            position: relative;
            color: #BBB;
            text-shadow: 2px 2px 5px rgba(255, 255, 255, 0.2);
            animation: glitch 0.2s infinite;
        }
        
        @keyframes glitch {
            0% { transform: translate(0, 0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(2px, -2px); }
            60% { transform: translate(-2px, -2px); }
            80% { transform: translate(2px, 2px); }
            100% { transform: translate(0, 0); }
        }
        
        .glitch::before, .glitch::after {
            content: attr(data-text);
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0.75;
        }
        .glitch::before {
            color: #f00;
            transform: translate(-3px, -3px);
            clip-path: polygon(0% 0%, 100% 0%, 100% 50%, 0% 50%);
        }
        .glitch::after {
            color: #0ff;
            transform: translate(3px, 3px);
            clip-path: polygon(0% 50%, 100% 50%, 100% 100%, 0% 100%);
        }
        
        .credit {
            position: absolute;
            bottom: 10px;
            right: 10px;
            font-size: 14px;
            color: white;
            opacity: 1;
            animation: blink 1s infinite alternate;
        }
        @keyframes blink {
            0% { opacity: 1; }
            100% { opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="background"></div>
    <div class="text glitch" id="realText" data-text="REAL">REAL</div>
    <div class="credit">Được làm bởi Real (Tiktok: 3u1c1dal)</div>
    <script>
        const textElement = document.getElementById("realText");
        const alternateChars = ["#", "@", "&", "$", "¢", "π", "0", "1", "5", "Ψ", "Ω", "§", "∑", "µ", "∆", "∇", "≠", "∫", "∞"];
        
        function getRandomColor() {
            const colors = ["#0ff", "#fff", "#000"];
            return colors[Math.floor(Math.random() * colors.length)];
        }
        
        function updateText() {
            let text = "REAL".split("");
            if (Math.random() < 0.5) { 
                let index = Math.floor(Math.random() * text.length);
                text[index] = alternateChars[Math.floor(Math.random() * alternateChars.length)];
                textElement.style.color = getRandomColor();
            } else {
                textElement.style.color = "#BBB";
            }
            let newText = text.join("");
            textElement.textContent = newText;
            textElement.setAttribute("data-text", newText);
        }
        
        setInterval(updateText, 200);
    </script>
</body>
</html>
