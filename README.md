<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Simulador de Obra Inteligente</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #0f172a;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    background: #1e293b;
    padding: 30px;
    border-radius: 12px;
    width: 350px;
    box-shadow: 0 0 20px rgba(0,0,0,0.5);
}

h1 {
    font-size: 20px;
    margin-bottom: 20px;
}

label {
    display: block;
    margin-top: 10px;
}

input, select {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    border-radius: 6px;
    border: none;
}

button {
    margin-top: 20px;
    width: 100%;
    padding: 10px;
    background: #22c55e;
    border: none;
    color: black;
    font-weight: bold;
    border-radius: 8px;
    cursor: pointer;
}

.result {
    margin-top: 20px;
    background: #020617;
    padding: 15px;
    border-radius: 8px;
}

.hidden {
    display: none;
}
</style>

</head>

<body>

<div class="container">
    <h1>Calculá tu obra en 1 minuto</h1>

    <label>Metros cuadrados</label>
    <input type="number" id="m2" placeholder="Ej: 20">

    <label>Altura de pared (m)</label>
    <input type="number" id="altura" value="2.6">

    <label>Tipo de ladrillo</label>
    <select id="tipo">
        <option value="12">Hueco estándar</option>
        <option value="10">Hueco liviano</option>
        <option value="15">Portante</option>
    </select>

    <button onclick="calcular()">CALCULAR</button>

    <div id="resultado" class="result hidden"></div>
</div>

<script>

function calcular() {
    let m2 = parseFloat(document.getElementById("m2").value);
    let altura = parseFloat(document.getElementById("altura").value);
    let tipo = parseFloat(document.getElementById("tipo").value);

    if (!m2 || m2 <= 0) {
        alert("Ingresá metros cuadrados válidos");
        return;
    }

    // Cálculo
    let ladrillos = m2 * tipo;
    let desperdicio = ladrillos * 0.10;
    let totalLadrillos = Math.ceil(ladrillos + desperdicio);

    let cemento = Math.ceil(m2 * 0.3);
    let arena = (m2 * 0.02).toFixed(2);

    // Precio estimado (editable)
    let precioLadrillo = 500;
    let precioCemento = 8000;

    let costo = (totalLadrillos * precioLadrillo) + (cemento * precioCemento);

    let resultadoHTML = `
        <h3>Resultado estimado:</h3>
        <p>🧱 Ladrillos: <strong>${totalLadrillos}</strong></p>
        <p>🧪 Cemento: <strong>${cemento} bolsas</strong></p>
        <p>🏖 Arena: <strong>${arena} m³</strong></p>
        <hr>
        <p>💰 Costo estimado: <strong>$${costo.toLocaleString()}</strong></p>
        <button onclick="whatsapp(${totalLadrillos}, ${cemento}, ${arena})">Consultar por WhatsApp</button>
    `;

    let resultadoDiv = document.getElementById("resultado");
    resultadoDiv.innerHTML = resultadoHTML;
    resultadoDiv.classList.remove("hidden");
}

function whatsapp(ladrillos, cemento, arena) {
    let mensaje = `Hola, necesito materiales:\nLadrillos: ${ladrillos}\nCemento: ${cemento}\nArena: ${arena} m3`;
    let url = "https://wa.me/549XXXXXXXXXX?text=" + encodeURIComponent(mensaje);
    window.open(url, "_blank");
}

</script>

</body>
</html>
