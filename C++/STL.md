# 표준 템플릿 라이브러리(STL: Standard Template Library)

<br/>

C++의 STL(Standard Template Library)은 크게 4가지 핵심 구성 요소로 나뉜다. 데이터를 담는 그릇인 `컨테이너`, 이를 조작하는 `알고리즘`, 그리고 둘을 이어주는 `반복자` 등이 유기적으로 연결되어 있다.

<br/>

## 컨테이너 (Containers)
데이터를 저장하는 객체로, 구조에 따라 세 가지로 분류된다.

### 시퀀스 컨테이너 (Sequence Containers) 
데이터를 선형적인 순서로 저장한다.

`vector`: 동적 배열. 뒤쪽에서 삽입/삭제가 빠르지만 중간 삽입은 느리다.   
`deque`: Double-Ended Queue. 앞뒤 양쪽에서 삽입/삭제가 가능하다.   
`list`: 이중 연결 리스트. 어느 위치에서든 삽입/삭제가 빠르지만 탐색은 느리다.   
`forward_list`: 단방향 연결 리스트 (C++11) 메모리 사용량이 적다.   
`array`: 고정 크기 배열 (C++11)   

### 연관 컨테이너 (Associative Containers)   
데이터를 정렬된 상태로 유지하며, '키(Key)'를 사용해 빠르게 검색한다.(보통 Red-Black Tree 구조)   

`set`: 중복되지 않는 키들의 집합이다.   
`multiset`: 키의 중복을 허용하는 set   
`map`: 키와 값(Value)의 쌍으로 이루어진 집합이다. 키는 중복될 수 없다.   
`multimap`: 키의 중복을 허용하는 map   

### 무순서 연관 컨테이너 (Unordered Associative Containers)   
해시 테이블을 사용하여 순서 없이 데이터를 저장한다. (C++11 추가)

`unordered_set`, `unordered_multiset`, `unordered_map`, `unordered_multimap`   

<br/>

## 반복자 (Iterators)
컨테이너의 원소에 접근하기 위한 포인터와 유사한 객체다.   
알고리즘이 컨테이너의 종류에 상관없이 동작할 수 있게 해주는 "다리" 역할을 한다.

입력/출력 반복자: 읽기 또는 쓰기 전용   
순방향/양방향 반복자: 앞으로 또는 앞뒤로 이동 가능   
임의 접근 반복자 (Random Access): +, - 연산을 통해 원하는 위치로 즉시 점프 가능 (vector, deque 등)   

## 알고리즘 (Algorithms)
컨테이너의 데이터를 처리하는 약 100여 개의 함수다. `<algorithm>` 헤더를 포함해야 한다.

정렬: `sort()`, `stable_sort()`, `partial_sort()`   
탐색: `find()`, `binary_search()`, `lower_bound()`   
수정: `copy()`, `swap()`, `replace()`, `fill()`   
제거: `remove()`, `unique()`   
개수 및 합계: `count()`, `accumulate()` (accumulate는 `<numeric>`에 있음)

<br/>

## 함수 객체 (Function Objects / Functors)
함수처럼 호출할 수 있는 객체다.   
알고리즘의 동작을 사용자 정의할 때 주로 사용한다.

`less<T>`, `greater<T>`: 크기 비교 시 사용.   
`plus<T>`, `minus<T>`: 산술 연산 시 사용.

**<참고사항>**   
`컨테이너 어댑터(Container Adapters)`   
특정 컨테이너를 변형하여 제한된 기능만 제공하는 클래스들입니다.

`stack`: LIFO (Last-In-First-Out) 구조   
`queue`: FIFO (First-In-First-Out) 구조   
`priority_queue`: 우선순위가 높은 데이터가 먼저 나오는 구조(내부적으로 힙 정렬 사용)   

<br/>

***

<br/>

### STL관련 팁들

unique()   
연속된 중복 요소들을 제거한다. 단, 실제로 제거하는건 아니고 중복되는 원소를 뒤로 다 밀어넣는다.(실제 반환값은 뒤로 밀려진 중복값중 첫번째 위치)   
따라서, erase()를 함께 써야 실제로 지워진다.   

```cpp
//erase(), unique()예시
#include <vector>
#include <algorithm> // sort, unique를 위해 선언

using namespace std;

bool compare(int a, int b) { // 정렬 기준 정의
    return a > b; 
}

vector<int> solution(vector<int> lst) {
    sort(lst.begin(), lst.end(), compare); // 내림차순으로 정렬
    lst.erase(unique(lst.begin(), lst.end()), lst.end()); // 중복값 제거

    return lst;
}
```

<br/>

***

<br/>

벡터로 변환
```cpp
// sum은 set<int>
vector<int> answer(sum.begin(), sum.end()); // 반환타입을 맞추기 위헤 벡터로 변환
```

