# 컬렉션 프레임워크

다수의 데이터를 쉽고 효과적으로 관리할 수 있는 표준화된 방법을 제공하는 클래스의 집합을 의미합니다.

자바 컬렉션에는 List, Set, Map 인터페이스를 기준으로 여러 구현체가 존재하고, 이에 더해 Stack, Queue 인터페이스도 존재합니다.

---

### List, Set, Map, Stack, Queue
````
List는 순서가 있는 데이터의 집합이며, 데이터의 중복을 허용합니다. 대표적인 구현체로는 ArrayList가 있고, 이는 Vector를 개선한 것입니다. 이외에도 LinkedList 등의 구현체가 있습니다.
 - Vector, ArrayList, LinkedList, Stack, Queue

Set은 순서가 없는 데이터의 집합이며, 데이터의 중복을 허용하지 않습니다. 대표적인 구현체로는 HashSet이 있고, 순서를 보장하기 위해서는 LinkedHashSet을 사용합니다. (Map의 key-value 구조에서 key 대신 value가 들어가 value를 key로 하는 자료구조)
 - HashSet, LinkedHashSet, TreeSet

Map은 키와 값이 한 쌍으로 이뤄져 있고, 키를 기준으로 중복을 허용하지 않으며, 순서가 없습니다. key의 순서를 보장하기 위해서는 LinkedHashMap을 사용합니다.
 - HashMap, TreeMap, HashTable, Properties

Stack 객체는 직접 new 키워드로 사용할 수 있으며, Queue 인터페이스는 LinkedList에 new 키워드를 적용해 사용할 수 있습니다.
````