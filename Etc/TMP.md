# TMP

<br/>

매일 상세하게 정리는 힘들어서 여기에 임시로 간략하게 메모하고 남는 시간 활용해서 정리할 예정   

>이 페이지는 26.03.10부터 시작   
정리 끝나면 <s>취소선</s> 표시

<br/>

*********************************************************************************************************************

<br/>


<!----------------------------- 26.03.10 ------------------------------>
<details>
  <summary><s>26.03.10</s></summary>
  <p>     

### 26.03.10

VSCode json 파일 다루는 법 공부(분할 컴파일 경로 오류때문에... 근데 경로 오류는 아니었음)
include된 파일 범위, 컴파일 종류(나는 gcc 사용), 버전 등등 정보를 직접 수정할 수 있음

코드카타 김서방찾기
반복자 연산한거 auto로 받아야함.

cmd에서 `mkdir 폴더명`은 폴더 만들기   
`cd 폴더명`은 폴더로 가기   
맨날 까먹어서 적어둠
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
  </p>
</details>

<!----------------------------- 26.03.11 ------------------------------>

<details>
  <summary><s>26.03.11</s></summary>
  <p>

### 03.11

<s>
오늘의 99%    
cpp 두번째 과제 작성

나머지 1%   
json 폴더에서 "args" 배열에 경로를 추가해줘야 hpp 파일만 include해도 오류가 안난다.
VSCode는 하나하나 다 설정해줘야함

분할 상환 분석 (Amortized Analysis)   

분할 상환 분석(Amortized Analysis)은 최악의 경우(Worst-case) 성능이 매우 나쁜 연산이 드물게 발생할 때, 일련의 전체 연산 비용을 평균화하여 실제적인 효율성을 분석하는 알고리즘 분석 기법입니다. 몇 번의 고비용 연산이 대부분의 저비용 연산에 의해 '분할 상환'되어, 전반적인 시간 복잡도를 더 정확하게 파악할 수 있게 합니다.   

</s>
  </p>
</details>

<!----------------------------- 26.03.12 ------------------------------>

<details>
  <summary><s>26.03.12</s></summary>
  <p>

### 03.12

두번째 과제 완료   
챕터2 강의자료 과제 완료   
게임개발자 c++문법 3-1 강의 듣기 완료   
3-1 강의 3가지 패턴 중 2가지 공부   

복사 생성자, 대입 연산자

til 밀린거 쭉 정리/복습   
tmp 3.11까지 정리 완료

deduction : 추상
iterator : 반복자
yield : 생산하다

배열 말고 2차원 벡터는 처음 써봐서
문법 눈에 익혀두기

```cpp
#include <string>
#include <vector>

using namespace std;

vector<vector<int>> solution(vector<vector<int>> arr1, vector<vector<int>> arr2) {
    vector<vector<int>> answer;
    
    for(size_t i = 0; i< arr1.size(); ++i)
    {
        answer.push_back(vector<int>());
        for(size_t j = 0; j< arr1[0].size(); ++j)
        {
            answer[i].push_back(arr1[i][j] + arr2[i][j]);
        }
    }
    
    return answer;
}
```


<br/>

챕터2 강의자료 과제 하면서 알게된 두가지   
첫번째. 람다식 쓰는법  
두번째. 인터페이스 활용법   
A클래스에서 기능을 확장하는 A+함수를 만들고 B클래스(인터페이스)로 확장할 기능을 가상함수로 정의하고 B1 B2에 상속해서 구현   
A+함수의 매개변수를 B클래스 자료형으로 받음   
A+함수를 호출할 때 B1, B2 클래스를 넣어서 부모->자식 관계를 호출하게 만든다.(저번에 배운 가상함수를 가장 잘 활용하는 방법) 

```cpp
// 람다 사용법
void compareMovies(vector<Movie> &movies)
{
    // Movie라는 구조체를 담는 백터의 래퍼런스 movies
    // movies에 담긴 구조체를 구조체 변수의 크기에 따라 내림차순 정렬
    sort(movies.begin(), movies.end(),
         [](const Movie &a, const Movie &b)
         {
             if (a.rating > b.rating)
             {
                 return true;
             }
             return false;
         });
}
```

  </p>
</details>

<!----------------------------- 26.03.13 ------------------------------>

<details>
  <summary><s>26.03.13</s></summary>
  <p>

### 03.13

코드카타 3진법 뒤집기 문제에서 생긴 오류

```cpp
for(auto i : reverse)
{
    answer += (i * pow(3, num));
    cout << i * pow(3, num) << " ";
    --num;
}

```

pow는 기본적으로 double형을 반환한다.   
그래서 값이 커지는 순간(체감상 100만단위?) 7.74841e+08 막 이런식으로 나와버린다.
위의 코드를 제대로 실행하게 하려면 아래와 같이 바꿔야함
  
```cpp
for(auto i : reverse)
{
    answer += (i * (int)pow(3, num));
    cout << i * (int)pow(3, num) << " ";
    --num;
}

```

<br/>

cpp 3번째 과제 시작
cpp 3번째 과제 완료   
cpp 4번째 과제 시작

디폴트 매개변수는 선언부/구현부 중 한 곳에만 쓰는게 규칙이다. 둘 다 쓰면 redeclaration 오류가 뜬다.   

템플릿 클래스 파일 분리 시 헤더 파일에 구현/선언을 다 넣는게 좋다. 모호한 타입이라 오류가 엄청 잘 발생한다.   


  </p>
</details>

<!----------------------------- 26.03.16 ------------------------------>

<details>
  <summary>26.03.16</summary>
  <p>

### 03.16

 과제4 완료  
 게임개발자 c++문법 3-2 강의 완료 
 const 멤버 함수는 반환값도 const로 해줘야한다. 


  </p>
</details>