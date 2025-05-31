<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Uma Carta Para Você 💌</title>
    
    <!-- Importando fontes românticas do Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;600;700&family=Great+Vibes&family=Pacifico&display=swap" rel="stylesheet">
    
    <style>
        /* Reset básico e configurações globais */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            min-height: 100vh;
            font-family: 'Dancing Script', cursive;
            overflow-x: hidden;
            /* Gradiente suave em tons pastéis */
            background: linear-gradient(135deg, 
                #ffeef8 0%, 
                #f0e6ff 25%, 
                #e6f3ff 50%, 
                #fff0f5 75%, 
                #f5f0ff 100%);
            background-attachment: fixed;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        
        /* Container principal */
        .container {
            width: 100%;
            max-width: 800px;
            padding: 20px;
            position: relative;
            z-index: 10;
        }
        
        /* Título inicial */
        .title {
            text-align: center;
            font-family: 'Great Vibes', cursive;
            font-size: 3rem;
            color: #d63384;
            margin-bottom: 2rem;
            opacity: 0;
            animation: fadeInDown 1.5s ease-out forwards;
            text-shadow: 2px 2px 4px rgba(214, 51, 132, 0.2);
        }
        
        /* Envelope/Carta fechada */
        .envelope {
            width: 300px;
            height: 200px;
            margin: 0 auto;
            position: relative;
            cursor: pointer;
            transition: transform 0.3s ease;
            opacity: 0;
            animation: fadeInUp 2s ease-out 0.5s forwards;
        }
        
        .envelope:hover {
            transform: scale(1.05);
        }
        
        /* Parte de trás do envelope */
        .envelope-back {
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #fff0f5, #ffeef8);
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(214, 51, 132, 0.2);
            position: relative;
            border: 2px solid #f8d7da;
        }
        
        /* Flap do envelope */
        .envelope-flap {
            width: 0;
            height: 0;
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            border-top: 100px solid #f8d7da;
            position: absolute;
            top: 0;
            left: 0;
            transform-origin: bottom center;
            transition: transform 0.8s ease;
            z-index: 2;
        }
        
        /* Selo decorativo */
        .stamp {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 40px;
            height: 30px;
            background: #d63384;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            border-radius: 3px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }
        
        /* Texto no envelope */
        .envelope-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-family: 'Pacifico', cursive;
            color: #d63384;
            font-size: 1.2rem;
            text-align: center;
            z-index: 1;
        }
        
        /* Carta aberta (inicialmente escondida) */
        .letter {
            display: none;
            max-width: 600px;
            margin: 2rem auto;
            background: #fffef7;
            padding: 3rem;
            border-radius: 15px;
            box-shadow: 0 15px 40px rgba(214, 51, 132, 0.15);
            border: 1px solid #f8d7da;
            position: relative;
            opacity: 0;
            transform: translateY(20px);
            animation: letterAppear 1s ease-out forwards;
        }
        
        /* Conteúdo da carta */
        .letter-content {
            font-size: 1.4rem;
            line-height: 1.8;
            color: #495057;
            text-align: center;
            margin-bottom: 2rem;
        }
        
        /* Container da foto especial */
        .special-photo-container {
            text-align: center;
            margin: 2rem 0;
            opacity: 0;
            animation: fadeIn 1s ease-out 0.8s forwards;
        }
        
        .special-photo-title {
            font-family: 'Great Vibes', cursive;
            font-size: 1.8rem;
            color: #d63384;
            margin-bottom: 1rem;
        }
        
        .special-photo {
            width: 100%;
            max-width: 300px;
            height: 300px;
            object-fit: cover;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(214, 51, 132, 0.2);
            border: 3px solid #f8d7da;
            cursor: pointer;
            transition: all 0.3s ease;
            filter: sepia(20%) saturate(1.2);
        }
        
        .special-photo:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(214, 51, 132, 0.3);
            filter: sepia(0%) saturate(1.4);
        }
        
        /* Player de música */
        .music-player {
            background: linear-gradient(135deg, #fff0f5, #ffeef8);
            border-radius: 15px;
            padding: 1.5rem;
            margin: 2rem 0;
            text-align: center;
            box-shadow: 0 8px 25px rgba(214, 51, 132, 0.1);
            border: 1px solid #f8d7da;
            opacity: 0;
            animation: fadeIn 1s ease-out 1.2s forwards;
        }
        
        .music-title {
            font-family: 'Dancing Script', cursive;
            font-size: 1.3rem;
            color: #d63384;
            margin-bottom: 1rem;
        }
        
        .play-button {
            background: linear-gradient(135deg, #d63384, #f8d7da);
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(214, 51, 132, 0.3);
            margin: 0 10px;
        }
        
        .play-button:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 25px rgba(214, 51, 132, 0.4);
        }
        
        .music-controls {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-top: 1rem;
        }
        
        .volume-control {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .volume-slider {
            width: 100px;
            height: 5px;
            border-radius: 5px;
            background: #f8d7da;
            outline: none;
            cursor: pointer;
        }
        
        .volume-slider::-webkit-slider-thumb {
            appearance: none;
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background: #d63384;
            cursor: pointer;
        }
        
        /* Assinatura */
        .signature {
            text-align: right;
            font-family: 'Great Vibes', cursive;
            font-size: 1.8rem;
            color: #d63384;
            margin-top: 2rem;
        }
        
        /* Botão de fechar */
        .close-button {
            display: block;
            margin: 2rem auto 0;
            padding: 15px 30px;
            background: linear-gradient(135deg, #d63384, #f8d7da);
            color: white;
            border: none;
            border-radius: 25px;
            font-family: 'Dancing Script', cursive;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(214, 51, 132, 0.3);
            opacity: 0;
            animation: fadeIn 1s ease-out 1.5s forwards;
        }
        
        .close-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(214, 51, 132, 0.4);
        }
        
        /* Corações flutuantes */
        .floating-hearts {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        .heart {
            position: absolute;
            color: rgba(214, 51, 132, 0.3);
            font-size: 1.5rem;
            animation: floatUp 6s linear infinite;
        }
        
        /* Modal para foto ampliada */
        .photo-modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
        }
        
        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            max-width: 90%;
            max-height: 90%;
        }
        
        .modal-photo {
            width: 100%;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 20px 60px rgba(214, 51, 132, 0.3);
        }
        
        .close-modal {
            position: absolute;
            top: -40px;
            right: 0;
            color: white;
            font-size: 2rem;
            cursor: pointer;
            background: rgba(214, 51, 132, 0.8);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        
        .close-modal:hover {
            background: rgba(214, 51, 132, 1);
            transform: scale(1.1);
        }
        
        /* Animações */
        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
        
        @keyframes letterAppear {
            from {
                opacity: 0;
                transform: translateY(20px) scale(0.95);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }
        
        @keyframes floatUp {
            from {
                bottom: -50px;
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            to {
                bottom: 100vh;
                opacity: 0;
                transform: translateX(100px);
            }
        }
        
        /* Responsividade */
        @media (max-width: 768px) {
            .title {
                font-size: 2.2rem;
                margin-bottom: 1.5rem;
            }
            
            .envelope {
                width: 250px;
                height: 167px;
            }
            
            .envelope-flap {
                border-left-width: 125px;
                border-right-width: 125px;
                border-top-width: 83px;
            }
            
            .letter {
                padding: 2rem 1.5rem;
                margin: 1rem;
            }
            
            .letter-content {
                font-size: 1.2rem;
            }
            
            .special-photo {
                max-width: 250px;
                height: 250px;
            }
        }
        
        @media (max-width: 480px) {
            .title {
                font-size: 1.8rem;
            }
            
            .envelope {
                width: 200px;
                height: 133px;
            }
            
            .envelope-flap {
                border-left-width: 100px;
                border-right-width: 100px;
                border-top-width: 67px;
            }
            
            .envelope-text {
                font-size: 1rem;
            }
            
            .letter-content {
                font-size: 1.1rem;
            }
            
            .special-photo {
                max-width: 200px;
                height: 200px;
            }
            
            .music-controls {
                flex-direction: column;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <!-- Container de corações flutuantes -->
    <div class="floating-hearts" id="hearts"></div>
    
    <!-- Modal para foto ampliada -->
    <div class="photo-modal" id="photoModal">
        <div class="modal-content">
            <span class="close-modal" onclick="closePhotoModal()">&times;</span>
            <img class="modal-photo" id="modalPhoto" src="" alt="Nossa foto especial">
        </div>
    </div>
    
    <!-- Container principal -->
    <div class="container">
        <!-- Título -->
        <h1 class="title">Para Alguém Especial</h1>
        
        <!-- Envelope/Carta fechada -->
        <div class="envelope" id="envelope" onclick="openLetter()">
            <div class="envelope-back">
                <div class="envelope-flap" id="flap"></div>
                <div class="stamp">💌</div>
                <div class="envelope-text">
                    Clique para abrir<br>
                    <small>com carinho...</small>
                </div>
            </div>
        </div>
        
        <!-- Carta aberta -->
        <div class="letter" id="letter">
            <div class="letter-content">
                Oi… só queria dizer que mesmo depois de tudo, ainda penso em você com carinho. 
                <br><br>
                Obrigado por cada momento que a gente viveu. Cada risada, cada conversa, cada silêncio compartilhado... 
                tudo isso fez parte de algo muito especial.
                <br><br>
                Espero que seu mundo continue cheio de luz, mesmo se eu não fizer mais parte dele. 
                Você merece toda a felicidade do mundo. 💖
            </div>
            
            <!-- Foto especial -->
            <div class="special-photo-container">
                <div class="special-photo-title">Nossa memória mais preciosa</div>
                <img class="special-photo" 
                     src="https://d41chssnpqdne.cloudfront.net/user_upload_by_module/chat_bot/files/107389843/P4j8AK8Hboibnn0B.jpeg?Expires=1749861555&Signature=bSsBpRF-3tpnQKjRD1pSXO3B4BsfUkkDUo9IdAWTZhHKxKundaZFctLxKEDQ9Xruvjvl~utakRS-YqOmLom-58dCzimCCLrrP8yV7hJ6~kdhT3LK1StfP0w8DOiMUntlxzt6mxS6VkCiApu-9kim2l9x6C0pTHY3NnNlF4~ilRXFOGiAhPR46JUS5jgHRtMSs~X2vCNTF2rcAk4KEFmir6cUI2YkB~obJvng1ZyaPouEbCKHDz2a~ccXfsFB5Oxbp29c~oxKFvBZh7xKr6Obrf7qoRNKco9VoI9b4MP985jx7VgLC8fSt-FgM9Yo6nJi5ZDuVGJmugCyu8fwOpypuA__&Key-Pair-Id=K3USGZIKWMDCSX" 
                     alt="Nossas mãos entrelaçadas" 
                     onclick="openPhotoModal(this.src)">
            </div>
            
            <!-- Player de música -->
            <div class="music-player">
                <div class="music-title">🎵 Nossa música: "Castles" - Lil Peep</div>
                <div class="music-controls">
                    <button class="play-button" id="playBtn" onclick="toggleMusic()">▶</button>
                    <div class="volume-control">
                        <span style="color: #d63384;">🔊</span>
                        <input type="range" class="volume-slider" id="volumeSlider" min="0" max="100" value="50" onchange="changeVolume()">
                    </div>
                </div>
                <small style="color: #6c757d; font-style: italic;">
                    *Clique no play para ouvir nossa música especial
                </small>
            </div>
            
            <div class="signature">
                Com amor e saudade... ✨
            </div>
            
            <!-- Botão para fechar -->
            <button class="close-button" onclick="closeLetter()">
                Fechar com carinho 💌
            </button>
        </div>
    </div>

    <!-- Audio element (hidden) -->
    <audio id="backgroundMusic" loop>
        <!-- Você precisará adicionar o arquivo de áudio aqui -->
        <source src="castles-lil-peep.mp3" type="audio/mpeg">
        <!-- Fallback para diferentes formatos -->
        <source src="castles-lil-peep.ogg" type="audio/ogg">
    </audio>

    <script>
        // Variáveis globais
        let isPlaying = false;
        let heartInterval;
        const audio = document.getElementById('backgroundMusic');
        const playBtn = document.getElementById('playBtn');
        const volumeSlider = document.getElementById('volumeSlider');
        
        // Configurar volume inicial
        audio.volume = 0.5;
        
        // Função para abrir a carta
        function openLetter() {
            const envelope = document.getElementById('envelope');
            const flap = document.getElementById('flap');
            const letter = document.getElementById('letter');
            
            // Anima o flap do envelope abrindo
            flap.style.transform = 'rotateX(180deg)';
            
            // Esconde o envelope e mostra a carta após um delay
            setTimeout(() => {
                envelope.style.display = 'none';
                letter.style.display = 'block';
                
                // Inicia a animação dos corações
                startHeartAnimation();
            }, 800);
        }
        
        // Função para fechar a carta
        function closeLetter() {
            const envelope = document.getElementById('envelope');
            const flap = document.getElementById('flap');
            const letter = document.getElementById('letter');
            
            // Para a música se estiver tocando
            if (isPlaying) {
                toggleMusic();
            }
            
            // Esconde a carta com animação
            letter.style.animation = 'fadeIn 0.5s ease-out reverse';
            
            setTimeout(() => {
                letter.style.display = 'none';
                envelope.style.display = 'block';
                
                // Reset do flap
                flap.style.transform = 'rotateX(0deg)';
                
                // Para a animação dos corações
                stopHeartAnimation();
            }, 500);
        }
        
        // Função para controlar a música
        function toggleMusic() {
            if (isPlaying) {
                audio.pause();
                playBtn.innerHTML = '▶';
                playBtn.style.background = 'linear-gradient(135deg, #d63384, #f8d7da)';
            } else {
                // Tentar reproduzir a música
                audio.play().then(() => {
                    playBtn.innerHTML = '⏸';
                    playBtn.style.background = 'linear-gradient(135deg, #28a745, #20c997)';
                }).catch((error) => {
                    // Se não conseguir reproduzir (arquivo não encontrado), mostrar mensagem
                    alert('🎵 Para ouvir "Castles" do Lil Peep, adicione o arquivo de áudio como "castles-lil-peep.mp3" na mesma pasta do HTML!');
                    console.log('Erro ao reproduzir áudio:', error);
                });
            }
            isPlaying = !isPlaying;
        }
        
        // Função para controlar volume
        function changeVolume() {
            audio.volume = volumeSlider.value / 100;
        }
        
        // Função para abrir modal da foto
        function openPhotoModal(imageSrc) {
            const modal = document.getElementById('photoModal');
            const modalPhoto = document.getElementById('modalPhoto');
            modalPhoto.src = imageSrc;
            modal.style.display = 'block';
            
            // Adiciona efeito de zoom na foto
            setTimeout(() => {
                modalPhoto.style.transform = 'scale(1.02)';
            }, 100);
        }
        
        // Função para fechar modal da foto
        function closePhotoModal() {
            const modal = document.getElementById('photoModal');
            modal.style.display = 'none';
        }
        
        // Fechar modal clicando fora da imagem
        window.onclick = function(event) {
            const modal = document.getElementById('photoModal');
            if (event.target === modal) {
                closePhotoModal();
            }
        }
        
        // Função para iniciar animação dos corações
        function startHeartAnimation() {
            const heartsContainer = document.getElementById('hearts');
            
            heartInterval = setInterval(() => {
                createHeart(heartsContainer);
            }, 800);
        }
        
        // Função para parar animação dos corações
        function stopHeartAnimation() {
            if (heartInterval) {
                clearInterval(heartInterval);
            }
            
            // Remove todos os corações existentes
            const heartsContainer = document.getElementById('hearts');
            heartsContainer.innerHTML = '';
        }
        
        // Função para criar um coração flutuante
        function createHeart(container) {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.innerHTML = Math.random() > 0.5 ? '💖' : '💕';
            
            // Posição aleatória horizontal
            heart.style.left = Math.random() * 100 + '%';
            
            // Duração aleatória da animação
            heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
            
            // Delay aleatório
            heart.style.animationDelay = Math.random() * 2 + 's';
            
            container.appendChild(heart);
            
            // Remove o coração após a animação
            setTimeout(() => {
                if (heart.parentNode) {
                    heart.parentNode.removeChild(heart);
                }
            }, 8000);
        }
        
        // Efeito de partículas sutis no fundo
        function createBackgroundParticles() {
            const body = document.body;
            
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const particle = document.createElement('div');
                    particle.style.position = 'fixed';
                    particle.style.width = '4px';
                    particle.style.height = '4px';
                    particle.style.background = 'rgba(214, 51, 132, 0.1)';
                    particle.style.borderRadius = '50%';
                    particle.style.left = Math.random() * 100 + '%';
                    particle.style.top = '100%';
                    particle.style.pointerEvents = 'none';
                    particle.style.animation = 'floatUp 15s linear infinite';
                    
                    body.appendChild(particle);
                    
                    setTimeout(() => {
                        if (particle.parentNode) {
                            particle.parentNode.removeChild(particle);
                        }
                    }, 15000);
                }, i * 3000);
            }
        }
        
        // Eventos de teclado para controlar música
        document.addEventListener('keydown', function(event) {
            if (event.code === 'Space' && document.getElementById('letter').style.display === 'block') {
                event.preventDefault();
                toggleMusic();
            }
        });
        
        // Inicia as partículas de fundo
        createBackgroundParticles();
        setInterval(createBackgroundParticles, 15000);
    </script>
</body>
</html>
