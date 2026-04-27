 <!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Sheyla Llivisaca</title>

<style>
body {
  margin: 0;
  overflow: hidden;
  font-family: Arial;
  text-align: center;
  transition: 0.5s;
  background: #87ceeb;
}

/* Suelo */
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

/* 🐱 GATO */
.gato {
  position: absolute;
  bottom: 120px;
  left: 0px;
  transition: left 0.4s linear;
}

/* Cuerpo */
.cuerpo {
  width: 120px;
  height: 40px;
  background: orange;
  border-radius: 20px;
  position: relative;
}

/* Cabeza */
.cabeza {
  width: 40px;
  height: 40px;
  background: #ffb74d;
  position: absolute;
  top: -15px;
  left: 80px;
  border-radius: 50%;
}

/* Orejas */
.oreja {
  width: 0;
  height: 0;
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
  border-bottom: 15px solid orange;
  position: absolute;
  top: -25px;
}

.o1 { left: 85px; }
.o2 { left: 105px; }

/* Ojos */
.ojo {
  width: 6px;
  height: 6px;
  background: black;
  border-radius: 50%;
  position: absolute;
  top: 0px;
}

.oj1 { left: 95px; }
.oj2 { left: 110px; }

/* Patas */
.pata {
  width: 15px;
  height: 15px;
  background: #e65100;
  position: absolute;
  bottom: -10px;
  border-radius: 5px;
}

.p1 { left: 15px; }
.p2 { left: 50px; }
.p3 { left: 85px; }

/* Animación */
@keyframes caminar {
  0% { transform: translateY(0); }
  50% { transform: translateY(-4px); }
  100% { transform: translateY(0); }
}

.caminando {
  animation: caminar 0.3s linear infinite;
}

/* 💨 Humo */
.humo {
  position: absolute;
  left: -20px;
  bottom: 10px;
  width: 10px;
  height: 10px;
  background: rgba(255,255,255,0.5);
  border-radius: 50%;
  opacity: 0;
}

@keyframes humoAnim {
  0% {
    transform: translateY(0) scale(1);
    opacity: 0.6;
  }
  100% {
    transform: translateY(-30px) scale(2);
    opacity: 0;
  }
}

.humo.activo {
  animation: humoAnim 1s infinite;
}

/* 🚦 SEÑALES */
.senal {
  position: absolute;
  bottom: 120px;
  width: 15px;
  height: 80px;
  background: #444;
  border-radius: 5px;
}

.senal::before {
  content: "";
  position: absolute;
  top: -25px;
  left: -7px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: 3px solid white;
}

/* Inicio (verde) */
.inicio {
  left: 20px;
}

.inicio::before {
  background: green;
  box-shadow: 0 0 10px green;
}

/* Fin (rojo) */
.final {
  right: 20px;
}

.final::before {
  background: red;
  box-shadow: 0 0 10px red;
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

<h1>Sheyla Llivisaca</h1>

<div id="distancia">Distancia: 0 cm</div>
<div id="estado">Estado: Detenido</div>

<div class="calle"></div>
<div class="linea"></div>

<!-- Señales -->
<div class="senal inicio"></div>
<div class="senal final"></div>

<!-- GATO -->
<div class="gato" id="gato">
  <div class="cuerpo"></div>
  <div class="cabeza"></div>

  <div class="oreja o1"></div>
  <div class="oreja o2"></div>

  <div class="ojo oj1"></div>
  <div class="ojo oj2"></div>

  <div class="pata p1"></div>
  <div class="pata p2"></div>
  <div class="pata p3"></div>

  <div class="humo" id="humo"></div>
</div>

<script>
let gato = document.getElementById("gato");
let distanciaTexto = document.getElementById("distancia");
let estadoTexto = document.getElementById("estado");
let humo = document.getElementById("humo");

setInterval(() => {
  let distancia = Math.floor(Math.random() * 100);

  distanciaTexto.innerHTML = "Distancia: " + distancia + " cm";

  if (distancia > 30) {
    gato.style.left = (distancia * 5) + "px";
    estadoTexto.innerHTML = "Estado: Caminando 🐱";

    gato.classList.add("caminando");
    humo.classList.add("activo");
  } else {
    estadoTexto.innerHTML = "Estado: Detenido";

    gato.classList.remove("caminando");
    humo.classList.remove("activo");
  }

}, 1000);
</script>

</body>
</html>
