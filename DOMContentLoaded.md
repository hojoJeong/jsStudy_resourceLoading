# DOMContentLoaded, load, beforeunload, unload 이벤트

***

HTML 문서의 생명주기엔 다음과 같은 3가지 주요 이벤트가 관여합니다.
* DOMContentLoaded : 브라우저가 HTML을 전부 읽고 DOM 트리를 완성하는 즉시 발생. 이미지 파일('.img')이나 스타일시트 등의 기타 자원은 기다리지 않습니다.
                     DOM이 준비된 것을 확인한 후 원하는 DOM 노드를 찾아 핸들러를 등록해 인터페이스를 초기화할 때 활용
* load : HTML로 DOM 트리를 만드는 게 완성되었을 뿐만 아니라 이미지, 스타일시트 같은 외부 자원도 모두 불러오는 것이 끝났을 때 발생합니다.
         이미지 사이즈를 확인할 때 등. 외부 자원이 로드된 후이기 때문에 스타일이 적용된 상태이므로 화면에 뿌려지는 요소의 실제 크기를 확인할 수 있음
* beforeunload : 사용자가 페이지를 떠날 때 발생합니다.
                 사용자가 사이트를 떠나려 할 때, 변경되지 않은 사항들을 저장했는지 확인시켜줄 때 활용
* unload : 사용자가 페이지를 떠날 때 발생합니다.
           사용자가 진짜 떠나기 전에 사용자 분석 정보를 담은 통계자료를 전송하고자 할 때

>메모리의 생명 주기
>* allocate(메모리 할당) : 프로그램이 사용할 수 있도록 운영체제가 메모리를 할당합니다.
>* use(메모리 사용) : 할당된 메모리를 실제로 프로그램이 사용하는 단계입니다. 개발자가 코드 상에서 할당된 변수를 사용함으로써 읽기와 쓰기 작업이 이루어집니다.
>* release(메모리 사용) : 프로그램에서 필요하지 않은 메모리 전체를 되돌려주어 다시 사용가능하게 만드는 단계입니다. 
>참고 : <https://engineering.huiseoul.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EA%B0%80-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC-4%EA%B0%80%EC%A7%80-%ED%9D%94%ED%95%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-%EB%8C%80%EC%B2%98%EB%B2%95-5b0d217d788d>

***

1. DOMContentLoaded

* DOMContentLoaded 이벤트는 document 객체에서 발생합니다. 따라서 이 이벤트를 다루려면 addEventListener를 사용해야 합니다.
```js
<script>
  function ready() {
    alert('DOM이 준비되었습니다!');
    // 이미지가 로드되지 않은 상태이기 때문에 사이즈는 0x0입니다.
    alert(`이미지 사이즈: ${img.offsetWidth}x${img.offsetHeight}`);
  }
  document.addEventListener("DOMContentLoaded", ready);
</script>

<img id="img" src="https://en.js.cx/clipart/train.gif?speed=1&cache=0">
```
* 브라우저는 HTML 문서를 처리하는 도중에 <script> 태그를 만나면, DOM 트리 구성을 멈추고 <script>를 실행하기 때문에 DOMContentLoaded 이벤트 역시 <script> 안에있는 스크립트가 처리고 난 후에 발생합니다.
```js
<script>
  document.addEventListener("DOMContentLoaded", () => {
    alert("DOM이 준비되었습니다!");
  });
</script> //3

<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.3.0/lodash.js"></script> //1

<script>
  alert("라이브러리 로딩이 끝나고 인라인 스크립트가 실행되었습니다."); //2
</script>
```

***

2. window.onload : window 객체의 load 이벤트는 **스타일, 이미지 등의 리소스들이 모두 로드되었을 때** 실행됩니다. load 이벤트는 onload 프로퍼티를 통해서도 사용할 수 있습니다. (DomContentLoaded와 차이점 주의!)
```js
<script>
  window.onload = function() { // window.addEventListener('load', (event) => {와 동일합니다.
    alert('페이지 전체가 로드되었습니다.');
    // 이번엔 이미지가 제대로 불러와 진 후에 얼럿창이 실행됩니다.
    alert(`이미지 사이즈: ${img.offsetWidth}x${img.offsetHeight}`);
  };
</script>

<img id="img" src="https://en.js.cx/clipart/train.gif?speed=1&cache=0">
```

3. window.onunload : window 객체의 unload 이벤트는 사용자가 페이지를 떠날 때, 즉 문서를 완전히 닫을 때 실행됩니다. unload 이벤트에선 팝업창을 닫는 것과 같은 딜레이가 없는 작업을 수행할 수 있습니다.
```js
let analyticsData = { /* 분석 정보가 담긴 객체 */ };

window.addEventListener("unload", function() {
  navigator.sendBeacon("/analytics", JSON.stringify(analyticsData));
};
```
>navigator.sendBeacon(url, data) : unload가 페이지를 떠날 때 실행되는 점을 활용한 메서드로, 다른페이지로 전환 시 데이터(64kb이하)를 백그라운드에서 전송하며 서버로 전송되기 떄문에 딜레이가 없습니다.

***

4. window.onbeforeunload : 사용자가 현재 페이지를 떠나려할 때 추가확인요청을 할 수 있으며, beforeunload 이벤트를 *취소*하려하면 브라우저는 사용자에게 확인 요청을 실행합니다.
```js
window.onbeforeunload = function() {
  return false;
};
```
>alert 창의 메시지은 beforeunload 남용을 방지하기 위해 커스터마이징 할 수 없음

***

5. readyState : 현재 로딩 상태를 알려주며 document.readyState프로퍼티를 사용합니다. 프로퍼티 값은 다음과 같은 세 종류가 있습니다.
* loading : 문서를 불러오는 중일 때
* interactive : 문서가 완전히 불러와졌을 때
* complete : 문서를 비롯한 이미지 등의 리소스들도 모두 불러와졌을 때
```js
function work() { /*...*/ }

if (document.readyState == 'loading') {
  // 아직 로딩 중이므로 이벤트를 기다립니다.
  document.addEventListener('DOMContentLoaded', work);
} else {
  // DOM이 완성되었습니다!
  work();
}
```

*readyStatechange는 상태가 변경되었을 때 실행
```js
// 현재 상태
console.log(document.readyState);

// 상태 변경 출력
document.addEventListener('readystatechange', () => console.log(document.readyState));
```
