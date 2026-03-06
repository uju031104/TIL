# 최대공약수 (GCD: Greatest Commen Divisor)

<br/>

### 유클리드 호제법(Euclidean algorithm)

<br/>

```c
#include <iostream>

int GCD(int a, int b)
{
    int tmp = 0;
    if (a < b)
    {
        tmp = a;
        a = b;
        b = tmp;
    }
    while (b != 0)
    {
        tmp = a % b;
        a = b;
        b = tmp;
    }
    
    return a;
}

int main()
{
    int gcd = GCD(6, 14);
    std::cout << gcd << std::endl;

    gcd = GCD(18, 12);
    std::cout << gcd << std::endl;

    return 0;
}

/* a와 b가 있을 때(a > b)
   a에는 b의 값을 넣고 b에는 a를 b로 나눈 나머지를 넣는다.
   이를 반복하다가 b 값이 0이 되면 a값이 최대공약수가 된다.

*/
```