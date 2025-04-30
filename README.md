<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>awokawok</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f2f2f2;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .calculator {
      position: relative;
      background: #1e1e1e;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
      width: 100%;
      max-width: 400px;
      box-sizing: border-box;
    }

    .menu-button {
      position: absolute;
      top: 10px;
      left: 10px;
      background: transparent;
      border: none;
      font-size: 24px;
      color: white;
      cursor: pointer;
    }

    .title {
      text-align: center;
      font-size: 1.8em;
      color: #ff9500;
      margin: 0;
      padding-top: 30px;
      padding-bottom: 10px;
    }

    .display {
      background: #000;
      color: #0f0;
      font-size: 2.2em;
      text-align: right;
      padding: 15px;
      border-radius: 8px;
      margin-bottom: 15px;
      overflow-x: auto;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      padding: 20px;
      font-size: 1.4em;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      background: #333;
      color: white;
      transition: background 0.1s;
      touch-action: manipulation;
    }

    button:active {
      transform: scale(0.97);
      background: #444;
    }

    .operator {
      background: #ff9500;
    }

    .operator:active {
      background: #e08e00;
    }

    .equal {
      background: #34c759;
    }

    .equal:active {
      background: #2fab49;
    }

    .clear {
      background: #ff3b30;
    }

    .clear:active {
      background: #d8352b;
    }

    .history {
      display: none;
      position: absolute;
      top: 0;
      left: 0;
      background: rgba(0,0,0,0.95);
      color: #fff;
      width: 100%;
      height: 100%;
      padding: 20px;
      border-radius: 12px;
      overflow-y: auto;
      z-index: 10;
    }

    .history h3 {
      margin-top: 0;
    }

    .history ul {
      padding-left: 20px;
    }

    .history ul li {
      margin-bottom: 5px;
      font-size: 1.1em;
    }

    .close-history {
      background: #ff3b30;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 6px;
      cursor: pointer;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <button class="menu-button" onclick="toggleHistory()">☰</button>

    <h1 class="title">awokawok</h1>
    <div id="display" class="display">0</div>

    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button onclick="append('%')">%</button>
      <button onclick="append('÷')">÷</button>
      <button class="operator" onclick="append('×')">×</button>

      <button onclick="append('7')">7</button>
      <button onclick="append('8')">8</button>
      <button onclick="append('9')">9</button>
      <button class="operator" onclick="append('−')">−</button>

      <button onclick="append('4')">4</button>
      <button onclick="append('5')">5</button>
      <button onclick="append('6')">6</button>
      <button class="operator" onclick="append('+')">+</button>

      <button onclick="append('1')">1</button>
      <button onclick="append('2')">2</button>
      <button onclick="append('3')">3</button>
      <button onclick="append('.')">.</button>

      <button onclick="append('0')">0</button>
      <button onclick="deleteLast()">⌫</button>
      <button class="equal" onclick="calculate()">=</button>
    </div>

    <div class="history" id="historyPanel">
      <button class="close-history" onclick="toggleHistory()">Tutup</button>
      <h3>Riwayat</h3>
      <ul id="historyList"></ul>
    </div>
  </div>

  <script>
    const display = document.getElementById("display");
    const historyList = document.getElementById("historyList");
    const historyPanel = document.getElementById("historyPanel");

    function append(value) {
      if (display.textContent === "0") {
        display.textContent = value;
      } else {
        display.textContent += value;
      }
    }

    function clearDisplay() {
      display.textContent = "0";
    }

    function deleteLast() {
      let current = display.textContent;
      if (current.length > 1) {
        display.textContent = current.slice(0, -1);
      } else {
        display.textContent = "0";
      }
    }

    function calculate() {
      let expression = display.textContent
        .replace(/×/g, '*')
        .replace(/÷/g, '/')
        .replace(/−/g, '-')
        .replace(/%/g, '/100');

      try {
        const result = eval(expression);
        historyList.innerHTML = `<li>${display.textContent} = ${result}</li>` + historyList.innerHTML;
        display.textContent = result;
      } catch {
        display.textContent = "Error";
      }
    }

    function toggleHistory() {
      historyPanel.style.display = historyPanel.style.display === "block" ? "none" : "block";
    }
  </script>
</body>
</html>
