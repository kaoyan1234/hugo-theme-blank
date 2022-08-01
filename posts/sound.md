---
title: "声音"
date: 2020-07-17T11:57:53+08:00
---

> 此页包含 javascript
> [yechentide](https://github.com/yechentide) 写的

| 选项           |                                                                                                                                                                                                                      值                                                                                                                                                                                                                       |
| -------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| 波形选择       | <input name="wave" type="radio" value="1" id="wave-1" onchange="play();"><label for="wave-1">正弦波</label> <input name="wave" type="radio" value="2" id="wave-2" onchange="play();"><label for="wave-2">方波</label> <input name="wave" type="radio" value="3" id="wave-3" onchange="play();"><label for="wave-3">锯齿波</label> <input name="wave" type="radio" value="4" id="wave-4" onchange="play();"><label for="wave-4">三角波</label> |
| 当前频率       |                                                                                                                                                              <input type="range" id="range_Hz" min="1" max="10000" value="440" onchange="play();"><span id="msg_Hz">440</span>Hz                                                                                                                                                              |
| 开始频率       |                                                                                                                                                                                         <input id="start" type="number" size=3 value="400" required>                                                                                                                                                                                          |
| 增加幅度       |                                                                                                                                                                                          <input id="plus" type="number" size=3 value="10" required>                                                                                                                                                                                           |
| 持续时间（秒） |                                                                                                                                                                                               <input id="time" type="number" size=3 value="1">                                                                                                                                                                                                |
| 网页音量       |                                                                                                                                                               <input type="range" id="range_vol" min="0" max="100" value="25" onchange="play();"><span id="msg_vol">25</span>%                                                                                                                                                                |
| 播放控制       |                                                                                                                                                                                <button onclick="play();">播放</button><button onclick="stop();">暂停</button>                                                                                                                                                                                 |

<script>
    let audioCtx, oscillator, gain, firstflg = true;
    let loop;
    // 初始化slider
    document.getElementById('range_Hz').value = document.getElementById("start").value;
    
    let play = () => {
        alert("存在一个由类型转换引起的 bug")
        stop();

        let range_vol = document.getElementById('range_vol').value;
        let range_Hz = document.getElementById('range_Hz').value;
        console.log(range_Hz)
        document.getElementById('msg_vol').value = range_vol;
        document.getElementById('msg_Hz').value = range_Hz;

        try {
            if (firstflg) {
                // AudioContextの生成
                audioCtx = new AudioContext();
                firstflg = false;
            }
            // 波形
            oscillator = audioCtx.createOscillator();
            if (document.getElementById("wave-1").checked) oscillator.type = "sine";
            if (document.getElementById("wave-2").checked) oscillator.type = "square";
            if (document.getElementById("wave-3").checked) oscillator.type = "sawtooth";
            if (document.getElementById("wave-4").checked) oscillator.type = "triangle";
            // 频率
            oscillator.frequency.value = range_Hz;
            console.log("当前频率: ", oscillator.frequency.value)
            // Gain(音量)
            gain = audioCtx.createGain();
            gain.gain.value = range_vol / 100;
            oscillator.connect(gain);
            gain.connect(audioCtx.destination);
            oscillator.start();
        } catch (e) {
            console.log(e);
        }

        let plus = () => {
            console.log("plus开始，当前频率: ", oscillator.frequency.value)
            let plus = document.getElementById("plus").value;
            console.log("plus: ", plus)

            // 这里有个 bug，传来的数字不能正常加法，垃圾 js 不修了
            oscillator.frequency.value += plus;
            console.log("当前频率: ", oscillator.frequency.value)
            document.getElementById('range_Hz').value = oscillator.frequency.value;
            document.getElementById('msg_Hz').value = oscillator.frequency.value;
        }
        let time = document.getElementById("time").value;
        console.log("time: ",time)
        loop = setInterval(plus, time * 1000);
    }

    let stop = () => {
        clearInterval(loop);
        document.getElementById("start").value = document.getElementById('range_Hz').value;
        if (oscillator) {
            oscillator.stop();
            gain.disconnect();
            oscillator.disconnect();
        }
    }
</script>
