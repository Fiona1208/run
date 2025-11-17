<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8" />
<title>南區逃脫遊戲</title>
<style>
  body {
    background-color: #cce7ff; /* 淺藍色背景 */
    font-family: "Microsoft JhengHei", Arial, sans-serif;
    margin: 0; padding: 0;
  }
  .container {
    max-width: 600px;
    margin: 40px auto;
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 0 15px #88b7ff;
    padding: 30px;
    text-align: center;
  }
  h2, h3 {
    color: #3366cc;
  }
  input[type="text"], textarea, button, select {
    font-size: 16px;
    padding: 8px 10px;
    margin: 10px 0;
    border-radius: 6px;
    border: 1px solid #aaa;
    width: 80%;
    box-sizing: border-box;
  }
  button {
    background-color: #3377ff;
    color: white;
    cursor: pointer;
    border: none;
  }
  textarea {
    resize: vertical;
  }
  .form-group {
    margin-bottom: 12px;
  }
  .hidden {
    display: none;
  }
  label {
    display: block;
    margin-top: 15px;
    font-weight: bold;
  }
  .answer-result {
    font-weight: bold;
    margin-top: 15px;
  }
</style>
</head>
<body>

<div class="container" id="step1">
  <h2>南區探險家逃脫大行動</h2>
  <p>故事背景：你們是探險家，今天準備要到南區進行解謎大行動，當中需要運用你們的指揮及團隊合作。各位探險家，你們準備好了嗎？祝你們一切順利！</p>
  <h3>關卡一：請輸入隊名</h3>
  <input type="text" id="teamName" placeholder="請輸入隊名" />
  <br />
  <button onclick="goStep(2)">下一關</button>
</div>

<div class="container hidden" id="step2">
  <h3>關卡二：請輸入隊員名稱（最多8人）</h3>
  <form id="membersForm" onsubmit="return false;">
    <div class="form-group"><input type="text" name="member" placeholder="隊員1" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員2" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員3" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員4" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員5" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員6" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員7" /></div>
    <div class="form-group"><input type="text" name="member" placeholder="隊員8" /></div>
    <button onclick="goStep(3)">下一頁</button>
  </form>
</div>

<div class="container hidden" id="step3">
  <h3>探險家們，準備好出發了嗎？</h3>
  <p>記得發揮你們的<strong>團隊合作</strong>，祝你們一切順利！</p>
  <button onclick="goStep(4)">繼續關卡三</button>
</div>

<div class="container hidden" id="step4">
  <h3>關卡三：請上載您與香港仔坊會總部大樓門前的最潮團隊自拍照</h3>
  <input type="file" accept="image/*" id="selfieUpload" />
  <br />
  <button onclick="goStep(5)">下一關</button>
</div>

<div class="container hidden" id="step5">
  <h3>關卡四：去漁光邨，問問街坊，重建時最擔心甚麼？</h3>
  <p>請記錄您的答案：</p>
  <textarea id="neighborAnswer" rows="4" style="width: 80%;" placeholder="輸入您的答案"></textarea>
  <br />
  <button onclick="goStep(6)">下一關</button>
</div>

<div class="container hidden" id="step6">
  <h3>關卡五：問問坊會同事香港仔坊會在哪一年成立？（選擇題）</h3>
  <form id="yearForm" onsubmit="return false;">
    <label><input type="radio" name="year" value="1930" /> A: 1930 </label>
    <label><input type="radio" name="year" value="1940" /> B: 1940 </label>
    <label><input type="radio" name="year" value="1950" /> C: 1950 </label>
    <label><input type="radio" name="year" value="1960" /> D: 1960 </label>
    <button onclick="checkYearAnswer()">提交答案</button>
  </form>
  <p id="yearAnswerResult" class="answer-result"></p>
</div>

<div class="container hidden" id="step7">
  <h3>關卡六：去南區地區康健中心 21 樓，問問職員，以下哪個地方沒有南區地區康健中心的附屬中心？（選擇題）</h3>
  <form id="centerForm" onsubmit="return false;">
    <label><input type="radio" name="center" value="赤柱" /> A: 赤柱</label>
    <label><input type="radio" name="center" value="利東邨" /> B: 利東邨</label>
    <label><input type="radio" name="center" value="置富花園" /> C: 置富花園</label>
    <label><input type="radio" name="center" value="香港仔" /> D: 香港仔</label>
    <label><input type="radio" name="center" value="田灣" /> E: 田灣</label>
    <button onclick="checkCenterAnswer()">提交答案</button>
  </form>
  <p id="centerAnswerResult" class="answer-result"></p>
</div>

<script>
  function goStep(step) {
    if (step === 2) {
      const teamName = document.getElementById('teamName').value.trim();
      if (!teamName) {
        alert('請輸入隊名');
        return;
      }
    }
    if (step === 3) {
      const members = document.querySelectorAll('#membersForm input[name="member"]');
      const hasMember = Array.from(members).some(m => m.value.trim() !== '');
      if (!hasMember) {
        alert('請至少輸入一位隊員名稱');
        return;
      }
    }
    if (step === 5) {
      const selfieFile = document.getElementById('selfieUpload').files;
      if (!selfieFile.length) {
        alert('請上載團隊自拍照片');
        return;
      }
    }
    if (step === 6) {
      const answer = document.getElementById('neighborAnswer').value.trim();
      if (!answer) {
        alert('請輸入漁光邨街坊擔心的事情');
        return;
      }
    }
    for (let i = 1; i <= 7; i++) {
      document.getElementById('step' + i).classList.add('hidden');
    }
    document.getElementById('step' + step).classList.remove('hidden');
  }

  function checkYearAnswer() {
    const radios = document.querySelectorAll('input[name="year"]');
    const selected = Array.from(radios).find(r => r.checked);
    const resultEl = document.getElementById('yearAnswerResult');
    if (!selected) {
      alert('請選擇一個答案');
      return;
    }
    if (selected.value === '1950') {
      resultEl.textContent = '答對了！香港仔坊會成立於1950年。';
      resultEl.style.color = 'green';
      setTimeout(() => goStep(7), 1500);
    } else {
      resultEl.textContent = '答案錯誤，請再試一次。';
      resultEl.style.color = 'red';
    }
  }

  function checkCenterAnswer() {
    const radios = document.querySelectorAll('input[name="center"]');
    const selected = Array.from(radios).find(r => r.checked);
    const resultEl = document.getElementById('centerAnswerResult');
    if (!selected) {
      alert('請選擇一個答案');
      return;
    }
    if (selected.value === '田灣') {
      resultEl.textContent = '答對了！田灣沒有南區地區康健中心的附屬中心。';
      resultEl.style.color = 'green';
    } else {
      resultEl.textContent = '答案錯誤，請再試一次。';
      resultEl.style.color = 'red';
    }
  }
</script>

</body>
<div class="interaction-scene">
  <img src="https://thumbs.dreamstime.com/b/family-relationship-children-adults-seniors-17760567.jpg" alt="Family Relationship with Children, Adults, Seniors" />
</div>
