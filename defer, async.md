# defer, async 스크립트

***

1. defer : 브라우저는 defer속성이 있는 스크립트 즉, 지연스크립트를 백그라운드에서 다운로드합니다. 따라서 지연 스크립트를 다운로드 하는 도중에도 HTML 파싱이 멈추지 않습니다. 
```js
<p>...스크립트 앞 콘텐츠...</p> //3

<script>
  document.addEventListener('DOMContentLoaded', () => alert("`defer` 스크립트가 실행된 후, DOM이 준비되었습니다!")); // 2
</script>

<script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script> //1

<p>...스크립트 뒤 콘텐츠...</p> //3
```
> 지연 스크립트는 페이지 생성을 절대 막지 않습니다.
>DOMContentLoaded 이벤트는 지연 스크립트 실행을 기다립니다. 따라서 얼럿창은 DOM 트리가 완성되고 지연 스크립트가 실행된 후에 뜹니다.

지연 스크립트는 HTML에 추가된 순으로 실행됩니다. 따라서 긴 스크립트가 앞에, 짧은 스크립트가 뒤에 있어도 다운로드는 작은 스크립트가 먼저 되지만 실행은 앞에 위치한 긴 스크립트가 먼저 됩니다.

>defer속성은 외부 스크립트(src)에만 유효합니다.

***

2. async : async속성의 스크립트는 페이지와 완전히 독립적으로 작동합니다. defer스크립트와 마찬가지로 백그라운드에서 다운로드 됩니다.

* DOMContentLoaded 이벤트를 포함하여 다른 스크립트들은 async스크립트를 기다리지 않습니다. 따라서 async스크립트의 실행 순서는 제각각이 됩니다. 실행은 다운로드가 끝난 순으로 진행됩니다.

```js
<script>
  document.addEventListener('DOMContentLoaded', () => alert("DOM이 준비 되었습니다!"));
</script>

<script async src="https://javascript.info/article/script-async-defer/long.js"></script> //2
<script async src="https://javascript.info/article/script-async-defer/small.js"></script> //1
```

***

3. 동적 스크립트 : 동적스크립트는 async스크립트처럼 행동하지만 script.async=false 를 삽입해주면 load-first order로 실행되지 않고 문서에 추가된 순서대로 실행됩니다.
```js
function loadScript(src) {
  let script = document.createElement('script');
  script.src = src;
  script.async = false;
  document.body.append(script);
}

// async=false이기 때문에 long.js가 먼저 실행됩니다.
loadScript("/article/script-async-defer/long.js");
loadScript("/article/script-async-defer/small.js");
```