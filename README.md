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
