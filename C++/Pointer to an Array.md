# Pointer to an Array(배열 포인터)

<br/>

배열 포인터는 배열 전체를 가리키는 포인터이다.  
즉 단일 변수가 아닌 배열 통째를 가리키는 변수다.   
보통 다차원 배열을 제어할 때 많이 사용한다.

<br/>

***

<br/>

### 예시 코드

<br/>

```c
#include <iostream>

// 배열 포인터: 배열 전체를 가리키는 포인터
int main() {
    int arr[3] = { 100, 200, 300 };
    int (*ptr)[3] = &arr; // 배열 포인터 선언

    // 배열 포인터를 이용하여 배열 요소 접근
    std::cout << "(*ptr)[0]: " << (*ptr)[0] << std::endl; // 100
    std::cout << "(*ptr)[1]: " << (*ptr)[1] << std::endl; // 200
    std::cout << "(*ptr)[2]: " << (*ptr)[2] << std::endl; // 300

    return 0;
}
/*
출력 결과:
(*ptr)[0]: 100
(*ptr)[1]: 200
(*ptr)[2]: 300
*/
```

<br/>

***

<br/>

### 배열 포인터의 구조

<br/>

<table border="2">
    <tr align = "center">
        <td colspan = "2">배열 포인터</td>
        <td rowspan = "3">&nbsp;&nbsp;&nbsp;&nbsp;</td>
        <td colspan = "5">배열</td>
    </tr>
    <tr align = "center">
        <td>주소</td>
        <td>3000</td>
        <td>주소</td>
        <td>1000</td>
        <td>1004</td>
        <td>1008</td>
        <td>1012</td>
    </tr>
    <tr align = "center">
        <td>값</td>
        <td>1000</td>
        <td>값</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
    </tr>
</table>



배열 포인터의 값은 배열의 주소값이 들어간다.   
따라서 배열 포인터를 역참조(*)하면 배열을 가리키게된다.



