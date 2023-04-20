# Trim()
 - JavaScript에서 문자열 양쪽의 공백(스페이스)을 제거하려면 trim() 함수를 사용하면 됩니다.
---
예를 들어, 아래와 같이 문자열 변수 str에 공백이 포함된 문자열이 들어 있다고 가정해보겠습니다.
````
let str = "  hello world   ";
````
이 경우, trim() 함수를 사용하여 문자열 양쪽의 공백을 제거할 수 있습니다.
````
let trimmedStr = str.trim();
console.log(trimmedStr); // "hello world"
````
위 코드에서 trim() 함수를 호출한 결과, 문자열 " hello world "의 양쪽 공백이 제거된 "hello world" 문자열이 반환됩니다.
