# Resource loading : onload, onerror

***

1. script.onload : script의 로드 이후에 실행되며 앞에서 다루었던 window.load와 같은 개념입니다.
```js
let script = document.createElement('script');

script.src = "https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.3.0/lodash.js"
document.head.append(script);

script.onload = function() { //스크립트가 로드 되었을 때
  alert(_); // alert창을 실행
};
```

***

2. script.onerror : 스크립트 로드 중 에러가 발생했을 때 실행할 수 있습니다. 이는 스크립트 로드가 완전히 실패했을 경우만 작동합니다. 따라서 스크립트는 성공적으로 로드 되었으나 작은 에러를 확인하고 싶을 때에는 window.onerror을 사용해야합니다. 

```js
let img = document.createElement('img');
img.src = "https://js.cx/clipart/train.gif"; // (*)

img.onload = function() {
  alert(`Image loaded, size ${img.width}x${img.height}`);
};

img.onerror = function() {
  alert("Error occurred while loading image");
};
```