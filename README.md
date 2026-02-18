<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>싱박게임 - 🍉</title>
    <style>
        body { margin: 0; padding: 0; overflow: hidden; background: #fff5f5; display: flex; justify-content: center; align-items: center; height: 100vh; }
        #score { position: absolute; top: 20px; font-size: 30px; font-weight: bold; color: #ff4757; z-index: 10; pointer-events: none; }
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

        // 바닥과 벽
        const ground = Bodies.rectangle(200, 590, 400, 20, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        const leftWall = Bodies.rectangle(5, 300, 10, 600, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        const rightWall = Bodies.rectangle(395, 300, 10, 600, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        Composite.add(engine.world, [ground, leftWall, rightWall]);

        // 클릭하면 사진(과일) 떨어뜨리기
        window.addEventListener("mousedown", (e) => {
            const x = e.clientX - window.innerWidth / 2 + 200;
            const fruit = Bodies.circle(x, 50, 20, {
                restitution: 0.5,
                render: { 
                    sprite: { 
                        texture: '1.png', // 올리신 사진 이름이 1.png인지 꼭 확인!
                        xScale: 0.1, 
                        yScale: 0.1 
                    } 
                }
            });
            Composite.add(engine.world, fruit);
        });

        Render.run(render);
        Runner.run(Runner.create(), engine);
    </script>
</body>
</html>
