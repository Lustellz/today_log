자료구조: 효율적으로 데이터를 관리할 수 있는 알고리즘

List: 순서가 존재, 중복을 허용(ArrayList - 전체 순회할 때/나 LinkedList - 수정과 삭제가 계속해서 발생할 때/로 객체 생성)

Map: key-value의 쌍, 순서 없음(LinkedList로 객체 생성)

Set: 중복을 허용하지 않음, 순서 없음(LinkedList로 객체 생성)

자료구조의 생성: `<Generic Type>`을 지정해야 함

출력: for문으로 전체를 순회하며 get하기, 향상된 for문으로 `for(i : List)`, `iterator().next()`

정렬: Comparable(정렬하고 싶을 때 Interface를 implement하여 compareTo 메서드를 overriding 해야 함), Comparator