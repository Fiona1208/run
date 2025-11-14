<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>[translate:南區版本密室逃脫]</title>
<style>
  body {
    background-color: #6a4b8c;
    color: #fff;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    margin: 0; padding: 20px;
  }
  .container {
    max-width: 700px;
    margin: 0 auto;
    background-color: #7e5aac;
    padding: 20px;
    border-radius: 10px;
  }
  h1, h2 {
    color: #e0c3fc;
  }
  label, p {
    margin-top: 15px;
    font-weight: bold;
  }
  input[type="text"], input[type="number"], select, textarea {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    border-radius: 5px;
    border: none;
  }
  button {
    margin-top: 20px;
    background-color: #8a65d6;
    border: none;
    padding: 12px 20px;
    color: white;
    font-weight: bold;
    border-radius: 7px;
    cursor: pointer;
  }
  button:hover {
    background-color: #a482d6;
  }
  .photo-preview {
    margin-top: 10px;
    max-width: 100%;
    border-radius: 8px;
  }
  .message {
    margin-top: 15px;
    font-style: italic;
    color: #ffd700;
  }
</style>
</head>
<body>
<div class="container">
  <h1>[translate:南區版本密室逃脫]</h1>

  <!-- 關卡一 -->
  <section id="stage1">
    <h2>[translate:關卡一：輸入隊名]</h2>
    <label for="teamName">[translate:請輸入隊名]</label>
    <input type="text" id="teamName" />
    <button onclick="goToStage(2)">[translate:開始]</button>
  </section>

  <!-- 關卡二 -->
  <section id="stage2" style="display:none;">
    <h2>[translate:關卡二：輸入隊員名稱]</h2>
    <p>[translate:開始進入解密旅程]</p>
    <label>1. <input type="text" name="member1" /></label>
    <label>2. <input type="text" name="member2" /></label>
    <label>3. <input type="text" name="member3" /></label>
    <label>4. <input type="text" name="member4" /></label>
    <label>5. <input type="text" name="member5" /></label>
    <label>6. <input type="text" name="member6" /></label>
    <label>7. <input type="text" name="member7" /></label>
    <label>8. <input type="text" name="member8" /></label>
    <p><strong>[translate:解密地點：石排灣邨]</strong></p>
    <button onclick="goToStage(3)">[translate:下一頁]</button>
  </section>

  <!-- 關卡三 -->
  <section id="stage3" style="display:none;">
    <h2>[translate:關卡三：團隊自拍上傳]</h2>
    <label for="teamPhoto">[translate:請上傳團隊自拍]</label>
    <input type="file" id="teamPhoto" accept="image/*" onchange="previewPhoto(event)" />
    <img id="photoPreview" class="photo-preview" style="display:none" alt="[translate:團隊自拍預覽]" />
    <button onclick="submitPhoto()">[translate:下一頁]</button>
  </section>

  <section id="stage3Success" style="display:none;">
    <p class="message">[translate:你地笑容太燦爛了！恭喜你們成功通關！]</p>
    <p><strong>[translate:解密地點：漁光邨]</strong></p>
    <button onclick="goToStage(4)">[translate:下一頁]</button>
  </section>

  <!-- 關卡四 -->
  <section id="stage4" style="display:none;">
    <h2>[translate:關卡四：實地問答—漁光邨街坊]</h2>
    <p>[translate:去漁光邨，問問街坊，重建時最擔心甚麼?]</p>
    <textarea id="q4answer"></textarea>
    <button onclick="goToStage(5)">[translate:下一頁]</button>
  </section>

  <!-- 關卡五 -->
  <section id="stage5" style="display:none;">
    <h2>[translate:關卡五：實地問答—漁光村1期社工服務隊]</h2>
    <p>[translate:導引玩家尋找社工地址，問職員可提供甚麽服務？]</p>
    <textarea id="q5answer"></textarea>
    <p><strong>[translate:解密地點：華富]</strong></p>
    <button onclick="goToStage(6)">[translate:下一頁]</button>
  </section>

  <!-- 關卡六 -->
  <section id="stage6" style="display:none;">
    <h2>[translate:關卡六：蛋撻價格問題]</h2>
    <p>[translate:銀都冰室或華富冰室，每人買一個蛋撻，一個蛋撻幾錢?]</p>
    <input type="number" id="q6answer" />
    <button onclick="goToStage(7)">[translate:下一頁]</button>
  </section>

  <!-- 關卡七 -->
  <section id="stage7" style="display:none;">
    <h2>[translate:關卡七：南區寒冬送暖大行動日期]</h2>
    <p>[translate:去南區長者綜合服務處，問職員，下次「南區寒冬送暖大行動」為幾月幾日?]</p>
    <input type="text" id="q7answer" />
    <p id="q7message"></p>
    <button onclick="checkStage7()">[translate:提交答案]</button>
  </section>

  <!-- 關卡八 -->
  <section id="stage8" style="display:none;">
    <h2>[translate:關卡八：瀑布灣佛像由來]</h2>
    <p>[translate:去華富瀑布灣道，問任何一個途人，瀑布灣佛像的由來?]</p>
    <textarea id="q8answer"></textarea>
    <button onclick="goToStage(9)">[translate:下一頁]</button>
  </section>

  <!-- 關卡九 -->
  <section id="stage9" style="display:none;">
    <h2>[translate:關卡九：南區長者綜合服務處服務]</h2>
    <p>[translate:問職員，中心有甚麼服務，並寫出其中一個服務]</p>
    <textarea id="q9answer"></textarea>
    <button onclick="goToStage(10)">[translate:下一頁]</button>
  </section>

  <!-- 關卡十 -->
  <section id="stage10" style="display:none;">
    <h2>[translate:關卡十：良躍社區藥房最平血壓計價格]</h2>
    <p>[translate:問問最平的血壓計幾錢。]</p>
    <input type="number" id="q10answer" />
    <p id="q10message"></p>
    <button onclick="checkStage10()">[translate:提交答案]</button>
  </section>

  <!-- 關卡十一 -->
  <section id="stage11" style="display:none;">
    <h2>[translate:關卡十一：良躍社區藥房門口影相]</h2>
    <p>[translate:問問華富遷拆，會搬去邊?]</p>
    <input type="text" id="q11answer" />
    <p id="q11message"></p>
    <label for="photoStage11">[translate:請上載照片]</label>
    <input type="file" id="photoStage11" accept="image/*" />
    <p><strong>[translate:解密地點：華貴]</strong></p>
    <button onclick="checkStage11()">[translate:提交答案]</button>
  </section>

  <!-- 關卡十二 -->
  <section id="stage12" style="display:none;">
    <h2>[translate:關卡十二：方王換娣長者鄰舍打卡及花名計數]</h2>
    <p>[translate:門口打卡，並算出10種花名]</p>
    <label for="photoStage12">[translate:請上載照片]</label>
    <input type="file" id="photoStage12" accept="image/*" />
    <label for="flowersCount">[translate:請書寫花名數量]</label>
    <input type="number" id="flowersCount" min="0" max="20" />
    <button onclick="goToStage(13)">[translate:下一頁]</button>
  </section>

  <!-- 關卡十三 -->
  <section id="stage13" style="display:none;">
    <h2>[translate:關卡十三：方王換娣長者鄰舍會員資格]</h2>
    <p>[translate:把全組的年齡加起來，問問可否成為會員?]</p>
    <select id="q13answer">
      <option value="">[translate:請選擇]</option>
      <option value="可以">[translate:可以]</option>
      <option value="不可以">[translate:不可以]</option>
    </select>
    <button onclick="goToStage(14)">[translate:下一頁]</button>
  </section>

  <!-- 關卡十四 -->
  <section id="stage14" style="display:none;">
    <h2>[translate:關卡十四：方樹泉青少年中心搬離年份]</h2>
    <p>[translate:問問職員/途人，方樹泉青少年中心甚麼年份搬離華貴邨。]</p>
    <input type="number" id="q14answer" />
    <p id="q14message"></p>
    <button onclick="checkStage14()">[translate:提交答案]</button>
  </section>

  <!-- 關卡十五 -->
  <section id="stage15" style="display:none;">
    <h2>[translate:關卡十五：珍維社區健康促進中心健康團隊相]</h2>
    <label for="photoStage15">[translate:請拍一張代表健康的團隊相，並上載]</label>
    <input type="file" id="photoStage15" accept="image/*" />
    <button onclick="goToStage(16)">[translate:下一頁]</button>
  </section>

  <!-- 關卡十六 -->
  <section id="stage16" style="display:none;">
    <h2>[translate:關卡十六：南區地區康健中心21樓周年問題]</h2>
    <p>[translate:問問職員，今年係DHC 成立幾多周年？]</p>
    <input type="number" id="q16answer" />
    <p id="q16message"></p>
    <button onclick="checkStage16()">[translate:提交答案]</button>
  </section>

  <!-- 關卡十七 -->
  <section id="stage17" style="display:none;">
    <h2>[translate:關卡十七：南區地區康健中心附屬中心選擇題]</h2>
    <p>[translate:以下哪一個地方沒有南區地區康健中心的附屬中心?]</p>
    <select id="q17answer">
      <option value="">[translate:請選擇]</option>
      <option value="赤柱">[translate:A. 赤柱]</option>
      <option value="利東邨">[translate:B. 利東邨]</option>
      <option value="置富花園">[translate:C. 置富花園]</option>
      <option value="香港仔">[translate:D. 香港仔]</option>
      <option value="田灣">[translate:E. 田灣]</option>
    </select>
    <button onclick="checkStage17()">[translate:提交答案]</button>
  </section>
</div>

<script>
function goToStage(stage) {
  for(let i=1;i<=17;i++){
    const el=document.getElementById("stage"+i);
    if(el) el.style.display="none";
  }
  if(stage==="stage3Success"){
    document.getElementById("stage3Success").style.display="block";
    return;
  }
  const target=document.getElementById("stage"+stage);
  if(target) target.style.display="block";
}

function previewPhoto(event) {
  const file = event.target.files[0];
  if(file){
    const reader=new FileReader();
    reader.onload=function(e){
      const img=document.getElementById('photoPreview');
      img.src=e.target.result;
      img.style.display="block";
    }
    reader.readAsDataURL(file);
  }
}

function submitPhoto(){
  const photoInput=document.getElementById('teamPhoto');
  const photoPreview=document.getElementById('photoPreview');
  if(photoInput.files.length >0 && photoPreview.src){
    document.getElementById('stage3').style.display='none';
    document.getElementById('stage3Success').style.display='block';
  }else{
    alert("[translate:請先上傳團隊自拍]");
  }
}

function checkStage7() {
  const answer=document.getElementById('q7answer').value.trim();
  const message=document.getElementById('q7message');
  if(answer==="12月14日"){
    message.style.color="lightgreen";
    message.textContent="[translate:成功通關！]";
    setTimeout(()=>goToStage(8),2000);
  }else{
    message.style.color="red";
    message.textContent="[translate:請再次嘗試]";
  }
}

function checkStage10() {
  const answer=document.getElementById('q10answer').value.trim();
  const message=document.getElementById('q10message');
  if(answer==="480"){
    message.style.color="lightgreen";
    message.textContent="[translate:成功通關！]";
    setTimeout(()=>goToStage(11),2000);
  }else{
    message.style.color="red";
    message.textContent="[translate:請再次嘗試]";
  }
}

function checkStage11() {
  const answer=document.getElementById('q11answer').value.trim();
  const message=document.getElementById('q11message');
  if(answer==="利東邨"){
    message.style.color="lightgreen";
    message.textContent="[translate:成功通關！]";
    setTimeout(()=>goToStage(12),2000);
  }else{
    message.style.color="red";
    message.textContent="[translate:請再次嘗試]";
  }
}

function checkStage14() {
  const answer=document.getElementById('q14answer').value.trim();
  const message=document.getElementById('q14message');
  if(answer==="2006"){
    message.style.color="lightgreen";
    message.textContent="[translate:成功通關！]";
    setTimeout(()=>goToStage(15),2000);
  }else{
    message.style.color="red";
    message.textContent="[translate:請再次嘗試]";
  }
}

function checkStage16() {
  const answer=document.getElementById('q16answer').value.trim();
  const message=document.getElementById('q16message');
  if(answer==="3"){
    message.style.color="lightgreen";
    message.textContent="[translate:成功通關！]";
    setTimeout(()=>goToStage(17),2000);
  }else{
    message.style.color="red";
    message.textContent="[translate:請再次嘗試]";
  }
}

function checkStage17() {
  const answer=document.getElementById('q17answer').value;
  if(answer==="田灣"){
    alert("[translate:成功通關！]");
    goToStage(1);
  }else{
    alert("[translate:請再次嘗試]");
  }
}
</script>
</body>
</html>
