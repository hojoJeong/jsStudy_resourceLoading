# Window 객체

1. 브라우저 객체 모델(BOM)이란

##### 자바스크립트를 이용하면 브라우저의 정보에 접근하거나 브라우저의 여러 기능들을 제어할 수 있습니다. 이때 사용할 수 있는 객체 모델이 바로 브라우저 객체 모델(BOM, Browser Object Model)입니다.

2. Window 객체

##### window 객체는 웹 브라우저의 창(window)을 나타내는 객체로, 대부분의 웹 브라우저에서 지원하고 있습니다.   자바스크립트의 모든 객체, 전역 함수, 전역 변수들은 자동으로 window 객체의 프로퍼티가 됩니다.   window 객체의 메소드는 전역 함수이며, window 객체의 프로퍼티는 전역 변수가 됩니다.   문서 객체 모델(DOM)의 요소들도 모두 window 객체의 프로퍼티가 됩니다.

3. 브라우저 창 크기 조절

##### window 객체의 innerHeight와 innerWidth 프로퍼티를 이용하면, 브라우저의 창 크기를 설정할 수 있습니다.   **여기서 브라우저 창이란 웹 브라우저의 뷰포트(viewport)를 의미하며, 브라우저의 툴바나 스크롤 바는 포함되지 않습니다.**

```js
// 기본 문법

window.innerHeight

window.innerWidth

// 익스플로러 5부터 7버전만을 위한 문법 1

document.documentElement.clientHeight

document.documentElement.clientWidth

// 익스플로러 5부터 7버전만을 위한 문법 2

document.body.clientHeight

document.body.clientWidth
```
> window 접두사는 생략 가능!
```js
document.write("현재 브라우저의 수평 위치는 " + screenX + "입니다.<br>"); 

document.write("현재 브라우저의 수평 위치는 " + window.screenY + "입니다.<br>"); // 같은 값을 출력
```

4. 브라우저 새 창 열기

##### window 객체의 open() 메소드를 이용하면, 새로운 브라우저 창을 열 수 있습니다.
##### 또한, 새로운 브라우저 창의 세부적인 옵션들도 일일이 설정할 수 있습니다.
```js
var newWindowObj;

// 변수 strWindowFeatures를 통해 새롭게 여는 브라우저 창의 옵션들을 일일이 설정할 수 있음.

var strWindowFeatures = "menubar = yes,location = yes,resizable = yes,scrollbars = yes,status = yes"; //

function openWindow() {

    newWindowObj = window.open("/html/intro", "HTML 개요", strWindowFeatures);

}
```

5. 브라우저 창 닫기   
###### window 객체의 close() 메소드를 이용하면, 현재 브라우저나 특정 브라우저 창을 닫을 수 있습니다.

```js
function openWindow() {

    newWindowObj = window.open("/html/intro", "HTML 개요", strWindowFeatures);

}

function closeNewWindow() { // 새롭게 연 브라우저 창을 window 객체를 이용하여 다시 닫을 수 있음.

    newWindowObj.close();

}
```