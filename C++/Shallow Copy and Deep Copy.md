# 얕은 복사와 깊은 복사(Shallow Copy and Deep Copy)

<br/>

### 얕은 복사(Shallow Copy)

<br/>

>`얕은 복사(Shallow Copy)`란,  클래스 내의 포인터 멤버를 복사할 때 포인터가 가리키는 데이터가 아닌 포인터가 저장하고 있는 주소값만 복사하는 것을 의미한다.   
즉, 두 객체가 동일한 동적 메모리 영역을 가리키게 된다.   
얕은 복사를 수행한 후 원본 객체가 메모리를 해제하면, 복사된 객체의 포인터는 해제된 메모리 영역을 가리키게 된다.   
즉 `dangling pointer`가 발생할 수 있다.   

<br/>

```cpp
#include <iostream>
using namespace std;

int main() {
    // 포인터 A가 동적 메모리를 할당하고 값을 30으로 설정
    int* A = new int(30);

    // 포인터 B가 A가 가리키는 메모리를 공유
    int* B = A;

    cout << "A의 값: " << *A << endl; // 출력: 30
    cout << "B의 값: " << *B << endl; // 출력: 30

    // A가 동적 메모리를 해제
    delete A;

    // 이제 B는 Dangling Pointer(해제된 메모리를 가리키는 포인터)
    // 이 시점에서 B를 통해 접근하면 Undefined Behavior 발생
    cout << "B의 값 (dangling): " << *B << endl; // 위험: 정의되지 않은 동작

    return 0;
}
```

<br/>

***

<br/>

### 깊은 복사(Deep Copy)

>`깊은 복사(Deep Copy)`는 클래스의 포인터 멤버가 가리키는 동적 데이터를 새로 할당된 독립적인 메모리 영역에 복제하는 것을 의미한다.   
따라서 원본 객체와 복사된 객체는 서로 독립적인 메모리 공간을 소유하므로 `dangling pointer`가 발생하지 않는다.

<br/>

```cpp
#include <iostream>
using namespace std;

int main() {
    // 포인터 A가 동적 메모리를 할당하고 값을 30으로 설정
    int* A = new int(30);

    // 포인터 B가 A가 가리키는 값을 복사 (깊은 복사)
    int* B = new int(*A);

    cout << "A의 값: " << *A << endl; // 출력: 30
    cout << "B의 값: " << *B << endl; // 출력: 30

    // A가 동적 메모리를 해제
    delete A;

    // B는 여전히 독립적으로 자신의 메모리를 관리
    cout << "B의 값 (깊은 복사 후): " << *B << endl; // 출력: 30

    // B의 메모리도 해제
    delete B;

    return 0;
}
```