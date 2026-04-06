<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Creepster&family=Bangers&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #000;
            font-family: 'Bangers', cursive;
            overflow: hidden;
            cursor: none;
        }
        
        .message {
            font-size: 8rem;
            color: #fff;
            text-align: center;
            text-shadow: 0 0 20px #ff00ff, 0 0 40px #ff00ff;
            animation: glow 1s ease-in-out infinite alternate;
            opacity: 0;
        }
        
        @keyframes glow {
            from { text-shadow: 0 0 20px #ff00ff, 0 0 40px #ff00ff; }
            to { text-shadow: 0 0 30px #00ffff, 0 0 60px #00ffff; }
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-30px); }
            60% { transform: translateY(-15px); }
        }
        
        .scare {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(1);
            width: 400px;
            height: 400px;
            background: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTAgCnb4POVgkcGqxUHAPlgW-sfYB_E9ZG5Xu1bM854gC9X7PwoGoptcHg&s') center/contain no-repeat;
            opacity: 0;
            z-index: 1000;
            transition: all 0.1s;
        }
        
        .scare.active {
            transform: translate(-50%, -50%) scale(1.2);
            opacity: 1;
        }
        
        body.dark { background: #000; }
        body.bright { background: #fff; }
        
        @media (max-width: 768px) {
            .message { font-size: 4rem; }
            .scare { width: 300px; height: 300px; }
        }
    </style>
</head>
<body>
    <div class="message" id="message1">WELCOME</div>
    <div class="message" id="message2">GOT U</div>
    <div class="scare" id="scare"></div>
    
    <script>
        const msg1 = document.getElementById('message1');
        const msg2 = document.getElementById('message2');
        const scare = document.getElementById('scare');
        const body = document.body;
        
        // Sequence timing
        setTimeout(() => {
            msg1.style.animation = 'glow 1s ease-in-out infinite alternate, bounce 1s ease-in-out';
            msg1.style.opacity = '1';
        }, 500);
        
        setTimeout(() => {
            msg1.style.opacity = '0';
            msg2.style.opacity = '1';
            msg2.style.animation = 'glow 0.8s ease-in-out infinite alternate, bounce 0.8s ease-in-out 0.2s';
        }, 3000);
        
        setTimeout(() => {
            msg2.style.opacity = '0';
            scare.classList.add('active');
            
            // Start screen flicker
            let flicker = 0;
            const flickerInterval = setInterval(() => {
                flicker++;
                body.className = flicker % 2 === 0 ? 'dark' : 'bright';
                
                // Stop after 10 seconds of chaos
                if (flicker > 200) {
                    clearInterval(flickerInterval);
                    body.style.background = '#000';
                }
            }, 50);
            
            // Audio assault (multiple overlapping screams)
            for (let i = 0; i < 3; i++) {
                setTimeout(() => {
                    playScarySound();
                }, i * 100);
            }
        }, 6000);
        
        function playScarySound() {
            try {
                // Multiple scream layers for maximum effect
                const screams = [
                    'data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAo',
                    'data:audio/wav;base64,UklGRp4GAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAo'
                ];
                screams.forEach(src => {
                    const audio = new Audio(src);
                    audio.volume = 1.0;
                    audio.play().catch(() => {});
                });
            } catch(e) {}
        }
        
        // Fullscreen trap (escape with F11 or ESC)
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' || e.key === 'F11') {
                document.exitFullscreen();
            }
        });
    </script>
</body>
</html>
