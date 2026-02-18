# index.html
싱박게임
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>싱박게임 - 싱믄 🍉</title>
    <style>
        body { margin: 0; background: #fff5f5; display: flex; justify-content: center; align-items: center; height: 100vh; overflow: hidden; font-family: sans-serif; }
        #game-canvas { border: 5px solid #ffb7b7; border-radius: 15px; background: #fff; cursor: pointer; }
        #score { position: absolute; top: 20px; font-size: 40px; font-weight: bold; color: #ff4757; z-index: 10; pointer-events: none; }
    </style>
</head>
<body>
    <div id="score">0</div>
    <canvas id="game-canvas"></canvas>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/matter-js/0.18.0/matter.min.js"></script>
    <script>
        // 싱박게임 엔진 가동!
        // singmeun 님의 11개 이미지를 게임에 연결하는 핵심 로직입니다.
        console.log("싱박게임 세팅 완료!");
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>싱박게임 - 두쫀쿠 싱믄 🍉</title>
    <style>
        body { margin: 0; background: #fff5f5; display: flex; justify-content: center; align-items: center; height: 100vh; overflow: hidden; font-family: sans-serif; }
        #score { position: absolute; top: 20px; font-size: 40px; font-weight: bold; color: #ff4757; z-index: 10; }
    </style>
</head>
<body>
    <div id="score">0</div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/matter-js/0.18.0/matter.min.js"></script>
    <script>
        const { Engine, Render, Runner, Bodies, Composite, Mouse, MouseConstraint, Events } = Matter;

        // 엔진 및 렌더러 설정
        const engine = Engine.create();
        const render = Render.create({
            element: document.body,
            engine: engine,
            options: { width: 400, height: 600, wireframes: false, background: '#ffffff' }
        });

        // 벽 만들기 (바닥, 왼쪽, 오른쪽)
        const ground = Bodies.rectangle(200, 590, 400, 20, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        const leftWall = Bodies.rectangle(5, 300, 10, 600, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        const rightWall = Bodies.rectangle(395, 300, 10, 600, { isStatic: true, render: { fillStyle: '#ffb7b7' } });
        Composite.add(engine.world, [ground, leftWall, rightWall]);

        // 마우스 클릭 시 과일 생성
        window.addEventListener("mousedown", () => {
            const circle = Bodies.circle(event.clientX - window.innerWidth/2 + 200, 50, 20, {
                restitution: 0.5,
                render: { sprite: { texture: '1.png', xScale: 0.1, yScale: 0.1 } } // 여기서 사진을 불러옵니다!
            });
            Composite.add(engine.world, circle);
        });

        Render.run(render);
        Runner.run(Runner.create(), engine);
    </script>
</body>
</html>
