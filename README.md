# Promise-day-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Our Promise Day Journey</title>
    <style>
        :root { --primary: #ff4d6d; --bg: #fff0f3; }
        body { margin: 0; background: var(--bg); font-family: 'Courier New', Courier, monospace; overflow: hidden; color: #333; }
        
        /* Intro Glitch Styles */
        #intro-screen { height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: center; background: #000; color: #0f0; z-index: 100; position: relative; }
        .glitch { font-size: 2rem; font-weight: bold; text-transform: uppercase; position: relative; text-shadow: 2px 0 red, -2px 0 blue; animation: glitch-anim 0.2s infinite; }
        @keyframes glitch-anim {
            0% { transform: translate(2px, 2px); }
            50% { transform: translate(-2px, -2px); }
            100% { transform: translate(1px, -1px); }
        }
        
        /* Game Styles */
        #game-screen, #final-screen { display: none; height: 100vh; flex-direction: column; align-items: center; justify-content: center; }
        #heart { position: absolute; font-size: 60px; cursor: pointer; user-select: none; z-index: 10; transition: transform 0.1s; }
        
        /* Slideshow Styles */
        .slideshow-img { max-width: 90%; max-height: 70vh; border-radius: 15px; border: 5px solid white; box-shadow: 0 10px 30px rgba(0,0,0,0.2); display: none; }
        .active-slide { display: block; animation: fadeIn 1s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .btn { background: var(--primary); color: white; border: none; padding: 15px 30px; border-radius: 50px; font-size: 1.2rem; cursor: pointer; margin-top: 20px; box-shadow: 0 4px 15px rgba(255, 77, 109, 0.4); }
        .counter { position: absolute; top: 20px; right: 20px; font-size: 1.2rem; font-weight: bold; color: var(--primary); }
    </style>
</head>
<body>

    <div id="intro-screen">
        <div id="glitch-text" class="glitch">SYSTEM REBOOTING...</div>
        <button id="start-btn" class="btn" style="display:none;" onclick="startGame()">START GAME ✨</button>
    </div>

    <div id="game-screen">
        <div class="counter">Hearts Found: <span id="count">0</span>/2</div>
        <h2 id="instruction">Catch 2 hearts to unlock my promises...</h2>
        <div id="heart">❤️</div>
    </div>

    <div id="final-screen">
        <h2 style="color: var(--primary);">Our Journey So Far...</h2>
        <div id="slideshow-container">
            <img src="5607.jpg" class="slideshow-img active-slide">
            <img src="5534.jpg" class="slideshow-img">
            <img src="5551.jpg" class="slideshow-img">
            <img src="5550.jpg" class="slideshow-img">
            <img src="6294.jpg" class="slideshow-img">
            <img src="6251.jpg" class="slideshow-img">
            <img src="6252.jpg" class="slideshow-img">
            <img src="6246.jpg" class="slideshow-img">
            <img src="35428.jpg" class="slideshow-img">
        </div>
        <p id="final-promise" style="margin-top: 20px; font-weight: bold;"></p>
    </div>

    <script>
        const glitchTexts = [
            "FEB 7: ROSE DAY 🌹",
            "FEB 8: PROPOSE DAY 💍",
            "FEB 9: CHOCOLATE DAY 🍫",
            "FEB 10: TEDDY DAY 🧸",
            "TODAY: PROMISE DAY... 🤝"
        ];
        
        let glitchIdx = 0;
        const glitchEl = document.getElementById('glitch-text');
        const startBtn = document.getElementById('start-btn');

        // Glitch sequence
        const glitchInterval = setInterval(() => {
            glitchEl.innerText = glitchTexts[glitchIdx];
            glitchIdx++;
            if(glitchIdx >= glitchTexts.length) {
                clearInterval(glitchInterval);
                glitchEl.classList.remove('glitch');
                glitchEl.style.color = "#ff4d6d";
                startBtn.style.display = "block";
            }
        }, 1500);

        function startGame() {
            document.getElementById('intro-screen').style.display = 'none';
            document.getElementById('game-screen').style.display = 'flex';
            moveHeart();
        }

        // Game Logic
        let heartsCaught = 0;
        const heart = document.getElementById('heart');
        const countEl = document.getElementById('count');

        function moveHeart() {
            const x = Math.random() * (window.innerWidth - 100);
            const y = Math.random() * (window.innerHeight - 100);
            heart.style.left = x + 'px';
            heart.style.top = y + 'px';
        }

        let mover = setInterval(moveHeart, 800);

        heart.addEventListener('click', () => {
            heartsCaught++;
            countEl.innerText = heartsCaught;
            
            if(heartsCaught === 1) {
                alert("One found! The next one is faster...");
                clearInterval(mover);
                mover = setInterval(moveHeart, 500); // Speed up
            } else if (heartsCaught === 2) {
                clearInterval(mover);
                showFinal();
            }
        });

        // Slideshow Logic
        function showFinal() {
            document.getElementById('game-screen').style.display = 'none';
            document.getElementById('final-screen').style.display = 'flex';
            
            let slides = document.querySelectorAll('.slideshow-img');
            let currentSlide = 0;

            setInterval(() => {
                slides[currentSlide].classList.remove('active-slide');
                currentSlide = (currentSlide + 1) % slides.length;
                slides[currentSlide].classList.add('active-slide');
            }, 3000);

            document.getElementById('final-promise').innerText = "I promise to stay by your side through every chapter of our story. ❤️";
        }
    </script>
</body>
</html>
