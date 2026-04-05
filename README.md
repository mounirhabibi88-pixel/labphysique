<!DOCTYPE html>
<html>
<head>
  <title>Chute libre avec axe OZ et vitesse</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.4.0/lib/p5.min.js"></script>
</head>
<body>

<h1>Simulation : Chute libre avec axe OZ et vitesse</h1>

<script>
let y = 0;         // position verticale (axe OZ)
let v = 0;         // vitesse verticale
let g = 0.5;       // gravité

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  // calcul de la vitesse et de la position
  v += g;
  y += v;

  // dessiner la balle
  ellipse(width/2, y, 30, 30);

  // afficher l'axe OZ
  stroke(0);
  line(width/2, 0, width/2, height);
  noStroke();

  // afficher la vitesse
  fill(0);
  textSize(16);
  text("Vitesse : " + v.toFixed(2) + " px/frame", 10, 20);

  // rebond au bas du canvas
  if (y > height) {
    y = 0;
    v = 0;
  }
}
</script>

</body>
</html>
