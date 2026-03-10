# TMP

<br/>

나눠서 정리만 하니까 커다란 범위의 `개념`에 대해서 복습하기엔 좋은데 시간도 오래 걸림   
그리고 그때 그때 몰랐던 작은 범위의 것들을 정리하기엔 애매해서 여기에 기록   
여기에 기록해뒀다가 차차 정리할 생각
```cpp
string A = "정리";
string B = "오늘 배운 모든 범위";
string TMP = "기록";
!(A += B);    // 한번에 하기 너무 힘들다
TMP = B;      // 그래서 일단 여기 기록하고
A += TMP;     // 세분화해서 정리한다.
```
이 페이지는 26.03.10부터 시작


### 03.10

VSCode json 파일 다루는 법 공부(분할 컴파일 경로 오류때문에... 근데 경로 오류는 아니었음)
include된 파일 범위, 컴파일 종류(나는 gcc 사용), 버전 등등 정보를 직접 수정할 수 있음
***
코드카타   
김서방 찾기      
find() 함수? 템플릿?을 사용하면 반환값이 반복자라서 int index 로 받았다가 오류가 떴음   
그래서 auto index로 받았고   
```cpp
index = find(seoul.begin(), seoul.end(), "Kim") - seoul.begin();   
``` 
위와 같이 반복자를 반환해줘서 나온 값에서 begin을 빼줘야 인덱스가 나왔음   
근데 그 인덱스가 정확히 어떤 자료형으로 나오는지는 아직 모름 확인해봐야할듯   
***
cmd에서 `mkdir 폴더명`은 폴더 만들기   
`cd 폴더명`은 폴더로 가기   
맨날 써도 까먹어서 적어둠
***
부모 클래스의 매개변수가 있는 생성자를 자식 클래스에서 쓰고 싶을 경우에는 명시적으로(explicitly) 적어줘야함   
```cpp
//간단한 예시
#include <iostream>
#include <vector>

class Parent
{
public:
    Parent(int a)
    {
        std::cout << "Parent(int a)" << std::endl;
    }

};

class Child : Parent
{
public:
    Child(int a) : Parent(a) // 이부분
    {
        std::cout << "Child(int a)" << std::endl;
    }
};

int main()
{
    Child a(1);
    return 0;
}
```
***
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
