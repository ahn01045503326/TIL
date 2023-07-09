# JSTL 개념

JSTL은 JavaServer Pages Standard Tag Library의 약어로, Java 코드를 바로 사용하지 않고 HTML 태그(<>) 형태로 직관적인 코딩을 지원하는 라이브러리입니다. 

어렵게 말하자면, JSTL은 JSP의 확장 태그라고 부릅니다. 일반적으로 HTML 태그만으로는 Java의 forEach 문과 같은 반복문을 사용할 수 없습니다. 

하지만, 아래의 예시 코드의 body 태그를 보시면, Java나 타 프로그래밍 언어처럼, 태그(<>) 안에 쓰임새가 직관적으로 파악되는 반복문을 확인할 수 있습니다. 

이러한 코딩을 지원하는 라이브러리가 JSTL입니다.

````
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>

	<!--jstl 문법: 태그 형식으로 코딩하는 방법(디자이너에게 직관적임)-->
	<c:forEach var ="i" begin = "1" end = "10">
		${i}
	</c:forEach>

</body>
</html>
````

---

### JSTL 장점
````
JSTL은 프로그래밍을 입문한 사람이면 코드의 쓰임새를 직관적으로 이해할 수 있다는 장점이 있습니다. 
즉, 위의 예시 코드에서 보실 수 있듯이, forEach 기반의 반복문이며, 변수는 i로 설정하고, 초기값은 1, 종료값은 10이며 해당 변수를 차례로 화면에 출력하는 코드라는 것을 쉽게 파악할 수 있습니다. 
이러한 장점 덕분에, 개발자가 아닌 HTML/CSS를 다루는 디자이너가 간단한 코드 작업을 쉽게 수행하는 데 효과적입니다.
````

### JSTL 사용방법

1. JSTL을 사용하기 위해서는 JSTL jar 파일과 JSTL 구현체(implementation)를 설치해야 합니다.
2. Tomcat 설치
3. 사용 중이신 OS 사양에 맞춰 톰캣을 설치합니다.
4. 앞서 설치한 JSTL jar 파일은 tomcat 폴더 > lib 폴더 내부로 이동시킵니다.
5. 이클립스 재실행 및 HTML 파일 생성
6. 이클립스를 재실행하고 hmtl 파일을 하나 생성합니다.
7. taglib 선언
8. JSP에서 JSTL을 사용하기 위해서는 Java에서 라이브러리를 Import 하는 것처럼 taglib 지시자로 라이브러리를 선언해야 합니다. JSTL Core 태그 선언문은 아래와 같습니다.

````
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
````

### 예제 코드
````
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<!--JavaServer Pages Standard Tag Library-->
	<!--jstl 문법: 태그 형식으로 코딩하는 방법(디자이너에게 직관적임)-->
	<c:forEach var ="i" begin = "1" end = "10">
		${i}
	</c:forEach>

</body>
</html>
````