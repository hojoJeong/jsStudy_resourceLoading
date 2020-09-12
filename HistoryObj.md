# History 객체

##### history 객체는 브라우저의 히스토리 정보를 문서와 문서 상태 목록으로 저장하는 객체입니다.  
##### 자바스크립트는 사용자의 개인 정보를 보호하기 위해 이 객체에 접근하는 방법을 일부 제한하고 있습니다.

***

1. 브라우저의 히스토리 목록 개수 반환
```js
unction openDocument() {

    location.assign("/javascript/js_bom_history");

}

document.getElementById("text").innerHTML =

"현재 브라우저의 히스토리 목록의 개수는 " + history.length + "개 입니다.";
```

2. 히스토리 목록 접근하기
##### history 객체에는 브라우저의 뒤로 가기와 앞으로 가기 버튼과 같은 동작을 하는 back()과 forward() 메소드를 가지고 있습니다.
##### 또한, go() 메소드를 이용하면 인수로 전달받는 정수만큼 히스토리 목록 사이를 이동할 수도 있습니다.

```js
//goBack() 사용
<button onclick="goBack()">이전 페이지로 가기</button>

...

<script>

    function goBack() {

        window.history.back();

    }

</script>

//go() 사용
<button onclick="go()">이전 페이지로 가기</button>

...

<script>

    function go() {

        window.history.go(-1);

    }

</script>

//goForward() 사용
<button onclick="goForward()">다음 페이지로 가기</button>

...

<script>

    function goForward() {

        window.history.forward();

    }

</script>
```

