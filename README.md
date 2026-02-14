<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be My Valentine?</title>
    <style>
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #fff5f8;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }

        .container {
            position: relative;
            z-index: 10;
            background: rgba(255, 255, 255, 0.85);
            padding: 30px;
            border-radius: 20px;
            backdrop-filter: blur(8px);
            box-shadow: 0 8px 32px rgba(214, 51, 132, 0.2);
            max-width: 90%;
            text-align: center;
        }

        .gif-bg {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 350px;
            z-index: 1;
            border-radius: 20px;
        }

        h1 {
            color: #d63384;
            font-size: 2rem;
            margin-bottom: 10px;
        }

        #message {
            height: 40px;
            margin: 10px 0;
            color: #ff4d6d;
            font-weight: bold;
            font-size: 1.1rem;
        }

        .buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            align-items: center;
            margin-top: 20px;
        }

        button {
            padding: 15px 25px;
            font-size: 1.2rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.1s ease;
        }

        #yesBtn {
            background-color: #ff4d6d;
            color: white;
            z-index: 1000;
        }

        #noBtn {
            background-color: #adb5bd;
            color: white;
        }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <iframe style="display:none" width="0" height="0" id="musicPlayer" 
        src="https://www.youtube.com/embed/gcS79B48m7Y?autoplay=1&loop=1&playlist=gcS79B48m7Y" 
        frameborder="0" allow="autoplay">
    </iframe>

    <img id="bgGif" class="gif-bg" src="96.gif" alt="Bears">

    <div id="valentine-card" class="container">
        <h1 id="question">Will you be my valentine?</h1>
        <p id="message"></p>
        <div class="buttons">
            <button id="yesBtn">yes ofc 😼</button>
            <button id="noBtn">no</button>
        </div>
    </div>

    <div id="success-screen" class="container hidden">
        <h1>Yay! I knew you'd say yes! ❤️</h1>
    </div>

    <script>
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const messageText = document.getElementById('message');
        const card = document.getElementById('valentine-card');
        const bgGif = document.getElementById('bgGif');
        const successScreen = document.getElementById('success-screen');

        let clickCount = 0;
        let yesScale = 1;

        const messages = [
            "why not bby?",
            "come on dont hurt me like this..",
            "please.",
            "do you really want this?..",
            "coms on bby you know how much it hurts me..",
            "please.."
        ];

        noBtn.addEventListener('click', () => {
            clickCount++;
            
            // Text change logic
            if (clickCount <= messages.length) {
                messageText.innerText = messages[clickCount - 1];
            } else {
                messageText.innerText = "please..";
            }

            // Growing Yes button logic
            yesScale += 0.8; 
            yesBtn.style.transform = `scale(${yesScale})`;

            // No button jump logic
            const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
            const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
            noBtn.style.position = 'fixed';
            noBtn.style.left = `${Math.max(20, Math.min(x, window.innerWidth - 100))}px`;
            noBtn.style.top = `${Math.max(20, Math.min(y, window.innerHeight - 50))}px`;

            // If Yes is massive, it covers No
            if (yesScale > 10) {
                noBtn.style.opacity = '0';
                noBtn.style.pointerEvents = 'none';
            }
        });

        yesBtn.addEventListener('click', () => {
            card.classList.add('hidden');
            successScreen.classList.remove('hidden');
            bgGif.src = "102.gif"; 
            bgGif.style.width = "450px";
        });
    </script>
</body>
</html>
