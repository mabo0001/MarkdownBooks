### 3.6　最终版的Text Arranger

Text Arranger最终版（3.0）集合了本章讨论的所有HTML5 Text API功能（见例3-1）。运行最终的程序，看看不同的选项如何互动。读者可能会发现有些情况很有意思。

+ 增加图案文本大小就是在画布上增加文本中图案的大小（如同图案上的蒙版或者窗口）。
+ 画布的宽度和高度受样式宽度和样式高度影响（缩放）。

例3-1　Text Arranger 3.0

```javascript
<!doctype html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>CH3EX3: Text Arranger 3.0</title>
<script src="modernizr.js"></script>
<script type="text/javascript" src="jscolor/jscolor.js"></script>
<script type="text/javascript">
window.addEventListener("load", eventWindowLoaded, false);
function eventWindowLoaded() {
　 canvasApp();
}
function canvasSupport () {
　　 return Modernizr.canvas;
}
function eventWindowLoaded() {
　　 var patternPreload = new Image();
　　 patternPreload.onload = eventAssetsLoaded;
　　 patternPreload.src = "texture.jpg";
}
function eventAssetsLoaded() {
　 canvasApp();
}
function canvasApp() {
　 var message = "your text";
　 var fontSize = "50";
　 var fontFace = "serif";
　 var textFillColor = "#ff0000";
　 var textAlpha = 1;
　 var shadowX = 1;
　 var shadowY = 1;
　 var shadowBlur = 1;
　 var shadowColor = "#707070";
　 var textBaseline = "middle";
　 var textAlign = "center";
　 var fillOrStroke ="fill";
　 var fontWeight = "normal";
　 var fontStyle = "normal";
　 var fillType = "colorFill";
　 var textFillColor2 = "#000000";
　 var pattern = new Image();
　 if (!canvasSupport()) {
　　　　　return;
　　　　}
　 var theCanvas = document.getElementById("canvasOne");
　 var context = theCanvas.getContext("2d");
　 var formElement = document.getElementById("textBox");
　 formElement.addEventListener("keyup", textBoxChanged, false);
　 formElement = document.getElementById("fillOrStroke");
　 formElement.addEventListener("change", fillOrStrokeChanged, false);
　 formElement = document.getElementById("textSize");
　 formElement.addEventListener("change", textSizeChanged, false);
　 formElement = document.getElementById("textFillColor");
　 formElement.addEventListener("change", textFillColorChanged, false);
　 formElement = document.getElementById("textFont");
　 formElement.addEventListener("change", textFontChanged, false);
　 formElement = document.getElementById("textBaseline");
　 formElement.addEventListener("change", textBaselineChanged, false);
　 formElement = document.getElementById("textAlign");
　 formElement.addEventListener("change", textAlignChanged, false);
　 formElement = document.getElementById("fontWeight");
　 formElement.addEventListener("change", fontWeightChanged, false);
　 formElement = document.getElementById("fontStyle");
　 formElement.addEventListener("change", fontStyleChanged, false);
　 formElement = document.getElementById("shadowX");
　 formElement.addEventListener("change", shadowXChanged, false);
　 formElement = document.getElementById("shadowY");
　 formElement.addEventListener("change", shadowYChanged, false);
　 formElement = document.getElementById("shadowBlur");
　 formElement.addEventListener("change", shadowBlurChanged, false);
　 formElement = document.getElementById("shadowColor");
　 formElement.addEventListener("change", shadowColorChanged, false);
　 formElement = document.getElementById("textAlpha");
　 formElement.addEventListener("change", textAlphaChanged, false);
　 formElement = document.getElementById("textFillColor2");
　 formElement.addEventListener("change", textFillColor2Changed, false);
　 formElement = document.getElementById("fillType");
　 formElement.addEventListener("change", fillTypeChanged, false);
　 formElement = document.getElementById("canvasWidth");
　 formElement.addEventListener("change", canvasWidthChanged, false);
　 formElement = document.getElementById("canvasHeight");
　 formElement.addEventListener("change", canvasHeightChanged, false);
　 formElement = document.getElementById("canvasStyleWidth");
　 formElement.addEventListener("change", canvasStyleSizeChanged, false);
　 formElement = document.getElementById("canvasStyleHeight");
　 formElement.addEventListener("change", canvasStyleSizeChanged, false);
　 formElement = document.getElementById("createImageData");
　 formElement.addEventListener("click", createImageDataPressed, false);
　 pattern.src = "texture.jpg";
　 drawScreen();
　 function drawScreen() {
　　 //背景
　　　context.globalAlpha = 1;
　　　context.shadowColor = "#707070";
　　　context.shadowOffsetX = 0;
　　　context.shadowOffsetY = 0;
　　　context.shadowBlur = 0;
　　　context.fillStyle = "#ffffaa";
　　　context.fillRect(0, 0, theCanvas.width, theCanvas.height);
　　　//边框
　　　context.strokeStyle = "#000000";
　　　context.strokeRect(5, 5, theCanvas.width-10, theCanvas.height-10);
　　　//文本
　　　context.textBaseline = textBaseline;
　　　context.textAlign = textAlign;
　　　context.font = fontWeight + " " + fontStyle + " " + fontSize + "px " + fontFace;
　　　context.shadowColor = shadowColor;
　　　context.shadowOffsetX = shadowX;
　　　context.shadowOffsetY = shadowY;
　　　context.shadowBlur = shadowBlur;
　　　context.globalAlpha = textAlpha;
　　　var xPosition = (theCanvas.width/2);
　　　var yPosition = (theCanvas.height/2);
　　　var metrics = context.measureText(message);
　　　var textWidth = metrics.width;
　　　var tempColor;
　　　if (fillType == "colorFill") {
　　　　 tempColor = textFillColor;
　　　} else if (fillType == "linearGradient") {
　　　　 var gradient = context.createLinearGradient(xPositiontextWidth/
　　　　　　2, yPosition, textWidth, yPosition);
　　　　 gradient.addColorStop(0,textFillColor);
　　　　 gradient.addColorStop(.6,textFillColor2);
　　　　 tempColor = gradient;
　　　} else if (fillType == "radialGradient") {
　　　　 var gradient = context.createRadialGradient(xPosition, yPosition,
　　　　　　 fontSize, xPosition+textWidth, yPosition, 1);
　　　　 gradient.addColorStop(0,textFillColor);
　　　　 gradient.addColorStop(.6,textFillColor2);
　　　　 tempColor = gradient;
　　　} else if (fillType == "pattern") {
　　　　 var tempColor = context.createPattern(pattern,"repeat")
　　　} else {
　　　　 tempColor = textFillColor;
　　　}
　　　switch(fillOrStroke) {
　　　　 case "fill":
　　　　　　context.fillStyle = tempColor;
　　　　　　　　context.fillText (message, xPosition,yPosition);
　　　　　　break;
　　　　 case "stroke":
　　　　　　context.strokeStyle = tempColor;
　　　　　　context.strokeText (message, xPosition,yPosition);
　　　　　　break;
　　　　 case "both":
　　　　　　context.fillStyle = tempColor;
　　　　　　　　context.fillText (message, xPosition,yPosition);
　　　　　　context.strokeStyle = "#000000";
　　　　　　context.strokeText (message, xPosition,yPosition);
　　　　　　break;
　　　}
　 }
　 function textBoxChanged(e) {
　　　var target = e.target;
　　　message = target.value;
　　　drawScreen();
　 }
　 function textBaselineChanged(e) {
　　　var target = e.target;
　　　textBaseline = target.value;
　　　drawScreen();
　 }
　 function textAlignChanged(e) {
　　　var target = e.target;
　　　textAlign = target.value;
　　　drawScreen();
　 }
　 function fillOrStrokeChanged(e) {
　　　var target = e.target;
　　　fillOrStroke = target.value;
　　　drawScreen();
　 }
　 function textSizeChanged(e) {
　　　var target = e.target;
　　　fontSize = target.value;
　　　drawScreen();
　 }
　 function textFillColorChanged(e) {
　　　var target = e.target;
　　　textFillColor = "#" + target.value;
　　　drawScreen();
　 }
　 function textFontChanged(e) {
　　　var target = e.target;
　　　fontFace = target.value;
　　　drawScreen();
　 }
　 function fontWeightChanged(e) {
　　　var target = e.target;
　　　fontWeight = target.value;
　　　drawScreen();
　 }
　 function fontStyleChanged(e) {
　　　var target = e.target;
　　　fontStyle = target.value;
　　　drawScreen();
　 }
　 function shadowXChanged(e) {
　　　var target = e.target;
　　　shadowX = target.value;
　　　drawScreen();
　 }
　 function shadowYChanged(e) {
　　　var target = e.target;
　　　shadowY = target.value;
　　　drawScreen();
　 }
　 function shadowBlurChanged(e) {
　　　var target = e.target;
　　　shadowBlur = target.value;
　　　drawScreen();
　 }
　 function shadowColorChanged(e) {
　　　var target = e.target;
　　　shadowColor = target.value;
　　　drawScreen();
　 }
　 function textAlphaChanged(e) {
　　　var target = e.target;
　　　textAlpha = (target.value);
　　　drawScreen();
　 }
　 function textFillColor2Changed(e) {
　　　var target = e.target;
　　　textFillColor2 = "#" + target.value;
　　　drawScreen();
　 }
　 function fillTypeChanged(e) {
　　　var target = e.target;
　　　fillType = target.value;
　　　drawScreen();
　 }
　 function canvasWidthChanged(e) {
　　　var target = e.target;
　　　theCanvas.width = target.value;
　　　drawScreen();
　 }
　 function canvasHeightChanged(e) {
　　　var target = e.target;
　　　theCanvas.height = target.value;
　　　drawScreen();
　 }
　 function canvasStyleSizeChanged(e) {
　　　var styleWidth = document.getElementById("canvasStyleWidth");
　　　var styleHeight = document.getElementById("canvasStyleHeight");
　　　var styleValue = "width:" + styleWidth.value + "px; height:" +
　　　　　styleHeight.value +"px;";
　　　theCanvas.setAttribute("style", styleValue );
　　　drawScreen();
　 }
　 function createImageDataPressed(e) {
　　　var imageDataDisplay = document.getElementById("imageDataDisplay");
　　　imageDataDisplay.value = theCanvas.toDataURL();
　　　window.open(imageDataDisplay.value,"canvasImage","left=0,top=0,width=" +
　　　　 theCanvas.width + ",height=" + theCanvas.height +
　　　　 ",toolbar=0,resizable=0");
　 }
}
</script>
</head>
<body>
<div style="position: absolute; top: 50px; left: 50px;">
<canvas id="canvasOne" width="500" height="300">
 Your browser does not support HTML5 Canvas.
</canvas>
<form>
　Text: <input id="textBox" placeholder="your text" />
　<br>
　Text Font: <select id="textFont">
　<option value="serif">serif</option>
　<option value="sans-serif">sans-serif</option>
　<option value="cursive">cursive</option>
　<option value="fantasy">fantasy</option>
　<option value="monospace">monospace</option>
　</select>
　<br>Font Weight:
 <select id="fontWeight">
 <option value="normal">normal</option>
 <option value="bold">bold</option>
 <option value="bolder">bolder</option>
 <option value="lighter">lighter</option>
 </select>
 <br>
 Font Style:
 <select id="fontStyle">
 <option value="normal">normal</option>
 <option value="italic">italic</option>
 <option value="oblique">oblique</option>
 </select>
 <br>
 Text Size: <input type="range" id="textSize"
　　　 min="0"
　　　 max="200"
　　　 step="1"
　　　 value="50"/>
　<br>
　Fill Type: <select id="fillType">
　<option value="colorFill">Color Fill</option>
　<option value="linearGradient">Linear Gradient</option>
　<option value="radialGradient">Radial Gradient</option>
　<option value="pattern">pattern</option>
　</select>
　<br>
　Text Color: <input class="color" id="textFillColor" value="FF0000"/>
　<br>
　Text Color 2: <input class="color" id="textFillColor2" value ="000000"/>
　<br>
　Fill Or Stroke: <select id="fillOrStroke">
　<option value="fill">fill</option>
　<option value="stroke">stroke</option>
　<option value="both">both</option>
　</select>
　<br>
　Text Baseline <select id="textBaseline">
　<option value="middle">middle</option>
　<option value="top">top</option>
　<option value="hanging">hanging</option>
　<option value="alphabetic">alphabetic</option>
　<option value="ideographic">ideographic</option>
　<option value="bottom">bottom</option>
　</select>
　<br>
　Text Align <select id="textAlign">
　<option value="center">center</option>
　<option value="start">start</option>
　<option value="end">end</option>
　<option value="left">left</option>
　<option value="right">right</option>
　</select>
<br>
Alpha: <input type="range" id="textAlpha"
　　　min="0.0"
　　　max="1.0"
　　　step="0.01"
　　　value="1.0"/>
<br>
Shadow X:<input type="range" id="shadowX"
　　　min="-100"
　　　max="100"
　　　step="1"
　　　value="1"/>
<br>
Shadow Y:<input type="range" id="shadowY"
　　　min="-100"
　　　max="100"
　　　step="1"
　　　value="1"/>
<br>
Shadow Blur: <input type="range" id="shadowBlur"
　　　min="1"
　　　max="100"
　　　step="1"
　　　value="1" />
<br>
Shadow Color: <input class="color" id="shadowColor" value="707070"/>
<br>
Canvas Width: <input type="range" id="canvasWidth"
　　　min="0"
　　　max="1000"
　　　step="1"
　　　value="500"/>
<br>
Canvas Height:
<input type="range" id="canvasHeight"
　　　min="0"
　　　max="1000"
　　　step="1"
　　　value="300"/>
<br>
Canvas Style Width: <input type="range" id="canvasStyleWidth"
　　　min="0"
　　　max="1000"
　　　step="1"
　　　value="500"/>
<br>
Canvas Style Height:
<input type="range" id="canvasStyleHeight"
　　　min="0"
　　　max="1000"
　　　step="1"
　　　value="300"/>
<br>
<input type="button" id="createImageData" value="Create Image Data">
<br>
<br>
<textarea id="imageDataDisplay" rows=10 cols=30></textarea>
</form>
</div>
</body>
</html>
```

