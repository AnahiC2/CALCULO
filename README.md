<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Dominio y Rango</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.11.0/math.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.13/nerdamer.core.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.13/Calculus.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 2rem;
            background-color: #f8f8f8;
        }
        h2 {
            text-align: center;
        }
        input, button, select {
            padding: 0.5rem;
            margin: 0.4rem 0;
            width: 100%;
            max-width: 400px;
        }
        .container {
            max-width: 500px;
            margin: auto;
            background: #fff;
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .result {
            background: #e7f4e4;
            padding: 1rem;
            margin-top: 1rem;
            border-radius: 8px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Dominio y Rango</h2>
        <label for="funcion">Ingresa la función f(x):</label>
        <input type="text" id="funcion" placeholder="Ej: x^2 - 4/x">
        <button onclick="calcularDominioYRango()">Calcular</button>

        <div class="result" id="resultado"></div>
    </div>

    <script>
        function calcularDominioYRango() {
            const fx = document.getElementById("funcion").value;
            let dominio = "ℝ (todos los reales)";
            let rango = "No calculado";

            try {
                // Verificar si tiene una división por 0
                if (fx.includes("/")) {
                    const partes = fx.split("/");
                    const denominador = partes[1];
                    if (denominador) {
                        const zeros = nerdamer(`solve(${denominador}=0,x)`).evaluate().text();
                        dominio = `ℝ excepto x = ${zeros}`;
                    }
                }

                // Rango aproximado con evaluación
                const valores = [];
                for (let x = -100; x <= 100; x += 0.5) {
                    try {
                        let valor = math.evaluate(fx, {x});
                        if (isFinite(valor)) valores.push(valor);
                    } catch {}
                }

                if (valores.length > 0) {
                    const min = Math.min(...valores);
                    const max = Math.max(...valores);
                    rango = `Aproximadamente: [${min.toFixed(2)}, ${max.toFixed(2)}]`;
                }

                document.getElementById("resultado").innerHTML = `
                    <b>Función:</b> f(x) = ${fx}<br>
                    <b>Dominio:</b> ${dominio}<br>
                    <b>Rango:</b> ${rango}
                `;
            } catch (error) {
                document.getElementById("resultado").innerHTML = "⚠️ Error en la función ingresada.";
            }
        }
    </script>
</body>
</html>
