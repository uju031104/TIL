# 힙 메모리(Heap Memory)

<br/>

스택 메모리는 메모리를 자동으로 회수해 주는 장점이 있는 반면, 단점도 존재한다. 가장 큰 단점은 아래와 같다.

>일반적으로 할당 가능한 스택 메모리의 크기가 제한적이다.   
변수의 스코프(생존 영역)을 벗어나면 자동으로 해제되므로, 메모리를 더 길거나 유연하게 관리하기 어렵다.

<br/>

이 문제를 해결하기 위해 힙(동적) 메모리를 사용할 수 있다.

>동적 할당 시 `new` 연산자를 사용하고, 해제 시 `delete` 연산자를 사용한다.   
스택과 달리 자동으로 해제되지 않으므로 메모리 누수 등의 위험이 있을 수 있다.   
동적 할당된 객체(또는 변수)의 생존 주기는 사용자가 `delete`로 해제할 때까지 유지된다.   

<br/>

***

<br/>

### 변수 하나의 영역에 대한 동적할당

<br/>

```cpp
#include <iostream>
using namespace std;

void func1() {
    int* ptr = new int(10);  // 힙 메모리에 정수 10 할당
    cout << "Value: " << *ptr << endl;
    delete ptr;             // 메모리 해제
}

int main() {
    func1();
    return 0;
}

```

<br/>

***

<br/>

### 배열의 동적 할당과 해제

<br/>

```cpp
#include <iostream>
using namespace std;

void func2() {
    int* arr = new int[5];  // 힙 메모리에 정수 배열 5개 할당
    for (int i = 0; i < 5; ++i) {
        arr[i] = i * 10;
        cout << "arr[" << i << "] = " << arr[i] << endl;
    }
    delete[] arr;  // 배열 메모리 해제
}

int main() {
    func2();
    return 0;
}
```

<br/>

***

<br/>

### 메모리 누수(Memory Leak)

<br/>

동적으로 할당한 메모리를 사용한 후 제대로 해제하지 않으면, 계속해서 사용하지 않는 메모리가 쌓이게 된다.   
이렇게 되면 프로그램이 점점 더 많은 메모리를 차지하게 되어 결국 사용할 수 있는 메모리가 부족해진다.   
**이런 현상을 `메모리 누수(Memory Leak)`라고 부른다.**   
사용하지 않는 영역을 해제하지 않고 계속해서 메모리 할당을 하다 보면, 더 이상 사용 가능한 메모리가 없을 수 있다.

<br/>

***

<br/>

### 댕글링 포인터(Dangling Pointer)

<br/>

이미 해제된 메모리를 가리키고 있는 포인터이다.   
Read만 하면 오류 발생은 없지만 Write를 하는 순간 치명적인 오류가 발생한다.

<br/>

```cpp
#include <iostream>
using namespace std;

void func5() {
    int* ptr = new int(40);  // 힙 메모리에 정수 40 할당
    int* ptr2 = ptr;

    cout << "ptr adress = " << ptr << endl;
    cout << "ptr2 adress = " << ptr2 << endl;
    cout << *ptr << endl;

    delete ptr;

    cout << *ptr2 << endl;
}

int main() {
    func5();
    return 0;
}
```