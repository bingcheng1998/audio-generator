# 基于tacotron2的人声唱段生成

<form action="PayslipServlet" method="get">
请输入需要演唱的句子:    <input type="text" name="lname" id="lname" value="猪猪侠打败了怪兽"><br/>
<br>
<button type="button" onClick="pr()">生成</button>
</form><p><span id="result"></span>
 <script>
function pr() {
var name = document.getElementById('lname').value
if (name.length != 8) {
document.getElementById("result").innerHTML = "输入有误，请确认输入8个汉字"
} else {
var getname = name.slice(0,3)+"~~AS"+name.slice(3,6)+"~~"+name.slice(-2)+"SA"
var nameprint = name.slice(0,3)+"~~[静音]"+name.slice(3,6)+"~~"+name.slice(-2)+"[吸气]"
var content = '开始生成: '+nameprint + '<p><audio controls="controls"><source src="http://genmusic.host.openmc.cn/'+getname+'" type="audio/wav" />Your browser does not support this audio format.</audio>'
document.getElementById("result").innerHTML = content}}</script>


---

该唱段由原始唱段作embedding后，修改汉字embedding，保留其他（如音调，时间长度，音色）部分，再进行生成得到。原始音频如下：

<audio controls="controls"><source src="./2001000006.wav" type="audio/wav" />

原embedding修改汉字为标准汉字embedding后复原的音频如下：

<audio controls="controls"><source src="http://genmusic.host.openmc.cn/%E6%BC%82%E6%B5%AE%E5%9C%A8~~AS%E4%B8%80~%E7%89%87~~%E6%97%A0%E5%A5%88SA" type="audio/wav" />

模型参考 PyTorch 实现的[tacotron2生成器](https://pytorch.org/hub/nvidia_deeplearningexamples_tacotron2/)。Tacotron2是一个文本转语音模型。在此基础上添加时常，音调，颤音等歌唱所需数据，修改后的模型详见[这里](https://github.com/bingcheng1998/audio-NYU-HPC-2022/blob/master/taco2_music/test_fft.ipynb)。

这个模型的训练依赖于英文的tacotron2预训练模型，在中文演唱方面，仅仅使用[Opencpop](https://wenet.org.cn/opencpop/)数据集。由于数据量过小，仅仅做演示用，且暂时只进行了单个汉字的生成，且模型已经过拟合。后续致力于连续唱段生成，消除汉字之间杂音，支持多人声生成等。





