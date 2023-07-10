# Vue.js
- 프론트엔드 개발을 쉽게하기 위한 react와 함께 대중적인 오픈소스 javascript 프레임워크
- MVVM패턴의 ViewModel에 해당하여, UI코드와 데이터제어 제어 로직을 분리
- SPA(Single Page Application)를 구축하는데 이용 가능

![Vue](/image/vue.png)

---

````
View(html DOM): 사용자에게 보이는 화면.
Model(JS): 데이터를 담는 용기, 보통 서버에서 가져온 데이터를 javascript 객체로 저장
ViewModel: View와 Model의 중간 영역으로 DomListener와 DataBinding을 제공하는 영역
DOM: HTML 문서에 들어가는 요소(tag, class, attribute 등)의 정보를 담고 있는 데이터 트리
DOM Listener: DOM의 변경에 대한 즉각적으로 반응하여 특정 로직을 수행하는 장치
Data Binding: View에 표시되는 내용과 모델의 데이터를 동기화
- Vue에서는 기본적으로 단방향 데이터바인딩으로 컴포넌트간 통신은 상위 컴포넌트->하위컴포넌트로 전달
````

### Vue.js 장점

````
1. 배우기 쉽다
2. React, Angular에 비해 가볍고 성능이 빠름
3. React(Virtual DOM), Angular(데이터 바인딩)의 장점을 취했음
4. 컴포넌트 기반 프레임워크로 레고 블록과 같이 컴포넌트 조합으로 뷰 구성, 코드 재사용 쉬움

Virtual DOM
- 화면에 변화가 있을 때마다 실시간으로 DOM Tree 를 수정하지 않고 변경사항이 반영된 Virtual DOM을 이용해 메모리에서 처리하고 한 번만 DOM 수정을 한다. 
- 결과적으로 브라우저는 한번만 렌더링을 하게 됨으로써 불필요한 렌더링 횟수를 줄여 렌더링 성능을 높인다
````