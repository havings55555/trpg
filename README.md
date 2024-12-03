<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TRPG 서버</title>
  <!-- Bootstrap CSS -->
  <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    .stat {
      margin-bottom: 20px;
    }
    .progress {
      height: 30px;
      width: 100%;
    }
    .btn-group {
      margin-right: 10px;
    }
    .stat-label {
      font-weight: bold;
    }
    .large-textarea {
      width: 500px;
      height: 500px !important;
      resize:  none;
    }
    .dice-section {
      margin-top: 30px;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 10px;
      background-color: #f9f9f9;
    }
    .dice-settings {
      display: flex;
      align-items: center;
    }
    .dice-settings span {
      margin-right: 10px;
      font-weight: bold;
    }
    .dice-settings input {
      width: 80px;
      margin-left: 5px;
    }
  </style>
</head>
<body>

  <!-- 사이트 제목 변경 -->
  <div class="mb-4">
    <label for="siteTitle">사이트 제목 변경:</label>
    <input type="text" id="siteTitle" class="form-control" placeholder="사이트 제목을 입력하세요" oninput="updateTitle()">
  </div>

  <!-- Navbar -->
  <nav class="navbar navbar-dark bg-dark">
    <a class="navbar-brand" href="#" id="navbarTitle">TRPG 서버</a>
  </nav>

  <!-- 주사위 버튼 -->
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

  <!-- 커스텀 주사위 설정 -->
  <h3 class="mt-4">주사위 설정</h3>
  <div class="dice-settings">
    <span>1 ~</span>
    <input type="number" id="diceMax" class="form-control" value="6" min="1" placeholder="최댓값 입력">
  </div>
  <button id="rollCustomDiceBtn" class="btn btn-primary mt-3">주사위 굴리기</button>
  <div class="mt-3">
    <span id="customDiceResult">결과: </span><br>
    <span id="previousDiceResult">이전 결과: 없음</span>
  </div>

  <!-- 메인 스탯 -->
  <h3 class="mt-5">메인 스탯</h3>
  <div class="container">
    <!-- 첫 번째 줄 -->
    <div class="row">
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">힘 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="strMax" value="20" oninput="updateMaxValue('str', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('str', 5)">+5</button>
          </div>
          <span id="strValue">0</span>
          <div class="progress mt-2">
            <div id="strBar" class="progress-bar" style="width: 0%; background-color: yellow;"></div>
          </div>
        </div>
      </div>
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">체력 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="hpMax" value="20" oninput="updateMaxValue('hp', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('hp', 5)">+5</button>
          </div>
          <span id="hpValue">0</span>
          <div class="progress mt-2">
            <div id="hpBar" class="progress-bar" style="width: 0%; background-color: red;"></div>
          </div>
        </div>
      </div>
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">속도 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="speedMax" value="20" oninput="updateMaxValue('speed', this.value)">
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
        </div>
      </div>
    </div>
    <!-- 두 번째 줄 -->
    <div class="row mt-4">
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">재능 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="talentMax" value="20" oninput="updateMaxValue('talent', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('talent', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('talent', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('talent', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('talent', 5)">+5</button>
          </div>
          <span id="talentValue">0</span>
          <div class="progress mt-2">
            <div id="talentBar" class="progress-bar" style="width: 0%; background-color: purple;"></div>
          </div>
        </div>
      </div>
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">매력 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="charmMax" value="20" oninput="updateMaxValue('charm', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('charm', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('charm', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('charm', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('charm', 5)">+5</button>
          </div>
          <span id="charmValue">0</span>
          <div class="progress mt-2">
            <div id="charmBar" class="progress-bar" style="width: 0%; background-color: pink;"></div>
          </div>
        </div>
      </div>
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">지능 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="intMax" value="20" oninput="updateMaxValue('int', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', 5)">+5</button>
          </div>
          <span id="intValue">0</span>
          <div class="progress mt-2">
            <div id="intBar" class="progress-bar" style="width: 0%; background-color: blue;"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="row mt-3">
    <div class="container">
      <div class="row">
      <!-- 지능 -->
        <div class="col-md-4">
          <div class="stat">
            <label class="stat-label">지능 (최대값 설정):</label>
            <input type="number" class="form-control mb-2" id="intMax" value="20" oninput="updateMaxValue('int', this.value)">
            <div class="btn-group">
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', -1)">-1</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', 1)">+1</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', -5)">-5</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('int', 5)">+5</button>
            </div>
            <span id="intValue">0</span>
            <div class="progress mt-2">
              <div id="intBar" class="progress-bar" style="width: 0%; background-color: cornflowerblue;"></div>
            </div>
          </div>
        </div>

      <!-- 행운 -->
        <div class="col-md-4">
          <div class="stat">
            <label class="stat-label">행운 (최대값 설정):</label>
            <input type="number" class="form-control mb-2" id="lukMax" value="20" oninput="updateMaxValue('luk', this.value)">
            <div class="btn-group">
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('luk', -1)">-1</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('luk', 1)">+1</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('luk', -5)">-5</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('luk', 5)">+5</button>
            </div>
            <span id="lukValue">0</span>
            <div class="progress mt-2">
              <div id="lukBar" class="progress-bar" style="width: 0%; background-color: greenyellow;"></div>
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <div class="stat">
            <label class="stat-label">정신력 (최대값 설정):</label>
            <input type="number" class="form-control mb-2" id="mindMax" value="20" oninput="updateMaxValue('mind', this.value)">
            <div class="btn-group">
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('mind', -1)">-1</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('mind', 1)">+1</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('mind', -5)">-5</button>
              <button class="btn btn-secondary btn-sm" onclick="adjustStat('mind', 5)">+5</button>
            </div>
            <span id="mindValue">0</span>
            <div class="progress mt-2">
              <div id="mindBar" class="progress-bar" style="width: 0%; background-color: pink;"></div>
            </div>
          </div>
        </div>
      </div>

  <!-- 추가 정보 입력란 -->
  <div class="my-4">
    <label for="mainStatNote">추가 정보 입력:</label>
    <textarea id="mainStatNote" class="form-control large-textarea" placeholder="이곳에 내용을 작성하세요..."></textarea>
  </div>

  <!-- Scripts -->
  <script>
    function updateTitle() {
      const title = document.getElementById('siteTitle').value;
      document.title = title;
      document.getElementById('navbarTitle').textContent = title;
    }

    const maxValues = {
      str: 20,
      hp: 20,
      speed: 20,
      talent: 20,
      charm: 20,
      int: 20,
      attack: 20,
      defense: 20,
      blackspark: 20,
      mind:20
    };

    function updateMaxValue(stat, max) {
      maxValues[stat] = parseInt(max) || 20;
    }

    function adjustStat(stat, amount) {
      const valueElement = document.getElementById(stat + 'Value');
      let currentValue = parseInt(valueElement.textContent);
      const newValue = Math.min(maxValues[stat], Math.max(0, currentValue + amount));
      valueElement.textContent = newValue;

      const progressBar = document.getElementById(stat + 'Bar');
      progressBar.style.width = (newValue / maxValues[stat]) * 100 + '%';
    }

    function rollDice(max, resultId) {
      const previous = document.getElementById(resultId).textContent.split(': ')[1] || '없음';
      const result = Math.floor(Math.random() * max) + 1;
      document.getElementById(resultId).textContent = `결과: ${result} (이전: ${previous})`;
    }

    document.getElementById('roll1to6Btn').addEventListener('click', () => rollDice(6, 'roll1to6Result'));
    document.getElementById('roll1to9Btn').addEventListener('click', () => rollDice(10, 'roll1to9Result'));
    document.getElementById('roll1to20Btn').addEventListener('click', () => rollDice(20, 'roll1to20Result'));
    document.getElementById('roll1to100Btn').addEventListener('click', () => rollDice(100, 'roll1to100Result'));

    let previousResult = "없음";
    document.getElementById('rollCustomDiceBtn').addEventListener('click', function () {
      const max = parseInt(document.getElementById('diceMax').value, 10);

      if (isNaN(max) || max < 1) {
        alert('올바른 최댓값을 입력하세요. (1 이상)');
        return;
      }

      const result = Math.floor(Math.random() * max) + 1;
      document.getElementById('customDiceResult').textContent = `결과: ${result}`;
      document.getElementById('previousDiceResult').textContent = `이전 결과: ${previousResult}`;
      previousResult = result;
    });
  </script>
</body>
</html>
