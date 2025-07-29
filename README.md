<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.9.1/gsap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Satoshi:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            background-color: #0c0a09;
            overflow: hidden;
        }

        .aurora-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: #0c0a09;
            overflow: hidden;
        }

        .aurora-bg .aurora {
            position: absolute;
            border-radius: 50%;
            animation: aurora-flow 15s infinite alternate;
        }

        .aurora.one {
            width: 50vw;
            height: 50vw;
            background: hsla(333, 70%, 55%, .4);
            top: -20%;
            left: -10%;
        }

        .aurora.two {
            width: 60vw;
            height: 60vw;
            background: hsla(282, 82%, 54%, .3);
            top: 20%;
            right: -15%;
            animation-duration: 17s;
        }

        .aurora.three {
            width: 55vw;
            height: 55vw;
            background: hsla(210, 89%, 60%, .3);
            bottom: -25%;
            left: 10%;
            animation-duration: 20s;
        }
        
        .aurora.four {
            width: 40vw;
            height: 40vw;
            background: hsla(35, 90%, 60%, .3);
            bottom: 5%;
            right: 20%;
            animation-duration: 18s;
        }

        @keyframes aurora-flow {
            0% {
                transform: scale(1) translate(0, 0) rotate(0deg);
            }
            100% {
                transform: scale(1.5) translate(10vw, -10vh) rotate(180deg);
            }
        }

        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        .card {
            background: rgba(23, 23, 23, 0.4);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        .font-heading {
            font-family: 'Playfair Display', serif;
        }

        .font-body {
            font-family: 'Satoshi', sans-serif;
        }
        
        .text-gradient {
            background: linear-gradient(to right, #f9a8d4, #fff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .btn-primary {
            background-image: linear-gradient(to right, #ec4899, #ef4444);
            box-shadow: 0 0 15px rgba(236, 72, 153, 0.5);
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px) scale(1.05);
            box-shadow: 0 0 25px rgba(236, 72, 153, 0.8);
        }
        
        .btn-primary:active {
            transform: translateY(0) scale(1);
        }

        .progress-track {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }
        
        .progress-bar {
             background-image: linear-gradient(to right, #ec4899, #ef4444);
        }

        .bento-grid {
            display: grid;
            gap: 1rem;
            grid-template-columns: repeat(2, 1fr);
            grid-template-rows: auto auto;
        }

        .bento-item {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 1rem;
            padding: 1.5rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .bento-item-large {
            grid-column: span 2;
        }

        .polaroid {
            background: #fff;
            padding: 1rem;
            padding-bottom: 3rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            position: relative;
            transform: rotate(-3deg);
            transition: transform 0.3s ease;
        }

        .polaroid:hover {
            transform: rotate(0deg) scale(1.05);
        }

        .polaroid img {
            width: 100%;
            height: auto;
        }

        .polaroid .caption {
            position: absolute;
            bottom: 1rem;
            left: 1rem;
            right: 1rem;
            text-align: center;
            font-family: 'Satoshi', sans-serif;
            color: #333;
        }

    </style>
</head>
<body class="text-gray-200 font-body">

    <div class="aurora-bg">
        <div class="aurora one"></div>
        <div class="aurora two"></div>
        <div class="aurora three"></div>
        <div class="aurora four"></div>
    </div>
    <canvas id="bg-canvas"></canvas>
    
    <div class="fixed top-4 left-1/2 -translate-x-1/2 w-1/3 max-w-sm h-2 rounded-full progress-track">
        <div id="progressBar" class="h-full rounded-full progress-bar" style="width: 20%;"></div>
    </div>

    <main class="w-full h-screen flex items-center justify-center p-4 overflow-hidden">
        
        <!-- Step 1: Welcome -->
        <div id="step-1" class="card rounded-2xl p-8 md:p-12 text-center w-full max-w-lg">
            <div class="text-6xl mb-4 animate-pulse">❤</div>
            <h1 class="text-4xl md:text-5xl font-heading text-gradient mb-4">Hey Beautiful,</h1>
            <p class="mb-8 text-gray-300">I built a little world for you, just to bring a smile to your face on your special day. I want to be your one and only for as long as time flies. I want to make your every living moment worth the while. I wanna be yours ~~ <3</p>
            <button class="btn-primary text-white font-bold py-3 px-8 rounded-full" onclick="goToStep(2)">Let's Begin</button>
        </div>

        <!-- Step 2: Core Message -->
        <div id="step-2" class="card rounded-2xl p-8 md:p-12 text-center w-full max-w-lg absolute opacity-0" style="visibility: hidden;">
            <div class="text-6xl mb-4">🎉</div>
            <h1 class="text-4xl md:text-5xl font-heading text-gradient mb-4">Happy Birthday!</h1>
            <p class="mb-8 text-gray-300">Another year of you making the world brighter. Your existence is a gift, and I'm so lucky to witness it. Happy Birthday to my little princess.</p>
            <button class="btn-primary text-white font-bold py-3 px-8 rounded-full" onclick="goToStep(3)">There's more...</button>
        </div>
        
        <!-- Step 3: Reasons Why -->
        <div id="step-3" class="card rounded-2xl p-8 md:p-12 w-full max-w-2xl absolute opacity-0" style="visibility: hidden;">
             <h1 class="text-4xl md:text-5xl font-heading text-gradient mb-8 text-center">A Few Things I Adore About You</h1>
             <div class="bento-grid">
                <div class="bento-item bento-item-large">
                    <h2 class="font-bold text-xl mb-2 text-pink-300">✨ Your Unmatched Kindness</h2>
                    <p class="text-gray-300">The genuine warmth you show to everyone is something truly rare and beautiful.</p>
                </div>
                <div class="bento-item">
                    <h2 class="font-bold text-xl mb-2 text-pink-300">😊 That Smile</h2>
                    <p class="text-gray-300">It's a work of art.</p>
                </div>
                 <div class="bento-item bento-item-large">
                     <h2 class="font-bold text-xl mb-2 text-pink-300">🌟 Your Radiant Spirit</h2>
                     <p class="text-gray-300">Your passion for life is infectious. Being around you makes everything feel more exciting and possible.</p>
                 </div>
             </div>
             <div class="text-center mt-8">
                <button class="btn-primary text-white font-bold py-3 px-8 rounded-full" onclick="goToStep(4)">Remember this?</button>
            </div>
        </div>

        <!-- Step 4: Shared Memory -->
        <div id="step-4" class="card rounded-2xl p-8 md:p-12 text-center w-full max-w-lg absolute opacity-0" style="visibility: hidden;">
             <h1 class="text-4xl md:text-5xl font-heading text-gradient mb-8">That One Time...</h1>
             <div class="flex justify-center mb-8">
                <div class="polaroid w-64">
                    <img src="crush.jpeg" alt="A shared memory">
                    <div class="caption">Our favorite memory.</div>
                </div>
            </div>
            <p class="mb-8 text-gray-300">Every moment with you feels like a scene from a movie I'd watch on repeat.</p>
            <button class="btn-primary text-white font-bold py-3 px-8 rounded-full" onclick="goToStep(5)">One last thing...</button>
        </div>
        
        <!-- Step 5: Finale -->
        <div id="step-5" class="card rounded-2xl p-8 md:p-12 text-center w-full max-w-lg absolute opacity-0" style="visibility: hidden;">
            <div class="text-6xl mb-4">🎂</div>
            <h1 class="text-4xl md:text-5xl font-heading text-gradient mb-4">My Wish For You</h1>
            <p class="mb-8 text-gray-300">May the next year bring you all the love, success, and pure happiness you so rightfully deserve. May your dreams soar higher than ever.</p>
            <div id="final-message-container" class="h-12">
                <p id="final-message" class="text-2xl text-pink-300 font-bold opacity-0"></p>
            </div>
            <button id="celebrate-btn" class="btn-primary text-white font-bold py-3 px-8 rounded-full" onclick="celebrate()">Celebrate!</button>
        </div>

    </main>
    
    <script>
        // Three.js 3D Hearts
        let scene, camera, renderer, hearts;
        const heartCount = 25;

        function initThree() {
            scene = new THREE.Scene();
            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            renderer = new THREE.WebGLRenderer({ canvas: document.getElementById('bg-canvas'), alpha: true });
            renderer.setSize(window.innerWidth, window.innerHeight);

            camera.position.z = 5;
            
            hearts = [];
            const heartShape = new THREE.Shape();
            heartShape.moveTo( 25, 25 );
            heartShape.bezierCurveTo( 25, 25, 20, 0, 0, 0 );
            heartShape.bezierCurveTo( -30, 0, -30, 35, -30, 35 );
            heartShape.bezierCurveTo( -30, 55, -10, 77, 25, 95 );
            heartShape.bezierCurveTo( 60, 77, 80, 55, 80, 35 );
            heartShape.bezierCurveTo( 80, 35, 80, 0, 50, 0 );
            heartShape.bezierCurveTo( 35, 0, 25, 25, 25, 25 );

            const extrudeSettings = { depth: 8, bevelEnabled: true, bevelSegments: 2, steps: 2, bevelSize: 1, bevelThickness: 1 };
            const geometry = new THREE.ExtrudeGeometry(heartShape, extrudeSettings).scale(0.02, 0.02, 0.02).center();
            
            for (let i = 0; i < heartCount; i++) {
                const material = new THREE.MeshStandardMaterial({
                    color: new THREE.Color(`hsl(${330 + Math.random() * 30}, 90%, 65%)`),
                    metalness: 0.5,
                    roughness: 0.1
                });
                const heart = new THREE.Mesh(geometry, material);
                heart.position.set(
                    (Math.random() - 0.5) * 10,
                    (Math.random() - 0.5) * 10,
                    (Math.random() - 0.5) * 5
                );
                heart.rotation.set(
                    Math.random() * Math.PI,
                    Math.random() * Math.PI,
                    Math.random() * Math.PI
                );
                heart.userData.baseY = heart.position.y;
                heart.userData.phase = Math.random() * Math.PI * 2;
                scene.add(heart);
                hearts.push(heart);
            }
            
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.3);
            scene.add(ambientLight);

            const pointLight = new THREE.PointLight(0xffffff, 1);
            pointLight.position.set(5, 5, 5);
            scene.add(pointLight);

            animate();
        }

        let isCelebrating = false;

        function animate() {
            requestAnimationFrame(animate);

            hearts.forEach(heart => {
                if (isCelebrating) {
                    heart.position.y += 0.05;
                    heart.rotation.x += 0.02;
                    heart.rotation.y += 0.02;
                } else {
                    heart.rotation.x += 0.001;
                    heart.rotation.y += 0.001;
                    heart.position.y = heart.userData.baseY + Math.sin(heart.userData.phase + Date.now() * 0.001) * 0.5;
                }
            });

            renderer.render(scene, camera);
        }
        
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
        
        initThree();
        
        // GSAP Animations & Step Logic
        let currentStep = 1;
        const totalSteps = 5;
        const progressBar = document.getElementById('progressBar');

        function goToStep(step) {
            const currentEl = document.getElementById(`step-${currentStep}`);
            const nextEl = document.getElementById(`step-${step}`);
            
            gsap.timeline()
              .to(currentEl, { opacity: 0, y: -50, duration: 0.5, ease: 'power2.in', onComplete: () => currentEl.style.visibility = 'hidden'})
              .set(nextEl, { y: 50, visibility: 'visible'})
              .to(nextEl, { opacity: 1, y: 0, duration: 0.5, ease: 'power2.out' });

            currentStep = step;
            updateProgressBar();
        }

        function updateProgressBar() {
            const progress = (currentStep / totalSteps) * 100;
            gsap.to(progressBar, { width: `${progress}%`, duration: 0.5, ease: 'power2.out' });
        }
        
        // Confetti & Finale
        function celebrate() {
            const celebrateBtn = document.getElementById('celebrate-btn');
            const finalMessage = document.getElementById('final-message');

            gsap.to(celebrateBtn, { opacity: 0, scale: 0.8, duration: 0.3, onComplete: () => celebrateBtn.style.display = 'none' });

            finalMessage.textContent = "Happy Birthday, my crush! ❤";
            gsap.to(finalMessage, { opacity: 1, y: -10, duration: 0.5, delay: 0.3 });
            
            isCelebrating = true;
            gsap.to(hearts.map(h => h.material), { opacity: 0, duration: 5, stagger: 0.05 });

            const duration = 5 * 1000;
            const animationEnd = Date.now() + duration;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

            function randomInRange(min, max) {
                return Math.random() * (max - min) + min;
            }

            const interval = setInterval(function() {
                const timeLeft = animationEnd - Date.now();

                if (timeLeft <= 0) {
                    return clearInterval(interval);
                }

                const particleCount = 50 * (timeLeft / duration);
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
                confetti({
                    particleCount: 2,
                    angle: 90,
                    spread: 180,
                    origin: { y: Math.random() },
                    shapes: ['emoji'],
                    shapeOptions: {
                        emoji: {
                            value: ['❤', '💖', '✨']
                        }
                    }
                });

            }, 250);
        }

    </script>
</body>
</html>
