# TMP

<br/>

매일 상세하게 정리는 힘들어서 여기에 임시로 간략하게 메모하고 남는 시간 활용해서 정리할 예정   

>이 페이지는 26.03.10부터 시작   
정리 끝나면 <s>취소선</s> 표시

<br/>

*********************************************************************************************************************

<br/>


#### <!-- 26.03.10 -->
<details>
  <summary><s>26.03.10</s></summary>
  <p>     
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

#### <!-- 26.03.11 -->
<details>
  <summary><s>26.03.11</s></summary>
  <p>

오늘의 99%    
cpp 두번째 과제 작성

나머지 1%   
json 폴더에서 "args" 배열에 경로를 추가해줘야 hpp 파일만 include해도 오류가 안난다.
VSCode는 하나하나 다 설정해줘야함

분할 상환 분석 (Amortized Analysis)   

분할 상환 분석(Amortized Analysis)은 최악의 경우(Worst-case) 성능이 매우 나쁜 연산이 드물게 발생할 때, 일련의 전체 연산 비용을 평균화하여 실제적인 효율성을 분석하는 알고리즘 분석 기법입니다. 몇 번의 고비용 연산이 대부분의 저비용 연산에 의해 '분할 상환'되어, 전반적인 시간 복잡도를 더 정확하게 파악할 수 있게 합니다.   

  </p>
</details>

#### <!-- 26.03.12 -->
<details>
  <summary><s>26.03.12</s></summary>
  <p>

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

#### <!-- 26.03.13 -->
<details>
  <summary><s>26.03.13</s></summary>
  <p>

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

#### <!-- 26.03.16 -->
<details>
  <summary><s>26.03.16</s></summary>
  <p>

 과제4 완료  
 게임개발자 c++문법 3-2 강의 완료 
 const 멤버 함수는 반환값도 const로 해줘야한다. 


  </p>
</details>

#### <!-- 26.03.17 -->
<details>
  <summary><s>26.03.17</s></summary>
  <p>

코드카타
문자 아스키코드 128부터 오버플로우 조심
 
```cpp
// 이 코드 다르게 다시 해보자
#include <string>
#include <vector>

using namespace std;

string solution(string s, int n) {
    string answer = "";
    
    for(char chr : s)
    {
        if(chr == ' ')
        {
            answer += chr;
        }
        else if(65 <= chr && chr <=90)
        {
            chr += n;
            if(90 < chr)
            {
                chr = (chr - 26);
            }
            answer += chr;
        }
        else
        {
            if(122 < chr + n)
            {
                chr = (chr - 26);
            }
            chr += n;
            answer += chr;
        }
    }
    
    return answer;
}
```

+코드카타 카카오 문제 깔끔한 버전 확인해보기

<br/>

**HLOD(Hierarchical Level of Detail)폴더**    
성능을 위해 엔진이 자동으로 만든 데이터 보관소   
알아서 최적화 해주는데 용량도 좀 차지해서 상황에 따라 켜거나 끄는거 추천   

***

<br/>

**객체를 따로 안만드는 이유**   
우리가 직접 new를 호출하지 않아도 언리얼 엔진의 '액터 생명주기(Actor Lifecycle)' 시스템이 우리 대신 객체를 만들고 관리해주기 때문

***

<br/>

**에디터에서 배치할 때**: 레벨(맵)에 액터를 드래그해서 놓으면, 레벨 파일 안에 해당 클래스의 정보가 저장된다.

**게임이 시작될 때**: 엔진이 레벨을 불러오면서 저장된 리스트를 보고 SpawnActor<AMyActor>()라는 내부 함수를 호출해 객체를 생성한다

***

<br/>

언리얼 엔진은 객체를 만든 후, 특정 시점이 되면 약속된 함수들을 순서대로 호출한다. 이를 콜백(Callback) 함수라고 한다

Constructor (생성자): 클래스가 메모리에 만들어질 때 (컴포넌트 조립 등)

PostInitializeComponents: 모든 컴포넌트가 세팅 완료되었을 때

BeginPlay: **"이제 진짜 게임이 시작되었으니 로직을 실행해도 좋다"** 라고 엔진이 신호를 보낼 때

***

<br/>

**Super::BeginPlay()의 역할**   
부모 클래스가 기본적으로 준비해야할 것들을 다 한뒤 자식 클래스의 로직 실행

UE5에선 필수적으로 int말고 int32을 쓴다. 32비트라고 확실하게 말해주는 역할.

***

<br/>

```cpp
//헤더파일
#include "Engine/Engine.h"
// GEngine이 존재하는지 확인 후 실행
if (GEngine)
{
    GEngine->AddOnScreenDebugMessage(-1, 3.0f, FColor::Red, FString::Printf(TEXT("Actor : %s"), *ActorLocation.ToString()));
}
```

위 코드에서 FString::Printf 안에서 %s는 TCHAR* 타입을 원한다. ActorLocation.ToString()은 FString 객체를 반환하므로, 그 앞에 **역참조 연산자(*)**를 붙여야 올바른 문자열 데이터로 변환된다.    

**더 자세한 설명**  
FString::Printf 함수에서 **%s**는 "여기에 문자열을 넣어줘"라는 약속이다. 그런데 표준 C++와 언리얼에서 %s는 FString 객체 그 자체를 이해하지 못한다.   

%s는 **"글자들이 적힌 종이의 시작점(주소)"**을 달라고 하는데, 우리는 **"종이가 들어있는 가방(FString 객체)"**을 통째로 던져주고 있는 상황이다.   

보통 C++에서 *는 포인터가 가리키는 실제 값을 가져오는 '역참조' 연산자이다. 하지만 언리얼의 FString 클래스는 이 * 연산자를 특별하게 재정의(Overloading) 해두었다.

FString 앞에 * 를 붙이면?  
"가방(객체) 안에 들어있는 실제 문자열 데이터(TCHAR*)의 시작 주소를 반환해라!"라는 뜻이 된다.   

***

<br/>

루프안에서 sleep(), delay()등을 쓰면 루프문 안에 있는동안 화면이 멈춘다. 그래서 비동기적인 방식인 타이머를 사용

  </p>
</details>

#### <!-- 26.03.18 -->
<details>
  <summary><s>26.03.18</s></summary>
  <p>

cpp 5번째 과제 제출 완료   
<br/>

***

cpp 코테 완전정복 2-4, 2-5, 3-1, 3-2

**코테 시간복잡도 관련 팁**   
문자열 '+'와 '+='의 성능 차이가 심하다.   
str = str + " ";   
str += " ";   
첫 번째는 문자열을 새로 만들어서 O(n)      
두 번째는 덧붙이는 방식이라 O(1)에 가깝다.   

for(auto a : ...)   
for(auto& a : ...)   
첫 번째는 복사를 해서 더 오래걸린다.   
참조 방식을 추천한다.   
<br/>

***
unique()
연속된 중복 요소들을 제거한다. 단, 실제로 제거하는건 아니고 중복되는 원소를 뒤로 다 밀어넣는다.(실제 반환값은 뒤로 밀려진 중복값중 첫번째 위치) 따라서 erase()를 함께 써야 실제로 지워진다.   

```cpp
//erase(), unique()예시
#include <vector>
#include <algorithm> // sort, unique를 위해 선언

using namespace std;

bool compare(int a, int b) { // 정렬 기준 정의
    return a > b; 
}

vector<int> solution(vector<int> lst) {
    sort(lst.begin(), lst.end(), compare); // 내림차순으로 정렬
    lst.erase(unique(lst.begin(), lst.end()), lst.end()); // 중복값 제거

    return lst;
}
```
<br/>

***
모듈러 연산으로 반복 패턴 표현   
```cpp
// 모듈러 연산 반복패턴 예시
...
    for (size_t i = 0; i < answer1.size(); ++i)
    {

        if (answer1[i] == SuPoJa1[i % SuPoJa1.size()])
        {
            Score[0] += 1;
        }
        if (answer1[i] == SuPoJa2[i % SuPoJa2.size()])
        {
            Score[1] += 1;
        }
        if (answer1[i] == SuPoJa3[i % SuPoJa3.size()])
        {
            Score[2] += 1;
        }
    }
...
// 수포자1~ 3벡터의 사이즈 만큼 반복하게 함
```

벡터로 변환
```cpp
// sum은 set<int>
vector<int> answer(sum.begin(), sum.end()); // 반환타입을 맞추기 위헤 벡터로 변환
```
  </p>
</details>


#### <!-- 26.03.19 -->
<details>
  <summary><s>26.03.19</s></summary>
  <p>

cpp 코테 완전정복 3-3 정렬   
삽입정렬, 계수정렬, 병합정렬, 힙정렬   
하나 하나 직접 구조 그려보면서 이해하기   
TIL, TMP파일 정리 안된거 싹 다 정리    


  </p>
</details>

#### <!-- 26.03.20 -->
<details>
  <summary><s>26.03.20</s></summary>
  <p>

cpp 코테 완전정복 3-4   
정렬 복습


```cpp
//코드카타 명예의 전당(1)
#include <string>
#include <vector>
#include <set>
#include <algorithm>

using namespace std;

vector<int> solution(int k, vector<int> score) {
    vector<int> answer;
    vector<int> tmp_vec;
    int index = 0;
    
    for(int value : score)
    {
        tmp_vec.push_back(value);
        sort(tmp_vec.begin(), tmp_vec.end());
        
        if(tmp_vec.size() < k)
        {
            answer.push_back(tmp_vec[0]);
        }
        else
        {
            answer.push_back(tmp_vec[tmp_vec.size() - k]);
        }
        
        ++index;
    }
    
    
    return answer;
}
// 벡터의 제일 오른쪽 값 3개가 크기순인걸로 풀었는데 이렇게 하면 나중에 tmp 벡터가 너무 길어져서 시간이 오래 걸린다. pop_back()을 활용하는게 좋다.

```
  
  </p>
</details>

#### <!-- 26.03.23 -->
<details>
  <summary><s>26.03.23</s></summary>
  <p>

시뮬레이션, 스택, 큐


**bitset**   

```cpp
// 비트셋을 이용하면 이진수 변환을 엄청 쉽게 할 수 있다. 아래에 나오는 substr() 활용하는법도 기억해두면 엄청 좋을듯.
#include <string>
#include <vector>
#include <algorithm>
#include <bitset>
#include <iterator>
#include <iostream>

using namespace std;

vector<int> solution(string s) {
  int transforms = 0;
  int removedZeros = 0;
  // s가 “1”이 될때까지 계속 반복
  while (s != "1") {
    transforms++;

    // '0' 개수를 세어 removedZeros에 누적
    removedZeros += count(s.begin(), s.end(), '0');

    // '1' 개수를 세고, 이를 이진수로 변환
    int onesCount = count(s.begin(), s.end(), '1');
    s = bitset<32>(onesCount).to_string();
    cout << s << endl;
    // s는 총 32비트라서 0000... 0110 이런식으로 나오게 된다. 따라서 밑에 코드로 앞에 0을 지워주는 방식을 택했다.
    s = s.substr(s.find('1'));
    // 처음으로 1이 나온 곳 부터 부분문자열로 만들어서 s에 저장한다. 
  }

  return {transforms, removedZeros};
}

using namespace std;

void print(vector<int> vec)
{
  copy(vec.begin(), vec.end(), std::ostream_iterator<int>(cout, " "));
  cout << endl;
}

int main()
{
  print(solution("110010101001")); // 출력값 : 3 8
  print(solution("01110")); // 출력값 : 3 3
  print(solution("1111111")); // 출력값 : 4 1
  
  return 0;
}
```
  
<br/> 

***

<br/> 

**스택**
```cpp
// 이 문제를 스택으로 풀어야 한다고 생각하고 접근했는데도 어떻게 해야할지 감도 안잡혔음. 이중 반복문으로 풀면 너무 쉬운 문제지만 시간복잡도 제한이 걸리면 이렇게 다른 방식으로 풀어야함.
// 특히 스택을 활용하면서 index 값을 넣는 방식을 쓴 것이 엄청 참신했음. 
// 현재값과 이전값을 비교할때 스택의 top()을 이전 값으로 활용
#include <iostream>
#include <vector>
#include <stack>

int main()
{
    std::stack<int> stack_index;
    std::vector<int> prices = {1, 2, 3, 2, 3};
    std::vector<int> result(prices.size());

    for (int i = 0; i < prices.size(); i++)
    {
        while (!stack_index.empty() && prices[i] < prices[stack_index.top()])
        {
            result[stack_index.top()] = i - stack_index.top();
            stack_index.pop();
        }
        stack_index.push(i);
    }

    while (!stack_index.empty())
    {
        result[stack_index.top()] = prices.size() - stack_index.top() - 1;
        stack_index.pop();
    }

    for (int i : result)
    {
        std::cout << i << " ";
    }

    return 0;
}

```

<br/> 

***

<br/>

**큐**

```cpp
// 오늘 코드카타로 풀었던 문제였는데 강의 듣다가 나옴. 코드카타에서 풀었을땐 직접적으로 큐를 이용하진 않고 의도치 않게 큐의 원리를 이용해서 풀었는데 마침 또 나와줘서 큐로 풀어봤음. 쉬운 문제라서 금방함. 강의 풀이에서는 goal까지 큐에 넣어서 활용했는데 굳이? 싶긴한데 더 깔끔하긴 할듯?
#include <iostream>
#include <queue>

std::string solution(std::vector<std::string> cards1, std::vector<std::string> cards2, std::vector<std::string> goal)
{
    std::queue<std::string> cards1_queue;
    std::queue<std::string> cards2_queue;
    for (std::string str : cards1)
    {
        cards1_queue.push(str);
    }
    for (std::string str : cards2)
    {
        cards2_queue.push(str);
    }
    for (std::string str : goal)
    {
        if (!cards1_queue.empty() && str == cards1_queue.front())
        {
            cards1_queue.pop();
        }
        else if (!cards2_queue.empty() && str == cards2_queue.front())
        {
            cards2_queue.pop();
        }
        else
        {
            return "No";
        }
    }
    return "Yes";
}

int main()
{
    std::cout << solution({"i", "drink", "water"}, {"want", "to"}, {"i", "want", "to", "drink", "water"}) << std::endl; // "Yes"
    std::cout << solution({"i", "water", "drink"}, {"want", "to"}, {"i", "want", "to", "drink", "water"}) << std::endl; // "No"
    return 0;
}

```

  </p>
</details>

#### <!-- 26.03.24 -->
<details>
<summary><s>26.03.24</s></summary>
<p> 

```cpp
// 덧칠하기 문제
// 풀었는데 논리 확인 한번만 더
#include <string>
#include <vector>

using namespace std;

int solution(int n, int m, vector<int> section) {
    int answer = 0;
    int tmp = 0;
    
    for(int i = 0; i < section.size(); ++i)
    {
        if(i == 0)
        {
            tmp = section[i] + m - 1;
            answer += 1;
        }
        
        if(tmp >= section[i])
        {
            continue;
        }
        else if(tmp < section[i])
        {
            if(section[i] >= n - m + 1)
            {
            answer += 1;
            break;
            }
            tmp = section[i] + m - 1;
            answer += 1;
        }       
    }   
    return answer;
}
```

트리 관련은 여기에 안하고 바로 정리   

코드카타 명예의 전당(1) 우선순위큐 사용해서 다시 풀어봄(정리 완)

트리에서 나온 문제 2개는 내일 정리

  </p>
</details>


#### <!-- 26.03.25 -->
<details> 
  <summary><s>26.03.25</s></summary>
  <p>
  예상 대진표/다단계 칫솔 판매 문제 정리(완)   
  코드카타 옹알이(2) 정리(완)   
  
  첫번째 팀 회의
  일단 기본에 충실하게 필수 기능 구현
  그리고 나서 도전기능 + 꾸미기 등등..

  </p>
</details>

#### <!-- 26.03.26 -->
<details> 
  <summary>26.03.26</summary>
  <p>
  </p>
</details>

