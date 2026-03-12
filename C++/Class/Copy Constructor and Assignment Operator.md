# 복사생성자와 대입연산자(Copy Constructor and Assignment Operator)

<br/>

```cpp
#include <iostream>

using namespace std;

class Widget {
public:
    string str;
    int number;

public:
    // 기본 생성자
    Widget()
    {
        number = 1;
        str = "기본 생성자를 호출했습니다.";
        cout << str << endl;
    }   

    // 복사 생성자
    Widget(const Widget& rhs)
    {
        number = 2;
        str = "복사 생성자를 호출했습니다.";
        cout << str << endl;

        // 아래와 같이 rhs의 멤버 변수를 읽어올 수 있다.
        this->number = rhs.number;
        // 하지만 rhs.number = this->number 은 불가능하다. => rhs가 const 이므로
    }  

    // 복사 대입 연산자
    Widget& operator = (const Widget& rhs)
    {
        if (this != &rhs) //다를때만 복사 수행
        { 
            str = "복사 대입연산자를 호출했습니다.";
            cout << str << endl;
        }

        return *this;
    } 

};

int main()
{
    Widget w1;  // 기본 생성자 호출

    Widget w2(w1);  // 복사 생성자 호출

    w1 = w2;    // 복사 대입 연산자(operator) 호출

    Widget w3 = w2;     // 복사 생성자 호출

    return 0;
}
```