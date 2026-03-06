# 시간복잡도(Time Complexity)

<br/>

`입력크기`(n)가 커질 때, `연산횟수`가 얼마나 증가하는지를 나타낸다.

<br/>

***

<br/>

### 빅오 표기법(Big-O Notation)

입력크기가 n일때 시간복잡도를 나타내는 표기법이다.
> O(1) -> 상수 시간   
> O(n) -> 선형 시간   
> O(n^2) -> 2차 시간(ex. 이중 반복문)   
> O(log n) -> 로그 시간(ex. 이진 탐색)   

<br/>

***

<br/>

### 1초에 1억번
cpu는 대략 `1초에 1억번`의 연산을 시행한다.   
따라서 코드를 짤 때 감각적으로 실행시간이 1초를 초과하는지 느낄 수 있어야 한다.

<br/>

<table border="2">
    <tr align = "center">
        <td colspan = "2">1초에 1억번 가정</td>
    </tr>
    <tr align = "center">
        <td colspan = "1">시간 복잡도</td>
        <td colspan = "1">최대 연산 횟수</td>
    </tr>
    <tr align = "center">
        <td>O(N!)</td>
        <td>10</td>
    </tr>
    <tr align = "center">
        <td>O(2^n)</td>
        <td>20~25</td>
    </tr>
    <tr align = "center">
        <td>O(N^3)</td>
        <td>200~300</td>
    </tr>
    <tr align = "center">
        <td>O(N^2)</td>
        <td>3,000~5,000</td>
    </tr>
    <tr align = "center">
        <td>O(NlogN)</td>
        <td>100만</td>
    </tr>
    <tr align = "center">
        <td>O(N)</td>
        <td>1000~2000만</td>
    </tr>
    <tr align = "center">
        <td>O(logN)</td>
        <td>10억</td>
    </tr>
</table>


<br/>

***

<br/>

### O(n) 예제 - 최대값 찾기

```c
#include <iostream>
#include <vector>

int main()
{           
    std::vector<int> arr = {3, 7, 2, 9, 1, 5, 8, 4, 6};
    int maxVal = arr[0];
    int i;

    for (i = 1; i < (int)arr.size(); ++i)
    {
        if (maxVal < arr[i])
        {
            maxVal = arr[i];
        }
    }

    std::cout << "최대값: " << maxVal;
    // 정렬이 안된 배열은 모두 확인해야한다.
    // O(n)
    return 0;
}
```

