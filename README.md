# wedding
mahadev bless you 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Avneesh ❤️ Sakshi Wedding</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    text-align: center;
    color: white;
    background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)),
                url('https://images.unsplash.com/photo-1519671482749-fd09be7ccebf') no-repeat center/cover;
}

/* Header */
.header {
    padding: 20px;
}

h1 {
    font-size: 28px;
}

h2 {
    font-size: 22px;
}

/* Couple Image */
.couple img {
    width: 90%;
    max-width: 300px;
    border-radius: 15px;
    border: 3px solid gold;
}

/* Fireworks */
canvas {
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
}

/* Form */
.form-box {
    background: rgba(0,0,0,0.7);
    padding: 15px;
    margin: 20px;
    border-radius: 10px;
}

input, select {
    width: 90%;
    padding: 8px;
    margin: 5px;
    border-radius: 5px;
    border: none;
}

/* Gallery */
.gallery img {
    width: 80px;
    border-radius: 10px;
    margin: 5px;
}

</style>
</head>

<body>

<canvas id="fireworks"></canvas>

<div class="header">
    <h1>🎉 Avneesh ❤️ Sakshi 🎉</h1>
    <h2>Wedding Date: 23 February 2026</h2>
    <p>
        Wishing them a beautiful life ahead 💖<br>
        हम अवनीश और साक्षी को उनके नए जीवन के लिए ढेर सारी शुभकामनाएं देते हैं 💐
    </p>
</div>

<div class="couple">
    <!-- Replace with your uploaded image -->
    <img src="groom-bride.jpg" alt="Bride & Groom">
</div>

<!-- Guest Form -->
<div class="form-box">
    <h3>Mark Your Presence / अपनी उपस्थिति दर्ज करें</h3>
    
    <input type="text" id="name" placeholder="Your Name / आपका नाम">
    
    <select id="side">
        <option value="">Select Side</option>
        <option>Bride Side</option>
        <option>Groom Side</option>
    </select>

    <input type="text" id="relation" placeholder="Relation (Friend, Cousin...)">
    
    <input type="file" id="photo">

    <button onclick="upload()">Submit</button>
</div>

<!-- Gallery -->
<div class="gallery" id="gallery"></div>

<!-- Firework Sound -->
<audio id="sound" src="https://www.soundjay.com/explosion/explosion-01.mp3"></audio>

<script>
// Fireworks Animation
const canvas = document.getElementById('fireworks');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];

function createFirework(x, y) {
    for (let i = 0; i < 50; i++) {
        particles.push({
            x: x,
            y: y,
            speedX: (Math.random() - 0.5) * 5,
            speedY: (Math.random() - 0.5) * 5,
            life: 100
        });
    }
    document.getElementById("sound").play();
}

function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    particles.forEach((p, i) => {
        p.x += p.speedX;
        p.y += p.speedY;
        p.life--;
        
        ctx.fillStyle = "gold";
        ctx.fillRect(p.x, p.y, 2, 2);

        if (p.life <= 0) particles.splice(i, 1);
    });

    requestAnimationFrame(animate);
}

setInterval(() => {
    createFirework(Math.random() * canvas.width, Math.random() * canvas.height / 2);
}, 1000);

animate();

// Upload function
function upload() {
    const name = document.getElementById("name").value;
    const relation = document.getElementById("relation").value;
    const side = document.getElementById("side").value;
    const file = document.getElementById("photo").files[0];

    if (!name || !relation || !side || !file) {
        alert("Please fill all details");
        return;
    }

    const reader = new FileReader();
    reader.onload = function(e) {
        const div = document.createElement("div");
        div.innerHTML = `
            <img src="${e.target.result}">
            <p>${name} (${relation})<br>${side}</p>
        `;
        document.getElementById("gallery").appendChild(div);
    };

    reader.readAsDataURL(file);
}
</script>

</body>
</html>
