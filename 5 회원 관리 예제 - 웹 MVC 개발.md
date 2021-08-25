# 5 회원 관리 예제 - 웹 MVC 개발

## 회원 웹 기능 - 홈 화면 추가 

* `@GetMapping("/")` 
  * localhost:8080/ 들어오면 (더 붙는 주소 없이 `/`만.) 어노테이션으로 표시한 함수를 호출하라.
* 컨트롤러가 정적 파일보다 호출 우선 순위가 높다. 따라서 예제에서 겟매핑 써서 홈컨트롤러를 만들면, `index/html`은 무시되고 홈컨트롤러가 호출된다.

## 회원 웹 기능 - 등록

### 회원 등록 폼 개발

오랜만에 html 폼

submit 누르면 입력된 정보 (name)이 서버의 컨트롤러로 넘어감.

이때 name="name" 이라 지정했는데, 이 "name"이 컨트롤러에서 다루는 데에 있어 중요하니 기억해둔다.

* `return "redirect:/"` form 생성 완료 후, 홈 화면으로 리다이렉트.
* 겟매핑과 포스트매핑 (아래 참고)

## 회원 웹 기능 - 조회

* thymeleaf의 사용

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
    
<div class="container">
	<div>
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>이름</th>
                </tr>
            </thead>
            <tbody>
			<tr th:each="member : ${members}">
					<td th:text="${member.id}"></td>
					<td th:text="${member.name}"></td>
			</tr>
			</tbody>
		</table>
	</div>
    
</div> <!-- /container -->
    
</body>
</html>
```

이걸 돌려서 페이지의 소스 보기를 하면, 등록된 member 수만큼 tr이 들어가있는 걸 확인할 수 있다. thymeleaf 엔진이 결과물을 렌더링하여 뿌려주었기 때문이다.



지금까지 연결한 방식은 자바 메모리에 데이터를 저장하는 방식이다. 따라서 서버를 내렸다가 다시 돌리면 (즉, 자바 어플리케이션을 재시작) 데이터가 사라져 있다.

이걸 이제 보관하기 위해서, 파일이나 데이터베이스와 연동하게 제작한다. 다음 시간부터~!



---

# 겟 매핑, 포스트 매핑

[참고](https://noahlogs.tistory.com/35)

## GET 이란?

Get 방식은, 클라이언트에서 서버로 어떤 리소스로부터, 정보를 요청하기 위해 사용되는 메소드이다.

예: 게시판의 게시물을 조회할 때.

Get 방식의 경우 주소를 직접 전달하며, URL에 `?`와 함께 전달되는 내용이 붙는다.

`www.example.com/show?name1=value1&name2=value2`

예를 들어 이렇게 하면 서버에서는 name1, name2 라는 파라미터에 대해 value1, value2를 전달받을 수 있다.

## POST 란?

POST 방식은 클라이언트에서 서버로 리소스를 생성하거나 업데이트 하기 위해 데이터를 보낼 때 사용되는 메소드이다.

예: 게시판에 게시글을 작성.

Post는 전송할 데이터를 HTTP 메시지 body 부에 담아서 서버로 보낸다.

HTML form에서 폼 결과의 도착지를 전송하는 방식이 post이다.

```html
<form action="/members/new" method="post">
    ...
</form>
```

## GET vs. POST

* get은 넘길 수 있는 길이 제한이 있다. 브라우저마다 다름. post는 길이 제한이 없다.
* get은 데이터가 그대로 URL에 노출되기 때문에 보안 수준이 낮다. post도 암호화하지 않으면 HTTP 메시지에서 확인될 수 있으나, 적어도 대놓고 드러나지는 않는다. 

