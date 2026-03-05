# Array of Pointers(포인터 배열)

<br/>

포인터 배열은 포인터를 원소로 갖는 배열이다.   
예를 들어, `int* ptrArr[4];`는 크기가 4이고, 각 원소가 `int*`인 배열

<br/>

***

<br/>

### 예시 코드

<br/>

```c
#include <iostream>

// 포인터 배열: 포인터를 원소로 갖는 배열
int main() {
    int a = 10, b = 20, c = 30;
    int* ptrArr[3] = { &a, &b, &c }; // 포인터 배열 선언 및 초기화

    // 포인터 배열을 이용하여 값 출력
    std::cout << "*ptrArr[0]: " << *ptrArr[0] << std::endl; // 10
    std::cout << "*ptrArr[1]: " << *ptrArr[1] << std::endl; // 20
    std::cout << "*ptrArr[2]: " << *ptrArr[2] << std::endl; // 30

    return 0;
}
/*
출력 결과:
*ptrArr[0]: 10
*ptrArr[1]: 20
*ptrArr[2]: 30
*/
```

<br/>

***

<br/>

### 참고 사항

```c
arr[k] == *(arr + k)
```