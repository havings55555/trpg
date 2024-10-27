<!DOCTYPE html>
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
  </style>
</head>
<body>

  <!-- Navbar using Bootstrap -->
  <nav class="navbar navbar-dark bg-dark">
    <a class="navbar-brand" href="#">TRPG용 서버</a>
  </nav>

  <div class="mb-4">
    <label for="playerName">이름 입력:</label>
    <input type="text" id="playerName" class="form-control" placeholder="이름을 입력하세요">
    <button class="btn btn-primary mt-2" onclick="displayPlayerName()">확인</button>
  </div>

  <!-- 플레이어 이름 표시 -->
  <h2 id="displayedPlayerName" class="mt-4"></h2>

  <!-- Random Number Buttons -->
  <div class="mt-4">
    <button id="roll1to6Btn" class="btn btn-primary mr-3">1 ~ 6 숫자 출력</button>
    <span id="roll1to6Result">결과: </span>
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

  <div class="container">
    <div class="row">
      <!-- 체력 -->
      <div class="col-md-4">
        <div class="stat">
          <label>힘:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', 5)">+5</button>
          </div>
          <span id="strValue">0</span>
          <div class="progress mt-2">
            <div id="strBar" class="progress-bar" style="width: 0%; background-color: red;"></div>
          </div>
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
      </div>

      <!-- 체력 -->
      <div class="col-md-4">
        <div class="stat">
          <label>힘:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', 5)">+5</button>
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
      </div>

      <!-- 속도 -->
      <div class="col-md-4">
        <div class="stat">
          <label>속도:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('speed', 5)">+5</button>
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
      </div>
    </div>

    <!-- 행운, 지능, 주력 -->
    <div class="row">
      <!-- 행운 -->
      <div class="col-md-4">
        <div class="stat">
          <label>행운:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('luck', 5)">+5</button>
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
      </div>

      <!-- 지능 -->
      <div class="col-md-4">
        <div class="stat">
          <label>지능:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('intelligence', 5)">+5</button>
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
      </div>

      <!-- 주력 -->
      <div class="col-md-4">
        <div class="stat">
          <label>주력:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('agi', 5)">+5</button>
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
    </div>

    <h3 class="mt-5">추가 스탯</h3>
    <div class="row">
      <!-- 흑섬성공확률 -->
      <div class="col-md-4">
        <div class="stat">
          <label>흑섬성공확률:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', 5)">+5</button>
          </div>
          <span id="blacksparkValue">0</span>
          <div class="progress mt-2">
            <div id="blacksparkBar" class="progress-bar" style="width: 0%; background-color: blue;"></div>
          </div>
          <table id="blacksparkTable">
            <thead>
              <tr>
                <th>어려움</th>
                <th>매우어려움</th>
                <th>극한</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td id="blacksparkHard">0</td>
                <td id="blacksparkVeryHard">0</td>
                <td id="blacksparkSveryHard">0</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- 재능 -->
      <div class="col-md-4">
        <div class="stat">
          <label>재능:</label>
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('domain', 5)">+5</button>
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
      </div>
      <div class="container mt-4">
        <div class="row">
          <!-- 주력 운용 능력 -->
          <div class="col-md-4">
            <div class="stat">
              <label>주력 운용 능력:</label>
              <div class="btn-group">
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('control', -1)">-1</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('control', 1)">+1</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('control', -5)">-5</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('control', 5)">+5</button>
              </div>
              <span id="controlValue">0</span>
              <div class="progress mt-2">
                <div id="controlBar" class="progress-bar" style="width: 0%; background-color: purple;"></div>
              </div>
              <table id="controlTable">
                <thead>
                  <tr>
                    <th>쉬움</th>
                    <th>보통</th>
                    <th>어려움</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td id="controlEasy">0</td>
                    <td id="controlNormal">0</td>
                    <td id="controlHard">0</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
    
          <!-- 주력이해도 -->
          <div class="col-md-4">
            <div class="stat">
              <label>주력이해도:</label>
              <div class="btn-group">
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('understand', -1)">-1</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('understand', 1)">+1</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('understand', -5)">-5</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('understand', 5)">+5</button>
              </div>
              <span id="understandValue">0</span>
              <div class="progress mt-2">
                <div id="understandBar" class="progress-bar" style="width: 0%; background-color: orange;"></div>
              </div>
              <table id="understandTable">
                <thead>
                  <tr>
                    <th>쉬움</th>
                    <th>보통</th>
                    <th>어려움</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td id="understandEasy">0</td>
                    <td id="understandNormal">0</td>
                    <td id="understandHard">0</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
  <!-- JavaScript -->
  <script>
    // 주사위 버튼 이벤트
    document.getElementById('roll1to6Btn').addEventListener('click', function() {
      const result = Math.floor(Math.random() * 6) + 1;
      document.getElementById('roll1to6Result').textContent = "결과: " + result;
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
      agi: 20,
      extraAgi: 100,
      idea: 20,
      blackspark: 20,
      domain: 20,
      control:20,
      feel:20,
      understand:20
    };

    function adjustStat(stat, amount) {
      const valueElement = document.getElementById(stat + 'Value');
      let currentValue = parseInt(valueElement.textContent);

      const newValue = Math.min(maxValues[stat], Math.max(0, currentValue + amount));
      valueElement.textContent = newValue;

      const progressBar = document.getElementById(stat + 'Bar');
      progressBar.style.width = (newValue / maxValues[stat]) * 100 + '%';

      // Update difficulty table
      if (stat === 'blackspark') {
        const hardValue = newValue;
        const veryhardValue = Math.round(newValue / 2.5);
        const sveryhardValue = Math.round(newValue / 5);

        document.getElementById(stat + 'Hard').textContent = hardValue;
        document.getElementById(stat + 'VeryHard').textContent = veryhardValue;
        document.getElementById(stat + 'SveryHard').textContent = sveryhardValue;
      }
      else {
          // 일반 스탯에 대한 쉬움, 보통, 어려움 계산
          const easyValue = Math.round(newValue * 5);
          const normalValue = Math.round(newValue * 2.5);
          const hardValue = newValue;

          document.getElementById(stat + 'Easy').textContent = easyValue;
          document.getElementById(stat + 'Normal').textContent = normalValue;
          document.getElementById(stat + 'Hard').textContent = hardValue;
      }
    }
  </script>

  <!-- Bootstrap JS and dependencies -->
  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>

</body>
</html>
