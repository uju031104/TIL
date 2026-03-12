# 업캐스팅(Upcasting)

<br/>

인터페이스 클래스를 만들기 위해 가상함수를 가진 클래스를 만드는데 여기서 이 기능을 더 강력하게 가져갈 수 있는 방법이 있다.   
업캐스팅(Upcasting)이라고 하는데 부모 클래스 포인터/참조형으로 자식 객체를 가리키면 된다.   
이러면 부모 클래스 멤버에는 접근이 가능하고 자식 고유 멤버는 접근이 불가능하다.  

```cpp
#include <iostream>
#include <vector>

class Parent
{
public:
    virtual void hello() = 0;
    virtual void world() = 0;
    int a = 1;
private:
    
    int b = 2;
    int c = 3;
};

class Child : public Parent
{
public:
    void hello() override
    {
        std::cout << "hello";
    }

    void world() override
    {  
        std::cout << ", world";
    }

    int d = 4;
};

int main()
{
    Parent* hw = new Child();
    // hw->d 처럼 Child의 멤버 변수에는 접근이 불가능하다.
    // hw->hello(), world(), a만 가능하다.
    hw->hello();
    hw->world();
    // hello, world 출력
    return 0;
}

// 이런식으로 Parent를 완전한 인터페이스 역할로만 쓸 수 있어서 좋다.
// Parent에서 붕어빵 틀만 제대로 만든다음 그 붕어빵 틀을 이용해서 다양한 붕어빵을 쭉 뽑아낼 수 있는셈.
```