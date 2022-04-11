# drawing

<html>

    <!DOCTYPE html>

    
<head>
<title>Teste </title>
<meta author="Voltarex68 / manoel Fohrer">
</head>
<body>
    <div class="toolbar" >
        <input type="color" aria-label="Sélectionner la couleur du crayon">
        <input type="range" min="1" max="30" value="300" aria-label="Sélectionner la taille de la pointe du crayon"><span class="output">20</span>
        <input type="button" value="Réinitialiser le dessin">
        <button onclick="window.location.href = 'http://drawing.e-monsite.com/blog/';">Publier</button>
        <p>Faire un screen !!</p>
      </div>
      
      <canvas class="myCanvas">
        <p>Votre navigateur ne semble pas prendre en charge cette fonctionnalité.</p>
      </canvas>



      



    

      
      <script>

var canvas = document.querySelector('.myCanvas');
var width = canvas.width = window.innerWidth;
var height = canvas.height = window.innerHeight-85;
var ctx = canvas.getContext('2d');

ctx.fillStyle = 'rgb(255, 255, 255 )';
ctx.fillRect(0,0,width,height);

var colorPicker = document.querySelector('input[type="color"]');
var sizePicker = document.querySelector('input[type="range"]');
var output = document.querySelector('.output');
var clearBtn = document.querySelector('input[type="button"]');

// On convertit des degrés en radians
function degToRad(degrees) {
  return degrees * Math.PI / 180;
};

// On met à jour la valeur pour le sélecteur
// de taille
sizePicker.oninput = function() {
  output.textContent = sizePicker.value;
}

// On enregistre les coordonnées du pointeur de la souris
// emouse pointer coordinates, and whether the button is pressed
var curX;
var curY;
var pressed = false;

// On met à jour les coordonnées du pointeur
document.onmousemove = function(e) {
  curX = (window.Event) ? e.pageX : e.clientX + (document.documentElement.scrollLeft ? document.documentElement.scrollLeft : document.body.scrollLeft);
  curY = (window.Event) ? e.pageY : e.clientY + (document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop);
}

canvas.onmousedown = function() {
  pressed = true;
};

canvas.onmouseup = function() {
  pressed = false;
}

clearBtn.onclick = function() {
  ctx.fillStyle = 'rgb(0,0,0)';
  ctx.fillRect(0,0,width,height);
}

function draw() {
  if(pressed) {
    ctx.fillStyle = colorPicker.value;
    ctx.beginPath();
    ctx.arc(curX, curY-85, sizePicker.value, degToRad(0), degToRad(360), false);
    ctx.fill();
  }

  requestAnimationFrame(draw);
}

draw();

      </script>

</body>
</html>
