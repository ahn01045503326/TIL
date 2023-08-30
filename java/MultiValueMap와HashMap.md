# MultiValueMap 와 HashMap 차이

---

### Map의 종류
````
1. HashMap
2. TreeMap
3. LinkedHashMap
````

### HashMap
````
Map의 기본 형식으로 key : value를 한 쌍으로 데이터를 저장하며 중복된 키가 존재하지 않는다.
Map에 있는 데이터는 키 값을 기준으로 가져온다.
````

### TreeMap
````
HashMap 기능 + 자동 정렬
TreeMap은 데이터가 들어올 때마다 key 값에 따라 자동 정렬된다.
````

### LinkedHashMap
````
HashMap 기능 +  입력 순서 보장
HashMap에 데이터를 C - B - A 순서로 했다면, 나중에 맵에 있는 모든 값을 출력할 때 C - B - A 순으로 출력된다는 보장이 없다.
하지만, LinkedHashMap은 이 문제를 해결해준다.
````

### MultiValueMap
키의 중복이 허용된다.
````
MultiValueMap<String, Integer> mvMap = new LinkedMultiValueMap<>();

mvMap.add("A", 100);
mvMap.add("A", 200);
mvMap.add("A", 300);

List<Integer> a = mvMap.get("A");

for(int data : a) {
    System.out.print(data + " ");	// output : 100 200 300
}
````

위와 같이 A 키의 데이터를 가져올 때 리스트 형태로 반환한다.

````
Map<String, Integer> map = new HashMap<>();

map.add("A", 100);
map.add("A", 200);
map.add("A", 300);

Integer a = map.get("A");
System.out.print(a + " ");	// output : 300
````

같은 로직을 HashMap에 적용하면, HashMap은 중복을 허용하지 않기 때문에 동일한 키 값에 대해 덮어쓰기를 해버린다.

물론, HashMap으로 방법이 아예 없는 것은 아니다.

Map의 Value Type을 List 형태로 잡아버리면 된다. 이는 값을 넣을 때 리스트를 새로 생성해 값을 집어 넣어야 하며, 파라미터 Value 값을 리스트로 감싼 형태로 직관성이 떨어져 MultiValueMap 에 비해 깔끔하지 않다.

````
Map<String, List<Integer>> listMap = new HashMap<>();

List<Integer> list = new ArrayList<>();
list.add(100);
list.add(200);
list.add(300);

listMap.put("A", list);
````
Map을 사용하고 싶은데, 중복된 키로  여러 Value 값을 온전히 저장하고 싶을 때 사용하면 좋다.