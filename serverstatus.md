# 服务器状态获取

在```<body>```之前添加如下代码引用jquery

```
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```

body内部添加如下代码，获取mc服务器的状态

颜色标签是自己添加的，不通用，用于别处时删除

```
<p>服务器状态: <span id="stat-1"><orange>正在获取信息...</orange></span></p>
<p>在线玩家: <span id="list-1"><orange>正在获取信息...</orange></span></p>

<p>服务器状态: <span id="stat-2"><orange>正在获取信息...</orange></span></p>
<p>在线玩家: <span id="list-2"><orange>正在获取信息...</orange></span></p>

<p>服务器状态: <span id="stat-3"><orange>正在获取信息...</orange></span></p>
<p>在线玩家: <span id="list-3"><orange>正在获取信息...</orange></span></p>

<script>

    // 获取服务器状态，API来自tool.mintimate.cn
    function fetchStat(url, timeout, resultVar, spanId) {
        let timeoutFlag = false;

        // 创建一个定时器，在n秒后标记为超时
        const timer = setTimeout(function () {
            timeoutFlag = true;
            window[resultVar] = "<red>请求超时</red>";
            $('#' + spanId).html(window[resultVar]);
        }, timeout);

        // 使用 jQuery 的 AJAX 请求
        $.ajax({
            url: 'https://tool.mintimate.cn/api/mcStatus?serverIP=' + url + '&serverType=Java',
            dataType: 'json',
            success: function (response) {
                if (!timeoutFlag) {  // 如果在超时之前返回
                    clearTimeout(timer);
                    if (response.status === "1") {
                        window[resultVar] = `<teal>在线人数${response.message.players.online}/${response.message.players.max}</teal>`;
                    } else {
                        window[resultVar] = "<red>离线</red>";
                    }
                    $('#' + spanId).html(window[resultVar]);
                }
            },
            error: function (xhr) {
                if (!timeoutFlag) {  // 如果在超时之前返回
                    clearTimeout(timer);
                    window[resultVar] = "<red>请求失败</red>";
                    $('#' + spanId).html(window[resultVar]);
                }
            }
        });
    }

    // 查看服务器在线人数，API来自api.mcsrvstat.us
    function fetchList(url, timeout, resultVar, spanId) {
        let timeoutFlag = false;

        // 创建一个定时器，在n秒后标记为超时
        const timer = setTimeout(function () {
            timeoutFlag = true;
            window[resultVar] = "<red>请求超时</red>";
            $('#' + spanId).html(window[resultVar]);
        }, timeout);

        // 使用 jQuery 的 AJAX 请求
        $.ajax({
            url: 'https://api.mcsrvstat.us/3/' + url,
            dataType: 'json',
            success: function (response) {
                if (!timeoutFlag) {  // 如果在超时之前返回
                    clearTimeout(timer);
                    console.log(response)
                    if (response.online === true) {
                        const players = response.players;
                        if (players.list && players.list.length > 0) {
                            let playerNames = players.list.map(player => player.name).join(', ');
                            window[resultVar] = '<teal>'+ playerNames + '</teal>';
                        } else {
                            window[resultVar] = '<red>未获取到玩家名称</red>';
                        }
                    } else {
                        window[resultVar] = "<red>未获取到玩家名称</red>";
                    }
                    $('#' + spanId).html(window[resultVar]);
                }
            },
            error: function (xhr) {
                if (!timeoutFlag) {  // 如果在超时之前返回
                    clearTimeout(timer);
                    window[resultVar] = "<red>请求失败</red>";
                    $('#' + spanId).html(window[resultVar]);
                }
            }
        });
    }

    $(document).ready(function () {
        //fetchStat('acffd71f-ea7f-c27d-101b-1344a5becd3e.ofalias.com:56226', 5000, 'result1', 'stat-1');
        //fetchStat('8fb74d2a-c7ab-8b1a-e414-31870fd3df78.ofalias.com:63562', 5000, 'result2', 'stat-2');
        //fetchStat('e61cf922-861f-7823-2c1e-a30a9e898996.ofalias.com:42129', 5000, 'result3', 'stat-3');
    });

    $(document).ready(function () {
        //fetchList('acffd71f-ea7f-c27d-101b-1344a5becd3e.ofalias.com:56226', 10000, 'list1', 'list-1');
        //fetchList('8fb74d2a-c7ab-8b1a-e414-31870fd3df78.ofalias.com:63562', 10000, 'list2', 'list-2');
        //fetchList('e61cf922-861f-7823-2c1e-a30a9e898996.ofalias.com:42129', 10000, 'list3', 'list-3');
    });

</script>

```
