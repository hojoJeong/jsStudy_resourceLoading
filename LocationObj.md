# Location 객체

##### location 객체는 현재 브라우저에 표시된 HTML 문서의 주소를 얻거나, 브라우저에 새 문서를 불러올 때 사용할 수 있습니다.   
##### 이 객체는 Window 객체의 location 프로퍼티와 Document 객체의 location 프로퍼티에 같이 연결되어 있습니다.
##### location 객체의 프로퍼티와 메소드를 이용하면, 현재 문서의 URL 주소를 다양하게 해석하여 처리할 수 있습니다.

***

1. 현재 문서의 URL 주소를 문자열로 반환

```js
document.write("현재 문서의 주소는 " + location.href + "입니다.");
```

2. 현재 문서의 호스트 이름을 반환
```js
document.write("현재 문서의 호스트 이름은 " + location.hostname + "입니다.");
```

3. 현재 문서 파일의 경로명을 반환
```js
document.write("현재 문서의 파일 경로명은 " + location.pathname + "입니다.");
```
> 호스트 이름(host name)과 파일 경로명(path name)을 합쳐 URL(Uniform Resource Locator)이라고 부릅니다.

4. 현재 창에 문서 불러오기
```js
	<p>아래 버튼을 눌러 새로운 문서를 연 후에 브라우저의 뒤로 가기 버튼을 눌러보세요!</p>
	<button onclick="openDocument()">새로운 문서 열기</button>
	<button onclick="openDocumentWithReplace()">이전 문서 삭제 후 새로운 문서 열기</button>
	
	<script>
		function openDocument() {
			location.assign("/index.php");
		}
		function openDocumentWithReplace() {
			location.replace("/index.php");
		}
	</script>
```
> 현재 문서를 브라우저의 히스토리에서 제거한다는 의미는 브라우저의 뒤로 가기 버튼을 눌러도 이전 페이지로 다시 돌아갈 수 없다는 의미입니다.

