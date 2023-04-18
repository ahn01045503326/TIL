# 배열 for문

---
- 배열 내의 모든 값을 순회하는 for문의 향상된 형태
- 배열의 모든 요소를 스캔하는 과정에서 인덱스 자체의 값이 필요하지 않을 때는 확장 for문이 유용함
- 확장 for문은 배열의 리스트를 순회할 때 요소의 값을 변경하지 않고 읽기만 할 때 주로 사용
````
for([배열 자료형][변수명]:[배열명] or [컬렉션 객체명]){
    // 각각의 변수에 적용할 Java Code;
    // 변수는 배열 내의 각각의 값을 뜻함
}
````
### ex) 사용 예시
````
public class ArgTest {

    public static void main(String[] args) {
        int[] arrayTest = new int[10];
        for (int i = 0; i < 10; i++) {
            arrayTest[i] = (i + 1) * 10;
        }

         // 확장 for문
        for(int num:arrayTest) {
            System.out.print(num + "\t");
        }
        // 10    20    30    40    50    60    70    80    90    100    
    }

}
````
