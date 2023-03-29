Fabric.js는 HTML5 캔버스(Canvas)를 사용하여 그래픽 디자인 및 이미지 처리를 쉽게 할 수 있는 오픈 소스 자바스크립트 라이브러리입니다. 아래는 Fabric.js를 사용하여 간단한 원을 그리는 예제입니다.

1. Fabric.js 라이브러리 추가하기
   - Fabric.js 라이브러리를 다운로드하거나 CDN 링크를 추가하여 사용할 수 있습니다.
````
[html]
<script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/4.5.0/fabric.min.js"></script>
````

2. 캔버스(Canvas) 생성하기
````
[html]
<canvas id="myCanvas" width="500" height="500"></canvas>
````

3. Fabric.js 객체 생성하기
````
[JavaScript]
   var canvas = new fabric.Canvas('myCanvas');
````

4. 원 객체 생성하기
````
[JavaScript]
var circle = new fabric.Circle({
  radius: 50,
  fill: 'red',
  left: 100,
  top: 100
});
````

5. 원 객체 캔버스에 추가하기
````
[JavaScript]
canvas.add(circle);
````