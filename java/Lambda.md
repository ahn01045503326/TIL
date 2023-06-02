# Lambda expression

---

````
(매개변수) -> 메서드 본문
````

````
// 메서드 본문의 중괄호 생략
(x, y) -> x + y;

// 메서드 본문의 중괄호 추가
(x, y) -> {
  // 함수형 인터페이스의 추상 메서드 반환 타입이 void가 아닌 경우 return문 작성
  return x + y;
};
````

````
FunctionInterface lambdaExistsBracket = (x, y) -> x + y;

````