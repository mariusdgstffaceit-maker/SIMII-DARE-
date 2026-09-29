# SIMII-DARE-Iată codul actualizat! Am adăugat titlul amuzant „Bună dragă Simina, cum dorești să ne facem date-ul pe sărăcie :)” și am păstrat tot fluxul interactiv (butonul care fuge, întrebările despre bancă, suc, flori/jeleuri și bârfă, plus rezumatul final):
Cum îl pui rapid online:
 * Intri pe codepen.io/pen.
 * Ștergi tot ce este în caseta HTML (stânga sus) și lipsești codul de mai jos.
 * Îți va apărea exact site-ul pregătit pentru ea!
<!DOCTYPE html>
<html lang="ro">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Date pe Sărăcie cu Simina</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
    body { background: #ffe4e6; display: flex; justify-content: center; align-items: center; min-height: 100vh; padding: 20px; }
    .card { background: white; padding: 30px; border-radius: 24px; box-shadow: 0 10px 25px rgba(0,0,0,0.08); width: 100%; max-width: 420px; text-align: center; position: relative; overflow: hidden; min-height: 420px; display: flex; flex-direction: column; justify-content: center; align-items: center; }
    h2 { color: #881337; font-size: 20px; margin-bottom: 12px; font-weight: 800; line-height: 1.3; }
    p { color: #9f1239; font-size: 15px; margin-bottom: 20px; }
    .emoji { font-size: 44px; margin-bottom: 10px; }
    .btn-group { display: flex; gap: 15px; justify-content: center; width: 100%; position: relative; min-height: 50px; }
    button { padding: 12px 24px; font-size: 15px; font-weight: bold; border-radius: 50px; border: none; cursor: pointer; transition: all 0.2s ease; margin-top: 10px; }
    .btn-yes { background: #e11d48; color: white; box-shadow: 0 4px 12px rgba(225,29,72,0.3); width: 100%; }
    .btn-yes:hover { transform: scale(1.02); background: #be123c; }
    .btn-no { background: #f3f4f6; color: #4b5563; position: absolute; width: auto; }
    .step { display: none; width: 100%; flex-direction: column; align-items: center; }
    .step.active { display: flex; }
    select, input { width: 100%; padding: 12px; margin-bottom: 12px; border-radius: 12px; border: 1px solid #fecdd3; outline: none; font-size: 14px; text-align: center; }
  </style>
</head>
<body>

  <div class="card">
    <!-- Step 1: Titlul personalizat și întrebarea -->
    <div id="step1" class="step active">
      <div class="emoji">💖💸</div>
      <h2>Bună dragă Simina, cum dorești să ne facem date-ul pe sărăcie :)</h2>
      <p>Mai întâi, accepți invitația? 👇</p>
      <div class="btn-group">
        <button class="btn-yes" style="width: auto;" onclick="nextStep(2)">DA!</button>
        <button class="btn-no" id="noBtn" onmouseover="moveButton()" onclick="moveButton()">Nu</button>
      </div>
    </div>

    <!-- Step 2: Reacția -->
    <div id="step2" class="step">
      <div class="emoji">🎉😭</div>
      <h2>WAIT YOU ACTUALLY SAID YES??</h2>
      <p>I was so ready for you to say no... 😂</p>
      <button class="btn-yes" onclick="nextStep(3)">Hai să stabilim detaliile ➔</button>
    </div>

    <!-- Step 3: Ora și Banca -->
    <div id="step3" class="step">
      <div class="emoji">⏰📍</div>
      <h2>Alegem locul și ora!</h2>
      <p>La cât dorești să ne vedem?</p>
      <input type="time" id="timeInput" value="18:00">
      <p>Pe ce bancă dorești să stăm?</p>
      <input type="text" id="benchInput" placeholder="Ex: Banca noastră din parc">
      <button class="btn-yes" onclick="nextStep(4)">Continuă ➔</button>
    </div>

    <!-- Step 4: Sucul și Flori/Jeleuri -->
    <div id="step4" class="step">
      <div class="emoji">🧃💐</div>
      <h2>Ce-ți iau bun?</h2>
      <p>Ce suc dorești să-ți iau?</p>
      <input type="text" id="drinkInput" placeholder="Ex: Cappy, Cola, Monster, Prigat...">
      <p>Flori sau jeleuri?</p>
      <select id="giftSelect">
        <option>Flori 🌸</option>
        <option>Jeleuri 🍬</option>
        <option>Și flori și jeleuri! 🌹🍬</option>
      </select>
      <p>Ce fel de jeleuri îți plac?</p>
      <input type="text" id="jellyInput" placeholder="Ex: Acrișoare, Haribo, râme...">
      <button class="btn-yes" onclick="nextStep(5)">Mai departe ➔</button>
    </div>

    <!-- Step 5: Bârfa și Subiectul -->
    <div id="step5" class="step">
      <div class="emoji">🗣️🤫</div>
      <h2>Agenda de bârfit!</h2>
      <p>Ce bârfă să vorbim?</p>
      <input type="text" id="gossipInput" placeholder="Despre cine / ce bârfești...">
      <p>Ce alt subiect să abordăm?</p>
      <input type="text" id="topicInput" placeholder="Topic interesant...">
      <button class="btn-yes" onclick="nextStep(6)">Gata! Vezi planul ➔</button>
    </div>

    <!-- Step 6: Rezumat -->
    <div id="step6" class="step">
      <div class="emoji">✨❤️</div>
      <h2>Date-ul pe sărăcie e stabilit!</h2>
      <p style="font-size: 14px; text-align: left; background: #fff1f2; padding: 12px; border-radius: 12px; width: 100%;">
        ⏰ <b>Ora:</b> <span id="resTime"></span><br>
        📍 <b>Bancă:</b> <span id="resBench"></span><br>
        🧃 <b>Suc:</b> <span id="resDrink"></span><br>
        🎁 <b>Cadou:</b> <span id="resGift"></span> (<span id="resJelly"></span>)<br>
        🤫 <b>Bârfă:</b> <span id="resGossip"></span><br>
        🗣️ <b>Subiect:</b> <span id="resTopic"></span>
      </p>
      <button class="btn-yes" style="margin-top: 15px;" onclick="alert('Abia aștept, Simina!')">De abia aștept! ❤️</button>
    </div>
  </div>

  <script>
    function moveButton() {
      const btn = document.getElementById('noBtn');
      const x = Math.random() * (200 - 100) - 100;
      const y = Math.random() * (150 - 80) - 80;
      btn.style.transform = `translate(${x}px, ${y}px)`;
    }

    function nextStep(stepNumber) {
      if(stepNumber === 6) {
        document.getElementById('resTime').innerText = document.getElementById('timeInput').value || 'Nestable';
        document.getElementById('resBench').innerText = document.getElementById('benchInput').value || 'Alegem pe loc';
        document.getElementById('resDrink').innerText = document.getElementById('drinkInput').value || 'Ceva bun';
        document.getElementById('resGift').innerText = document.getElementById('giftSelect').value;
        document.getElementById('resJelly').innerText = document.getElementById('jellyInput').value || 'Toate';
        document.getElementById('resGossip').innerText = document.getElementById('gossipInput').value || 'Top secret';
        document.getElementById('resTopic').innerText = document.getElementById('topicInput').value || 'Tot ce vrem';
      }

      document.querySelectorAll('.step').forEach(step => step.classList.remove('active'));
      document.getElementById('step' + stepNumber).classList.add('active');
    }
  </script>
</body>
</html>

