# 포인터와 상수 키워드(Pointer and Const)

<br/>

다른 함수에 포인터가 인자로 전달되면 원본이 바뀔 위험이 있다.   
만약 이런 실수가 발생한다면 전역적인 문제로 번질 가능성이 농후하다.

<br/>

***

<br/>

### const pointer to integer

>메모리 주소를 보호하는 포인터   
자료형* const 변수명 = 주소;

<br/>

***

<br/>

### pointer to const integer

>메모리 주소 속에 값을 보호    
const 자료형* 변수명 = 주소;

<br/>

***

<br/>

### const pointer to an const integer

>주소도 보호하고 값도 보호   
const 자료형* const 변수명 = 주소;

