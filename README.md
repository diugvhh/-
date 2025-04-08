# -<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>封锁的房间</title>
  <style>
    body {
      margin: 0;
      font-family: "Courier New", monospace;
      background: #fff;
      color: #000;
      text-align: center;
      background-image: url('https://i.imgur.com/ElTPG0v.png'); /* 手绘背景占位图 */
      background-size: cover;
      background-position: center;
    }
    .scene {
      padding: 30px;
      background-color: rgba(255, 255, 255, 0.85);
      margin: 50px auto;
      max-width: 600px;
      border: 2px dashed black;
    }
    button {
      background: none;
      border: 2px solid black;
      padding: 10px 20px;
      font-size: 18px;
      margin: 10px;
      cursor: pointer;
    }
    input {
      padding: 10px;
      font-size: 16px;
      border: 1px solid black;
      width: 80px;
    }
    #message {
      margin-top: 20px;
      font-weight: bold;
    }
    audio {
      display: none;
    }
  </style>
</head>
<body>
  <div class="scene">
    <h1>封锁的房间</h1>
    <p>你醒来在一间黑白风格的房间中，门被锁上了。</p>

    <button onclick="checkPainting()">查看墙上的画</button>
    <button onclick="checkBook()">查看桌上的书</button>
    <button onclick="checkBox()">查看密码箱</button>

    <div id="message"></div>

    <div id="codeInput" style="display:none; margin-top: 20px;">
      <p>请输入三位密码：</p>
      <input type="text" id="code" maxlength="3">
      <button onclick="submitCode()">提交</button>
    </div>

    <audio id="bgm1" src="https://example.com/music/room1.mp3" loop></audio>
    <audio id="bgm2" src="https://example.com/music/room2.mp3" loop></audio>
    <audio id="bgm3" src="https://example.com/music/room3.mp3" loop></audio>
  </div>

  <script>
    let paintingSeen = false;
    let bookSeen = false;
    let boxOpen = false;

    function playMusic(room) {
      document.getElementById("bgm1").pause();
      document.getElementById("bgm2").pause();
      document.getElementById("bgm3").pause();
      
      if (room === 1) {
        document.getElementById("bgm1").play();
      } else if (room === 2) {
        document.getElementById("bgm2").play();
      } else if (room === 3) {
        document.getElementById("bgm3").play();
      }
    }

    function checkPainting() {
      document.getElementById('message').innerText = "画背面写着：‘数字在书中’";
      paintingSeen = true;
      playMusic(1); // Start music for Room 1
    }

    function checkBook() {
      document.getElementById('message').innerText = "书中写着：‘画有几边，桌有几脚？用前者减去后者。’";
      bookSeen = true;
    }

    function checkBox() {
      if (paintingSeen && bookSeen) {
        document.getElementById('message').innerText = "你发现密码箱有三位数密码，准备输入。";
        document.getElementById('codeInput').style.display = "block";
        playMusic(2); // Start music for Room 2
      } else {
        document.getElementById('message').innerText = "箱子上有密码锁，得先找到线索。";
      }
    }

    function submitCode() {
      const code = document.getElementById('code').value;
      if (code === "042") {
        document.getElementById('message').innerText = "密码正确！你打开了箱子，找到钥匙，成功逃脱！";
        document.getElementById('codeInput').style.display = "none";
        playMusic(3); // Start music for Room 3
      } else {
        document.getElementById('message').innerText = "密码错误，再想想。";
      }
    }
  </script>
</body>
</html>