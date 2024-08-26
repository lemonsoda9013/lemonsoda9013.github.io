# 服务器状态获取

在```<body>```之前添加如下代码引用jquery

```
<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
```

body内部添加如下js代码，获取mc服务器的状态

```
<script>
  function getMinecraftServerStatus(serverAddress, callback) {
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'https://tool.mintimate.cn/api/mcStatus?serverIP=' + serverAddress + '&serverType=Java', true);
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4 && xhr.status === 200) {
        var data = JSON.parse(xhr.responseText);
        if (data.status === "1") {
          var { max, online } = data.message.players;
          callback(`在线人数${online}/${max}`);
        } else {
          callback("离线");
        }
      } else {
        callback("离线");
      }
    };
    xhr.send();
  }
  getMinecraftServerStatus("acffd71f-ea7f-c27d-101b-1344a5becd3e.ofalias.com:56226", function (status) {
    document.getElementById("stat1").textContent = status;
  });
  getMinecraftServerStatus("8fb74d2a-c7ab-8b1a-e414-31870fd3df78.ofalias.com:63562", function (status) {
    document.getElementById("stat2").textContent = status;
  });
  getMinecraftServerStatus("e61cf922-861f-7823-2c1e-a30a9e898996.ofalias.com:42129", function (status) {
    document.getElementById("stat3").textContent = status;
  });
</script>
```

文章正文部分（```</article>```前面）修改如下
```
<h2 id="sprint-racer">Sprint Racer</h2>
<div>
  <p>当前服务器<span id="stat1">检测中...</span></p>
</div>

<h2 id="super-voxel-party">Super Voxel Party</h2>
<div>
  <p>当前服务器<span id="stat2">检测中...</span></p>
</div>

<h2 id="yet-another-bingo">Yet Another BINGO</h2>
<div>
  <p>当前服务器<span id="stat3">检测中...</span></p>
</div>
```