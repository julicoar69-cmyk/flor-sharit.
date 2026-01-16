<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Flor para Sharit</title>
    <style>
        body {
            margin: 0;
            background: black;
            overflow: hidden;
            cursor: none;
            font-family: Arial, sans-serif;
        }
        canvas {
            display: block;
        }
        .link {
            position: fixed;
            bottom: 15px;
            width: 100%;
            text-align: center;
            cursor: default;
        }
        .link a {
            color: #ffd54f;
            text-decoration: none;
            font-size: 16px;
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 16px;
            border-radius: 20px;
        }
        .link a:hover {
            background: rgba(255, 213, 79, 0.3);
        }
    </style>
</head>
<body>

<canvas id="canvas"></canvas>

<div class="link">
    <!-- AQUÍ CAMBIAS EL LINK CUANDO LO TENGAS -->
    <a href="https://tulink-aqui.com" target="_blank">
        💛 Enlace especial para Sharit 💛
    </a>
</div>

<script>
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");

    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    // ⭐ Estrellas
    const stars = [];
    for (let i = 0; i < 120; i++) {
        stars.push({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            r: Math.random() * 2,
            speed: Math.random() * 0.6 + 0.2
        });
    }

    function drawStars() {
        ctx.fillStyle = "white";
        stars.forEach(s => {
            ctx.beginPath();
            ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
            ctx.fill();

            s.y += s.speed;
            if (s.y > canvas.height) {
                s.y = 0;
                s.x = Math.random() * canvas.width;
            }
        });
    }

    // 🌼 Flor
    let x = canvas.width / 2;
    let y = canvas.height / 2;

    window.addEventListener("mousemove", e => {
        x = e.clientX;
        y = e.clientY;
    });

    function drawFlower(px, py) {
        ctx.save();
        ctx.translate(px, py);

        for (let i = 0; i < 12; i++) {
            ctx.rotate(Math.PI * 2 / 12);
            let grad = ctx.createRadialGradient(0, -60, 10, 0, -60, 50);
            grad.addColorStop(0, "#fffde7");
            grad.addColorStop(1, "#fbc02d");

            ctx.beginPath();
            ctx.ellipse(0, -80, 30, 70, 0, 0, Math.PI * 2);
            ctx.fillStyle = grad;
            ctx.fill();
        }

        let centerGrad = ctx.createRadialGradient(0, 0, 5, 0, 0, 40);
        centerGrad.addColorStop(0, "#fff176");
        centerGrad.addColorStop(1, "#f57f17");

        ctx.beginPath();
        ctx.arc(0, 0, 40, 0, Math.PI * 2);
        ctx.fillStyle = centerGrad;
        ctx.fill();

        ctx.font = "bold 28px Arial";
        ctx.fillStyle = "white";
        ctx.textAlign = "center";
        ctx.fillText("sharit", 0, 160);

        ctx.restore();
    }

    function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        drawStars();
        drawFlower(x, y);
        requestAnimationFrame(animate);
    }

    animate();

    window.addEventListener("resize", () => {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    });
</script>

</body>
</html>
