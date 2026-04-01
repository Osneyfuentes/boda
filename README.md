<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Invitación de Boda - Alejandro y Valeria</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Montserrat:wght@300;400&display=swap" rel="stylesheet">

    <style>
        /* CSS: DISEÑO Y ESTILO DE LA TARJETA */
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #f4eae3; /* Un beige suave de fondo */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden; /* Evita que salgan barras de desplazamiento por los corazones */
        }

        .card {
            background-color: #ffffff;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 400px;
            width: 90%;
            border: 2px solid #e0c8b0;
            position: relative; /* Necesario para que las partículas se posicionen respecto a la tarjeta */
        }

        .romantic-font {
            font-family: 'Dancing Script', cursive;
            color: #b08d57; /* Un tono dorado mate */
            font-size: 3em;
            margin: 10px 0;
        }

        h3 { font-weight: 300; color: #555; text-transform: uppercase; letter-spacing: 2px; font-size: 0.9em;}
        p { color: #777; line-height: 1.6; }

        .date-box {
            border-top: 1px solid #eee;
            border-bottom: 1px solid #eee;
            padding: 15px 0;
            margin: 20px 0;
        }

        /* ESTILO DEL BOTÓN "MÁGICO" */
        #magicButton {
            background-color: #b08d57;
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 30px;
            font-family: 'Montserrat', sans-serif;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(176, 141, 87, 0.4);
            transition: all 0.3s ease;
            position: relative;
            z-index: 10; /* Asegura que el botón esté sobre los corazones */
        }

        #magicButton:hover {
            background-color: #967540;
            transform: translateY(-2px);
        }

        /* CSS PARA LOS CORAZONES DE LA EXPLOSIÓN */
        .heart-particle {
            position: absolute;
            color: #d63031; /* Color rojo vibrante */
            font-size: 20px;
            pointer-events: none; /* Los corazones no se pueden clicar */
            opacity: 0;
            /* La animación se asignará dinámicamente con JavaScript */
        }

        /* Definimos la animación de la partícula */
        @keyframes explode {
            0% { transform: translate(0, 0) scale(1); opacity: 1; }
            100% { transform: translate(var(--tx), var(--ty)) scale(0); opacity: 0; }
        }
    </style>
</head>
<body>

    <div class="card" id="cardContainer">
        <h3>Nos Casamos</h3>
        
        <div class="romantic-font">Alejandro</div>
        <div style="font-size: 1.5em; color: #b08d57;">&</div>
        <div class="romantic-font">Valeria</div>
        
        <p>Tenemos el placer de invitarte a compartir la alegría de nuestra unión.</p>
        
        <div class="date-box">
            <p>Sábado, 14 de Septiembre de 2024</p>
            <p>18:30 Horas</p>
        </div>
        
        <p>Hacienda El Estribo, Cabimas</p>

        <button id="magicButton">¡Confirmar Asistencia!</button>
    </div>

    <script>
        const button = document.getElementById('magicButton');
        const card = document.getElementById('cardContainer');

        // Función que crea la explosión
        function createExplosion(e) {
            // Número de corazones por explosión
            const numberOfHearts = 40;

            for (let i = 0; i < numberOfHearts; i++) {
                // 1. Crear el elemento del corazón
                const heart = document.createElement('div');
                heart.classList.add('heart-particle');
                heart.innerHTML = '❤️'; // Usamos el emoji

                // 2. Posicionar el corazón inicialmente sobre el botón
                // Usamos offsetLeft/Top para que sea relativo a la tarjeta (que tiene position: relative)
                const x = button.offsetLeft + button.offsetWidth / 2;
                const y = button.offsetTop + button.offsetHeight / 2;
                heart.style.left = x + 'px';
                heart.style.top = y + 'px';

                // 3. Generar una dirección aleatoria (360 grados)
                const destinationX = (Math.random() - 0.5) * 300; // Distancia horizontal (-150px a 150px)
                const destinationY = (Math.random() - 0.5) * 300; // Distancia vertical

                // 4. Asignar las variables de destino al CSS
                heart.style.setProperty('--tx', `${destinationX}px`);
                heart.style.setProperty('--ty', `${destinationY}px`);

                // 5. Variar el tamaño y la duración aleatoriamente para naturalidad
                const size = Math.random() * 10 + 15; // 15px a 25px
                heart.style.fontSize = `${size}px`;
                
                const duration = Math.random() * 1 + 0.5; // 0.5s a 1.5s
                heart.style.animation = `explode ${duration}s ease-out forwards`;

                // 6. Añadir el corazón a la tarjeta y borrarlo cuando acabe la animación
                card.appendChild(heart);

                setTimeout(() => {
                    heart.remove();
                }, duration * 1000);
            }
        }

        // Evento: Al hacer clic en el botón
        button.addEventListener('click', createExplosion);
    </script>
</body>
</html>
