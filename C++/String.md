# 문자열(String)

<br/>

문자열은 문자들이 연속적으로 나열된 데이터다.   
C++에서 문자열을 사용하기 위해 `#include<string>` 헤더를 포함해야 하며,
표준 라이브러리에서 제공하는 string(엄연히 말하면 클래스)을 통해 문자열을 다룰 수 있다.

<br/>

***

<br/>

### 문자열 메서드

<br/>

<table border="2">
    <tr align = "center", bgcolor = "gray">
        <td>이름</td>
        <td>사용법</td>
        <td>인자 설명</td>
        <td>메서드의 동작</td>
        <td>시간 복잡도</td>
    </tr>
    <tr align = "center">
        <td>length()</td>
        <td>s.length()</td>
        <td>없음</td>
        <td>문자열의 길이를 반환</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>size()</td>
        <td>s.size()</td>
        <td>없음</td>
        <td>문자열의 길이를 반환</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>empty()</td>
        <td>s.empty()</td>
        <td>없음</td>
        <td>문자열이 비어있으면 true 아니면 false 반환</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>clear()</td>
        <td>s.clear()</td>
        <td>없음</td>
        <td>문자열을 비움</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>append()</td>
        <td>s.append(str) 또는 s += str</td>
        <td>str: 추가할 문자열</td>
        <td>문자열 끝에 str을 추가</td>
        <td>O(n + m)<br/>(n: 기존 문자열 길이, m: 삽입할 문자열 길이)</td>
    </tr>
    <tr align = "center">
        <td>find()</td>
        <td>s.find(str, pos)</td>
        <td>str: 찾을 문자열, pos: 탐색 시작 위치</td>
        <td>str의 위치를 찾아서 값을 반환</td>
        <td>O(n)</td>
    </tr>
    <tr align = "center">
        <td>insert()</td>
        <td>s.insert(pos, str)</td>
        <td>pos: 삽입 위치, str: 삽입할 문자열</td>
        <td>pos 위치에 str을 삽입</td>
        <td>O(n + m)<br/>(n: 기존 문자열 길이, m: 삽입할 문자열의 길이)</td>
    </tr>
    <tr align = "center">
        <td>erase()</td>
        <td>s.erase(pos, len)</td>
        <td>pos: 삭제 시작 위치, len: 삭제할 길이</td>
        <td>pos부터 len만큼 삭제</td>
        <td>O(n - pos)<br/>(n: 기존 문자열 길이, pos: 삭제 시작 위치)</td>
    </tr>
    <tr align = "center">
        <td>replace()</td>
        <td>s.replace(pos, len, str)</td>
        <td>pos: 시작 위치, len: 바꿀 길이, str: 대체할 문자열</td>
        <td>지정된 부분을 str로 교체</td>
        <td>O(n - pos + m)<br/>(n: 기존 문자열 길이, pos: 교체 시작 위치, m: 대체할 문자열의 길이)</td>
    </tr>
    <tr align = "center">
        <td>substr()</td>
        <td>s.substr(pos, len)</td>
        <td>pos: 시작 위치, len: 길이(생략 가능)</td>
        <td>pos부터 len 길이의 부분 문자열 반환</td>
        <td>O(m)<br/>(m: 반환할 부분 문자열의 길이)</td>
    </tr>
    <tr align = "center">
        <td>compare()</td>
        <td>s.compare(str)</td>
        <td>str: 비교할 문자열</td>
        <td>사전 순 비교 (< 0, = 0, > 0 반환)</td>
        <td>O((n - pos) * m)<br/>(n: 기존 문자열 길이, pos: 검색 시작 위치, m: 검색할 문자열의 길이)</td>
    </tr>
    <tr align = "center">
        <td>at()</td>
        <td>s.at(pos)</td>
        <td>pos: 접근할 위치</td>
        <td>pos 위치의 문자 반환 (범위 검사 포함)</td>
        <td>O(pos * m)<br/>(pos: 문자열 내 검색 범위, m: 검색할 문자열의 길이)</td>
    </tr>
    <tr align = "center">
        <td>operator[]</td>
        <td>s[pos]</td>
        <td>pos: 접근할 위치</td>
        <td>pos 위치의 문자 반환 (범위 검사 없음)</td>
        <td>O(min(n, m))<br/>(n: 기본 문자열의 길이, m: 비교할 문자열의 길이)</td>
    </tr>
    <tr align = "center">
        <td>push_back()</td>
        <td>s.push_back(c)</td>
        <td>c: 추가할 문자</td>
        <td>문자열의 끝에 문자 c 추가</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>pop_back()</td>
        <td>s.pop_back()</td>
        <td>없음</td>
        <td>문자열의 마지막 문자 제거</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>resize()</td>
        <td>s.resize(n, c)</td>
        <td>n: 새 크기, c: 추가할 문자(생략 가능)</td>
        <td>문자열 크기 조정 (추가된 부분을 c로 채움)</td>
        <td>O(1)<br/>(상황에 따라 재할당 시 O(n))</td>
    </tr>
    <tr align = "center">
        <td>swap()</td>
        <td>s.swap(s2)</td>
        <td>s2: 교환할 문자열</td>
        <td>s와 s2를 교환</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>toupper()</td>
        <td>std::toupper(c)</td>
        <td>c: 변환할 문자</td>
        <td>소문자를 대문자로 변환</td>
        <td>O(1)</td>
    </tr>
    <tr align = "center">
        <td>tolower()</td>
        <td>std::tolower(c)</td>
        <td>c: 변환할 문자</td>
        <td>대문자를 소문자로 변환</td>
        <td>O(1)</td>
    </tr>
</table>