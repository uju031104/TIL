# 문자열 스트림(String Stream)

<br/>

`stringstream`은 문자열을 마치 스트림처럼 다룰 수 있도록 해주는 클래스다.   
즉 문자열을 입력 스트림처럼 처리하여, `cin`에서 데이터를 추출하듯이 문자열에서도 값을 추출할 수 있다.   

여기서 스트림은 데이터를 연속적으로 읽거나 쓸 수 있는 데이터 흐름을 말한다.   
이미 우리는 `cin`이라는 입력 스트림과 `cout`이라는 출력 스트림을 사용하고 있다.

<br/>

***

<br/>

### 공백 기준으로 분리

<br/>

>공백을 기준으로 문자열을 분리하는 방법   
이 방식은 cin을 사용할 때 기본적으로 공백 단위로 입력을 받았던 것과 유사하다.
우선, 분리할 문자열을 stringstream의 생성자에 전달하여 입력 스트림으로 설정한다.   
그 후 >>연산자를 이용해 문자열에서 원하는 데이터를 차례대로 변수에 저장합니다.

<br/>

```cpp
#include <iostream>
#include <sstream>
#include <string>

using namespace std;

int main()
{
	string str = "123 X 67";
	stringstream stream(str);

	int num;
	char c;
	float f;

	stream >> num >> c >> f;

	cout << num << endl;
	cout << c << endl;
	cout << f << endl;
}
```

<br/>

***

<br/>

### 특정 문자 기준으로 분리

<br/>

>단순한 공백이 아닌 특정 문자 기준으로 분리하는 방법   
기본적인 원리는 이전과 비슷하지만, 공백 대신 문자로 구분하기 위해서는 getline 함수를 사용할 수 있다.

<br/>

```cpp
// 목적: 쉼표(,)를 기준으로 문자열을 분할하여 토큰화
// 동작: getline() 함수를 사용하여 구분자를 지정

#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
    string text = "apple,banana,grape,orange";
    stringstream ss(text);
    string token;

    while (getline(ss, token, ',')) {
        cout << token << endl;
    }

    return 0;
}

/*
출력결과
apple
banana
grape
orange
*/
```

<br/>

***

<br/>

### 진법 변환(16진수 ↔ 10진수)

<br/>

>stringstream과 조작자(hex)를 활용하면 훨씬 간단하게 처리가능하다.

```cpp
/*
    코드의 목적 및 동작:
    - 10진수를 16진수 문자열로 변환 후 저장
*/
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
    int decimalNumber = 4095;
    stringstream ss;

    // 1) 10진수 -> 16진수 문자열
    ss << hex << decimalNumber; 
    string hexStr = ss.str();

    cout << "원본 10진수 : " << decimalNumber << endl;
    cout << "16진수 문자열: " << hexStr << endl;
    /*
    출력결과
    원본 10진수 : 4095
    16진수 문자열: fff
    */
    return 0;
}
```

<br/>

```cpp
/*
    코드의 목적 및 동작:
    - 16진수 문자열(hex)을 입력받아 10진수(decimal) 형태의 정수로 변환
    - stringstream을 활용하여 변환 후 결과 정수를 출력
*/
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
    string hexStr = "ff";
    stringstream ss(hexStr);
    int decimalNumber;

    // 16진수 형태로 파싱하도록 조작자를 설정
    ss >> hex >> decimalNumber;

    cout << "16진수: " << hexStr << endl;
    cout << "10진수: " << decimalNumber << endl;

    /*
    출력결과
    16진수: ff
    10진수: 255
    */
    return 0;
}
```