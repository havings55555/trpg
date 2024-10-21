
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TRPG용 서버</title>
  <!-- Bootstrap CSS -->
  <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    /* Stat bars */
    .stat {
      margin-bottom: 20px;
    }
    .progress {
      height: 30px; /* Set bar height to 30px */
      width: 200px;
    }
    /* Table styles */
    table {
      margin-top: 10px;
      border-collapse: collapse;
      width: 200px;
      font-size: 12px;
    }
    table, th, td {
      border: 1px solid black;
    }
    th, td {
      padding: 8px;
      text-align: center;
      width: 200px;
      height: 30px; /* Set table cell height to 30px */
    }
    .btn-group {
      margin-right: 10px;
    }
    /* Hide additional stats by default */
    #additionalStats {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Navbar using Bootstrap -->
  <nav class="navbar navbar-dark bg-dark">
    <a class="navbar-brand" href="#">TRPG용 서버</a>
  </nav>

  <!-- Random Number Buttons -->
  <div class="mt-4">
    <button id="roll1to6Btn" class="btn btn-primary mr-3">1 ~ 6 숫자 출력</button>
    <span id="roll1to9Result">결과: </span>
    <br><br>
    <button id="roll1to9Btn" class="btn btn-primary mr-3">1 ~ 10 숫자 출력</button>
    <span id="roll1to9Result">결과: </span>
    <br><br>
    <button id="roll1to20Btn" class="btn btn-primary mr-3">1 ~ 20 숫자 출력</button>
    <span id="roll1to20Result">결과: </span>
    <br><br>
    <button id="roll1to100Btn" class="btn btn-primary mr-3">1 ~ 100 숫자 출력</button>
    <span id="roll1to100Result">결과: </span>
  </div>

  <!-- 메인 스탯 -->
  <h3 class="mt-5">메인 스탯</h3>
  <div class="mt-4">
    <!-- 힘 -->
    <div class="stat">
      <label>힘:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', -1)">-1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', 1)">+1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="strValue">0</span>
      <div class="progress mt-2">
        <div id="strBar" class="progress-bar" style="width: 0%; background-color: red;"></div>
      </div>
      <!-- Difficulty Table -->
      <table id="strTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="strEasy">0</td>
            <td id="strNormal">0</td>
            <td id="strHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- 체력 -->
    <div class="stat">
      <label>체력:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', -1)">-1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', 1)">+1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="hpValue">0</span>
      <div class="progress mt-2">
        <div id="hpBar" class="progress-bar" style="width: 0%; background-color: green;"></div>
      </div>
      <table id="hpTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="hpEasy">0</td>
            <td id="hpNormal">0</td>
            <td id="hpHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- 속도 -->
    <div class="stat">
      <label>속도:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', -1)">-1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', 1)">+1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="speedValue">0</span>
      <div class="progress mt-2">
        <div id="speedBar" class="progress-bar" style="width: 0%; background-color: skyblue;"></div>
      </div>
      <table id="speedTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="speedEasy">0</td>
            <td id="speedNormal">0</td>
            <td id="speedHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- 행운 -->
    <div class="stat">
      <label>행운:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', -1)">-1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', 1)">+1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="luckValue">0</span>
      <div class="progress mt-2">
        <div id="luckBar" class="progress-bar" style="width: 0%; background-color: purple;"></div>
      </div>
      <table id="luckTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="luckEasy">0</td>
            <td id="luckNormal">0</td>
            <td id="luckHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- 지능 (메인 스탯) -->
    <div class="stat">
      <label>지능:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', -1)">-1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', 1)">+1</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="intelligenceValue">0</span>
      <div class="progress mt-2">
        <div id="intelligenceBar" class="progress-bar" style="width: 0%; background-color: lightgreen;"></div>
      </div>
      <table id="intelligenceTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="intelligenceEasy">0</td>
            <td id="intelligenceNormal">0</td>
            <td id="intelligenceHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- 주력 (Max 200) -->
    <div class="stat">
      <label>주력:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', -5)">-5</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', 5)">+5</button>
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', -10)">-10</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', 10)">+10</button> <!-- 추가 -->
      </div>
      <span id="agiValue">0</span>
      <div class="progress mt-2">
        <div id="agiBar" class="progress-bar" style="width: 0%; background-color: orange;"></div>
      </div>
      <table id="agiTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="agiEasy">0</td>
            <td id="agiNormal">0</td>
            <td id="agiHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <h3 class="mt-5">추가 스탯</h3>
    <!-- 아이디어 (추가 스탯) -->
    <div class="stat">
      <label>아이디어:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('idea', -1)">-1</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('idea', 1)">+1</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('idea', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('idea', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="ideaValue">0</span>
      <div class="progress mt-2">
        <div id="ideaBar" class="progress-bar" style="width: 0%; background-color: blue;"></div>
      </div>
      <table id="ideaTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="ideaEasy">0</td>
            <td id="ideaNormal">0</td>
            <td id="ideaHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="stat">
      <label>흑섬성공확률:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', -1)">-1</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', 1)">+1</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="blacksparkValue">0</span>
      <div class="progress mt-2">
        <div id="blacksparkBar" class="progress-bar" style="width: 0%; background-color: blue;"></div>
      </div>
      <table id="blacksparkTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="blacksparkEasy">0</td>
            <td id="blacksparkNormal">0</td>
            <td id="blacksparkHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="stat">
      <label>영역:</label>
      <div class="btn-group">
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', -1)">-1</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', 1)">+1</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', -5)">-5</button> <!-- 추가 -->
        <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', 5)">+5</button> <!-- 추가 -->
      </div>
      <span id="domainValue">0</span>
      <div class="progress mt-2">
        <div id="domainBar" class="progress-bar" style="width: 0%; background-color: blue;"></div>
      </div>
      <table id="domainTable">
        <thead>
          <tr>
            <th>쉬움</th>
            <th>보통</th>
            <th>어려움</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="domainEasy">0</td>
            <td id="domainNormal">0</td>
            <td id="domainHard">0</td>
          </tr>
        </tbody>
      </table>
    </div>
  <!-- JavaScript -->
  <script>
    // 주사위 버튼 이벤트
    document.getElementById('roll1to6Btn').addEventListener('click', function() {
      const result = Math.floor(Math.random() * 6) + 1;
      document.getElementById('roll1to9Result').textContent = "결과: " + result;
    });

    document.getElementById('roll1to9Btn').addEventListener('click', function() {
      const result = Math.floor(Math.random() * 10) + 1;
      document.getElementById('roll1to9Result').textContent = "결과: " + result;
    });

    document.getElementById('roll1to20Btn').addEventListener('click', function() {
      const result = Math.floor(Math.random() * 20) + 1;
      document.getElementById('roll1to20Result').textContent = "결과: " + result;
    });

    document.getElementById('roll1to100Btn').addEventListener('click', function() {
      const result = Math.floor(Math.random() * 100) + 1;
      document.getElementById('roll1to100Result').textContent = "결과: " + result;
    });

    // Stat limits
    const maxValues = {
      str: 20,
      hp: 20,
      speed: 20,
      luck: 20,
      intelligence: 20,
      agi: 200,
      extraAgi: 100,
      idea: 20,
      blackspark: 20,
      domain: 20
    };

    function adjustStat(stat, amount) {
      const valueElement = document.getElementById(stat + 'Value');
      let currentValue = parseInt(valueElement.textContent);

      const newValue = Math.min(maxValues[stat], Math.max(0, currentValue + amount));
      valueElement.textContent = newValue;

      const progressBar = document.getElementById(stat + 'Bar');
      progressBar.style.width = (newValue / maxValues[stat]) * 100 + '%';

      // Update difficulty table
      const easyValue = Math.round(newValue * 5);
      const normalValue = Math.round(newValue * 2.5);
      const hardValue = newValue;

      document.getElementById(stat + 'Easy').textContent = easyValue;
      document.getElementById(stat + 'Normal').textContent = normalValue;
      document.getElementById(stat + 'Hard').textContent = hardValue;
    }

    
  </script>

  <!-- Bootstrap JS and dependencies -->
  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>

</body>
</html>
