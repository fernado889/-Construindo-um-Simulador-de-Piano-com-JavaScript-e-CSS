# -Construindo-um-Simulador-de-Piano-com-JavaScript-e-CSS
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Simulador de Piano</title>
</head>
<body>
    <div class="piano">
        <div class="white-key" data-note="C"></div>
        <div class="black-key" data-note="C#"></div>
        <div class="white-key" data-note="D"></div>
        <div class="black-key" data-note="D#"></div>
        <div class="white-key" data-note="E"></div>
        <div class="white-key" data-note="F"></div>
        <div class="black-key" data-note="F#"></div>
        <div class="white-key" data-note="G"></div>
        <div class="black-key" data-note="G#"></div>
        <div class="white-key" data-note="A"></div>
        <div class="black-key" data-note="A#"></div>
        <div class="white-key" data-note="B"></div>
        <div class="white-key" data-note="C2"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
}

.piano {
    display: flex;
    position: relative;
}

.white-key {
    width: 60px;
    height: 200px;
    background: white;
    border: 1px solid #ccc;
    position: relative;
    z-index: 1;
}

.black-key {
    width: 40px;
    height: 120px;
    background: black;
    position: absolute;
    margin-left: -20px;
    margin-right: -20px;
    z-index: 2;
}

.black-key:nth-child(2),
.black-key:nth-child(4),
.black-key:nth-child(7),
.black-key:nth-child(9),
.black-key:nth-child(11) {
    left: 40px;
}

.black-key:nth-child(3),
.black-key:nth-child(6),
.black-key:nth-child(8),
.black-key:nth-child(10),
.black-key:nth-child(12) {
    left: 100px;
}

.white-key:active, .black-key:active {
    background: #e0e0e0;
}
const keys = document.querySelectorAll('.white-key, .black-key');

keys.forEach(key => {
    key.addEventListener('click', () => {
        playSound(key.dataset.note);
        key.classList.add('active');
        setTimeout(() => {
            key.classList.remove('active');
        }, 200);
    });
});

document.addEventListener('keydown', (event) => {
    const note = event.key.toUpperCase();
    const key = Array.from(keys).find(key => key.dataset.note === note);
    if (key) {
        playSound(note);
        key.classList.add('active');
        setTimeout(() => {
            key.classList.remove('active');
        }, 200);
    }
});

function playSound(note) {
    const audio = new Audio(`sounds/${note}.mp3`);
    audio.play();
}
