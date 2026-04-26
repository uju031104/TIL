# Basic_Algorithm_STL

<br/>

### 시간복잡도와 알고리즘

`시간복잡도` : 입력크기(n)가 커질 때, 연산 횟수가 얼마나 증가하는지를 나타낸다.    
`알고리즘` : 문제를 해결하기 위한 절차나 규칙의 집합    
-> 입력/출력/명확성/유한성/효율성을 가지고 있어야 알고리즘 취급    


### 표준 템플릿 라이브러리(STL: Standard Template Library)

<br/>

C++의 STL(Standard Template Library)은 크게 4가지 핵심 구성 요소로 나뉜다.   
데이터를 담는 그릇인 `컨테이너`, 이를 조작하는 `알고리즘`, 그리고 둘을 이어주는 `반복자` 등이 유기적으로 연결되어 있다.

<br/>

## 컨테이너 (Containers)
데이터를 저장하는 객체로, 구조에 따라 세 가지로 분류된다.   

<br/>

### 시퀀스 컨테이너 (Sequence Containers) 
데이터를 선형적인 순서로 저장한다.

`vector`: 동적 배열. 뒤쪽에서 삽입/삭제가 빠르지만 중간 삽입은 느리다.   
`deque`: Double-Ended Queue. 앞뒤 양쪽에서 삽입/삭제가 가능하다.   
`list`: 이중 연결 리스트. 어느 위치에서든 삽입/삭제가 빠르지만 탐색은 느리다.   
`forward_list`: 단방향 연결 리스트 (C++11) 메모리 사용량이 적다.   
`array`: 고정 크기 배열 (C++11)   

<br/>

***

<br/>

### 연관 컨테이너 (Associative Containers)   
데이터를 정렬된 상태로 유지하며, '키(Key)'를 사용해 빠르게 검색한다.(보통 Red-Black Tree 구조)   

`set`: 중복되지 않는 키들의 집합이다.   
`multiset`: 키의 중복을 허용하는 set   
`map`: 키와 값(Value)의 쌍으로 이루어진 집합이다. 키는 중복될 수 없다.   
`multimap`: 키의 중복을 허용하는 map   

<br/>

***

<br/>

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

<br/>

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

<br/>

**<참고사항>**   
`컨테이너 어댑터(Container Adapters)`   
특정 컨테이너를 변형하여 제한된 기능만 제공하는 클래스들이다.

`stack`: LIFO (Last-In-First-Out) 구조   
`queue`: FIFO (First-In-First-Out) 구조   
`priority_queue`: 우선순위가 높은 데이터가 먼저 나오는 구조(내부적으로 힙 정렬 사용)   

<br/>

***

<br/>

### unique()

<br/>
   
연속된 중복 요소들을 제거한다.   
단, 실제로 제거하는건 아니고 중복되는 원소를 뒤로 다 밀어넣는다.(실제 반환값은 뒤로 밀려진 중복값중 첫번째 위치)   
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

### 벡터로 변환
```cpp
// sum은 set<int>
vector<int> answer(sum.begin(), sum.end()); // 반환타입을 맞추기 위헤 벡터로 변환
```

<br/>

***

<br/>

### map의 key, value 접근법

```cpp
// C++ 17 부터는 이렇게 사용하면 더 편하다고 한다
for (const auto& [id, name] : students) {
    // .first 대신 id, .second 대신 name을 바로 사용!
    std::cout << "학번: " << id << ", 이름: " << name << std::endl;
}
```


<br/>

***

<br/>

### 벡터와 배열

<br/>

vector는 연속된 동적 배열이다.   
vector는 size와 capacity가 있다.    
공간이 꽉 차면 기존의 2배 크기의 capacity를 가진 새 메모리를 재할당한다.   
재할당은 O(n)의 시간복잡도

```cpp
// 미리 크기를 알면 reserve(n)으로 재할당 방지를 한다.   
v.reserve(100);   

// insert()와 erase()는 O(n)의 시간복잡도고 나머지는 O(1)   
v.insert(v.begin() + 2);    
v.erase(v.begin() + 2);   
// 실제 인덱스 위치(2)에 삽입/삭제   
```

<br/>

***

<br/>

### stack과 queue, deque

queue는 front()와 back()으로 양 쪽 다 접근 가능   
stack과 queue는 컨테이너 어댑터라고 부른다.   
둘 다 deque라는 기본 컨테이너를 감싸서 접근 방식을 제한 한 것이다.   

stack은 deque의 back만 사용, queue는 deque의 양쪽 끝 사용   

deque는 **여러 개의 고정 크기 메모리 블록(Chunk)**을 할당하고 이를 관리하는 맵(Map) 형태의 인덱스 체계를 가진다.   

메모리 불연속성: 데이터가 여러 블록에 나뉘어 저장되지만, 사용자 입장에서는 마치 하나의 연속된 배열처럼 인덱스 접근([])이 가능하다. (대신 임의 접근은 블록 계산을 해야해서 조금 느림)   
양방향 확장: 앞(Front)과 뒤(Back) 양쪽 모두에서 원소를 추가/제정하는 것이 $O(1)$ 성능으로 매우 빠르다.   

stack과 queue가 deque를 기본 컨테이너로 쓰는 이유   
메모리 재할당 효율성: vector는 용량이 꽉 차면 전체 데이터를 새로운 메모리 공간으로 복사해야 하지만, deque는 새로운 메모리 블록을 하나 더 할당하기만 하면 됩니다. 대량의 데이터를 다룰 때 훨씬 안정적이다.   
앞부분 삽입/삭제 성능: queue는 앞에서 데이터를 빼는 작업이 빈번합니다. vector는 앞에서 빼면 뒤의 모든 데이터를 당겨야($O(N)$) 하지만, deque는 앞쪽 블록만 건드리면 되므로 $O(1)$이다.   
메모리 해제: vector는 clear()를 해도 할당된 메모리(capacity)를 들고 있는 경우가 많지만, deque는 블록 단위로 메모리를 관리하므로 상대적으로 메모리 관리가 유연하다.   

<br/>

***

<br/>

### string과 여러 함수들  

```cpp
// hello를 찾아서 첫 인덱스를 리턴   
s.find("hello");   
// 인덱스 7부터 검색, 없으면 string::npos를 리턴한다.  
s.find("hello", 7);   
 
// 0부터 총 5개 즉 인덱스 0, 1, 2, 3, 4 이렇게 잘라서 리턴함 
s.substr(0, 5);
// 인덱스 10부터 끝까지   
s.substr(10);   

// replace는 원본이 바뀐다.   
std::string str = "Hello, World! World is great.";
std::string to_replace = "World";
std::string replacement = "C++";

size_t pos = 0;
while ((pos = str.find(to_replace, pos)) != std::string::npos) 
{
    str.replace(pos, to_replace.length(), replacement);
    pos += replacement.length(); // 다음 검색 위치를 설정
}  
```
   
<br/>

***

<br/>

**<Map과 함수들>**    

m.count(key값); 으로 확인하고 접근   

insert 대신 emplace 추천   

