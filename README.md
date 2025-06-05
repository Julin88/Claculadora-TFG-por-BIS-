<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Calculadora TFG - Iniciativa de Berlín (BIS1)</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 600px;
      margin: 2rem auto;
      padding: 1rem;
      background: #f9f9f9;
      color: #333;
    }
    h1, h2 {
      color: #2c3e50;
      text-align: center;
    }
    label {
      display: block;
      margin-top: 1rem;
    }
    input, select {
      width: 100%;
      padding: 0.5rem;
      margin-top: 0.25rem;
      font-size: 1rem;
    }
    button {
      margin-top: 1.5rem;
      padding: 0.75rem;
      width: 100%;
      background-color: #2980b9;
      color: white;
      font-size: 1.1rem;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #1c5980;
    }
    .resultado {
      margin-top: 2rem;
      padding: 1rem;
      background: #dff0d8;
      border: 1px solid #d0e9c6;
      border-radius: 4px;
      font-size: 1.2rem;
      text-align: center;
    }
    .explicacion {
      margin-top: 2rem;
      background: #e8f4fc;
      border-left: 4px solid #2980b9;
      padding: 1rem;
      font-size: 0.95rem;
      line-height: 1.5;
    }
    .formula {
      font-family: "Courier New", Courier, monospace;
      background: #f0f0f0;
      padding: 0.5rem;
      margin-top: 0.5rem;
      border-radius: 4px;
      text-align: center;
    }
  </style>
</head>
<body>

  <h1>Calculadora TFG - Iniciativa de Berlín (BIS1)</h1>

  <form id="calcForm">
    <label for="creatinina">Creatinina sérica (mg/dL):</label>
    <input type="number" step="0.01" min="0.1" max="20" id="creatinina" required />

    <label for="edad">Edad (años):</label>
    <input type="number" min="70" max="120" id="edad" required />

    <label for="sexo">Sexo:</label>
    <select id="sexo" required>
      <option value="" disabled selected>Seleccione...</option>
      <option value="M">Masculino</option>
      <option value="F">Femenino</option>
    </select>

    <button type="submit">Calcular TFG</button>
  </form>

  <div class="resultado" id="resultado" style="display:none;"></div>

  <section class="explicacion">
    <h2>Sobre la Iniciativa de Berlín (BIS1)</h2>
    <p>
      La fórmula BIS1 fue desarrollada para estimar la tasa de filtrado glomerular (TFG) en adultos mayores de 70 años,
      ya que las fórmulas estándar (MDRD, CKD-EPI) tienden a sobreestimar la función renal en esta población.
      Utiliza la creatinina sérica, la edad y el sexo para proporcionar una estimación más precisa.
    </p>
    <h3>Fórmula BIS1:</h3>
    <div class="formula">
      eGFR = 3736 × (Creatinina)<sup>-0.87</sup> × (Edad)<sup>-0.95</sup> × 0.82 (si es mujer)
    </div>
  </section>

  <script>
    document.getElementById('calcForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const creatinina = parseFloat(document.getElementById('creatinina').value);
      const edad = parseInt(document.getElementById('edad').value);
      const sexo = document.getElementById('sexo').value;

      if (!creatinina || !edad || !sexo) {
        alert('Por favor, complete todos los campos correctamente.');
        return;
      }

      // Cálculo fórmula BIS1
      let eGFR = 3736 * Math.pow(creatinina, -0.87) * Math.pow(edad, -0.95);
      if (sexo === 'F') {
        eGFR *= 0.82;
      }

      eGFR = eGFR.toFixed(2);

      // Mostrar resultado
      const resultadoDiv = document.getElementById('resultado');
      resultadoDiv.style.display = 'block';
      resultadoDiv.textContent = `TFG estimada (BIS1): ${eGFR} ml/min/1.73 m²`;
    });
  </script>

</body>
</html>
