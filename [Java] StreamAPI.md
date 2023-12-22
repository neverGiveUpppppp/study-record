## 1.스트림 생성

.stream() : 컬렉션을 stream으로 변환

<br>

## 2.중개연산

.map() : 각 요소에 대해 주어진 함수를 적용하여 새로운 요소를 생성하는 연산을 수행

.filter() : 특정 요소 search

참고자료 : 쉬운 필터 이해 [https://isntyet.github.io/java/java-stream-정리(filter)/](https://isntyet.github.io/java/java-stream-%EC%A0%95%EB%A6%AC(filter)/)

<br>

## 3.최종연산

.collect() : 스트림의 요소를 하나의 결과로 모으는 최종 연산수행

.count() : 요소의 개수 계산

.min() : 요소의 최소값 뽑아내기

.max() : 요소의 최대값 뽑아내기

.forEach() : 모든 요소에 대해 특정동작 반복 수행

.reduce() : 초기값과 BinaryOperator(두 개의 인수를 받아 하나의 값을 반환하는 함수)를 이용하여 스트림의 요소들을 반복적으로 조합




- collect()
    
    1. 주요 Collectors 클래스의 메서드:
    
    - Collectors.toList(): 리스트로 결과를 모음.
    - Collectors.toSet(): 집합(Set)으로 결과를 모음.
    - Collectors.toMap(): 맵(Map)으로 결과를 모음.
    - Collectors.joining(): 문자열로 결과를 모음.
    - Collectors.groupingBy(): 그룹핑하여 맵으로 결과를 모음.
    - Collectors.partitioningBy(): 분할하여 맵으로 결과를 모음.
    - 등...
    
    3. 커스텀 컬렉터:
    
    - Collector 인터페이스를 구현하여 사용자 정의 컬렉터를 만들 수 있습니다. 이는 상당히 강력하며 복잡한 로직을 적용할 수 있도록 합니다.
    
    예를 들어, 스트림의 요소를 쉼표로 구분된 문자열로 모으는 경우:
    
    ```java
    javaCopy code
    String result = list.stream()
            .collect(Collectors.joining(", "));
    
    ```
    
    **`joining()`** 메서드는 문자열로 결과를 모으는데, 각 요소를 쉼표로 구분하여 하나의 문자열로 만듭니다. 여러 형태의 컬렉터를 사용하여 스트림의 결과를 적절한 형태로 모으는 것은 스트림 API의 강력한 기능 중 하나입니다.
    
