- jQuery를 사용하여 input 요소를 비활성화(disabled)시키는 방법

````
// id가 myInput인 input 요소를 선택하고 disabled 속성을 true로 설정합니다.
$('#myInput').prop('disabled', true);
````

- input 요소를 활성화시키려면 prop('disabled', false)로 설정

````
// id가 myInput인 input 요소를 선택하고 disabled 속성을 false로 설정하여 활성화시킵니다.
$('#myInput').prop('disabled', false);
````