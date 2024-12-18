<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bāru kalkulātors</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f9;
      color: #333;
      text-align: center;
      margin: 20px;
    }
    h1 {
      color: #333;
      font-size: 28px;
    }
    #screen {
      width: 300px;
      height: 50px;
      margin: 20px auto;
      font-size: 24px;
      text-align: right;
      padding: 10px;
      border: 2px solid #4CAF50;
      background-color: #fff;
      border-radius: 10px;
    }
    .button {
      width: 60px;
      height: 60px;
      margin: 10px;
      font-size: 24px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 10px;
      transition: background-color 0.3s ease;
    }
    .button:hover {
      background-color: #45a049;
    }
    #keypad {
      display: inline-block;
    }
    .button:active {
      background-color: #3e8e41;
    }
    #keypad button {
      margin: 5px;


    }
  </style>
</head>
<body>
  <h1>Bāru kalkulātors</h1>
  <div id="screen">0</div>
  <div id="keypad">
    <!-- Number buttons -->
    <button class="button" onclick="pressKey('1')">1</button>
    <button class="button" onclick="pressKey('2')">2</button>
    <button class="button" onclick="pressKey('3')">3</button><br>
    <button class="button" onclick="pressKey('4')">4</button>
    <button class="button" onclick="pressKey('5')">5</button>
    <button class="button" onclick="pressKey('6')">6</button><br>
    <button class="button" onclick="pressKey('7')">7</button>
    <button class="button" onclick="pressKey('8')">8</button>
    <button class="button" onclick="pressKey('9')">9</button><br>
    <button class="button" onclick="pressKey('0')">0</button>
    <button class="button" onclick="clearScreen()">C</button>
    <button class="button" onclick="deleteLast()">⌫</button><br>
    <!-- Conversion buttons -->
    <button class="button" onclick="convert('Pa')">Pa</button>
    <button class="button" onclick="convert('kPa')">kPa</button>
    <button class="button" onclick="convert('MPa')">MPa</button>
    <button class="button" onclick="convert('GPa')">GPa</button>
  </div>
  <script>
    let input = ""; // Хранит текущее введённое значение в барах

    function pressKey(key) {
      // Добавляем нажатую цифру в ввод
      input += key;
      updateScreen(input);
    }

    function clearScreen() {
      // Полностью очищает экран
      input = "";
      updateScreen("0");
    }

    function deleteLast() {
      // Удаляет последний символ
      input = input.slice(0, -1);
      updateScreen(input === "" ? "0" : input);
    }

    function convert(unit) {
      // Конвертирует значение из баров в выбранную единицу
      if (input === "") return; // Если ничего не введено, ничего не делать

      const valueInBars = parseFloat(input); // Преобразуем ввод в число
      let result = 0;

      switch (unit) {
        case "Pa":
          result = valueInBars * 100000; // В паскали
          break;
        case "kPa":
          result = valueInBars * 100; // В килопаскали
          break;
        case "MPa":
          result = valueInBars * 0.1; // В мегапаскали
          break;
        case "GPa":
          result = valueInBars * 0.0001; // В гигапаскали
          break;
      }

      // Отображаем результат с округлением до 6 знаков после запятой
      updateScreen(`${result.toFixed(6)} ${unit}`);
    }

    function updateScreen(value) {
      // Обновляет текст на экране
      document.getElementById("screen").textContent = value;
    }
  </script>
</body>
</html>
