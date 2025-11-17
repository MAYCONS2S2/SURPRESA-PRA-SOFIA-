<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Pedido de Namoro</title>

    <style>
        body {
            background: #ffdde6;
            font-family: Arial, sans-serif;
            text-align: center;
            overflow: hidden;
        }

        .card {
            background: white;
            max-width: 420px;
            width: 90%;
            margin: 80px auto;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 0 15px rgba(0,0,0,0.2);
            position: relative; /* importantíssimo para o botão NÃO */
            z-index: 10;
        }

        h2, h3 {
            color: #d6336c;
            margin-bottom: 15px;
        }

        button {
            padding: 15px 25px;
            border: none;
            border-radius: 12px;
            font-size: 20px;
            cursor: pointer;
            margin: 10px;
            transition: 0.2s;
            width: 70%;
            max-width: 250px;
        }

        .sim {
            background: #ff5c8a;
            color: white;
            position: relative;
            z-index: 20;
        }

        .nao {
            background: #999;
            color: white;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        /* Corações caindo */
        .heart {
            position: fixed;
            color: #ff5c8a;
            font-size: 30px;
            animation: fall linear;
            pointer-events: none;
        }

        @keyframes fall {
            0% { transform: translateY(-50px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }

        #tiktok-container {
            margin-top: 20px;
        }

    </style>
</head>

<body>

    <div class="card">
        <h2>Sofia...</h2>
        <h3>Eu queria te perguntar algo muito especial 💗</h3>
        <h3>Você aceitaria namorar comigo?</h3>

        <button class="sim" id="btnSim">Sim 💖</button>
        <button class="nao" id="nao">Não 😢</button>

        <p id="resultado" style="margin-top:20px; font-size:20px; color:#d6336c;"></p>

        <div id="tiktok-container"></div>
    </div>

    <script>
        let fugas = 0;

        const btnNao = document.getElementById("nao");
        const card = document.querySelector(".card");

        btnNao.addEventListener("click", () => {
            // Área centralizada dentro do card
            const largura = card.offsetWidth - btnNao.offsetWidth;
            const altura = card.offsetHeight - btnNao.offsetHeight;

            const x = Math.random() * largura;
            const y = Math.random() * altura;

            btnNao.style.left = x + "px";
            btnNao.style.top = y + "px";

            fugas++;

            if (fugas >= 3) {
                document.getElementById("resultado").innerHTML =
                    "Nossa, você não quer mesmo, aceita logo 🔪☠😍";
            }
        });

        document.getElementById("btnSim").addEventListener("click", () => {
            document.getElementById("resultado").innerHTML =
                "Eu sabia que você diria sim, Sofia! 💕💍<br>Agora começa a nossa história!";

            // Criar corações
            setInterval(() => {
                const heart = document.createElement("div");
                heart.innerHTML = "❤";
                heart.classList.add("heart");
                heart.style.left = Math.random() * 100 + "vw";
                heart.style.fontSize = Math.random() * 40 + 30 + "px";
                heart.style.animationDuration = Math.random() * 3 + 3 + "s";
                document.body.appendChild(heart);
                setTimeout(() => heart.remove(), 6000);
            }, 150);

            // Inserir TikTok embed dinamicamente
            const container = document.getElementById("tiktok-container");
            container.innerHTML = `
            <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@fernandaphx/video/7367535233597459718" data-video-id="7367535233597459718" style="max-width: 605px;min-width: 325px;">
                <section>
                    <a target="_blank" title="@fernandaphx" href="https://www.tiktok.com/@fernandaphx?refer=embed">@fernandaphx</a>
                </section>
            </blockquote>
            `;
            // Criar script separadamente
            const script = document.createElement("script");
            script.src = "https://www.tiktok.com/embed.js";
            script.async = true;
            container.appendChild(script);
        });
    </script>

</body>
</html>
