# ManiaProject041

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ブロック崩しゲーム</title>
<style>
  body {
    margin: 0;
    padding: 0;
    overflow: hidden;
  }
  canvas {
    display: block;
  }
</style>
</head>
<body>
<canvas id="gameCanvas"></canvas>
<script>
  const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");

  // パドルの初期設定
  const paddleWidth = 100;
  const paddleHeight = 10;
  let paddleX = (canvas.width - paddleWidth) / 2;

  // ボールの初期設定
  const ballRadius = 10;
  let ballX = canvas.width / 2;
  let ballY = canvas.height - 30;
  let ballSpeedX = 3;
  let ballSpeedY = -3;

  // ブロックの初期設定
  const brickRowCount = 5;
  const brickColumnCount = 5;
  const brickWidth = 75;
  const brickHeight = 20;
  const brickPadding = 10;
  const brickOffsetTop = 30;
  const brickOffsetLeft = 30;

  const bricks = [];
  for (let col = 0; col < brickColumnCount; col++) {
    bricks[col] = [];
    for (let row = 0; row < brickRowCount; row++) {
      bricks[col][row] = { x: 0, y: 0, status: 1 };
    }
  }

  // パドルの描画
  function drawPaddle() {
    ctx.beginPath();
    ctx.rect(paddleX, canvas.height - paddleHeight, paddleWidth, paddleHeight);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
  }

  // ボールの描画
  function drawBall() {
    ctx.beginPath();
    ctx.arc(ballX, ballY, ballRadius, 0, Math.PI * 2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
  }

  // ブロックの描画
  function drawBricks() {
    for (let col = 0; col < brickColumnCount; col++) {
      for (let row = 0; row < brickRowCount; row++) {
        if (bricks[col][row].status === 1) {
          const brickX = col * (brickWidth + brickPadding) + brickOffsetLeft;
          const brickY = row * (brickHeight + brickPadding) + brickOffsetTop;
          bricks[col][row].x = brickX;
          bricks[col][row].y = brickY;
          ctx.beginPath();
          ctx.rect(brickX, brickY, brickWidth, brickHeight);
          ctx.fillStyle = "#0095DD";
          ctx.fill();
          ctx.closePath();
        }
      }
    }
  }

  // ゲームの描画
  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawBricks();
    drawBall();
    drawPaddle();
    requestAnimationFrame(draw);
  }

  // ゲーム開始
  draw();

</script>
</body>
</html>
