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
      height: 500px;
      resize: none; /* Prevent resizing */
    }
  </style>
</head>
<body>

  <!-- Site title section -->
  <div class="mb-4">
    <label for="siteTitle">사이트 제목 변경:</label>
    <input type="text" id="siteTitle" class="form-control" placeholder="사이트 제목을 입력하세요" oninput="updateTitle()">
  </div>

  <!-- Navbar -->
  <nav class="navbar navbar-dark bg-dark">
    <a class="navbar-brand" href="#" id="navbarTitle">TRPG 서버</a>
  </nav>

  <!-- Random number buttons -->
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

  <!-- Main stats section -->
  <h3 class="mt-5">메인 스탯</h3>
  <div class="container">
    <div class="row">
      <!-- 힘 -->
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

      <!-- 체력 -->
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

      <!-- 속도 -->
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">속도 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="curseMax" value="20" oninput="updateMaxValue('speed', this.value)">
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

      <div class="container">
        <div class="row">
          <!-- 재능 -->
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
    
          <!-- 매력 -->
          <div class="col-md-4">
            <div class="stat">
              <label class="stat-label">매력 (최대값 설정):</label>
              <input type="number" class="form-control mb-2" id="charmMax" value="20" oninput="MaxValue('charm', this.value)">
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
    
          <!-- 주력 -->
          <div class="col-md-4">
            <div class="stat">
              <label class="stat-label">속도 (최대값 설정):</label>
              <input type="number" class="form-control mb-2" id="curseMax" value="20" oninput="updateMaxValue('curse', this.value)">
              <div class="btn-group">
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('curse', -1)">-1</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('curse', 1)">+1</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('curse', -5)">-5</button>
                <button class="btn btn-secondary btn-sm" onclick="adjustStat('curse', 5)">+5</button>
              </div>
              <span id="curseValue">0</span>
              <div class="progress mt-2">
                <div id="curseBar" class="progress-bar" style="width: 0%; background-color: blue;"></div>
              </div>
            </div>
          </div>
    

    <!-- Text area between Main Stats and Additional Stats -->
    <div class="my-4">
      <label for="mainStatNote">추가 정보 입력:</label>
      <textarea id="mainStatNote" class="form-control large-textarea" placeholder="이곳에 내용을 작성하세요..."></textarea>
    </div>
        </div>
    <!-- Additional stats section -->
    <h3 class="mt-5">추가 스탯</h3>
    <div class="row">
      <!-- 공격력 -->
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">공격력 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="attackMax" value="20" oninput="updateMaxValue('attack', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('attack', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('attack', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('attack', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('attack', 5)">+5</button>
          </div>
          <span id="attackValue">0</span>
          <div class="progress mt-2">
            <div id="attackBar" class="progress-bar" style="width: 0%; background-color: darkred;"></div>
          </div>
        </div>
      </div>

      <!-- 방어력 -->
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">방어력 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="defenseMax" value="20" oninput="updateMaxValue('defense', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('defense', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('defense', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('defense', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('defense', 5)">+5</button>
          </div>
          <span id="defenseValue">0</span>
          <div class="progress mt-2">
            <div id="defenseBar" class="progress-bar" style="width: 0%; background-color: red;"></div>
          </div>
        </div>
      </div>

      <!-- 흑섬확률 -->
      <div class="col-md-4">
        <div class="stat">
          <label class="stat-label">흑섬확률 (최대값 설정):</label>
          <input type="number" class="form-control mb-2" id="blacksparkMax" value="20" oninput="updateMaxValue('blackspark', this.value)">
          <div class="btn-group">
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', -1)">-1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', 1)">+1</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', -5)">-5</button>
            <button class="btn btn-secondary btn-sm" onclick="adjustStat('blackspark', 5)">+5</button>
          </div>
          <span id="blacksparkValue">0</span>
          <div class="progress mt-2">
            <div id="blacksparkBar" class="progress-bar" style="width: 0%; background-color: skyblue;"></div>
          </div>
        </div>
      </div>
    </div>
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
      curse: 20,
      attack: 20,
      defense: 20,
      blackspark: 20
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
    document.getElementById('roll1to6Btn').addEventListener('click', function() {
      const previous = document.getElementById('roll1to6Result').textContent;
      const result = Math.floor(Math.random() * 6) + 1;
      document.getElementById('roll1to6Result').textContent = `결과: ${result} (이전: ${previous.split(': ')[1] || '없음'})`;
    });

    document.getElementById('roll1to9Btn').addEventListener('click', function() {
      const previous = document.getElementById('roll1to9Result').textContent;
      const result = Math.floor(Math.random() * 10) + 1;
      document.getElementById('roll1to9Result').textContent = `결과: ${result} (이전: ${previous.split(': ')[1] || '없음'})`;
    });

    document.getElementById('roll1to20Btn').addEventListener('click', function() {
      const previous = document.getElementById('roll1to20Result').textContent;
      const result = Math.floor(Math.random() * 20) + 1;
      document.getElementById('roll1to20Result').textContent = `결과: ${result} (이전: ${previous.split(': ')[1] || '없음'})`;
    });

    document.getElementById('roll1to100Btn').addEventListener('click', function() {
      const previous = document.getElementById('roll1to100Result').textContent;
      const result = Math.floor(Math.random() * 100) + 1;
      document.getElementById('roll1to100Result').textContent = `결과: ${result} (이전: ${previous.split(': ')[1] || '없음'})`;
    });
  </script>
</body>
</html>
