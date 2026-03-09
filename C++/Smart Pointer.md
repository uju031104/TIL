# 스마트 포인터(Smart Pointer)

<br/>

Heap은 여러 가지 장점들을 제공하지만, 메모리를 직접 관리해야 한다는 부담이 있다.   
C++에서는 Dangling Pointer가 발생하지 않도록 자동으로 관리해주는 `스마트 포인터`를 제공한다.

스마트 포인터의 핵심 원리는 new / delete를 사용하지 않는 자동 메모리 관리이다.
delete를 직접 호출해서 메모리를 관리하는 방식 대신, 각 스마트 포인터의 목적에 맞게 자동으로 메모리 관리를 한다.

<br/>

***

<br/>

### unique_ptr

<br/>

>`unique_ptr`은 객체에 대한 단일 소유권을 관리한다.   
객체의 소유권을 명확히 하고 소유권 이전을 통해 효율적인 자원관리가 가능하다.   
`move`를 통해 소유권을 이동하는 식으로 관리된다.  
소유권의 개념만 있기 때문에 사 혹은 대입이 불가능하다. (컴파일 에러)

<br/>

```cpp
// 기본적인 uinque_ptr 사용법
#include <iostream>
#include <memory> // unique_ptr 사용
using namespace std;

int main() {
    // unique_ptr 생성
    unique_ptr<int> ptr1 = make_unique<int>(10);

    // unique_ptr이 관리하는 값 출력
    cout << "ptr1의 값: " << *ptr1 << endl;

    // unique_ptr은 복사가 불가능
    // unique_ptr<int> ptr2 = ptr1; // 컴파일 에러 발생!

    // 범위를 벗어나면 메모리 자동 해제
    return 0;
}
```

<br/>

```cpp
// move로 소유권 이전
#include <iostream>
#include <memory>
using namespace std;

int main() {
    // unique_ptr 생성
    unique_ptr<int> ptr1 = make_unique<int>(20);

    // 소유권 이동 (move 사용)
    unique_ptr<int> ptr2 = move(ptr1);

    if (!ptr1) {
        cout << "ptr1은 이제 비어 있습니다." << endl;
    }
    cout << "ptr2의 값: " << *ptr2 << endl;

    return 0;
}
```

<br/>

```cpp
// 일반 클래스에서 unique_ptr 사용
#include <iostream>
#include <memory>
using namespace std;

class MyClass {
public:
    MyClass(int val) : value(val) {
        cout << "MyClass 생성: " << value << endl;
    }
    ~MyClass() {
        cout << "MyClass 소멸: " << value << endl;
    }
    void display() const {
        cout << "값: " << value << endl;
    }
private:
    int value;
};

int main() {
    // unique_ptr로 MyClass 객체 관리
    unique_ptr<MyClass> myObject = make_unique<MyClass>(42);

    // MyClass 멤버 함수 호출
    myObject->display();

    // 소유권 이동
    unique_ptr<MyClass> newOwner = move(myObject);

    if (!myObject) {
        cout << "myObject는 이제 비어 있습니다." << endl;
    }
    newOwner->display();

    // 범위를 벗어나면 newOwner가 관리하는 메모리 자동 해제
    return 0;
}
```

<br/>

***

<br/>

### shared_ptr

<br/>

>`shared_ptr`은 레퍼런스 카운트를 관리한다.   
`레퍼런스 카운트`란 현재 객체를 참조하는 포인터의 개수를 카운팅 하는 것이다.   
레퍼런스 카운트가 0이 되면 객체는 자동으로 메모리 해제가 된다.   
이를 활용해서 `Dangling Pointer` 및 `MemoryLeak` 문제를 효과적으로 방지할 수 있다.

<br/>

```cpp
// 기본적인 shared_ptr 사용법
#include <iostream>
#include <memory> // shared_ptr 사용
using namespace std;

int main() {
    // shared_ptr 생성
    shared_ptr<int> ptr1 = make_shared<int>(10);

    // ptr1의 참조 카운트 출력
    cout << "ptr1의 참조 카운트: " << ptr1.use_count() << endl; // 출력: 1

    // ptr2가 ptr1과 리소스를 공유
    shared_ptr<int> ptr2 = ptr1;
    cout << "ptr2 생성 후 참조 카운트: " << ptr1.use_count() << endl; // 출력: 2

    // ptr2가 범위를 벗어나면 참조 카운트 감소
    ptr2.reset();
    cout << "ptr2 해제 후 참조 카운트: " << ptr1.use_count() << endl; // 출력: 1

    // 범위를 벗어나면 ptr1도 자동 해제
    return 0;
}
```

<br/>

```cpp
// 일반 클래스에서 shared_ptr 사용법
#include <iostream>
#include <memory>
using namespace std;

class MyClass {
public:
    MyClass(int val) : value(val) {
        cout << "MyClass 생성: " << value << endl; // 출력: MyClass 생성: 42
    }
    ~MyClass() {
        cout << "MyClass 소멸: " << value << endl; // 출력: MyClass 소멸: 42
    }
    void display() const {
        cout << "값: " << value << endl; // 출력: 값: 42
    }
private:
    int value;
};

int main() {
    // shared_ptr로 MyClass 객체 관리
    shared_ptr<MyClass> obj1 = make_shared<MyClass>(42);

    // 참조 공유
    shared_ptr<MyClass> obj2 = obj1;

    cout << "obj1과 obj2의 참조 카운트: " << obj1.use_count() << endl; // 출력: 2

    obj2->display(); // 출력: 값: 42

    // obj2를 해제해도 obj1이 객체를 유지
    obj2.reset();
    cout << "obj2 해제 후 obj1의 참조 카운트: " << obj1.use_count() << endl; // 출력: 1

    return 0;
}
```

<br/>

***

<br/>

### weak_ptr

<br/>

>`weak_ptr`은 객체의 소유권을 공유하지 않는다.   
다른 스마트 포인터와 다르게 레퍼런스 카운트를 증가시키지 않는 `약한 참조`를 한다.   
`shared_ptr` 는 유용하지만 순환참조가 발생할 수 있습니다.   
`순환 참조`란, 두 개 이상의 객체가 서로를 shared_ptr로 가리켜 참조하는 상황을 말한다.   
이러한 순환 참조는 메모리 누수를 유발할 수 있다.   
이 상황에서 서로 순환하고 있는 shared_ptr중 하나를 weak_ptr로 대체하면 순환 고리가 끊어지게 되므로 문제를 해결할 수 있다.   
정리하면 shared_ptr은 관찰과 소유를 하는 반면, weak_ptr은 관찰만 한다고 표현한다.   

<br/>

```cpp
// lock()함수로 유효성을 확인하고 weak_ptr를 사용하는 법
#include <iostream>
#include <memory>

class A {
public:
    void say_hello() {
        std::cout << "Hello from A\n";
    }
};

class B {
public:
    std::weak_ptr<A> a_ptr;

    void useA() {
        if (auto a_shared = a_ptr.lock()) { // 유효한지 확인
            a_shared->say_hello();
        } else {
            std::cout << "A is no longer available.\n";
        }
    }
};

int main() {
    std::shared_ptr<B> b = std::make_shared<B>();
    
    {
        std::shared_ptr<A> a = std::make_shared<A>();
        b->a_ptr = a;
        b->useA(); // A가 유효하므로 Hello 출력
    } // A는 scope을 벗어나며 소멸됨

    b->useA(); // A는 이미 소멸되었기 때문에 메시지 출력
}
```

<br/>

```cpp
//  shared_ptr를 사용해서 순환참조 발생
#include <iostream>
#include <memory>

class B; // Forward declaration

class A {
public:
    std::shared_ptr<B> b_ptr;
    ~A() { std::cout << "A destroyed\n"; }
};

class B {
public:
    std::shared_ptr<A> a_ptr;
    ~B() { std::cout << "B destroyed\n"; }
};

int main() {
    auto a = std::make_shared<A>();
    auto b = std::make_shared<B>();

    a->b_ptr = b;
    b->a_ptr = a;

    // main 함수가 끝나도 A와 B는 서로 참조 중이라 메모리 해제가 안 됨
    return 0;
}
```

<br/>

```cpp
// weak_ptr로 순환참조 해결
#include <iostream>
#include <memory>

class B; // Forward declaration

class A {
public:
    std::shared_ptr<B> b_ptr;
    ~A() { std::cout << "A destroyed\n"; }
};

class B {
public:
    std::weak_ptr<A> a_ptr; // weak_ptr로 변경
    ~B() { std::cout << "B destroyed\n"; }
};

int main() {
    auto a = std::make_shared<A>();
    auto b = std::make_shared<B>();

    a->b_ptr = b;
    b->a_ptr = a; // weak_ptr로 참조

    return 0;
}
```