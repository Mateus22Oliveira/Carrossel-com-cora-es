![SJDV 25 1](https://github.com/user-attachments/assets/5f32fe82-33aa-4901-b3da-970fc2edc161)
![NATAL](https://github.com/user-attachments/assets/3ab9edb0-ce30-45a4-8ccf-f5b6bce294f8)
![M+S](https://github.com/user-attachments/assets/8d1d8d2f-6af0-4bce-96dc-18670be63072)
![IMG_9418](https://github.com/user-attachments/assets/d10adc87-f89e-4dad-aba3-2ba641bea548)
![DTN](https://github.com/user-attachments/assets/034fa2b1-06b9-4925-9a42-f1d80979530a)
![Corrida](https://github.com/user-attachments/assets/557e0da6-a840-4415-a72b-3897e07f36a1)
![ARRASTA](https://github.com/user-attachments/assets/c196ead2-58be-46b2-b35a-8b43ad151712)
![SJDV 25](https://github.com/user-attachments/assets/26d2649a-297e-4a80-8ecf-5f654ef250fb)
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carrossel Romântico</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="carrossel-container">
        <button class="prev">&#10094;</button>
        <div class="carrossel-slide"></div>
        <button class="next">&#10095;</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: linear-gradient(135deg, #ffc1cc, #ffebf0);
    font-family: 'Arial', sans-serif;
    margin: 0;
    overflow: hidden;
}

.carrossel-container {
    position: relative;
    width: 400px;
    height: 300px;
    overflow: hidden;
    border-radius: 20px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.3);
    z-index: 1;
}

.carrossel-slide {
    display: flex;
    width: 100%;
    height: 100%;
    transition: transform 0.7s ease-in-out;
}

.foto-container {
    position: relative;
    width: 100%;
    height: 100%;
}

.foto-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 20px;
}

.legenda {
    position: absolute;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    background: rgba(255, 255, 255, 0.7);
    padding: 6px 12px;
    border-radius: 15px;
    font-weight: bold;
    text-align: center;
    color: #ff0055;
}

.prev, .next {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background-color: rgba(255,255,255,0.8);
    border: none;
    font-size: 2rem;
    padding: 5px 12px;
    cursor: pointer;
    border-radius: 50%;
    transition: background 0.3s;
    z-index: 2;
}

.prev:hover, .next:hover {
    background-color: rgba(255,255,255,1);
}

.prev { left: 10px; }
.next { right: 10px; }

/* Corações flutuantes */
.coracao {
    position: absolute;
    width: 20px;
    height: 20px;
    background-color: #ff3366;
    transform: rotate(45deg);
    animation: flutuar linear infinite;
    border-radius: 3px;
}

.coracao::before,
.coracao::after {
    content: "";
    position: absolute;
    width: 20px;
    height: 20px;
    background-color: #ff3366;
    border-radius: 50%;
}

.coracao::before {
    top: -10px;
    left: 0;
}

.coracao::after {
    left: 10px;
    top: 0;
}

@keyframes flutuar {
    0% {
        transform: translateY(0) rotate(45deg);
        opacity: 1;
    }
    100% {
        transform: translateY(-600px) rotate(45deg);
        opacity: 0;
    }
}
const slide = document.querySelector('.carrossel-slide');
const prev = document.querySelector('.prev');
const next = document.querySelector('.next');
let counter = 0;

// Carregar automaticamente todas as imagens da pasta "imagens"
const imagens = [
    'imagens/foto1.jpg',
    'imagens/foto2.jpg',
    'imagens/foto3.jpg'
    // Adicione aqui mais fotos se quiser
];

// Criar elementos do carrossel
imagens.forEach((src, index) => {
    const container = document.createElement('div');
    container.classList.add('foto-container');

    const img = document.createElement('img');
    img.src = src;
    img.alt = `Foto ${index+1}`;

    const legenda = document.createElement('div');
    legenda.classList.add('legenda');
    legenda.textContent = `Foto ${index+1} 💖`;

    container.appendChild(img);
    container.appendChild(legenda);
    slide.appendChild(container);
});

// Função para atualizar a posição do carrossel
function updateSlide() {
    slide.style.transform = `translateX(${-counter * 100}%)`;
}

// Navegação com setas
next.addEventListener('click', () => {
    counter++;
    if (counter >= imagens.length) counter = 0;
    updateSlide();
});

prev.addEventListener('click', () => {
    counter--;
    if (counter < 0) counter = imagens.length - 1;
    updateSlide();
});

// Transição automática a cada 3 segundos
setInterval(() => {
    counter++;
    if (counter >= imagens.length) counter = 0;
    updateSlide();
}, 3000);

// Corações flutuantes
function criarCoracao() {
    const coracao = document.createElement('div');
    coracao.classList.add('coracao');
    coracao.style.left = Math.random() * window.innerWidth + 'px';
    coracao.style.animationDuration = (3 + Math.random() * 2) + 's';
    coracao.style.width = coracao.style.height = (10 + Math.random() * 20) + 'px';
    document.body.appendChild(coracao);
    setTimeout(() => { coracao.remove(); }, 5000);
}
setInterval(criarCoracao, 400);

