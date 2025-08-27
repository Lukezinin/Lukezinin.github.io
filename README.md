<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Mini Photoshop</title>
<style>
  body { margin: 0; font-family: sans-serif; display: flex; flex-direction: column; align-items: center; background: #333; color: white; }
  canvas { border: 2px solid #fff; margin-top: 10px; cursor: crosshair; }
  #controls { margin-top: 10px; }
  input, button { margin: 0 5px; padding: 5px; }
</style>
</head>
<body>
<h1>Mini Photoshop</h1>
<div id="controls">
  <input type="color" id="colorPicker" value="#ff0000">
  <input type="range" id="brushSize" min="1" max="50" value="5">
  <button id="eraser">Borracha</button>
  <button id="clear">Limpar</button>
  <input type="file" id="upload" accept="image/*">
  <button id="save">Salvar</button>
</div>
<canvas id="canvas" width="800" height="600"></canvas>

<script>
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
let painting = false;
let erasing = false;
let brushColor = document.getElementById('colorPicker').value;
let brushSize = document.getElementById('brushSize').value;

// Funções de desenho
function startPosition(e) { painting = true; draw(e); }
function endPosition() { painting = false; ctx.beginPath(); }
function draw(e) {
  if (!painting) return;
  ctx.lineWidth = brushSize;
  ctx.lineCap = 'round';
  ctx.strokeStyle = erasing ? '#333' : brushColor;
  
  ctx.lineTo(e.offsetX, e.offsetY);
  ctx.stroke();
  ctx.beginPath();
  ctx.moveTo(e.offsetX, e.offsetY);
}

// Eventos do canvas
canvas.addEventListener('mousedown', startPosition);
canvas.addEventListener('mouseup', endPosition);
canvas.addEventListener('mousemove', draw);

// Controle de cor e tamanho
document.getElementById('colorPicker').addEventListener('change', e => { brushColor = e.target.value; erasing = false; });
document.getElementById('brushSize').addEventListener('input', e => { brushSize = e.target.value; });

// Borracha
document.getElementById('eraser').addEventListener('click', () => { erasing = true; });

// Limpar canvas
document.getElementById('clear').addEventListener('click', () => {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
});

// Upload de imagem
document.getElementById('upload').addEventListener('change', e => {
  const file = e.target.files[0];
  const reader = new FileReader();
  reader.onload = function(event) {
    const img = new Image();
    img.onload = function() { ctx.drawImage(img, 0, 0, canvas.width, canvas.height); }
    img.src = event.target.result;
  }
  if (file) reader.readAsDataURL(file);
});

// Salvar imagem
document.getElementById('save').addEventListener('click', () => {
  const link = document.createElement('a');
  link.download = 'miniphotoshop.png';
  link.href = canvas.toDataURL();
  link.click();
});
</script>
</body>
</html>
