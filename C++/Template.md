# 템플릿(Template)

<br/>

템플릿 문법을 사용하면, 다양한 자료형에 유연하게 대응하는 일반화된 코드를 작성할 수 있다.

<br/>

***

<br/>

### 함수 오버로딩(Function Overloading)

<br/>

>C언어와 달리 특정 규칙만 지키면, C++에서는 동일한 이름의 함수를 여러 개 정의할 수 있다.   
그 이유는 C언어는 함수 이름으로만 함수를 구분하지만, C++은 함수 이름과 매개변수 타입 정보를 함께 사용해 구분하기 때문이다.   
이런 식으로 함수 이름 구분을 위해 내부적으로 고유한 이름을 부여하는 것을 `네임 맹글링(Name Mangling)` 이라고 한다.   
단, 함수의 반환형만으로는 오버로딩이 성립하지 않는다.   
함수 오버로딩을 적용하려면, 이름이 같아도 각 함수가 명확히 구분되어야 한다.   
함수 오버로딩이 유효해지는 조건을 몇 가지 보면  다음과 같다.  
> 
>1.**매개변수 타입이 다른 경우**   
>2.**매개변수의 개수가 다른 경우**

<br/>

**매개변수 타입이 다른 함수 오버로딩**
```cpp
#include <iostream>
using namespace std;

void print(int a) {
    cout << "정수 출력: " << a << endl;
}

void print(double a) {
    cout << "실수 출력: " << a << endl;
}

int main() {
    print(10);     // 정수 출력
    print(3.14);   // 실수 출력
    return 0;
}

// 출력결과:
// 정수 출력: 10
// 실수 출력: 3.14
```

<br/>

**매개변수 개수 다른 함수 오버로딩**
```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
    return a + b;
}

int add(int a, int b, int c) {
    return a + b + c;
}

int main() {
    cout << add(1, 2) << endl;        // 두 개의 인자 사용
    cout << add(1, 2, 3) << endl;     // 세 개의 인자 사용
    return 0;
}

// 출력결과:
// 3
// 6
```

<br/>

***

<br/>

### 템플릿(Template)

<br/>

>템플릿은 타입에 관계없이 일반화된 코드를 작성하기 위한 문법이다.   
`template <typename T>` 

<br/>

**예시**
```cpp
#include <iostream>
using namespace std;

template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    cout << add(3, 5) << endl;        // 정수 더하기
    cout << add(2.5, 4.1) << endl;    // 실수 더하기
    return 0;
}

// 출력결과:
// 8
// 6.6
```
