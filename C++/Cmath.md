# cmath

<br/>

숫자를 다룰 때 필요한 헤더

<br/>

***

<br/>

### 반올림/올림/버리기

<br/>

```c
#include <iostream>
#include <cmath>

int main() {

    /* 반올림은 주어진 숫자에서 가장 '가까운' 정수를 반환
    0에서 먼 쪽(away from zero)으로 반올림한다.*/
    std::cout << round(-3.2) << std::endl;  // -3
    std::cout << round(-3.5) << std::endl;  // -4
    std::cout << round(-3.8) << std::endl;  // -4

    /* 올림은 주어진 숫자보다 '크거나 같은' 가장 작은 정수를 반환 */
    std::cout << ceil(-3.2) << std::endl;  // -3
    std::cout << ceil(-3.5) << std::endl;  // -3
    std::cout << ceil(-4.0) << std::endl;  // -4

   /* 내림은 주어진 숫자에서 가장 '가까운 작은 정수'를 반환 */
    std::cout << floor(3.2) << std::endl;  // 3
    std::cout << floor(-3.5) << std::endl;  // -4
    std::cout << floor(-4.0) << std::endl;  // -4

    return 0;
}
```