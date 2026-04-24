<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Auto Deportivo </title>

<style>
body {
  margin: 0;
  overflow: hidden;
  font-family: Arial;
  text-align: center;
  transition: 0.5s;
  background: #87ceeb;
}

/* Calle */
.calle {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 120px;
  background: #2b2b2b;
}

.linea {
  position: absolute;
  bottom: 60px;
  width: 100%;
  height: 5px;
  background: repeating-linear-gradient(
    to right,
    white 0px,
    white 40px,
    transparent 40px,
    transparent 80px
  );
}

/* 🚗 Auto */
.auto {
  position: absolute;
  bottom: 120px;
  left: 0px;
  transition: left 0.4s linear;
}

/* Cuerpo */
.cuerpo {
  width: 120px;
  height: 40px;
  background: red;
  border-radius: 20px 20px 10px 10px;
  position: relative;
}

/* Techo */
.techo {
  width: 60px;
  height: 25px;
  background: #c62828;
  position: absolute;
  top: -20px;
  left: 30px;
  border-radius: 10px;
}

/* Ventana */
.ventana {
  width: 40px;
  height: 15px;
  background: #90caf9;
  position: absolute;
  top: 3px;
  left: 10px;
  border-radius: 5px;
}

/* Luces */
.luz {
  width: 8px;
  height: 8px;
  background: yellow;
  position: absolute;
  left: -5px;
  top: 15px;
  border-radius: 50%;
  box-shadow: 0 0 10px yellow;
}

.freno {
  width: 8px;
  height: 8px;
  background: red;
  position: absolute;
  right: -5px;
  top: 15px;
  border-radius: 50%;
  box-shadow: 0 0 10px red;
  opacity: 0;
}

/* Ruedas */
.rueda {
  width: 25px;
  height: 25px;
  background: black;
  border-radius: 50%;
  position: absolute;
  bottom: -15px;
}

.r1 { left: 15px; }
.r2 { left: 80px; }

@keyframes girar {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.girando {
  animation: girar 0.3s linear infinite;
}

/* 💨 Humo */
.humo {
  position: absolute;
  left: -20px;
  bottom: 10px;
  width: 12px;
  height: 12px;
  background: gray;
  border-radius: 50%;
  opacity: 0;
}

@keyframes humoAnim {
  0% { transform: translateY(0) scale(1); opacity: 0.6; }
  100% { transform: translateY(-40px) scale(2); opacity: 0; }
}

.humo.activo {
  animation: humoAnim 1s infinite;
}

/* Texto */
#distancia {
  margin-top: 20px;
  font-size: 22px;
}

#estado {
  font-size: 24px;
  margin-top: 10px;
}

</style>
</head>

<body>

<h1>🏎️ Auto Deportivo Inteligente</h1>
<div id="distancia">Cargando...</div>
<div id="estado"></div>

<div class="auto" id="auto">

  <div class="cuerpo">
    <div class="techo">
      <div class="ventana"></div>
    </div>
    <div class="luz"></div>
    <div class="freno" id="freno"></div>
  </div>

  <div class="rueda r1" id="r1"></div>
  <div class="rueda r2" id="r2"></div>

  <div class="humo" id="humo"></div>

</div>

<div class="calle"></div>
<div class="linea"></div>

<script>

const token = "d5d327b5-b402-4f2e-8fd3-f08d67986b2f";

function actualizar() {

  fetch("https://api.tago.io/data?variable=distancia", {
    headers: { "Device-Token": "11cfe7e5-0dcf-4345-b739-f60b7ed76f3e" }
  })
  .then(res => res.json())
  .then(data => {

    let d = data.result[0].value;

    document.getElementById("distancia").innerHTML =
      "Distancia: " + d + " cm";

    let auto = document.getElementById("auto");
    let estado = document.getElementById("estado");
    let freno = document.getElementById("freno");
    let humo = document.getElementById("humo");

    let r1 = document.getElementById("r1");
    let r2 = document.getElementById("r2");

    // 👉 MOVIMIENTO COMPLETO DE IZQUIERDA A DERECHA
    let max = window.innerWidth - 150;
    let pos = (d / 100) * max;

    if (pos < 0) pos = 0;
    if (pos > max) pos = max;

    auto.style.left = pos + "px";

    // 🌙 modo noche
    if (d < 20) {
      document.body.style.background = "#0b1a2a";
    } else {
      document.body.style.background = "#87ceeb";
    }

    // 🚨 comportamiento
    if (d < 15) {
      estado.innerHTML = "🚨 FRENANDO";
      freno.style.opacity = 1;
      humo.classList.remove("activo");
      r1.classList.remove("girando");
      r2.classList.remove("girando");
    } 
    else if (d < 30) {
      estado.innerHTML = "⚠️ Acercándose";
      freno.style.opacity = 0;
      humo.classList.add("activo");
      r1.classList.add("girando");
      r2.classList.add("girando");
    } 
    else {
      estado.innerHTML = "🟢 A TODA VELOCIDAD";
      freno.style.opacity = 0;
      humo.classList.add("activo");
      r1.classList.add("girando");
      r2.classList.add("girando");
    }

  })
  .catch(err => console.log(err));
}

setInterval(actualizar, 700);

</script>

</body>
</html>
