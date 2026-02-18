<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>싱박게임 - 🍉</title>
    <style>
        body { margin: 0; padding: 0; overflow: hidden; background: #fff5f5; display: flex; justify-content: center; align-items: center; height: 100vh; }
        #score { position: absolute; top: 20px; font-size: 40px; font-weight: bold; color: #ff4757; z-index: 10; pointer-events: none; text-shadow: 2px 2px white; }
    </style>
</head>
<body>
    <div id="score">0</div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/matter-js/0.18.0/matter.min.js"></script>
    <script>
        const { Engine, Render, Runner, Bodies, Composite, Events } = Matter;
        const engine = Engine.create();
        const render = Render.create({
            element: document.body,
            engine: engine,
            options: { width: 400, height: 600, wireframes: false, background: '#ffffff' }
        });

        const ground = Bodies.rectangle(200, 590, 400, 20, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        const leftWall = Bodies.rectangle(5, 300, 10, 600, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        const rightWall = Bodies.rectangle(395, 300, 10, 600, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        Composite.add(engine.world, [ground, leftWall, rightWall]);

        let score = 0;
        const FRUITS = [
            { radius: 20, score: 2, scale: 0.15 }, // 싱박01.png
            { radius: 30, score: 4, scale: 0.22 }, // 싱박02.png
            { radius: 45, score: 8, scale: 0.3 },  // 싱박03.png
            { radius: 60, score: 16, scale: 0.4 }  // 싱박04.png...
        ];

        window.addEventListener("mousedown", (e) => {
            const x = e.clientX - window.innerWidth / 2 + 200;
            addFruit(x, 50, 0); 
        });

        function addFruit(x, y, index) {
            if (index >= 11) return;
            // 파일 이름을 '싱박01', '싱박02' 형식으로 맞춰주는 부분
            const fileName = `싱박${(index + 1).toString().padStart(2, '0')}.png`;
            
            const fruit = Bodies.circle(x, y, FRUITS[index]?.radius || 20, {
                index: index,
                restitution: 0.3,
                render: { 
                    sprite: { 
                        texture: fileName, 
                        xScale: FRUITS[index]?.scale || 0.2, 
                        yScale: FRUITS[index]?.scale || 0.2 
                    } 
                }
            });
            Composite.add(engine.world, fruit);
        }

        Events.on(engine, "collisionStart", (event) => {
            event.pairs.forEach((collision) => {
                if (collision.bodyA.index !== undefined && collision.bodyA.index === collision.bodyB.index) {
                    const index = collision.bodyA.index;
                    if (index >= 10) return;

                    const newX = (collision.bodyA.position.x + collision.bodyB.position.x) / 2;
                    const newY = (collision.bodyA.position.y + collision.bodyB.position.y) / 2;

                    Composite.remove(engine.world, [collision.bodyA, collision.bodyB]);
                    addFruit(newX, newY, index + 1);
                    
                    score += FRUITS[index]?.score || 10;
                    document.getElementById("score").innerText = score;
                }
            });
        });

        Render.run(render);
        Runner.run(Runner.create(), engine);
    </script>
</body>
</html>
