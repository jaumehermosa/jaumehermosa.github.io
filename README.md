# jaumehermosa.github.io
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Página de Criptografía</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f5f5f5;
      color: #333;
    }
    header {
      background: #222;
      color: white;
      padding: 1rem;
      position: sticky;
      top: 0;
      z-index: 1000;
    }
    nav {
      display: flex;
      justify-content: space-around;
    }
    nav a {
      color: white;
      text-decoration: none;
      padding: 0.5rem 1rem;
      transition: background 0.3s;
    }
    nav a:hover {
      background: #444;
      border-radius: 5px;
    }
    section {
      padding: 2rem;
      max-width: 800px;
      margin: auto;
    }
    #presentacion {
      background: #fff;
      border-radius: 10px;
      padding: 2rem;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    footer {
      text-align: center;
      padding: 1rem;
      background: #222;
      color: white;
      margin-top: 2rem;
    }
  </style>
</head>
<body>

  <header>
    <nav>
      <a href="#presentacion">Presentació</a>
      <a href="#cifrado-cesar">Xifratge Cèsar</a>
      <a href="#cifrado-vigenere">Xifratge Vigènere</a>
      <a href="#cifrado-enigma">Xifratge Enigma</a>
      <a href="#sim-vs-asim">Simètrica vs Asimètrica</a>
      <a href="#stream-cipher">Xifratge de fluxe</a>
      <a href="#aes-demo"> AES</a>
      <a href="#rsa-demo"> RSA</a>
      <a href="#svp-demo"> Kyber</a>
      <a href="#sis-demo"> Dilithium</a>
      <a href="#contacto">Contacto</a>
    </nav>
  </header>

  <main>
    <section id="presentacion">
      <h1>Crpiptografia Interactiva</h1>
      <p>
        <!-- Aquí puedes escribir un texto de presentación sobre ti -->
        Aquesta pàgina web té l'objectiu de poder aprendre diferents aspectes de la criptografia amb eines visuals i interactives. Mitjançant aquesta pàgina, és pot veure l'evolució de la criptografia desde la criptografia precomputacional, fins a la criptografia postquàntica.
      </p>
    </section>
<section id="cifrado-cesar">
  <h2>Xifratge Cèsar</h2>
<p id="descripcion-cesar">
  <!-- Aquí puedes escribir una breve explicación sobre el cifrado César -->
  Descripció...
</p>

 <div style="display:flex;gap:1rem;flex-wrap:wrap;align-items:flex-end;">
    <div style="flex:1;min-width:220px;display:flex;flex-direction:column;justify-content:flex-end;">
      <label for="mensaje">Missatge:</label><br>
      <input type="text" id="mensaje" placeholder="Escriu el teu missatge aquí" style="width:100%;padding:0.5rem;margin-top:0.25rem;">
    </div>

    <div style="width:160px;">
      <label for="clave">Clau (número):</label><br>
      <input type="number" id="clave" value="3" min="0" style="width:100%;padding:0.5rem;margin-top:0.25rem;">
    </div>

    <div style="min-width:220px;display:flex;gap:0.5rem;align-items:center;">
      <button id="btnCifrar" style="padding:0.5rem 0.8rem;">Xifrar</button>
      <button id="iniciarAnimacion" style="padding:0.5rem 0.8rem;">▶ Iniciar animació</button>
      <button id="detenerAnimacion" style="padding:0.5rem 0.8rem;">⏹ Aturar</button>
    </div>
  </div>
<style>
  #btnCifrar {
    margin-top: auto;   /* empuja el botón hacia abajo */
    align-self: flex-end;
  }
</style>
    <style>
  #detenerAnimacion {
    margin-top: auto;   /* empuja el botón hacia abajo */
    align-self: flex-end;
  }
</style>

  <p style="margin-top:0.8rem;"><strong>Missatge original:</strong></p>
  <div id="mensajeDisplay" class="message"></div>

  <div id="abecedarios" style="margin-top:1rem;">
    <p><strong>Abecedari normal</strong></p>
    <div id="abc-normal" class="abc"></div>

    <p style="margin-top:0.6rem;"><strong>Abecedari desplaçat</strong></p>
    <div id="abc-shifted" class="abc"></div>
  </div>

  <p style="margin-top:1rem;"><strong>Missatge xifrat (text complet):</strong> <span id="resultadoTexto"></span></p>
  <p><strong>Missatge xifrat (animat):</strong></p>
  <div id="resultadoDisplay" class="message output"></div>

  <p id="estadoAnim" style="margin-top:0.6rem;color:#555;"></p>

  <style>
    /* Estilos locales para esta sección */
    .abc {
      font-family: monospace;
      display:flex;
      gap:0.25rem;
      flex-wrap:wrap;
      user-select: none;
    }
    .abc span {
      display:inline-block;
      padding:0.25rem 0.35rem;
      min-width:1.2ch;
      text-align:center;
      border-radius:4px;
      transition: box-shadow 0.18s, transform 0.12s;
    }
    .message {
      padding:0.5rem;
      background:#fff;
      border-radius:8px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.06);
      min-height:2.4rem;
      display:flex;
      gap:0.25rem;
      align-items:center;
      flex-wrap:wrap;
      font-family: inherit;
    }
    .message .letter {
      display:inline-block;
      padding:0.18rem 0.25rem;
      min-width:1ch;
      text-align:center;
      border-radius:4px;
      transition: background 0.18s, transform 0.12s;
    }
    .nonletter { opacity:0.7; }

    /* Resaltados (distintos colores para cada paso) */
    .highlight-source { background:#fff59d; transform: translateY(-2px); box-shadow:0 4px 8px rgba(0,0,0,0.08); }
    .highlight-normal { background:#90caf9; transform: scale(1.06); }
    .highlight-shifted { background:#ffcc80; transform: scale(1.06); }
    .highlight-output { background:#a5d6a7; transform: translateY(-2px); }

    /* Salida (cada letra del resultado) */
    .output .letter { opacity:0.4; }
    .output .letter.visible { opacity:1; }

    /* Botones deshabilitados */
    button[disabled] { opacity:0.5; pointer-events:none; }
  </style>

  <script>
    (function(){
      const ABC = "ABCDEFGHIJKLMNÑOPQRSTUVWXYZ";
      const lenABC = ABC.length;

      const mensajeInput = document.getElementById("mensaje");
      const claveInput = document.getElementById("clave");
      const btnCifrar = document.getElementById("btnCifrar");
      const btnIniciar = document.getElementById("iniciarAnimacion");
      const btnDetener = document.getElementById("detenerAnimacion");
      const abcNormalDiv = document.getElementById("abc-normal");
      const abcShiftDiv = document.getElementById("abc-shifted");
      const mensajeDisplay = document.getElementById("mensajeDisplay");
      const resultadoDisplay = document.getElementById("resultadoDisplay");
      const resultadoTexto = document.getElementById("resultadoTexto");
      const estadoAnim = document.getElementById("estadoAnim");

      let cipherText = "";
      let currentMensaje = "";
      let animando = false;
      let stopRequested = false;
      const stepDelay = 600; // ms por sub-paso (puedes ajustar)

      function normalizarClave(n) {
        const k = ((Number(n) % lenABC) + lenABC) % lenABC;
        return k;
      }

      function generarAbecedarios(clave) {
        abcNormalDiv.innerHTML = "";
        abcShiftDiv.innerHTML = "";
        for (let i=0; i<lenABC; i++) {
          const sN = document.createElement("span");
          sN.textContent = ABC[i];
          abcNormalDiv.appendChild(sN);

          // shifted[i] es la letra que queda "debajo" de normal[i]
          const sS = document.createElement("span");
          sS.textContent = ABC[(i + clave) % lenABC];
          abcShiftDiv.appendChild(sS);
        }
      }

      function renderMensaje(mensaje) {
        mensajeDisplay.innerHTML = "";
        for (let i=0; i<mensaje.length; i++) {
          const ch = mensaje[i];
          const sp = document.createElement("span");
          sp.className = "letter" + (ABC.includes(ch) ? "" : " nonletter");
          sp.textContent = ch;
          sp.dataset.index = i;
          mensajeDisplay.appendChild(sp);
        }
      }

      function prepararResultadoPlaceholders(length) {
        resultadoDisplay.innerHTML = "";
        for (let i=0; i<length; i++) {
          const sp = document.createElement("span");
          sp.className = "letter";
          sp.dataset.index = i;
          sp.textContent = ""; // se llenará durante la animación
          resultadoDisplay.appendChild(sp);
        }
      }

      function cifrarCesar() {
        const mensajeRaw = mensajeInput.value || "";
        const mensaje = mensajeRaw.toUpperCase();
        const clave = normalizarClave(claveInput.value);
        currentMensaje = mensaje;

        generarAbecedarios(clave);
        renderMensaje(mensaje);
        prepararResultadoPlaceholders(mensaje.length);

        // generar texto cifrado (sin tocar elementos visibles todavía)
        let resultado = "";
        for (const ch of mensaje) {
          if (ABC.includes(ch)) {
            const pos = ABC.indexOf(ch);
            resultado += ABC[(pos + clave) % lenABC];
          } else {
            resultado += ch;
          }
        }
        cipherText = resultado;
        resultadoTexto.textContent = resultado;
        estadoAnim.textContent = "";
      }

      // util sleep
      function sleep(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
      }

      // limpia resaltados en todo
      function limpiarResaltados() {
        document.querySelectorAll(".highlight-source, .highlight-normal, .highlight-shifted, .highlight-output").forEach(el => {
          el.classList.remove("highlight-source", "highlight-normal", "highlight-shifted", "highlight-output");
        });
      }

      // función principal de animación, usa async/await para secuencias
      async function playAnimation() {
        // si ya animando, no hacer nada
        if (animando) return;
        // recalcula estado actual (asegura que se haya cifrado con la clave actual)
        cifrarCesar();

        animando = true;
        stopRequested = false;
        btnIniciar.disabled = true;
        btnCifrar.disabled = true;
        estadoAnim.textContent = "Animant...";

        const spansMensaje = Array.from(mensajeDisplay.querySelectorAll("span"));
        const spansNormal = Array.from(abcNormalDiv.querySelectorAll("span"));
        const spansShifted = Array.from(abcShiftDiv.querySelectorAll("span"));
        const spansResultado = Array.from(resultadoDisplay.querySelectorAll("span"));

        for (let i = 0; i < currentMensaje.length; i++) {
          if (stopRequested) break;
          limpiarResaltados();

          const ch = currentMensaje[i];
          // 1) resaltar letra original en el mensaje
          if (spansMensaje[i]) {
            spansMensaje[i].classList.add("highlight-source");
          }
          await sleep(stepDelay);
          if (stopRequested) break;

          if (ABC.includes(ch)) {
            // letra válida: buscar posición en ABC
            const pos = ABC.indexOf(ch);

            // 2) resaltar en abecedario normal (posición pos)
            if (spansNormal[pos]) {
              spansNormal[pos].classList.add("highlight-normal");
            }
            await sleep(stepDelay);
            if (stopRequested) break;

            // 3) resaltar en abecedario desplazado la letra que está *debajo* (misma columna -> index pos)
            if (spansShifted[pos]) {
              spansShifted[pos].classList.add("highlight-shifted");
            }
            await sleep(stepDelay);
            if (stopRequested) break;

            // 4) escribir e iluminar la letra cifrada en la salida (misma posición i)
            const outChar = cipherText[i];
            if (spansResultado[i]) {
              spansResultado[i].textContent = outChar;
              spansResultado[i].classList.add("visible", "highlight-output");
            }
            await sleep(stepDelay);
            if (spansResultado[i]) spansResultado[i].classList.remove("highlight-output");
          } else {
            // no es una letra del abecedario: mostrarla en salida y hacer un único parpadeo
            if (spansResultado[i]) {
              spansResultado[i].textContent = ch;
              spansResultado[i].classList.add("visible", "highlight-output");
            }
            await sleep(stepDelay);
            if (spansResultado[i]) spansResultado[i].classList.remove("highlight-output");
          }
        }

        limpiarResaltados();
        animando = false;
        stopRequested = false;
        btnIniciar.disabled = false;
        btnCifrar.disabled = false;
        estadoAnim.textContent = stopRequested ? "⏹ Animació aturada" : "✅ Animació completada";
      }

      // detiene la animación de forma amable
      function detener() {
        if (!animando) {
          estadoAnim.textContent = "No hi ha animació en curs.";
          return;
        }
        stopRequested = true;
        estadoAnim.textContent = "⏳ Aturant animació...";
        // la animación comprobará stopRequested en la siguiente pausa y terminará
      }

      // Eventos
      btnCifrar.addEventListener("click", cifrarCesar);
      btnIniciar.addEventListener("click", () => {
        playAnimation();
      });
      btnDetener.addEventListener("click", detener);

      // Enter en el campo mensaje lanza cifrar (comodidad)
      mensajeInput.addEventListener("keydown", (e) => {
        if (e.key === "Enter") {
          e.preventDefault();
          cifrarCesar();
        }
      });

      // inicializa con valores por defecto
      cifrarCesar();

    })();
  </script>
</section>

</p>
    </section>

<section id="cifrado-vigenere">
  <h2>Xifratge de Vigenère</h2>
  <p id="descripcion-vigenere">
    <!-- Aquí puedes escribir una breve explicación sobre el cifrado de Vigenère -->
    Descripció...
  </p>

  <div style="display:flex;gap:1rem;flex-wrap:wrap;align-items:flex-end;">
    <div style="flex:1;min-width:220px;">
      <label for="mensajeV">Missatge:</label><br>
      <input type="text" id="mensajeV" placeholder="Escriu el teu missatge aquí" style="width:100%;padding:0.5rem;margin-top:0.25rem;">
    </div>

    <div style="flex:1;min-width:220px;">
      <label for="claveV">Clau (text):</label><br>
      <input type="text" id="claveV" placeholder="Escriu la teva clau aquí" style="width:100%;padding:0.5rem;margin-top:0.25rem;">
    </div>

    <div style="min-width:220px;display:flex;gap:0.5rem;align-items:flex-end;">
      <button id="btnCifrarV" style="padding:0.5rem 0.8rem;">Xifrar</button>
      <button id="iniciarAnimacionV" style="padding:0.5rem 0.8rem;">▶ Iniciar animació</button>
      <button id="detenerAnimacionV" style="padding:0.5rem 0.8rem;">⏹ Aturar</button>
    </div>
  </div>

  <p style="margin-top:0.8rem;"><strong>Missatge original:</strong></p>
  <div id="mensajeVDisplay" class="message"></div>

  <div id="tabla-vigenere" style="overflow-x:auto;margin-top:1rem;"></div>

  <p style="margin-top:1rem;"><strong>Missatge xifrat (text complet):</strong> <span id="resultadoTextoV"></span></p>
  <p><strong>Missatge xifrat (animat):</strong></p>
  <div id="resultadoVDisplay" class="message output"></div>

  <p id="estadoAnimV" style="margin-top:0.6rem;color:#555;"></p>

  <style>
    /* estilos compartidos con la sección anterior */
    #cifrado-vigenere .message {
      padding:0.5rem;
      background:#fff;
      border-radius:8px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.06);
      min-height:2.4rem;
      display:flex;
      gap:0.25rem;
      align-items:center;
      flex-wrap:wrap;
      font-family: inherit;
    }
    #cifrado-vigenere .message .letter {
      display:inline-block;
      padding:0.18rem 0.25rem;
      min-width:1ch;
      text-align:center;
      border-radius:4px;
      transition: background 0.18s, transform 0.12s;
    }
    #cifrado-vigenere .output .letter { opacity:0.4; }
    #cifrado-vigenere .output .letter.visible { opacity:1; }
    /* tabla de vigenere */
    #tabla-vigenere table {
      border-collapse: collapse;
      font-family: monospace;
      font-size: 0.9rem;
    }
    #tabla-vigenere th, #tabla-vigenere td {
      border: 1px solid #ccc;
      padding: 0.2rem 0.4rem;
      text-align: center;
    }
    #tabla-vigenere th {
      background: #eee;
    }
    .highlight-col { background:#90caf9 !important; }
    .highlight-row { background:#ffcc80 !important; }
    .highlight-cell { background:#a5d6a7 !important; font-weight:bold; }
    .highlight-source { background:#fff59d; }
    .highlight-output { background:#a5d6a7; }
  </style>

  <script>
    (function(){
      const ABC = "ABCDEFGHIJKLMNÑOPQRSTUVWXYZ";
      const lenABC = ABC.length;

      const mensajeInput = document.getElementById("mensajeV");
      const claveInput = document.getElementById("claveV");
      const btnCifrar = document.getElementById("btnCifrarV");
      const btnIniciar = document.getElementById("iniciarAnimacionV");
      const btnDetener = document.getElementById("detenerAnimacionV");

      const mensajeDisplay = document.getElementById("mensajeVDisplay");
      const resultadoDisplay = document.getElementById("resultadoVDisplay");
      const resultadoTexto = document.getElementById("resultadoTextoV");
      const tablaDiv = document.getElementById("tabla-vigenere");
      const estadoAnim = document.getElementById("estadoAnimV");

      let cipherText = "";
      let currentMensaje = "";
      let currentClave = "";
      let animando = false;
      let stopRequested = false;
      const stepDelay = 600;

      // genera tabla vigenere
      function generarTabla() {
        let html = "<table><thead><tr><th></th>";
        for (let c of ABC) html += "<th>"+c+"</th>";
        html += "</tr></thead><tbody>";
        for (let i=0; i<lenABC; i++) {
          html += "<tr><th>"+ABC[i]+"</th>";
          for (let j=0; j<lenABC; j++) {
            html += "<td>"+ABC[(i+j)%lenABC]+"</td>";
          }
          html += "</tr>";
        }
        html += "</tbody></table>";
        tablaDiv.innerHTML = html;
      }

      function renderMensaje(mensaje) {
        mensajeDisplay.innerHTML = "";
        for (let i=0; i<mensaje.length; i++) {
          const ch = mensaje[i];
          const sp = document.createElement("span");
          sp.className = "letter";
          sp.textContent = ch;
          sp.dataset.index = i;
          mensajeDisplay.appendChild(sp);
        }
      }

      function prepararResultadoPlaceholders(length) {
        resultadoDisplay.innerHTML = "";
        for (let i=0; i<length; i++) {
          const sp = document.createElement("span");
          sp.className = "letter";
          sp.dataset.index = i;
          sp.textContent = "";
          resultadoDisplay.appendChild(sp);
        }
      }

      function cifrarVigenere() {
        const mensaje = (mensajeInput.value || "").toUpperCase();
        const clave = (claveInput.value || "").toUpperCase();
        currentMensaje = mensaje;
        currentClave = clave;

        renderMensaje(mensaje);
        prepararResultadoPlaceholders(mensaje.length);

        // expandir clave
        let claveExpandida = "";
        for (let i=0, j=0; i<mensaje.length; i++) {
          const ch = mensaje[i];
          if (ABC.includes(ch)) {
            claveExpandida += clave[j % clave.length];
            j++;
          } else {
            claveExpandida += ch;
          }
        }

        // cifrar
        let resultado = "";
        for (let i=0; i<mensaje.length; i++) {
          const m = mensaje[i];
          const k = claveExpandida[i];
          if (ABC.includes(m) && ABC.includes(k)) {
            const row = ABC.indexOf(k);
            const col = ABC.indexOf(m);
            resultado += ABC[(row+col)%lenABC];
          } else {
            resultado += m;
          }
        }
        cipherText = resultado;
        resultadoTexto.textContent = resultado;
        estadoAnim.textContent = "";
      }

      function sleep(ms){ return new Promise(r=>setTimeout(r,ms)); }
      function limpiarResaltados() {
        document.querySelectorAll(".highlight-col, .highlight-row, .highlight-cell, .highlight-source, .highlight-output")
          .forEach(el => el.classList.remove("highlight-col","highlight-row","highlight-cell","highlight-source","highlight-output"));
      }

      async function playAnimation() {
        if (animando) return;
        cifrarVigenere();
        animando = true;
        stopRequested = false;
        btnIniciar.disabled = true;
        btnCifrar.disabled = true;
        estadoAnim.textContent = "Animant...";

        const spansMensaje = Array.from(mensajeDisplay.querySelectorAll("span"));
        const spansResultado = Array.from(resultadoDisplay.querySelectorAll("span"));
        const tabla = tablaDiv.querySelector("table");

        for (let i=0; i<currentMensaje.length; i++) {
          if (stopRequested) break;
          limpiarResaltados();

          const chM = currentMensaje[i];
          const chK = (currentClave && currentClave.length>0) ? currentClave[i % currentClave.length].toUpperCase() : "A";

          if (ABC.includes(chM) && ABC.includes(chK)) {
            const row = ABC.indexOf(chK);
            const col = ABC.indexOf(chM);
            const result = ABC[(row+col)%lenABC];

            // 1) resaltar letra mensaje
            spansMensaje[i].classList.add("highlight-source");
            await sleep(stepDelay); if (stopRequested) break;

            // 2) resaltar columna mensaje
            for (let r=0; r<=lenABC; r++) {
              const cell = tabla.rows[r].cells[col+1];
              if (cell) cell.classList.add("highlight-col");
            }
            await sleep(stepDelay); if (stopRequested) break;

            // 3) resaltar fila clave
            for (let c=0; c<=lenABC; c++) {
              const cell = tabla.rows[row+1].cells[c];
              if (cell) cell.classList.add("highlight-row");
            }
            await sleep(stepDelay); if (stopRequested) break;

            // 4) resaltar intersección
            const cell = tabla.rows[row+1].cells[col+1];
            if (cell) cell.classList.add("highlight-cell");
            await sleep(stepDelay); if (stopRequested) break;

            // 5) mostrar en resultado
            spansResultado[i].textContent = result;
            spansResultado[i].classList.add("visible","highlight-output");
            await sleep(stepDelay);
            spansResultado[i].classList.remove("highlight-output");

          } else {
            // símbolo no cifrable
            spansResultado[i].textContent = chM;
            spansResultado[i].classList.add("visible");
            await sleep(stepDelay);
          }
        }

        limpiarResaltados();
        animando = false;
        stopRequested = false;
        btnIniciar.disabled = false;
        btnCifrar.disabled = false;
        estadoAnim.textContent = stopRequested ? "⏹ Animació aturada" : "✅ Animació completada";
      }

      function detener() {
        if (!animando) {
          estadoAnim.textContent = "No hi ha cap animació en curs.";
          return;
        }
        stopRequested = true;
        estadoAnim.textContent = "⏳ Aturant animació...";
      }

      btnCifrar.addEventListener("click", cifrarVigenere);
      btnIniciar.addEventListener("click", playAnimation);
      btnDetener.addEventListener("click", detener);

      generarTabla();
      cifrarVigenere();
    })();
  </script>
</section>

      <section id="cifrado-enigma">
  <h2>Xifratge amb Màquina Enigma (simplificada)</h2>
  <p id="descripcion-enigma">
    <!-- Aquí puedes poner una descripción de cómo funciona la máquina Enigma -->
    Descripció...
  </p>

  <div style="display:flex;gap:1rem;flex-wrap:wrap;align-items:flex-end;">
    <div style="flex:1;min-width:220px;">
      <label for="mensajeE">Missatge:</label><br>
      <input type="text" id="mensajeE" placeholder="Escriu el teu missatge aquí" style="width:100%;padding:0.5rem;margin-top:0.25rem;">
    </div>

    <div style="flex:1;min-width:220px;">
      <label for="claveE">Clau inicial (ex: ABC):</label><br>
      <input type="text" id="claveE" placeholder="Clau de 3 lletras" maxlength="3" style="width:100%;padding:0.5rem;margin-top:0.25rem;">
    </div>

    <div style="min-width:220px;display:flex;gap:0.5rem;align-items:flex-end;">
      <button id="btnCifrarE" style="padding:0.5rem 0.8rem;">Xifrar</button>
      <button id="iniciarAnimacionE" style="padding:0.5rem 0.8rem;">▶ Iniciar animació</button>
      <button id="detenerAnimacionE" style="padding:0.5rem 0.8rem;">⏹ Aturar</button>
    </div>
  </div>

  <p style="margin-top:0.8rem;"><strong>Missatge original:</strong></p>
  <div id="mensajeEDisplay" class="message"></div>

  <div id="enigma-diagrama" style="margin-top:1rem;">
    <div><strong>Rotors:</strong></div>
    <div id="rotoresE" style="display:flex;gap:1rem;margin:0.5rem 0;">
      <div class="rotor" id="rotor1">Rotor I: A</div>
      <div class="rotor" id="rotor2">Rotor II: A</div>
      <div class="rotor" id="rotor3">Rotor III: A</div>
    </div>
    <div><strong>Reflector:</strong> (mapeja lletras en mirall)</div>
  </div>

  <p style="margin-top:1rem;"><strong>Missatge xifrat (text complet):</strong> <span id="resultadoTextoE"></span></p>
  <p><strong>Missatge xifrat (animat):</strong></p>
  <div id="resultadoEDisplay" class="message output"></div>

  <p id="estadoAnimE" style="margin-top:0.6rem;color:#555;"></p>

  <style>
    #cifrado-enigma .message {
      padding:0.5rem;
      background:#fff;
      border-radius:8px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.06);
      min-height:2.4rem;
      display:flex;
      gap:0.25rem;
      align-items:center;
      flex-wrap:wrap;
      font-family:inherit;
    }
    #cifrado-enigma .message .letter {
      display:inline-block;
      padding:0.18rem 0.25rem;
      min-width:1ch;
      text-align:center;
      border-radius:4px;
      transition: background 0.18s, transform 0.12s;
    }
    #cifrado-enigma .output .letter { opacity:0.4; }
    #cifrado-enigma .output .letter.visible { opacity:1; }
    .rotor {
      padding:0.5rem;
      border:1px solid #ccc;
      border-radius:6px;
      background:#f9f9f9;
      width:100px;
      text-align:center;
    }
    .highlight-source { background:#fff59d; }
    .highlight-output { background:#a5d6a7; }
    .highlight-rotor { background:#90caf9; }
  </style>

  <script>
    (function(){
      const ABC = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
      const lenABC = ABC.length;

      // ejemplo de configuraciones de rotores (simplificadas)
      const ROTORS = [
        "EKMFLGDQVZNTOWYHXUSPAIBRCJ", // Rotor I
        "AJDKSIRUXBLHWTMCQGZNPYFVOE", // Rotor II
        "BDFHJLCPRTXVZNYEIWGAKMUSQO"  // Rotor III
      ];
      const REFLECTOR = "YRUHQSLDPXNGOKMIEBFZCWVJAT"; // reflector B simplificado

      let positions = [0,0,0]; // posiciones iniciales
      let currentMensaje = "";
      let cipherText = "";
      let animando = false;
      let stopRequested = false;
      const stepDelay = 700;

      const mensajeInput = document.getElementById("mensajeE");
      const claveInput = document.getElementById("claveE");
      const btnCifrar = document.getElementById("btnCifrarE");
      const btnIniciar = document.getElementById("iniciarAnimacionE");
      const btnDetener = document.getElementById("detenerAnimacionE");
      const mensajeDisplay = document.getElementById("mensajeEDisplay");
      const resultadoDisplay = document.getElementById("resultadoEDisplay");
      const resultadoTexto = document.getElementById("resultadoTextoE");
      const estadoAnim = document.getElementById("estadoAnimE");
      const rotorEls = [document.getElementById("rotor1"), document.getElementById("rotor2"), document.getElementById("rotor3")];

      function setRotorPositions(clave){
        positions = clave.split("").map(ch => ABC.indexOf(ch));
        for (let i=0; i<3; i++){
          rotorEls[i].textContent = `Rotor ${i+1}: ${ABC[positions[i]]}`;
        }
      }

      function avanzarRotores(){
        positions[2] = (positions[2]+1)%lenABC;
        if (positions[2]===0) {
          positions[1] = (positions[1]+1)%lenABC;
          if (positions[1]===0) {
            positions[0] = (positions[0]+1)%lenABC;
          }
        }
        for (let i=0; i<3; i++){
          rotorEls[i].textContent = `Rotor ${i+1}: ${ABC[positions[i]]}`;
        }
      }

      function enigmaCifrarLetra(ch){
        if (!ABC.includes(ch)) return ch;
        let c = ABC.indexOf(ch);

        // paso hacia delante
        for (let i=2; i>=0; i--){
          c = (ROTORS[i][(c+positions[i])%lenABC].charCodeAt(0)-65 - positions[i] + lenABC) % lenABC;
        }

        // reflector
        c = REFLECTOR[c].charCodeAt(0)-65;

        // paso hacia atrás
        for (let i=0; i<3; i++){
          let idx = (c+positions[i])%lenABC;
          c = (ROTORS[i].indexOf(ABC[idx]) - positions[i] + lenABC)%lenABC;
        }

        avanzarRotores();
        return ABC[c];
      }

      function renderMensaje(mensaje) {
        mensajeDisplay.innerHTML = "";
        for (let i=0; i<mensaje.length; i++) {
          const sp = document.createElement("span");
          sp.className = "letter";
          sp.textContent = mensaje[i];
          sp.dataset.index = i;
          mensajeDisplay.appendChild(sp);
        }
      }

      function prepararResultadoPlaceholders(length) {
        resultadoDisplay.innerHTML = "";
        for (let i=0; i<length; i++) {
          const sp = document.createElement("span");
          sp.className = "letter";
          sp.dataset.index = i;
          sp.textContent = "";
          resultadoDisplay.appendChild(sp);
        }
      }

      function cifrarEnigma() {
        const mensaje = (mensajeInput.value || "").toUpperCase();
        const clave = (claveInput.value || "AAA").toUpperCase();
        currentMensaje = mensaje;
        setRotorPositions(clave);
        renderMensaje(mensaje);
        prepararResultadoPlaceholders(mensaje.length);

        let resultado = "";
        for (let i=0; i<mensaje.length; i++){
          resultado += enigmaCifrarLetra(mensaje[i]);
        }
        cipherText = resultado;
        resultadoTexto.textContent = resultado;
        estadoAnim.textContent = "";
      }

      function sleep(ms){ return new Promise(r=>setTimeout(r,ms)); }

      async function playAnimation(){
        if (animando) return;
        cifrarEnigma();
        animando = true;
        stopRequested = false;
        btnIniciar.disabled = true;
        btnCifrar.disabled = true;
        estadoAnim.textContent = "Animando...";

        const spansMensaje = Array.from(mensajeDisplay.querySelectorAll("span"));
        const spansResultado = Array.from(resultadoDisplay.querySelectorAll("span"));

        setRotorPositions(claveInput.value.toUpperCase() || "AAA");

        for (let i=0; i<currentMensaje.length; i++){
          if (stopRequested) break;
          const ch = currentMensaje[i];

          if (!ABC.includes(ch)){
            spansResultado[i].textContent = ch;
            spansResultado[i].classList.add("visible");
            continue;
          }

          spansMensaje[i].classList.add("highlight-source");
          await sleep(stepDelay);
          spansMensaje[i].classList.remove("highlight-source");

          const enc = enigmaCifrarLetra(ch);

          spansResultado[i].textContent = enc;
          spansResultado[i].classList.add("visible","highlight-output");
          await sleep(stepDelay);
          spansResultado[i].classList.remove("highlight-output");
        }

        animando = false;
        stopRequested = false;
        btnIniciar.disabled = false;
        btnCifrar.disabled = false;
        estadoAnim.textContent = stopRequested ? "⏹ Animación detenida" : "✅ Animación completada";
      }

      function detener(){
        if (!animando){
          estadoAnim.textContent = "No hay animación en curso.";
          return;
        }
        stopRequested = true;
        estadoAnim.textContent = "⏳ Parando animación...";
      }

      btnCifrar.addEventListener("click", cifrarEnigma);
      btnIniciar.addEventListener("click", playAnimation);
      btnDetener.addEventListener("click", detener);

      cifrarEnigma();
    })();
  </script>
</section>

      <section id="sim-vs-asim">
  <h2>Criptografia Simètrica vs. Asimètrica</h2>
  <p>
   Descripció...
  </p>

  <!-- Simétrica -->
  <h3>Simètrica</h3>
  <div class="escena">
    <div class="actor alice">👩 Alice</div>
    <div class="actor bob">👨 Bob</div>
    <div class="actor eve">🕵️ Eve</div>
    <div class="clave alice">🔑 Clau secreta</div>
    <div class="clave bob">🔑 Clau secreta</div>
    <div class="mensaje" id="msg-s">📄</div>
  </div>
  <div class="controls">
    <button onclick="animarSimetrica()">▶ Animar</button>
  </div>

  <!-- Asimétrica -->
  <h3>Asimètrica</h3>
  <div class="escena">
    <div class="actor alice">👩 Alice</div>
    <div class="actor bob">👨 Bob</div>
    <div class="actor eve">🕵️ Eve</div>
    <div class="clave alice">🔓 Pública de Bob</div>
    <div class="clave bob">🔒 Privada de Bob</div>
    <div class="mensaje" id="msg-a">📄</div>
  </div>
  <div class="controls">
    <button onclick="animarAsimetrica()">▶ Animar</button>
  </div>

  <style>
    .escena {
      position:relative;
      border:1px solid #ccc;
      border-radius:8px;
      height:260px;
      margin:1rem 0;
      background:#fdfdfd;
      overflow:hidden;
    }
    .controls {
      text-align:center;
      margin-bottom:2rem;
    }
    .actor {
  position:absolute;
  font-size:1.2rem;
}
.alice { left:10px; top:20px; }
.bob { right:10px; top:20px; }
.eve { left:50%; bottom:20px; transform:translateX(-50%); }
    .clave {
      position:absolute;
      font-size:1rem;
      top:90px;
    }
    .clave.alice { left:40px; }
    .clave.bob { right:40px; }
    .mensaje {
      position:absolute;
      top:40px;
      left:80px;
      font-size:1.4rem;
      transition: all 1s ease;
    }
  </style>

  <script>
    function animarSimetrica(){
      const msg = document.getElementById("msg-s");
      msg.textContent = "📄";
      msg.style.left = "80px"; msg.style.top = "40px"; msg.style.transform="";

      // 2. baja hacia clave de Alice
      setTimeout(()=>{ msg.style.top="80px"; msg.style.left="100px"; },500);

      // 3. poner candado
      setTimeout(()=>{ msg.textContent="📄🔒"; },1500);

      // 4. va al centro
      setTimeout(()=>{ msg.style.left="50%"; msg.style.transform="translateX(-50%)"; },2200);

      // 5. Eve intercepta (pero no descifra)
      setTimeout(()=>{
        const escena = msg.parentElement;
        const intercepto = document.createElement("div");
        intercepto.textContent = "📄🔒";
        intercepto.style.position="absolute";
        intercepto.style.top="140px";
        intercepto.style.left="50%";
        intercepto.style.transform="translateX(-50%)";
        escena.appendChild(intercepto);
        setTimeout(()=>escena.removeChild(intercepto),2000);
      },2500);

      // 6. va hacia clave de Bob
      setTimeout(()=>{ msg.style.left="calc(100% - 100px)"; msg.style.transform=""; },3000);

      // 7. quitar candado
      setTimeout(()=>{ msg.textContent="📄"; },4000);

      // 8. sube a Bob
      setTimeout(()=>{ msg.style.top="40px"; msg.style.left="calc(100% - 120px)"; },4800);
    }

    function animarAsimetrica(){
      const msg = document.getElementById("msg-a");
      msg.textContent = "📄";
      msg.style.left = "80px"; msg.style.top = "40px"; msg.style.transform="";

      // 2. baja hacia clave pública de Bob
      setTimeout(()=>{ msg.style.top="80px"; msg.style.left="100px"; },500);

      // 3. se cifra con pública
      setTimeout(()=>{ msg.textContent="📄🔒"; },1500);

      // 4. va al centro
      setTimeout(()=>{ msg.style.left="50%"; msg.style.transform="translateX(-50%)"; },2200);

      // 5. Eve intercepta
      setTimeout(()=>{
        const escena = msg.parentElement;
        const intercepto = document.createElement("div");
        intercepto.textContent = "📄🔒";
        intercepto.style.position="absolute";
        intercepto.style.top="140px";
        intercepto.style.left="50%";
        intercepto.style.transform="translateX(-50%)";
        escena.appendChild(intercepto);
        setTimeout(()=>escena.removeChild(intercepto),2000);
      },2500);

      // 6. va hacia clave privada de Bob
      setTimeout(()=>{ msg.style.left="calc(100% - 100px)"; msg.style.transform=""; },3000);

      // 7. descifra con privada
      setTimeout(()=>{ msg.textContent="📄"; },4000);

      // 8. sube a Bob
      setTimeout(()=>{ msg.style.top="40px"; msg.style.left="calc(100% - 120px)"; },4800);
    }
  </script>
</section>

      <section id="stream-cipher">
  <h2>Xifratge de flux (XOR)</h2>
  <p>
   Descripció...
  </p>

  <div style="display:flex;gap:1rem;flex-wrap:wrap;align-items:flex-start;">
    <div style="min-width:240px;flex:1;">
      <label>Missatge (bits):</label><br>
      <input id="mensaje-flujo" type="text" value="10101" style="width:100%;padding:0.4rem;margin-top:0.25rem;">
    </div>

    <div style="min-width:200px;flex:1;">
      <label>Seed (bits):</label><br>
      <input id="seed-flujo" type="text" value="110" style="width:100%;padding:0.4rem;margin-top:0.25rem;">
    </div>

    <div style="min-width:200px;display:flex;gap:0.5rem;align-items:center;">
      <button id="btnCifrarFlujo">Xifrar</button>
      <button id="btnStartFlujo">▶ Iniciar animació</button>
      <button id="btnStopFlujo">⏹ Aturar</button>
      <label style="margin-left:0.5rem">Vel: <input id="velFlujo" type="number" value="800" style="width:80px;"></label>
    </div>
  </div>

  <!-- Visualización de bits -->
  <div style="margin-top:16px;">
    <div><strong>Missatge:</strong></div>
    <div id="bits-msg" class="bits-row"></div>

    <div style="margin-top:8px;"><strong>Clau (PRF expandida):</strong></div>
    <div id="bits-key" class="bits-row"></div>

    <div style="margin-top:8px;"><strong>Resultat (missatge XOR clau):</strong></div>
    <div id="bits-res" class="bits-row"></div>
  </div>

  <!-- Tabla XOR -->
  <div id="tabla-xor" style="margin-top:18px;">
    <table id="xor-table" style="border-collapse:collapse;">
      <thead>
        <tr>
          <th style="padding:6px 10px;border:1px solid #ccc;background:#f0f0f0;">XOR</th>
          <th id="xor-col-0" style="padding:6px 10px;border:1px solid #ccc;background:#f0f0f0;">0</th>
          <th id="xor-col-1" style="padding:6px 10px;border:1px solid #ccc;background:#f0f0f0;">1</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th id="xor-row-0" style="padding:6px 10px;border:1px solid #ccc;background:#f0f0f0;">0</th>
          <td id="xor-cell-00" style="padding:8px 14px;border:1px solid #ccc;">0</td>
          <td id="xor-cell-01" style="padding:8px 14px;border:1px solid #ccc;">1</td>
        </tr>
        <tr>
          <th id="xor-row-1" style="padding:6px 10px;border:1px solid #ccc;background:#f0f0f0;">1</th>
          <td id="xor-cell-10" style="padding:8px 14px;border:1px solid #ccc;">1</td>
          <td id="xor-cell-11" style="padding:8px 14px;border:1px solid #ccc;">0</td>
        </tr>
      </tbody>
    </table>
  </div>

  <div style="margin-top:14px;">
    <strong>Missatge xifrat (text):</strong> <span id="resultado-flujo-text"></span>
  </div>

  <style>
    /* Estilos para filas de bits y resaltados */
    .bits-row { margin-top:6px; padding:8px; background:#fff; border-radius:6px; display:flex; gap:6px; flex-wrap:wrap; min-height:40px; align-items:center; }
    .bit { display:inline-block; min-width:18px; text-align:center; padding:6px 8px; border-radius:4px; background:#f7f7f7; border:1px solid #e0e0e0; font-family:monospace; }
    .bit.highlight { background:#fff59d; box-shadow:0 4px 8px rgba(0,0,0,0.06); transform:translateY(-3px); }
    .bit.highlight-key { background:#90caf9; }
    .bit.highlight-res { background:#a5d6a7; }
    /* tabla */
    #xor-table td, #xor-table th { text-align:center; font-family:monospace; }
    .xor-col-highlight { background:#ffe082 !important; }
    .xor-row-highlight { background:#b3e5fc !important; }
    .xor-cell-highlight { background:#c8e6c9 !important; font-weight:bold; }
  </style>

  <script>
    (function(){
      // elementos
      const mensajeInput = document.getElementById("mensaje-flujo");
      const seedInput = document.getElementById("seed-flujo");
      const btnCifrar = document.getElementById("btnCifrarFlujo");
      const btnStart = document.getElementById("btnStartFlujo");
      const btnStop = document.getElementById("btnStopFlujo");
      const velInput = document.getElementById("velFlujo");

      const bitsMsgDiv = document.getElementById("bits-msg");
      const bitsKeyDiv = document.getElementById("bits-key");
      const bitsResDiv = document.getElementById("bits-res");
      const resultadoText = document.getElementById("resultado-flujo-text");

      // tabla elementos
      const xorCol0 = document.getElementById("xor-col-0");
      const xorCol1 = document.getElementById("xor-col-1");
      const xorRow0 = document.getElementById("xor-row-0");
      const xorRow1 = document.getElementById("xor-row-1");
      const xorCell = (r,c) => document.getElementById(`xor-cell-${r}${c}`);

      // estado de animación
      let pasos = [];
      let idxPaso = 0;
      let intervalo = null;

      // PRF sencillo (toy): extender seed repitiéndola
      function prf(seed, length) {
        if (!seed || seed.length === 0) return null;
        let out = "";
        while (out.length < length) out += seed;
        return out.slice(0, length);
      }

      // validación bits
      function validarBits(s) {
        return /^[01]*$/.test(s);
      }

      // render filas de bits como spans
      function renderBitsRow(container, bits) {
        container.innerHTML = "";
        for (let i=0;i<bits.length;i++){
          const sp = document.createElement("span");
          sp.className = "bit";
          sp.dataset.index = i;
          sp.textContent = bits[i];
          container.appendChild(sp);
        }
      }

      // calcular XOR string-wise (bits como chars '0'/'1')
      function xorStrings(a,b) {
        let r = "";
        for (let i=0;i<a.length;i++){
          r += ((a[i] ^ b[i]) ? "1" : "0");
        }
        return r;
      }

      // limpiar resaltados
      function limpiarResaltados() {
        document.querySelectorAll(".bit").forEach(el=>el.className = "bit");
        [xorCol0,xorCol1,xorRow0,xorRow1].forEach(h => h.classList.remove("xor-col-highlight","xor-row-highlight"));
        ["xor-cell-00","xor-cell-01","xor-cell-10","xor-cell-11"].forEach(id=>{
          const el = document.getElementById(id);
          if (el) el.classList.remove("xor-cell-highlight");
        });
      }

      // destacar columna (col = '0'|'1')
      function highlightColumn(col) {
        if (col === "0") {
          xorCol0.classList.add("xor-col-highlight");
          // destacar celdas de la columna 0
          xorCell(0,0).classList.add("xor-cell-highlight");
          xorCell(1,0).classList.add("xor-cell-highlight");
        } else {
          xorCol1.classList.add("xor-col-highlight");
          xorCell(0,1).classList.add("xor-cell-highlight");
          xorCell(1,1).classList.add("xor-cell-highlight");
        }
      }

      // destacar fila (row = '0'|'1')
      function highlightRow(row) {
        if (row === "0") {
          xorRow0.classList.add("xor-row-highlight");
          xorCell(0,0).classList.add("xor-cell-highlight");
          xorCell(0,1).classList.add("xor-cell-highlight");
        } else {
          xorRow1.classList.add("xor-row-highlight");
          xorCell(1,0).classList.add("xor-cell-highlight");
          xorCell(1,1).classList.add("xor-cell-highlight");
        }
      }

      function limpiarColRowHighlights() {
        [xorCol0,xorCol1,xorRow0,xorRow1].forEach(h => h.classList.remove("xor-col-highlight","xor-row-highlight"));
        ["xor-cell-00","xor-cell-01","xor-cell-10","xor-cell-11"].forEach(id=>{
          const el = document.getElementById(id);
          if (el) el.classList.remove("xor-cell-highlight");
        });
      }

      // destacar celda específica (r, c = '0'|'1')
      function highlightCell(r,c) {
        const cell = xorCell(r,c);
        if (cell) cell.classList.add("xor-cell-highlight");
      }

      // resaltar bit en una fila (message/key/result)
      function highlightBitRow(container, idx, klass) {
        const spans = container.querySelectorAll(".bit");
        if (idx >= 0 && idx < spans.length) {
          spans[idx].classList.add("highlight");
          if (klass) spans[idx].classList.add(klass);
        }
      }

      // preparar pasos de animación
      function prepararPasos(mensaje, clave, resultado) {
        pasos = [];
        for (let i=0;i<mensaje.length;i++){
          const m = mensaje[i];
          const k = clave[i];
          pasos.push({tipo:"msg", idx:i});                  // 1
          pasos.push({tipo:"tabla-msg", bit:m});            // 2 (columna)
          pasos.push({tipo:"key", idx:i});                  // 3
          pasos.push({tipo:"tabla-key", bit:k});            // 4 (fila)
          pasos.push({tipo:"tabla-res", m:m, k:k});         // 5 (celda [k][m])
          pasos.push({tipo:"res", idx:i});                  // 6 (resultado bit)
        }
        idxPaso = 0;
      }

      // ejecutar un paso
      function ejecutarPaso() {
        const mensaje = mensajeInput.value.trim();
        const seed = seedInput.value.trim();
        const clave = prf(seed, mensaje.length);
        const resultado = xorStrings(mensaje, clave || "");

        if (!pasos || idxPaso >= pasos.length) {
          detenerAnimacion();
          return;
        }
       // limpiarResaltados();
        const paso = pasos[idxPaso];

        if (paso.tipo === "msg") {
            limpiarResaltados();
            highlightBitRow(bitsMsgDiv, paso.idx, "highlight");
        } else if (paso.tipo === "tabla-msg") {
            highlightColumn(paso.bit);
        } else if (paso.tipo === "key") {
          highlightBitRow(bitsKeyDiv, paso.idx, "highlight-key");
        } else if (paso.tipo === "tabla-key") {
          highlightRow(paso.bit);
        } else if (paso.tipo === "tabla-res") {
          // celda: fila = clave bit (k) ; columna = mensaje bit (m)
          limpiarColRowHighlights();
            highlightCell(paso.k, paso.m);
        } else if (paso.tipo === "res") {
            highlightBitRow(bitsResDiv, paso.idx, "highlight-res");
        }

        idxPaso++;
      }

      // iniciar/detener animación
      function iniciarAnimacion() {
        // validar
        const mensaje = mensajeInput.value.trim();
        const seed = seedInput.value.trim();
        if (!mensaje.length) { alert("Escriu un missatge binari (0/1)."); return; }
        if (!validarBits(mensaje)) { alert("El missatge només pot contenir 0 y 1."); return; }
        if (!validarBits(seed)) { alert("La seed només pot contenir 0 y 1."); return; }
        const clave = prf(seed, mensaje.length);
        if (!clave) { alert("La seed ha de tenir al menys 1 bit."); return; }

        // render
        renderBitsRow(bitsMsgDiv, mensaje);
        renderBitsRow(bitsKeyDiv, clave);
        const resultado = xorStrings(mensaje, clave);
        renderBitsRow(bitsResDiv, resultado);
        resultadoText.textContent = resultado;

        // preparar pasos y lanzar
        prepararPasos(mensaje, clave, resultado);

        // velocidad
        const vel = Math.max(100, Number(velInput.value) || 800);

        detenerAnimacion(); // limpiar intervalos previos
        intervalo = setInterval(ejecutarPaso, vel);
      }

      function detenerAnimacion() {
        if (intervalo) { clearInterval(intervalo); intervalo = null; }
        limpiarResaltados();
      }

      // cifrar sin animar (prepara las filas)
      function cifrarAhora() {
        const mensaje = mensajeInput.value.trim();
        const seed = seedInput.value.trim();
        if (!validarBits(mensaje)) { alert("El mensaje sólo puede contener 0 y 1."); return; }
        if (!validarBits(seed)) { alert("La seed sólo puede contener 0 y 1."); return; }
        const clave = prf(seed, mensaje.length);
        if (!clave) { alert("La seed debe tener al menos 1 bit."); return; }
        const resultado = xorStrings(mensaje, clave);
        renderBitsRow(bitsMsgDiv, mensaje);
        renderBitsRow(bitsKeyDiv, clave);
        renderBitsRow(bitsResDiv, resultado);
        resultadoText.textContent = resultado;
        // preparar pasos por si el usuario quiere animar a continuación
        prepararPasos(mensaje, clave, resultado);
      }

      // eventos
      btnCifrar.addEventListener("click", cifrarAhora);
      btnStart.addEventListener("click", iniciarAnimacion);
      btnStop.addEventListener("click", detenerAnimacion);

      // inicializa con valores por defecto
      cifrarAhora();

    })();
  </script>
</section>

    <section class="section" id="aes-demo">
  <h2>AES — 1 ronda (4×4 bytes)</h2>
  <p>
   Descripció...
  </p>

  <div style="display:flex;gap:1.5rem;align-items:flex-start;flex-wrap:wrap;">
    <!-- tabla 4x4 -->
    <div style="min-width:360px;">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;">
        <button id="genState">Generar estat aleatori</button>
        <button id="genKey">Generar clau s1</button>
        <button id="runRound">▶ Executar 1 ronda</button>
        <button id="stopAnim">⏹ Aturar</button>
        <span style="margin-left:8px;font-weight:600;">Vel:</span>
        <input id="velAES" type="number" value="600" style="width:80px;">
      </div>
  <div style="display:flex;gap:1.5rem;align-items:flex-start;flex-wrap:wrap;">
    <!-- tabla 4x4 -->
    <div style="min-width:360px;">
      <table id="aes-table">
        <thead>
          <tr>
            <th colspan="4">Estat 4×4 (bytes)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="byte" data-r="0" data-c="0"></td>
            <td class="byte" data-r="0" data-c="1"></td>
            <td class="byte" data-r="0" data-c="2"></td>
            <td class="byte" data-r="0" data-c="3"></td>
          </tr>
          <tr>
            <td class="byte" data-r="1" data-c="0"></td>
            <td class="byte" data-r="1" data-c="1"></td>
            <td class="byte" data-r="1" data-c="2"></td>
            <td class="byte" data-r="1" data-c="3"></td>
          </tr>
          <tr>
            <td class="byte" data-r="2" data-c="0"></td>
            <td class="byte" data-r="2" data-c="1"></td>
            <td class="byte" data-r="2" data-c="2"></td>
            <td class="byte" data-r="2" data-c="3"></td>
          </tr>
          <tr>
            <td class="byte" data-r="3" data-c="0"></td>
            <td class="byte" data-r="3" data-c="1"></td>
            <td class="byte" data-r="3" data-c="2"></td>
            <td class="byte" data-r="3" data-c="3"></td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- caja S-box -->
    <div style="min-width:220px;">
      <div style="border:1px solid #ddd;padding:10px;border-radius:8px;background:#fafafa;">
        <div style="font-weight:700;margin-bottom:6px;">S-box</div>
        <div style="display:flex;flex-direction:column;gap:6px;align-items:center;">
          <div>Entrada</div>
          <div id="sbox-in" class="sbox-cell">-</div>
          <div>Sortida</div>
          <div id="sbox-out" class="sbox-cell">-</div>
        </div>
      </div>
    </div>
  </div>
  <div style="margin-top:12px;border:1px solid #eee;padding:8px;border-radius:8px;background:#fff;">
            <div style="font-weight:700;">Clau s1 (16 bytes)</div>
            <div id="key-box" style="margin-top:6px;display:flex;gap:6px;flex-wrap:wrap;"></div>
          </div>

          <div style="margin-top:12px;font-weight:700;">Etapa:</div>
          <div id="stage" style="margin-top:6px;padding:8px;border-radius:6px;background:#fff;border:1px solid #eee;">—</div>
        </div>
      </div>
            <div id="mix-box" style="margin-top:14px;display:flex;gap:12px;align-items:flex-start;">
        <div style="min-width:120px;">
          <div style="font-weight:700;margin-bottom:6px;">MixColumns (matriu)</div>
          <div id="mix-matrix" style="display:grid;grid-template-columns:repeat(2,1fr);gap:6px;padding:8px;border-radius:6px;border:1px solid #eee;background:#fff;">
            <div style="grid-column:1/span:2;text-align:center;font-family:monospace;">[ 2 3 1 1 ]</div>
            <div style="grid-column:1/span:2;text-align:center;color:#666;font-size:0.9rem;">(aplicada per columna)</div>
          </div>
        </div>
      </div>
    </div>
  </div>
        
  <style>
    /* --- forzamos comportamiento de tabla --- */
    #aes-table { 
      border-collapse: collapse; 
      background:#fff; 
      table-layout: fixed; 
      width: 360px;
      display: table; /* forzamos */
    }
    #aes-table thead { display: table-header-group; }
    #aes-table tbody { display: table-row-group; }
    #aes-table tr { display: table-row; }
    #aes-table th, 
    #aes-table td { 
      display: table-cell; 
      border:1px solid #ccc; 
      text-align:center; 
      width:80px; 
      height:56px; 
    }
    #aes-table td.byte {
      font-family: monospace; 
      background:#fafafa; 
      cursor:pointer;
    }

    .sbox-cell {
      min-width:80px;
      min-height:28px;
      border-radius:6px;
      border:1px dashed #ccc;
      display:flex;
      align-items:center;
      justify-content:center;
      background:#fff;
      font-family: monospace;
      font-weight: 700;
    }
  </style>

  <script>
    (function(){
      // --- S-box AES estándar (256 bytes) ---
      const SBOX = [
      0x63,0x7c,0x77,0x7b,0xf2,0x6b,0x6f,0xc5,0x30,0x01,0x67,0x2b,0xfe,0xd7,0xab,0x76,
      0xca,0x82,0xc9,0x7d,0xfa,0x59,0x47,0xf0,0xad,0xd4,0xa2,0xaf,0x9c,0xa4,0x72,0xc0,
      0xb7,0xfd,0x93,0x26,0x36,0x3f,0xf7,0xcc,0x34,0xa5,0xe5,0xf1,0x71,0xd8,0x31,0x15,
      0x04,0xc7,0x23,0xc3,0x18,0x96,0x05,0x9a,0x07,0x12,0x80,0xe2,0xeb,0x27,0xb2,0x75,
      0x09,0x83,0x2c,0x1a,0x1b,0x6e,0x5a,0xa0,0x52,0x3b,0xd6,0xb3,0x29,0xe3,0x2f,0x84,
      0x53,0xd1,0x00,0xed,0x20,0xfc,0xb1,0x5b,0x6a,0xcb,0xbe,0x39,0x4a,0x4c,0x58,0xcf,
      0xd0,0xef,0xaa,0xfb,0x43,0x4d,0x33,0x85,0x45,0xf9,0x02,0x7f,0x50,0x3c,0x9f,0xa8,
      0x51,0xa3,0x40,0x8f,0x92,0x9d,0x38,0xf5,0xbc,0xb6,0xda,0x21,0x10,0xff,0xf3,0xd2,
      0xcd,0x0c,0x13,0xec,0x5f,0x97,0x44,0x17,0xc4,0xa7,0x7e,0x3d,0x64,0x5d,0x19,0x73,
      0x60,0x81,0x4f,0xdc,0x22,0x2a,0x90,0x88,0x46,0xee,0xb8,0x14,0xde,0x5e,0x0b,0xdb,
      0xe0,0x32,0x3a,0x0a,0x49,0x06,0x24,0x5c,0xc2,0xd3,0xac,0x62,0x91,0x95,0xe4,0x79,
      0xe7,0xc8,0x37,0x6d,0x8d,0xd5,0x4e,0xa9,0x6c,0x56,0xf4,0xea,0x65,0x7a,0xae,0x08,
      0xba,0x78,0x25,0x2e,0x1c,0xa6,0xb4,0xc6,0xe8,0xdd,0x74,0x1f,0x4b,0xbd,0x8b,0x8a,
      0x70,0x3e,0xb5,0x66,0x48,0x03,0xf6,0x0e,0x61,0x35,0x57,0xb9,0x86,0xc1,0x1d,0x9e,
      0xe1,0xf8,0x98,0x11,0x69,0xd9,0x8e,0x94,0x9b,0x1e,0x87,0xe9,0xce,0x55,0x28,0xdf,
      0x8c,0xa1,0x89,0x0d,0xbf,0xe6,0x42,0x68,0x41,0x99,0x2d,0x0f,0xb0,0x54,0xbb,0x16
      ];

      // --- estado y clave (arrays 4x4, row-major in our state[][] representation) ---
      let state = [
        [0,0,0,0],
        [0,0,0,0],
        [0,0,0,0],
        [0,0,0,0]
      ];
      let key = new Array(16).fill(0);

      // DOM refs
      const tbody = document.querySelector("#aes-table tbody");
      const sboxIn = document.getElementById("sbox-in");
      const sboxOut = document.getElementById("sbox-out");
      const keyBox = document.getElementById("key-box");
      const stageEl = document.getElementById("stage");
      const velInput = document.getElementById("velAES");

      // control flags
      let STOP = false;
      let STEP_MS = 600;

      // ---- GF(2^8) helpers ----
      function xtime(a){ return ((a<<1) & 0xFF) ^ ((a & 0x80) ? 0x1b : 0x00); }
      function mul(a,b){
        if (b === 1) return a & 0xFF;
        if (b === 2) return xtime(a) & 0xFF;
        if (b === 3) return (xtime(a) ^ a) & 0xFF;
        // generic fallback (unused)
        let res = 0;
        for (let i=0;i<8;i++){
          if ((b & 1) === 1) res ^= a;
          let hi = (a & 0x80);
          a = (a << 1) & 0xFF;
          if (hi) a ^= 0x1b;
          b >>= 1;
        }
        return res & 0xFF;
      }

      // RENDER: fill static 4x4 cells
     function renderTable(){
  for (let r=0;r<4;r++){
    for (let c=0;c<4;c++){
      const td = tbody.querySelector(`td[data-r='${r}'][data-c='${c}']`);
      if (!td) continue;
      // NO reseteamos colores ni clases aquí
      td.innerHTML = `
        <div style="font-weight:700">${state[r][c]}</div>
        <div class="small">0x${state[r][c].toString(16).padStart(2,"0").toUpperCase()}</div>
      `;
    }
  }
}

      // click handler via delegation
      tbody.addEventListener("click", function(e){
        const td = e.target.closest("td.byte");
        if (!td) return;
        const r = Number(td.dataset.r);
        const c = Number(td.dataset.c);
        const v = prompt("Introduce un valor 0–255 (decimal):", String(state[r][c]));
        if (v === null) return;
        const n = Number(v);
        if (!Number.isInteger(n) || n<0 || n>255){ alert("Valor inválido"); return; }
        state[r][c] = n & 0xFF;
        renderTable();
      });

      // crear estado aleatorio
      function genRandomState(){
        for (let r=0;r<4;r++) for (let c=0;c<4;c++) state[r][c] = Math.floor(Math.random()*256);
        renderTable();
      }

      function genRandomKey(){
        for (let i=0;i<16;i++) key[i] = Math.floor(Math.random()*256);
        renderKey();
      }

      function renderKey(){
        keyBox.innerHTML = "";
        for (let i=0;i<16;i++){
          const sp = document.createElement("span");
          sp.textContent = key[i].toString(10);
          keyBox.appendChild(sp);
        }
      }

      function sleep(ms){ return new Promise(r => setTimeout(r, ms)); }
      function setStage(txt){ stageEl.textContent = txt; }
      function highlightCell(r,c,cls){
        const td = tbody.querySelector(`td[data-r='${r}'][data-c='${c}']`);
        if (!td) return;
        td.classList.add(cls);
      }
     function clearCellHighlights(){
  tbody.querySelectorAll("td").forEach(td => {
    td.classList.remove("cell-highlight","cell-sub","cell-mix");
    td.style.background = "#fafafa"; // ahora sí, aquí limpiamos todo
  });
}

      // AddRoundKey visual
      async function addRoundKeyVisual(prefix="AddRoundKey"){
        setStage(prefix);
        const ms = STEP_MS = Number(velInput.value) || STEP_MS;
        // highlight all first
        tbody.querySelectorAll("td").forEach(td => td.classList.add("cell-highlight"));
        await sleep(ms);
        for (let c=0;c<4;c++){
          for (let r=0;r<4;r++){
            if (STOP) return;
            const keyByte = key[c*4 + r]; // column-major mapping
            state[r][c] ^= keyByte;
            renderTable();
            highlightCell(r,c,"cell-highlight");
            await sleep(Math.round(ms/3));
            if (STOP) return;
          }
        }
        await sleep(Math.round(ms/2));
        tbody.querySelectorAll("td").forEach(td => td.classList.remove("cell-highlight"));
      }

      // SubBytes visual
      async function subBytesVisual(){
        setStage("SubBytes");
        const ms = STEP_MS = Number(velInput.value) || STEP_MS;
        for (let c=0;c<4;c++){
          for (let r=0;r<4;r++){
            if (STOP) return;
            clearCellHighlights();
            highlightCell(r,c,"cell-sub");
            sboxIn.textContent = state[r][c];
            await sleep(Math.round(ms/3));
            const out = SBOX[state[r][c] & 0xFF];
            sboxOut.textContent = out;
            await sleep(Math.round(ms/3));
            state[r][c] = out;
            renderTable();
            await sleep(Math.round(ms/3));
          }
        }
        clearCellHighlights();
        sboxIn.textContent = "-";
        sboxOut.textContent = "-";
      }

      // ShiftRows visual
      async function shiftRowsVisual(){
        setStage("ShiftRows");
        const ms = STEP_MS = Number(velInput.value) || STEP_MS;
        const colors = ["#ffd54f","#90caf9","#a5d6a7","#ffab91"];
        // color original columns
        for (let c=0;c<4;c++){
          tbody.querySelectorAll(`td[data-c='${c}']`).forEach(td=>{
            td.style.background = colors[c];
          });
        }
        await sleep(ms);

        // perform shift rows (row r shift left r)
        const copy = JSON.parse(JSON.stringify(state));
        for (let r=0;r<4;r++){
          const row = copy[r].slice();
          const shifted = row.slice(r).concat(row.slice(0,r));
          for (let c=0;c<4;c++){
            if (STOP) return;
            state[r][c] = shifted[c];
            renderTable();
            await sleep(Math.round(ms/4));
          }
        }
        // recolor to show mixing: origin column for each cell
        await sleep(Math.round(ms/3));
        for (let c=0;c<4;c++){
          for (let r=0;r<4;r++){
            const originCol = (c + r) % 4; // where the cell came from
            const td = tbody.querySelector(`td[data-r='${r}'][data-c='${c}']`);
            if (td) td.style.background = colors[originCol];
          }
        }
        await sleep(ms);
        // reset background
        tbody.querySelectorAll("td").forEach(td => td.style.background = "#fafafa");
      }

      // MixColumns visual
      async function mixColumnsVisual(){
        setStage("MixColumns");
        const ms = STEP_MS = Number(velInput.value) || STEP_MS;
        for (let c=0;c<4;c++){
          if (STOP) return;
          // mark column
          tbody.querySelectorAll("td").forEach(td => td.classList.remove("cell-mix"));
          tbody.querySelectorAll(`td[data-c='${c}']`).forEach(td => td.classList.add("cell-mix"));
          await sleep(Math.round(ms/3));
          // compute mix
          const a = [ state[0][c], state[1][c], state[2][c], state[3][c] ];
          const b0 = (mul(a[0],2) ^ mul(a[1],3) ^ mul(a[2],1) ^ mul(a[3],1)) & 0xFF;
          const b1 = (mul(a[0],1) ^ mul(a[1],2) ^ mul(a[2],3) ^ mul(a[3],1)) & 0xFF;
          const b2 = (mul(a[0],1) ^ mul(a[1],1) ^ mul(a[2],2) ^ mul(a[3],3)) & 0xFF;
          const b3 = (mul(a[0],3) ^ mul(a[1],1) ^ mul(a[2],1) ^ mul(a[3],2)) & 0xFF;
          const resCol = [b0,b1,b2,b3];
          for (let r=0;r<4;r++){
            if (STOP) return;
            state[r][c] = resCol[r];
            renderTable();
            await sleep(Math.round(ms/3));
          }
          await sleep(Math.round(ms/3));
        }
        tbody.querySelectorAll("td").forEach(td => td.classList.remove("cell-mix"));
      }

      // one round flow
      async function runOneRound(){
        STOP = false;
        STEP_MS = Number(velInput.value) || STEP_MS;
        await addRoundKeyVisual("AddRoundKey (XOR) - inici");
        if (STOP) { setStage("Detenido"); return; }
        await subBytesVisual();
        if (STOP) { setStage("Detenido"); return; }
        await shiftRowsVisual();
        if (STOP) { setStage("Detenido"); return; }
        await mixColumnsVisual();
        if (STOP) { setStage("Detenido"); return; }
        await addRoundKeyVisual("AddRoundKey (XOR) - final");
        if (STOP) { setStage("Detenido"); return; }
        setStage("Ronda completada");
        renderTable();
      }

      function stopAll(){ STOP = true; }

      // events
      document.getElementById("genState").addEventListener("click", ()=>{ genRandomState(); setStage("Estat aleatori generat"); });
      document.getElementById("genKey").addEventListener("click", ()=>{ genRandomKey(); setStage("Clau s1 generada"); });
      document.getElementById("runRound").addEventListener("click", async ()=>{ 
        if (key.every(v=>v===0)) { if (!confirm("Clau s1 està vuida (tot zeros). ¿Generar clau aleatoria ara?")) { return; } genRandomKey(); }
        await runOneRound();
      });
      document.getElementById("stopAnim").addEventListener("click", ()=>{ stopAll(); setStage("Aturant..."); });

      // init
      genRandomState();
      genRandomKey();
      renderTable();
      setStage("pulsa Executar 1 ronda");
    })();
  </script>
</section>

<section class="section" id="rsa-demo">
  <h2>RSA — Factorizació y estimació de temps</h2>
  <p>
    Descripció...
  </p>

  <div style="display:flex;flex-direction:column;gap:1rem;max-width:600px;">
    <!-- Entrada manual -->
    <div style="border:1px solid #eee;padding:12px;border-radius:8px;background:#fafafa;">
      <div style="font-weight:700;margin-bottom:6px;">Número a factoritzar:</div>
      <input id="rsa-number" type="text" placeholder="Introdueix un número" style="width:100%;padding:6px;font-family:monospace;">
      <div style="margin-top:6px;">
        <button id="btnFactorizar">Factoritzar</button>
      </div>
      <div style="margin-top:6px;">
        <strong>Factors:</strong> <span id="rsa-factors">—</span>
      </div>
      <div style="margin-top:4px;">
        <strong>Estimació clàsic:</strong> <span id="rsa-time-classic">—</span>
      </div>
      <div style="margin-top:2px;">
        <strong>Estimació quàntic (Shor):</strong> <span id="rsa-time-quantum">—</span>
      </div>
    </div>

    <!-- Generación aleatoria -->
    <div style="border:1px solid #eee;padding:12px;border-radius:8px;background:#fafafa;">
      <div style="font-weight:700;margin-bottom:6px;">Generar número RSA aleatori:</div>
      <label>Quantitat de dígits:</label>
      <input id="rsa-digits" type="number" min="2" max="20" value="5" style="width:80px;padding:4px;margin-left:4px;">
      <button id="btnGenRSA" style="margin-left:8px;">Generar</button>
      <div style="margin-top:6px;">
        <strong>N:</strong> <span id="rsa-gen-number">—</span>
      </div>
      <div style="margin-top:2px;">
        <strong>Factors:</strong> <span id="rsa-gen-factors">—</span>
      </div>
      <div style="margin-top:2px;">
        <strong>Estimació clàsic:</strong> <span id="rsa-gen-time-classic">—</span>
      </div>
      <div style="margin-top:2px;">
        <strong>Estimació quàntic (Shor):</strong> <span id="rsa-gen-time-quantum">—</span>
      </div>
    </div>
  </div>

  <style>
    #rsa-demo input { font-family: monospace; }
    #rsa-demo button { padding: 6px 10px; cursor: pointer; }
  </style>

  <script>
    (function(){
      const numInput = document.getElementById("rsa-number");
      const btnFactorizar = document.getElementById("btnFactorizar");
      const factorsEl = document.getElementById("rsa-factors");
      const timeClassicEl = document.getElementById("rsa-time-classic");
      const timeQuantumEl = document.getElementById("rsa-time-quantum");

      const digitsInput = document.getElementById("rsa-digits");
      const btnGenRSA = document.getElementById("btnGenRSA");
      const genNumberEl = document.getElementById("rsa-gen-number");
      const genFactorsEl = document.getElementById("rsa-gen-factors");
      const genTimeClassicEl = document.getElementById("rsa-gen-time-classic");
      const genTimeQuantumEl = document.getElementById("rsa-gen-time-quantum");

      // Estimaciones educativas según cantidad de dígitos
      function estimateClassic(digits){
        if (digits <= 5) return "segundos";
        if (digits <= 10) return "minutos";
        if (digits <= 15) return "horas";
        if (digits <= 20) return "días";
        if (digits <= 50) return "años";
        return "milenios";
      }
      function estimateQuantum(digits){
        if (digits <= 5) return "milisegundos";
        if (digits <= 10) return "segundos";
        if (digits <= 15) return "minutos";
        if (digits <= 20) return "horas";
        return "días";
      }

      // factorizar por trial division (solo números pequeños)
      function factorize(n){
        n = BigInt(n);
        if (n <= 1n) return [n.toString()];
        if (n.toString().length > 15) return ["Error"]; // <-- nuevo límite
        for (let i=2n;i*i<=n;i++){
          if (n % i === 0n) return [i.toString(), (n/i).toString()];
        }
        return [n.toString()]; // primo
      }

      btnFactorizar.addEventListener("click", ()=>{
        const val = numInput.value.trim();
        if (!/^\d+$/.test(val)) { alert("Introduce un número válido"); return; }
        const factors = factorize(val);
        factorsEl.textContent = factors.join(" × ");
        timeClassicEl.textContent = estimateClassic(val.length);
        timeQuantumEl.textContent = estimateQuantum(val.length);
      });

      // generar primo pequeño (probabilístico simple)
      function genPrime(max){
        max = BigInt(max);
        while(true){
          let p = BigInt(Math.floor(Math.random() * Number(max-2n))) + 2n;
          // test simple de divisibilidad
          let ok = true;
          for (let i=2n;i*i<=p;i++){
            if (p % i === 0n){ ok=false; break; }
          }
          if (ok) return p;
        }
      }

      btnGenRSA.addEventListener("click", ()=>{
        const digits = Number(digitsInput.value);
        if (!(digits>1)) { alert("Número de dígitos >1"); return; }
          if(digits<=15){
        const min = 10n**BigInt(digits-1);
        const max = 10n**BigInt(digits)-1n;
        const p = genPrime(max);
        const q = genPrime(max);
        const N = p*q;
        genNumberEl.textContent = N.toString();
              }
        if (digits <= 15) {
          genFactorsEl.textContent = p.toString()+" × "+q.toString();
        } else {
          genFactorsEl.textContent = "Error";
        }
        genTimeClassicEl.textContent = estimateClassic(2*digits);
        genTimeQuantumEl.textContent = estimateQuantum(2*digits);
      });
    })();
  </script>
</section>

      <section class="section" id="svp-demo">
  <h2>Criptografia post-quàntica — Kyber i SVP</h2>
  <p>
    Descripció...
  </p>

  <div style="display:flex;flex-wrap:wrap;gap:1.5rem;align-items:flex-start;">

    <!-- Vectores y malla -->
    <div style="min-width:360px;">
      <div style="margin-bottom:6px;font-weight:700;">Vectors 2D:</div>
      <label>Vector v1 (x,y):</label>
      <input id="vec1-x" type="number" value="1" style="width:60px;"> ,
      <input id="vec1-y" type="number" value="0" style="width:60px;">
      <br>
      <label>Vector v2 (x,y):</label>
      <input id="vec2-x" type="number" value="0" style="width:60px;"> ,
      <input id="vec2-y" type="number" value="1" style="width:60px;">
      <br>
      <button id="btnDrawLattice" style="margin-top:6px;">Dibuixar retícle</button>

      <canvas id="lattice-canvas" width="360" height="360" style="border:1px solid #ccc;margin-top:12px;background:#fff;"></canvas>
      <div style="margin-top:6px;">
        <strong>Vector més curt:</strong> <span id="shortest-vector">—</span>
      </div>
    </div>

    <!-- Estimaciones dimensiones -->
    <div style="min-width:240px;">
      <div style="font-weight:700;margin-bottom:6px;">Estimacions per dimensió</div>
      <label>Dimensions (n):</label>
      <input id="svp-dim" type="number" min="2" value="2" style="width:80px;">
      <button id="btnEstimate" style="margin-left:6px;">Calcular estimacions</button>
      <div style="margin-top:6px;">
        <strong>Estimació clàsic:</strong> <span id="svp-time-classic">—</span>
      </div>
      <div style="margin-top:2px;">
        <strong>Estimació quàntic:</strong> <span id="svp-time-quantum">—</span>
      </div>
    </div>

  </div>

  <style>
    #lattice-canvas { background:#fafafa; }
  </style>

  <script>
    (function(){
      const canvas = document.getElementById("lattice-canvas");
      const ctx = canvas.getContext("2d");

      const vec1x = document.getElementById("vec1-x");
      const vec1y = document.getElementById("vec1-y");
      const vec2x = document.getElementById("vec2-x");
      const vec2y = document.getElementById("vec2-y");
      const btnDraw = document.getElementById("btnDrawLattice");
      const shortestEl = document.getElementById("shortest-vector");

      const dimInput = document.getElementById("svp-dim");
      const btnEstimate = document.getElementById("btnEstimate");
      const timeClassicEl = document.getElementById("svp-time-classic");
      const timeQuantumEl = document.getElementById("svp-time-quantum");

      // --- dibujar malla ---
      function drawLattice(){
        ctx.clearRect(0,0,canvas.width,canvas.height);

        const v1 = [Number(vec1x.value), Number(vec1y.value)];
        const v2 = [Number(vec2x.value), Number(vec2y.value)];

        // rango de coeficientes enteros para dibujar (de -5 a 5)
        const range = 5;
        const points = [];
        for (let i=-range;i<=range;i++){
          for (let j=-range;j<=range;j++){
            const x = i*v1[0] + j*v2[0];
            const y = i*v1[1] + j*v2[1];
            points.push([x,y]);
          }
        }

        // encontrar vector más corto (no nulo)
        let minLen = Infinity;
        let shortest = null;
        for (const p of points){
          if (p[0]===0 && p[1]===0) continue;
          const len = Math.hypot(p[0],p[1]);
          if (len<minLen){ minLen = len; shortest = p; }
        }

        shortestEl.textContent = `[${shortest[0]}, ${shortest[1]}]`;

        // centro canvas
        const cx = canvas.width/2;
        const cy = canvas.height/2;
        const scale = 20; // píxeles por unidad

        // dibujar puntos
        for (const p of points){
          const px = cx + p[0]*scale;
          const py = cy - p[1]*scale;
          ctx.beginPath();
          ctx.arc(px, py, 3,0,2*Math.PI);
          ctx.fillStyle = (p[0]===shortest[0] && p[1]===shortest[1]) ? "#ff5722" : "#1976d2";
          ctx.fill();
        }

        // dibujar vectores originales
        ctx.strokeStyle = "#388e3c";
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.moveTo(cx, cy);
        ctx.lineTo(cx+v1[0]*scale, cy-v1[1]*scale);
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(cx, cy);
        ctx.lineTo(cx+v2[0]*scale, cy-v2[1]*scale);
        ctx.stroke();
      }

      btnDraw.addEventListener("click", drawLattice);

      // --- estimaciones por dimensiones ---
      function estimateClassic(n){
        if (n<=10) return "segundos";
        if (n<=20) return "minutos";
        if (n<=40) return "horas";
        if (n<=60) return "días";
        return "> años";
      }
      function estimateQuantum(n){
        if (n<=10) return "milisegundos";
        if (n<=20) return "segundos";
        if (n<=40) return "minutos";
        if (n<=80) return "horas";
        if (n<=120) return "dias";
        return "> años";
      }

      btnEstimate.addEventListener("click", ()=>{
        const n = Number(dimInput.value);
        if (n<2) { alert("Número de dimensiones ≥ 2"); return; }
        timeClassicEl.textContent = estimateClassic(n);
        timeQuantumEl.textContent = estimateQuantum(n);
      });

      // init
      drawLattice();
    })();
  </script>
</section>

      <section class="section" id="sis-demo">
  <h2>Dilithium — problema SIS (3×5)</h2>
  <p>
   Descripció...
  </p>

  <div style="display:flex;gap:2rem;flex-wrap:wrap;">

    <!-- matriz y botones -->
    <div style="min-width:380px;">
      <button id="genMatrix">Generar matriu aleatoria</button>
      <label style="margin-left:8px;">Mòdul p:</label>
      <input id="mod-p" type="number" value="7" min="2" style="width:60px;">
      <br><br>
      <table id="matrix-table" style="border-collapse:collapse;">
        <tbody></tbody>
      </table>
    </div>

    <!-- vector usuario -->
    <div style="min-width:220px;">
      <div style="font-weight:700;margin-bottom:6px;">Vector x:</div>
      <div id="vector-x" style="display:flex;gap:6px;"></div>
      <button id="calcProduct" style="margin-top:6px;">Calcular A·x mod p</button>
      <div style="margin-top:8px;">
        <strong>Resultat:</strong>
        <div id="vector-res" style="margin-top:4px;display:flex;gap:6px;"></div>
      </div>
      <button id="showSIS" style="margin-top:6px;">Mostrar vector que cumpleix A·x=0 mod p</button>
      <div style="margin-top:6px;">
        <strong>Vector SIS:</strong> <span id="sis-vector">—</span>
      </div>
    </div>

  </div>

  <style>
    #matrix-table td, #matrix-table th { border:1px solid #ccc; padding:6px 10px; text-align:center; font-family:monospace; width:40px; height:32px; }
    #vector-x span, #vector-res span { display:inline-block; width:40px; height:32px; line-height:32px; text-align:center; border:1px solid #ccc; border-radius:4px; background:#fafafa; font-family:monospace; cursor:pointer; }
    #vector-x span.editing { background:#fff59d; }
  </style>

  <script>
    (function(){
      const tbody = document.querySelector("#matrix-table tbody");
      const vectorXDiv = document.getElementById("vector-x");
      const vectorResDiv = document.getElementById("vector-res");
      const btnGenMatrix = document.getElementById("genMatrix");
      const btnCalc = document.getElementById("calcProduct");
      const btnSIS = document.getElementById("showSIS");
      const sisEl = document.getElementById("sis-vector");
      const modInput = document.getElementById("mod-p");

      let rows = 3;
      let cols = 5;
      let matrix = [];
      let p = Number(modInput.value);

      function genMatrix(){
        p = Number(modInput.value);
        matrix = [];
        tbody.innerHTML = "";
        for (let r=0;r<rows;r++){
          const tr = document.createElement("tr");
          const row = [];
          for (let c=0;c<cols;c++){
            const val = Math.floor(Math.random()*p);
            row.push(val);
            const td = document.createElement("td");
            td.textContent = val;
            tr.appendChild(td);
          }
          matrix.push(row);
          tbody.appendChild(tr);
        }
        vectorXDiv.innerHTML = "";
        for (let i=0;i<cols;i++){
          const sp = document.createElement("span");
          sp.textContent = "0";
          sp.dataset.idx = i;
          vectorXDiv.appendChild(sp);
        }
        vectorResDiv.innerHTML = "";
        sisEl.textContent = "—";
      }

      vectorXDiv.addEventListener("click", e=>{
        const sp = e.target.closest("span");
        if(!sp) return;
        const val = prompt("Introduce valor entero:", sp.textContent);
        if(val===null) return;
        const n = parseInt(val);
        if(isNaN(n)){ alert("Valor inválido"); return; }
        sp.textContent = n;
      });

      btnCalc.addEventListener("click", ()=>{
        p = Number(modInput.value);
        const x = [];
        vectorXDiv.querySelectorAll("span").forEach(sp=>x.push(Number(sp.textContent)));
        const res = [];
        for (let r=0;r<rows;r++){
          let s=0;
          for (let c=0;c<cols;c++){
            s += matrix[r][c]*x[c];
          }
          res.push((s%p + p)%p);
        }
        vectorResDiv.innerHTML = "";
        res.forEach(v=>{
          const sp = document.createElement("span");
          sp.textContent = v;
          vectorResDiv.appendChild(sp);
        });
      });

      // encuentra un vector pequeño no trivial que cumpla A·x=0 mod p
      btnSIS.addEventListener("click", ()=>{
        p = Number(modInput.value);
        let found = false;
        let result = null;
        const limit = p; 
        // búsqueda bruta para vectores 5 elementos, rango -p+1..p-1
        const candidates = [];
        for(let x0=-limit+1;x0<limit;x0++){
          for(let x1=-limit+1;x1<limit;x1++){
            for(let x2=-limit+1;x2<limit;x2++){
              for(let x3=-limit+1;x3<limit;x3++){
                for(let x4=-limit+1;x4<limit;x4++){
                  if(x0===0 && x1===0 && x2===0 && x3===0 && x4===0) continue;
                  const res = [];
                  for(let r=0;r<rows;r++){
                    let s=0;
                    const xs = [x0,x1,x2,x3,x4];
                    for(let c=0;c<cols;c++) s+= matrix[r][c]*xs[c];
                    res.push((s%p + p)%p);
                  }
                  if(res.every(v=>v===0)){
                    result = [x0,x1,x2,x3,x4];
                    found=true;
                    break;
                  }
                }
                if(found) break;
              }
              if(found) break;
            }
            if(found) break;
          }
          if(found) break;
        }
        if(found){
          sisEl.textContent = `[${result.join(", ")}]`;
        } else {
          sisEl.textContent = "No hay vector no trivial";
        }
      });

      btnGenMatrix.addEventListener("click", genMatrix);
      genMatrix();
    })();
  </script>
</section>

    <section id="contacto">
      <h2>Contacte</h2>
      <p>
        <!-- Aquí puedes poner tu email, redes sociales o un formulario -->
        jaumehermosa@gmail.com
      </p>
    </section>
  </main>

  <footer>
    <p>Pàgina creada per Jaume Hermosa Domènech </p>
  </footer>

</body>
</html>
