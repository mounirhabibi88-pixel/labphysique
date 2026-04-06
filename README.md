<!DOCTYPE html>
<html>
<head>
  <title>Chute d'une bille dans un fluide</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.4.0/lib/p5.min.js"></script>
</head>
<body>

<h1>Chute d'une bille dans un fluide avec v = f(t)</h1>

<script>
let y = 50;          // position initiale (axe OZ)
let v = 0;           // vitesse initiale
let g = 0.5;         // gravité
let k = 0.02;        // coefficient de résistance fluide
let dt = 1;          // pas de temps
let vitesseData = []; // tableau pour stocker vitesse au cours du temps

function setup() {
  createCanvas(600, 400);
  frameRate(60);
}

function draw() {
  background(240);

  // ---- Calcul physique ----
  // Résistance fluide : F_resistance = -k*v
  let a = g - k*v;     // accélération : gravité - résistance
  v += a * dt;
  y += v * dt;

  // stocker la vitesse pour tracer
  vitesseData.push(v);

  // ---- Dessin de la bille ----
  fill(255, 0, 0);
  ellipse(width/4, y, 30, 30);

  // ---- Dessin de l'axe OZ ----
  stroke(0);
  line(width/4, 0, width/4, height);

  // ---- Tracé de la courbe v=f(t) ----
  stroke(0, 0, 255);
  noFill();
  beginShape();
  for (let i = 0; i < vitesseData.length; i++) {
    let vx = map(i, 0, vitesseData.length, width/2, width-20);
    let vy = map(vitesseData[i], 0, 10, height-20, 20); // vitesse max≈10
    vertex(vx, vy);
  }
  endShape();

  // ---- Affichage de la vitesse ----
  noStroke();
  fill(0);
  textSize(16);
  text("Vitesse : " + v.toFixed(2) + " px/frame", 20, 20);

  // ---- Recommencer si la bille sort du canvas ----
  if (y > height) {
    y = 50;
    v = 0;
    vitesseData = [];
  }
}
</script>

</body>
</html>
