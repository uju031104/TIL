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
  <summary><s>26.03.26</s></summary>
  <p>

  팀 프로젝트 시작

  생성자와 소멸자   
  소멸자 앞에 virtual을 붙이면 해당 클래스가 소멸할때 자식이 있다고 알려줌   
  이렇게 해야 업캐스팅한 애가 소멸될 때 메모리 누수가 없음

  git add를 한 상태에서 pull 하려니까 실패함   
  git stash로 임시 저장소에 치우고 pull을 해줘야함   


  A - B - C 순으로 부모/자식 관계인 클래스가 있다.   
  A클래스에서 순수 가상 함수를 정의하고 B클래스에서 재정의 하지 않은채 C클래스에서 재정의를 한다.   
  이런 경우 B클래스는 객체를 생성하지 못해서 쓸모 없어 보이지만 B클래스는 객체 생성 목적이 아닌 자식 클래스에게 조금더 구체적인 정보를 전달하는 역할을 수행한다.   
  
  </p>
</details>

#### <!-- 26.03.27 -->
<details> 
  <summary><s>26.03.27</s></summary>
  <p>

하루종일 팀 프로젝트 진행(Monster 클래스 뼈대 완성 후 push)   
git 관련해서 엄청 많이 배웠음   
add stash pop restore 등등

vcxproj 파일에서 .h .cpp 파일 등을 include해준다   
vcxproj.filters에서는 비주얼 스튜디오 오른쪽에 보이는 폴더, 파일 등의 UI?를 구성해준다.   

서로 push를 하다보면 새로운 파일이 올라오는데 그걸 저 두 파일에 업데이트 안하고 올려버리면 pull해서 받는 사람한테 충돌이 생긴다.   
(물론 두 파일에 추가만 해줘도 돼서 금방 해결)   

근데 저 두 파일에 업데이트를 해서 올려주더라도 내가 새로운 파일을 작성하고 있으면(Local에만 있는 상태) 서로 충돌이 일어나는데 그럴땐 VSCode로 열면 충돌이 난 부분을 어떻게 할 것인지 선택지가 뜨고 거기서 선택하면 쉽게 해결   

    
  </p>
</details>

#### <!-- 26.03.30 -->
<details> 
  <summary><s>26.03.30</s></summary>
  <p>

코드카타 이후 하루종일 팀 프로젝트

구현하다보니 A->B->C 순서로 상속된 내 클래스 구조에서 접근 불가능한 상황이 왔다.(A로 업캐스팅 된 C인데 B에서 생성한 메서드에 접근해야하는 상황...)   
접근 가능하게 하려면 최상위 클래스에 구현해야하는데 그걸 건드리면 나 포함 총 3명이 다 뜯어 고쳐야해서 큰일났나 했는데 다운캐스팅이 생각났다.   
밑에는 고친 코드   

```cpp
auto monsterPtr = std::dynamic_pointer_cast<Monster>(enemy); // getAsciiArt()에 접근하기 위한 다운캐스팅
```

<br/>

확률에 따라 몬스터가 등장하게 만들때 사용한 코드   
이렇게 간단하게 구현할 수 있다.   
```cpp
// 가중치 기반(거리에 따른 몬스터 확률) 랜덤 선택 (0 ~ 99)
int dice = rand() % 100;      // 랜덤한 값 저장
int cumulative = 0;           // 누적 값
int selectedIndex = 0;        // 뽑힌 몬스터의 인덱스

for (int i = 0; i < 5; i++)
{
				cumulative += table.monster[i];   // 계속 더하기 때문에 마지막엔 무조건 100이 돼서 뽑힘
				if (dice < cumulative)
				{
					selectedIndex = i;
					break;
				
```
    
  </p>
</details>


#### <!-- 26.03.31 -->
<details> 
  <summary><s>26.03.31</s></summary>
  <p>

코드카타 이후 하루종일 팀 프로젝트

몬스터, 플레이어 스탯 밸런싱/몬스터 골드 드랍 추가/전투 출력 개선   

던전에서 캐릭터 사망 시 아무런 변화가 없던 문제 수정(죽으면 피 회복하고 던전에서 마을로 추방됨)   

포션을 사용하면 maxHP 이상으로 차는 현상 수정   

경험치 스크롤을 사용할때 플레이어의 경험치가 비정상적으로 쌓이고 레벨업이 안되는 현상 수정

 ppt, 대본 작성   
  </p>
</details>


#### <!-- 26.04.01 -->
<details> 
  <summary><s>26.04.01</s></summary>
  <p>

코드카타

```cpp
    // 처음에 오류난 코드
    for(const char &chr : s)
    {
        char tmp = chr;
        int indx = index;
        while(indx != 0)
        {
            if(skip_map.find(tmp) != skip_map.end())  // skip 해야하는 상황
            {
                ++tmp;
            }
            else // skip 안하는 상황
            {
                ++tmp;
                --indx;
            }
            
            if(tmp > 122)
            {
                tmp = 'a';
            }
        }
        answer += tmp;
    }

    // 수정한 코드. 논리 순서가 잘못된거였음
    for(char tmp : s)
    {
        int count = 0;
        while(count < index)
        {
            tmp++;
            
            if(tmp > 122)
            {
                tmp = 'a';
            }
            
            if(skip_map.find(tmp) == skip_map.end())  // skip 안하면
            {
                ++count;
            }
        }
        answer += tmp;
    }
```
 
 코드카타 67 둘만의 암호   
-> 코드 논리적 순서 차이로 갈림. 다시 확인(완료)   

코드카타 68 햄버거 만들기   
나름 stack을 잘 활용해서 뿌듯함   
-> 다른사람풀이 봤는데 벡터를 스택처럼 활용하고 코드도 짧다. 같은 원린데 코드 길이가 너무 차이난다.

코드카타 69번 성격유형검사   
-> map 사용해서 쉽게함.

코드카타 70번 바탕화면 정리
-> x, y축이 헷갈렸지만 금방 풀었다.

코드카타 71번 개인정보 수집 유효기간   
-> 내 방식이 코드가 좀 길어서 다른사람 풀이를 봤는데 일수로 환산하는게 더 효율적인듯하다.

  </p>
</details>

#### <!-- 26.04.02 -->
<details> 
  <summary><s>26.04.02</s></summary>
  <p>
  
  cpp 배치고사 하는데 template 기본 문법이 생각이 안나서 TIL보고 참고했음 

```cpp
// 얜 진짜 봐도봐도 안익숙하다
// 앞으로 좀 써봐야겠다
template <typename T>
```

map 쓰는 문제에서 구현하는부분 말고 이미 적혀있던 출력 부분에서 map을 first, second 값으로 루프 돌릴 수 있다는걸 알게됨   
평소에 코테 문제 풀 때 map을 많이 썼는데 중복이 없고 특정 값에 빠르게 접근하는 용도로만 쓰다보니 저 문법이 머릿속에 없었음(까먹은건가?)

근데 굳이 value가 필요없어서 set을 써도 될 것 같은 문제들이 은근히 많은데 set을 워낙 안써서 습관적으로 map이랑 unordered_map만 쓴다. set을 좀 써봐야할듯. 

```cpp
// C++ 17 부터는 이렇게 사용하면 더 편하다고 한다
for (const auto& [id, name] : students) {
    // .first 대신 id, .second 대신 name을 바로 사용!
    std::cout << "학번: " << id << ", 이름: " << name << std::endl;
}
```


이력서 세션 후기 : 코테랑 포트폴리오에 목숨걸자

  </p>
</details>


#### <!-- 26.04.03 -->
<details> 
  <summary><s>26.04.03</s></summary>
  <p>

vector에서 find()로 반복자를 찾았을때 그 반복자를 활용하는 방법을 알게됨   
단순하게 -1 같은 연산을 해서 주변 값으로 접근도 가능하고 prev()를 쓰면 이전 값으로 간다   
그리고 그 반복자에 *를 붙여주면 값이 나온다(인덱스 아님)

distance(v.begin, it) 이런식으로 하면 맵의 인덱스 값도 알 수 있음. 하지만 효율은 떨어짐

코드카타 72번   
-> map을 사용하여 풀었지만 index 값을 따로 관리 안해서 distance를 이용하다보니 시간초과가 떴음   
단순하게 map에서 인덱스도 같이 포함시키고 벡터 값을 서로 바꿀때 map의 값도 바꿔주는 형식으로 풀었더니 바로 풀림   
너무 어렵게 생각해서 오래 걸림.   

**오늘 커리어 데이 한거 간단하게 정리**   
(캡쳐 따로 해놓긴 했음)  
 
면접 준비는 지금부터...   
서류 코테 등 통과하고 준비하면 무조건 버벅인다.   
지금부터 간단한 1분 자기소개, 장단점, 갈등 해결사례 등등을 생각해보고 적어두고 말해보자.   

코테는 매우 중요
DFS, BFS, 탐욕기법 등은 기본

(세상에서 가장 어려운) 매일 매일 꾸준히 하는게 제일 중요.   

언리얼 엔진은 게임에만 쓰는게 아니다. 시야를 넓혀서 보자.   

공고를 보고 내가 키워야하는 역량을 잘 분석하자.   
같은 클라 개발자라도 매우 다양하다.   
일단 나는 전투 쪽으로 가고싶어서 여러가지 구상을 미리 하는중   


  </p>
</details>

#### <!-- 26.04.06 -->
<details> 
  <summary><s>26.04.06</s></summary>
  <p>

**<UE5 초반 설명, 팁 들>**  
솔루션 구조: 비주얼 스튜디오에 있는 폴더구조

`Engine`: 말 그대로 엔진의 코드들을 담고 있는 폴더   
`Games`: 실제로 작업할 폴더
-> Games 폴더에 project가 있는데 이게 루트 폴더
Programs: 유틸리티, 외부 툴 등   
`Config`: 게임의 여러가지 설정들이 담겨있는 폴더   
`Rules`: 빌드 규칙들을 담아놓은 폴더   
`Visualizers`: 디버깅 할때 언리얼의 자료구조를 편하게 하기위한 파일설정들이 담겨있는 폴더   

VS에서 빌드를 하면 dll 파일을 갱신하는데 언리얼 에디터가 켜져있으면 이전 dll을 붙잡고 있는 경우가 많아서 에디터를 끄고 빌드하는걸 추천   

빌드가 꼬였을 때 대처하는 방법   
-> 에디터, VS 다 끄고 프로젝트 폴더로 가서 `Derivedcache`(캐시 파일 저장 폴더), `Intermediate`(임시 빌드 파일 저장 폴더), `Saved`(로그 파일 저장 폴더) 이 3개를 삭제해준다. 추가로 `Binaries`(Win64 등 구동한 OS 저장 폴더) 삭제를 해도 된다.   
그리고 uproject 파일을 우클릭해서 Generate Visual Studio project files를 클릭해준다.   
이 상태에서 uproject를 실행하면 된다.(리빌드 뭐시기 뜨면 ok 누르기)    
이 방법으로 60~ 70%는 해결된다.   

이 방법으로도 안되면   
-> 솔루션 파일로 들어가서 Build - Clean Solution 클릭 (클린빌드, 이전에 빌드된걸 깔끔하게 정리)   
그리고 다시 전체 빌드해주기   

이 두 방법이면 90%는 해결된다.   


모든 클래스는 오브젝트 클래스를 상속받는다.   
오브젝트 클래스는 배치할 수 있지 않고 추상적인 개념이다. 데이터나 로직을 담당(캐릭터 스탯 등)   

액터를 상속받는 애들은 실제로 배치가 가능하다.(물론 액터도 오브젝트 클래스를 상속받음)   

액터를 삭제하고 싶으면 VS에서 솔루션 구조에 있는 .h, .cpp 파일을 삭제하면 되는게 아니고 실제 폴더로 들어가서 삭제도 해줘야한다.   

액터는 최소한 하나의 root 컴포넌트가 있어야 좌표도 인식하고 제대로된 기능을 한다.   

Root 컴포넌트는 자동으로 리플렉션 시스템에 등록된다.   

X축 값을 `Roll`   
Y축 값을 `Pitch`   
Z축 값을 `yaw`   

World 좌표와 Local 좌표   
블루프린트에서 Set Actor Location의 그 좌표가 World 좌표이다.   
Set Relative Location을 사용하면 Local 좌표를 수정한다.   
Local 좌표는 Root Component와 상대적인 위치를 나타낸다.   

**<컴포넌트 붙이기(구조 설정)>**   
```cpp
AItem::AItem()
{
    SceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneRoot"));
    // 루트 컴포넌트로 설정해주기(+루트는 자동으로 리플렉션 시스템에 등록)
    SetRootComponent(SceneRoot);

    StaticMeshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("StaticMesh"));
    // 컴포넌트 붙이기
    StaticMeshComp->SetupAttachment(SceneRoot);

    static ConstructorHelpers::FObjectFinder<UStaticMesh> MeshAsset(TEXT("/Game/Resources/Props/SM_Chair.SM_Chair"));
    if (MeshAsset.Succeeded())
    {
        StaticMeshComp->SetStaticMesh(MeshAsset.Object);
    }

    // Metarial은 여러개가 될 수 있어서 아래처럼 (0, 머터리얼 변수명.Object)로 1개만 쓴다고 알려줘야함
    static ConstructorHelpers::FObjectFinder<UMaterial> MaterialAsset(TEXT("Game/Resources/Materials/M_Metal_Gold.M_Metal_Gold"));
    if (MaterialAsset.Succeeded())
    {
        StaticMeshComp->SetMaterial(0, MaterialAsset.Object);
    }
}
```

<br/>

**<오디오 컴포넌트 에러>**   
오디오 컴포넌트 붙이는 과정에서 에러가 뜨길래 이유를 찾아봤더니 헤더파일이 없어서 그랬다. 스태틱 메쉬는 기본으로 포함되는데 오디오는 따로 포함시켜줘야 했다.

```cpp
#include "Components/AudioComponent.h"
// 오디오 컴포넌트를 쓰기 위한 헤더파일
```

위 코드를 강의를 보면서 따라 작성했는데 스태틱 메시는 루트에 붙어있고 오디오는 메시에 붙어있어서 꼭 이렇게 해야하는지 확인해봤더니 상속 관계를 설정하는거였다.   
위 처럼 설정하면 스태틱 메쉬가 움직이면 오디오도 움직이고 따로 Root를 상속받게 하면 서로 영향을 안준다.   

<br/>

**<헤더 파일 위치 오류>**   
```cpp
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Item.generated.h"
#include "Components/AudioComponent.h"
```

이런식으로 했더니 generated.h가 무조건 마지막에 와야한다고 에러가 났다.   
위치를 바꿨더니 바로 해결   

<br/>

**<오디오 문법 오류>**   

헤더파일에 UAudioComponent 클래스를 사용하여 포인터 변수를 만들어줘서 사용할때도 오디오 관련으로 해야하는줄 알았는데 오디오는 기계의 개념이고 여기서 `Sound`를 설정해야하는거였다.   

```cpp
static ConstructorHelpers::FObjectFinder<USoundBase> SoundAsset(TEXT("/Game/Resources/Audio/Fire01_Cue.Fire01_Cue"));
if (SoundAsset.Succeeded())
{
    // 사운드 세팅
    AudioComp->SetSound(SoundAsset.Object);

    // 사운드 자동재생 세팅
    AudioComp->bAutoActivate = true;
}
```

<br/>

**<머터리얼이 출력 안되는 오류>**   
사운드를 넣고나서 실행했더니 사운드는 들리는데 금색 머터리얼이 안입혀졌다.   
알고보니 머터리얼 경로 붙여넣은거에 / 하나가 빠져있었다...   

<br/>

**<로그 메세지>**   

```cpp
UE_LOG(LogTemp, Warning, TEXT("My Log!"));
// LogTemp는 카테고리
// Display는 흰색, Warning은 노란색, Error는 빨간색으로 나온다.
// TEXT는 출력 메세지
```

<br/>

**<로그 카테고리 만들기>**    
```cpp
// LogSparta는 만든 카테고리 이름
// Warning이상의 메세지 출력
// All은 나중에 필요하면 모든 Log를 쓸 수 있게 열어두는 것
// 이 부분은 헤더에 정의
DECLARE_LOG_CATEGORY_EXTERN(LogSparta, Warning, All);

// cpp에 구현
DEFINE_LOG_CATEGORY(LogSparta);

보통은 로그만 모아둔 헤더를 따로 만들어서 관리
```

<br/>

**<Life Cycle 함수>**   

생성자   
-> 메모리에 생김. 딱 한번 호출

PostInitializeComponents()   
-> 컴포넌트가 완성된 직후 호출. 컴포넌트끼리 데이터 주고받기, 상호작용   

BeginPlay()   
-> 배치(Spawn) 직후   

Tick(float DeltaTime)   
-> 매 프레임마다 호출됨   

Destroyed()   
-> 삭제되기 직전에 호출된다(리소스 정리하면 좋음)   

EndPlay()   
-> 게임 종료, 파괴(Destroyed()), 레벨 전환   

Destroyed()를 부르면 EndPlay()도 호출된다.   
근데 게임을 그냥 종료해버는 상황이라면 EndPlay()만 호출   

팁 : 로그 찍을 때 Destroyed()와 EndPlay()는 Super::~ 부분 위에 하는게 좋다.   

<br/>

**<액터를 배치할때 로그가 더 많이 뜨는 현상>**   

액터를 배치하면 Constructor Log만 떠야할 것 같은데 Constructor - Destroyed - Constructor 순서로 뜨길래 뭔지 찾아봤음   

에디터 내부에서 액터 재생성(Reconstruction) 과정을 거친다고 함   
액터를 뷰포트에 끌어다 놓을때 생성되고 위치가 확정될 때 파괴되고 그 직후 최종 액터가 생성된다고 함   

<br/>

**<Tick()에서 LOG가 안뜨는 현상>**   

```cpp
PrimaryActorTick.bCanEverTick = true;
// 생성자에 이걸 추가해주면 된다. 틱은 기본적으로 false
```

<br/>

**<Actor Transform 변경>**   

```cpp
void AItem::BeginPlay()
{
    Super::BeginPlay();
    
    SetActorLocation(FVector(300.0f, 200.0f, 100.0f));
    SetActorRotation(FRotator(0.0f, 90.0f, 0.0f)); // pitch, yaw, roll 짐벌락 문제? Quaternion
    SetActorScale3D(FVector(2.0f)); // 하나만 적으면 전체가 다 2배된다.

    // 3가지를 한 번에 관리하는 방법
    FVector NewLocation(300.0f, 200.0f, 100.0f);
    FRotator NewRotation(0.0f, 90.0f, 0.0f);
    FVector NewScale(2.0f);
    FTransform NewTransform(NewRotation, NewLocation, NewScale);

    SetActorTransform(NewTransform);
}
```

<br/>

**<Tick() 함수>**   

```cpp
void AItem::Tick(float DeltaTime)
{
    // 120프레임 - 1초 / 120 = DeltaTime
    //  30프레임 - 1초 /  30 = DeltaTime 
    // 1초에 90도씩 회전
    // 90도 / 120 ,  90도 / 30
    Super::Tick(DeltaTime);

    if (!FMath::IsNearlyZero(RotationSpeed))
    {
        AddActorLocalRotation(FRotator(0.0f, RotationSpeed * DeltaTime, 0.0f));
    }

    //AddActorLocalRotation(FRotator(0.0f, RotationSpeed, 0.0f));  // 컴퓨터 마다 프레임이 달라서 이런 방식은 안된다.  

}
```
컴퓨터마다 프레임이 다르기 때문에 Tick으로 호출하면 안된다. 따라서 DeltaTime을 사용해야한다.   
DeltaTime은 1프레임당 시간이다. 따라서, 프레임이 높을수록 DeltaTime은 작아진다.   
회전하는 값에 DeltaTime을 곱해주면 프레임에 상관없이 같은 시간에 같은 값만큼 회전하게 된다.    

**<IsNearlyZero>**   

위 예시에서 `FMath::IsNearlyZero()`를 썼는데 부동소수점은 정확한 0인지 판단하기 어렵기 때문에 이걸 써줘야 판단이 가능하다.   

<br/>

**<헤더에서 함수를 호출했을때 오류>**   

시간을 가져오는 함수를 써서 변수를 만들어놓으려고 헤더파일에 구현을 했다. 그랬더니 nullptr를 반환하고 오류가 났다.   
```cpp
float Time = GetWorld()->GetTimeSeconds();
// BeginPlay()(월드 시간 가져오기)나 Tick()(현재 흐르는 시간)에서 구현하자.
```

<br/>

**<Scale은 변화를 주는 로직이 다르다>**   

Location과 Rotation은 변화를 주는 함수가 존재한다.   
`AddActorLocalOffset()`과 `AddActorLocalRotation()`   

하지만 Scale은 따로 변화를 담은 변수를 만들고 그걸로 `SetActorScale3D()`를 다시 써야한다.

```cpp
void ASquare::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

    // 현재 흐르는 시간(초단위)
	float Time = GetWorld()->GetTimeSeconds();
    // 2.0f 스케일에서 -1 ~ 1 범위로 변동
	float ScaleSpeed = 2.0f + FMath::Sin(Time);

	SetActorScale3D(FVector(ScaleSpeed));
}
```

<br/>

**<FMath::Sin() 사용법>**   

```cpp
// 시간 세팅
float Time = GetWorld()->GetTimeSeconds();

// 기본적인 -1 ~ 1의 범위
float S = FMath::Sin(Time);
// 5.0f는 속도이다. 높을수록 빨라진다.
float S = FMath::Sin(Time * 5.0f);
// 50.0f는 범위이다. 높을수록 범위가 크다.
float S = FMath::Sin(Time * 5.0f) * 50.0f;
```

**<리플렉션 시스템>**      

메시나 머터리얼 등을 UE5 에디터에서 손쉽게 만질 수 있게 하는 기능 

<br/>

**<Class 리플렉션>**   

```cpp
#include "Item.generated.h"
// 위에서 오류의 원인이었던 헤더파일인데 이 파일이 리플렉션 시스템을 지원하는 헤더파일이다.
UCLASS()
// 클래스를 리플렉션 시스템을 등록해주는 기능을 한다.
GENERATED_BODY()
// 리플렉션 데이터를 자동으로 생성하기 위해서 엔진이 사용하는 매크로
```

UCLASS()은 인자들이 있다.
UCLASS(Blueprintable, BlueprintType)는 인자에 아무것도 안 쓴 상태(UCLASS())랑 같다.

Blueprintable은 상속이 가능하다는 뜻인데 NotBlueprintable처럼 상속을 막을수도 있다.   

BlueprintType은 블루프린트에서 해당 클래스를 상속받거나 변수로 선언하거나 참조할 수 있게 한다.   

UCLASS(BlueprintType)   
이렇게만 하면 상속은 불가능해서 헷갈릴 수 있다. 명시적으로 써주는게 좋다.   

<br/>

**<변수 리플렉션>**   

```cpp
UPROPERTY()
USceneComponent* SceneRoot;
// 이런식으로 변수 위에 적으면 해당 변수가 리플렉션 시스템에 등록됨 
```

클래스와 다르게 변수는 디폴트 인자값이 없어서 따로 설정해줘야 한다.

```cpp
UPROPERTY(값 수정 유무, 블루프린트 get/set 유무, 카테고리 설정)
```

값 수정   
`VisibleAnywhere`: 둘 다 수정 불가   
`EditAnywhere`: 클래스 디폴트, 인스턴스 수정 가능   
`EditInstanceOnly`: 인스턴스만 수정 가능   
`EditDefaultsOnly`: 클래스 디폴트만 수정가능   

블루프린트   
`BlueprintReadOnly`: Get()만 가능   
`BlueprintReadWrite`: Get(), Set() 가능   

카테고리   
`Category="Item|Properties"`  
-> Item 하위 Properties에 넣겠다.

<br/>

**<함수 리플렉션>**   

```cpp
UFUNCTION(블루프린트 get/set 유무, 카테고리 설정)
```
함수도 인자를 적어줘야 한다.

`BlueprintCallable`: 블루프린트에서 호출 가능   
`BlueprintPure`: 블루프린트에서 값만 반환받는 함수로 호출   
`BlueprintImplementableEvent`: 구현을 C++이 아닌 블루프린트에서 했는데 C++에서도 호출 가능하게 한다   


  </p>
</details>

#### <!-- 26.04.07 -->
<details> 
  <summary>26.04.07</summary>
  <p>

**<Root 설정에 따른 차이>**

Root를 누구로 설정하냐에 따라 바뀌는 점이 궁금해서 찾아봄   

SceneComponent를 Root로 설정하면 가상의 점이 중심이 된다. 따라서 그 가상의 점을 옮겨서 그걸 중심으로 회전하는 등 다양한 구현이 가능   
하지만 그만큼 복잡해질 수 있다.

StaticMeshComponent를 Root로 설정하면 그 자체로 중심이 된다. 따라서 기본적인 물리 엔진을 적용할때 편하다.   
하지만 복잡한 구조는 불가능하다.   

**<UActorComponent 사용>**   

다양한 움직임을 가진 큐브들을 만들때 클래스를 하나하나 만들어야 하진 않을테고 방법을 찾아봤다.   
 UActorComponent를 상속받은 클래스를 하나 만들어서 해당 클래스에 다양한 움직임들을 구현한 후 에디터에서 Actor의 Detail 창에서 Add 해주면 된다고 한다.   

```cpp
// 헤더파일에 열거형 클래스를 하나 만들어주고
UENUM(BlueprintType)
enum class EMoveAction : uint8 {
	Idle UMETA(DisplayName = "Idle"),
	UpDown UMETA(DiaplayName = "UpDown"),
	LeftRight UMETA(DisplayName = "LeftRight"),
	Scale UMETA(DisplayName = "Scale"),
	Rotate UMETA(DisplayName = "Rotate")
};

// Switch문으로 나눠준다.

	switch (SeletedAction)
	{
	case EMoveAction::UpDown:
		Owner->AddActorLocalOffset(FVector(0, 0, Range * Value * DeltaTime));
		break;
	case EMoveAction::LeftRight:
		Owner->AddActorLocalOffset(FVector(0, Range * Value * DeltaTime, 0));
		break;
	case EMoveAction::Scale:
		Owner->SetActorScale3D(FVector(1.0f + (Range + 1) / 2));
		break;
	case EMoveAction::Rotate:
		Owner->AddActorLocalRotation(FRotator(0, Speed * DeltaTime, 0));
		break;
	}
```

**<짐벌락(Gimbal Lock)이란?>**  

3차원 공간 회전을 계산할 때 사용하는 오일러 각도(Euler Angles) 방식(Roll, Pitch, Yaw)의 구조적 결함   
세 개의 회전축 중 두 개의 축이 겹쳐지면서 한 방향의 자유도를 완전히 잃게됨   

언리얼의 `AddActorLocalRotation`은 이를 어느정도 보정을 해주는데, 아주 정교한 작업을 할 때는 `FQuat`를 써야한다.   

FQuat 예시   
```cpp
// 1. 원하는 회전량을 FRotator로 만듦
    FRotator DeltaRotation(0, Speed * DeltaTime, 0);

    // 2. 이를 쿼터니언(FQuat)으로 변환하여 적용 (짐벌락 방지)
    Owner->AddActorLocalRotation(DeltaRotation.Quaternion());
    break;
```

<br/>

이것 저것 만지다 보니 Root의 Transform과 StaticMesh의 Transform이 달라져서 회전축이 이상하거나 이동도 이상해진다... 신경써야겠다.   

**<큐브가 기존 위치로 오지 않는 현상>**   

큐브가 상하운동을 하는데 내가 설정한 처음 위치에 딱 맞게 오지 않았다. 검색해보니 흔한 부동소수점의 오차로 발생하는 현상이라고 한다. `AddActorLocalOffset`을 사용하다 보니 이 오차가 계속 더해지고 빼지고 한다.   

그래서 로직을 바꿔서 기존 위치에서 설정해준 sin의 범위만큼 더한 값으로 새로 `SetActorLocation`을 해줬다. 이렇게 하니 오차가 거의 없는 수준으로 느껴지는데 문제는 입력해야하는 범위값이 너무 커졌다.   
원래는 Value에 1000.0f를 넣어놨는데 얘는 그만큼 움직이려면 거의 5000.0f는 필요한느낌이다.   

-> 원인  
프레임 독립적이게 `DeltaTime`을 쓴 것이 오히려 문제였다. 내 로직에서는 `GetWorld()->GetTimeSeconds()`를 써서 이미 프레임과 상관없는 시간초로 설정을 해놨기 때문에 굳이 DeltaTime을 쓸 필요가 없었다.   
근데 Scale 빼고 모든곳에 DeltaTime을 써놔서 이것도 수정해봐야겠다. 어쩐지 다른 애들도 입력값과는 조금 다른 거리를 움직인다했다...   

여기서 `DeltaTime`과 `GetTimeSeconds()`의 차이가 궁금해서 찾아봄   

`GetTimeSeconds()`: 함수 방식이며 반복되는 정확한 패턴을 만들 때 사용하면 좋음   
`DeltaTime`: 누적 방식이며 상호작용과 물리적인 움직임에서 사용하면 좋음   
결론: 알잘딱으로 쓰면 좋고 두 방식을 섞어서 쓰는 경우도 있다.   

지금 내가 만들고 있는 첫 번째 과제는 정확한 반복 패턴을 요구하기 때문에 누적방식 보다는 함수 방식이 훨씬 좋을 것 같다. 그래서 수정해야겠다.   
수정하다보니 Rotation은 DeltaTime의 누적방식이 오히려 권장된다고 하는데 억지로 함수 방식으로도 구현을 한번 해봤다.  

-> 추가로 구현   
 Root(태양)를 기준으로 회전(공전)하는 Cube(지구)가 자전을 하게 만들고 싶어졌는데 여기서 문제가 이런 움직이는 기능들을 따로 `UActorComponent`로 만들었는데(정확히는 상속 받은 클래스) 여기서 액터의 컴포넌트에 접근하는 방법을 모른다는거다.   

 그래서 찾아봤더니
```cpp
// 헤더 파일에 스태틱 매쉬를 추가
#include "Components/StaticMeshComponent.h"


// cpp 파일에 코드 추가
// Cube가 자전하는 기능을 위해 StaticMeshComponent에 접근한다.
UStaticMeshComponent* StaticMesh = GetOwner()->FindComponentByClass<UStaticMeshComponent>();
if (StaticMesh)
{
	StaticMesh->AddLocalRotation(FRotator(0, -Speed * DeltaTime, 0));
}
break;
```
-> 여기서 알게된 사실   
공전과 자전을 같은 값으로 하고 부호만 반대로 하니까 액터가 가만히 멈춘 상태로 공전을 하게된다ㅋㅋ   


<br/>

**<생성자에서 컴포넌트를 불러와서 생긴 오류>**   

Component가 아직 다 Attach 안됐는데 실수로 `InitialLocation = GetOwner()->GetActorLocation()`를 생성자에 작성해버렸다. 바로 nullptr 에러가 떠버림.   
바로 BeginPlay()에 옮겼다.   
익숙하지 않아서 실수가 엄청 많다.   



  </p>
</details>

#### <!-- 26.04.08 -->
<details> 
  <summary>26.04.08</summary>
  <p>
어제 작성했던 자전기능을 위한 Owner()의 스태틱 메쉬에 접근하는 코드를 Tick()에 넣어놨는데 이러면 비용이 많이 든다.   

->수정   
헤더파일에 변수 선언하고 BeginPlay()에서 값을 넣어준다.   

Scale은 다른 이동에 비해 매우 작은 값이 필요해서 따로 변수를 만들어줘야겠다.   
추가로 회전 속도도 만듦   

**<3초마다 이동이 바뀌는 로직에서 회전만 안되는 문제>**

가만히, 위아래, 좌우, 크기변경 까지는 잘 되는데 회전만 실행이 안된다.   
원인 파악을 위해 일단 로그를 찍어보았다.   
로테이션은 실행 되는데 알고보니 공전, 자전을 세팅했던 코드가 문제였다. 서로 상쇄돼서 회전이 안되는것.   

**<타입 캐스팅 문법>**   
`static_cast<T>(v)` 방식으로 쓰면 안전성과 가독성이 높아지고 실수를 했을 때 컴파일 에러를 발생시켜줘서 좋다.   

**<언리얼에서의 열거형>**   
`enum class EnumName : uint8` 이런식으로 써주는데 enum class를 사용하면 EnumName::Name 처럼 호출하기 때문에 이름이 겹치는 오류에서 안전하다.   
그리고 강제로 `static_cast`를 써서 숫자와 계산을 하게 만들기 때문에 안정성이 높아진다.   
또한 `uint8(1바이트)`를 사용해서 메모리를 아낄 수 있고 uint8은 언리얼의 리플렉션 시스템이랑 제일 잘 맞는다.   





Map + delegate + struct를 활용해서 5가지 이동방식을 나누는 방법을 시도하는 중...   



  </p>
</details>

#### <!-- 26.04.09 -->
<details> 
  <summary>26.04.09</summary>
  <p>

모의면접시간에 나온 여러가지 질문들/팁 

구조체를 클래스가 상속 받을 수 있나?   
캡슐화 말고 객체지향의 특징은?   
구조체 new 생성가능?   
가비지 컬렉션에 대해서 더 깊이 설명?   

대답할때 버퍼링이 생길경우 물은 한모금 마셔서 시간을 벌거나/ 면접관에게 너무 긴장해서 생각할 시간 조금만 달라고 하기   

**<Delegate 관련 알게된 점>**   

Delegate를 정의할때 받을 함수 인자의 갯수에 따라 다르게 정의해야 한다.   
오버로드 기능이 없기 때문에 실행할 함수중 인자의 갯수가 가장 많은 함수를 기준으로 정의해야한다.   

```cpp
// 인자 0개
DECLARE_DELEGATE(FActionDelegate);
// float형 인자 1개
DECLARE_DELEGATE_OneParam(FActionDelegate, float);
// float, FVector 인자 2개
DECLARE_DELEGATE_TwoParams(FActionDelegate, float, FVector);

// 이런식으로 작성한다.
```

https://dev.epicgames.com/documentation/unreal-engine/delegates-and-lambda-functions-in-unreal-engine   
공식 문서인데 아직 익숙하지 않아서 머리아프다..

<br/>

**<IsVaild() 잘 쓰기>**   

```cpp
IsValid(GetOwner())
```
`GetOwner()`가 destroyed 되거나 그 직전 상황인 경우 크래시가 날 수 있기 때문에 무조건 검사를 하는 습관을 기르자.   

<br/>

**<random 값 간단하게 만들기>**   

```cpp
FVector RandomOffset(
	FMath::RandRange(-100.0f, 100.0f),
	FMath::RandRange(-100.0f, 100.0f),
	FMath::RandRange(-100.0f, 100.0f)
);
```
위 코드처럼 `FMath::RandRange()`에 범위를 넣어주면 된다. float를 넣으면 자동으로 float이 나온다. 매우 편하다.   

<br/>

**<Clamp: 범위 내에 가두기>**

```cpp
float Health = 120.0f;
Health = FMath::Clamp(Health, 0.0f, 100.0f); 
// 결과: 100.0f (체력은 100을 넘을 수 없음!)
```
아주 유용하다.   

<br/>

**<Lerp: 점진적인 연결>**   

$$FMath::Lerp(Start, End, Alpha)$$
Lerp는 Linear Interpolation(선형 보간)의 약자.   
-> 두 지점 사이의 중간값을 비율로 찾기   

부드러운 연출을 나타내기에 매우 훌륭하다.   

```cpp
ElapsedTime += DeltaTime;

// 0.0 ~ 1.0 범위로 정하고 (경과된 시간 / 내가 정해준 시간)으로 로직을 설정했다.
// 내가 정한 시간만큼 흐르면 Alpha값이 최대값인 1.0이 된다.
float Alpha = FMath::Clamp(ElapsedTime / ActionMap[EAction::Disappear].Duration, 0.0f, 1.0f);

// 시간이 흐를수록 Alpha값이 1.0에 다가가게 하여 
// 현재 크기부터 0까지 부드럽게 줄어들게 만듦
FVector NewScale = FMath::Lerp(StartScale, FVector::ZeroVector, Alpha);
```

<br/>

**<SpawnActor 사용법>**   

이 친구가 좀 머리아프게 했는데, 알고보니 BP 클래스 하나 만들어서 걔를 스폰하게 하는애였다.   
그래서 BP_Cube 하나 만들어서 내가 만든 ActorComponent 붙이고 스폰에 성공했다.

```cpp
// 이런식으로 블루프린트 연결할 변수와 생성할 개수를 담는 변수를 만들어주고(헤더파일에)
UPROPERTY(EditAnywhere, Category = "Spawn")
TSubclassOf<AActor> ActorToSpawn;

UPROPERTY(EditAnywhere, Category = "Spawn")
int32 SpawnCount = 5;

// 생성할 기준을 설정하여 World에 스폰해준다.
World->SpawnActor<AActor>(ActorToSpawn, RandomLocation, RandomRotation);
```

  </p>
</details>

#### <!-- 26.04.10 -->
<details> 
  <summary>26.04.10</summary>
  <p>

**<UBT, UDT, CDO, Reflection>**   

**UBT**

UBT(Unreal Build Tool)는 전체 빌드 프로세서를 관리한다.   

소스 코드를 분석해서 모듈 간의 의존성을 파악하고 컴파일러에게 어떤 파일을 빌드 할지 명령한다. 필요한 경우 UHT를 실행시킨다.  

<br/>

**UHT**   

UHT(Unreal Header Tool)는 소스 코드 내의 매크로(UCLASS, UPROPERTY, UFUNCTION 등)를 감지하는 파서(Parser)이다.   

헤더 파일에서 언리얼 매크로를 발견하면 해당 클래스의 리플렉션 정보를 담은 별도의 C++ 코드(.generated.h 및 gen.cpp)를 자동으로 생성한다.   

<br/>

**CDO**   

CDO(Class Default Object)는 언리얼의 메모리 최적화와 기본값 관리를 위한 핵심 개념이다.   
각 클래스 마다 딱 하나만 존재하는 기본 객체이며 생성자를 통해 생성된 기본 값들을 여기에 저장한다.   
이를 이용해서 새로운 인스턴스를 생성할 때, CDO를 복사해서 만든다.(템플릿)   

<br/>

**Reflection**   

리플렉션은 프로그램 실행중에 자기 자신의 구조(클래스, 변수, 함수 등)를 조사하고 수정할 수 있는 능력이다.   
언리얼은 UClass와 같은 메타데이터를 가진 객체를 생성하여 이를 관리한다.   

<br/>

**추가사항**   

UBT는 헤더파일의 상태를 두 가지 방식으로 체크한다.   

수정시간(TimeStamp): 헤더 파일의 수정시간을 확인하여 최신화가 됐으면 UHT의 분석 대상이 된다.   
파일내용(Check-Sum): 주석/공백 등의 수정만 있어서 리플렉션에 영향이 없으면 .generated.h 파일을 다시 쓰지 않는다.   

.generated.h 파일이 수정되면 다시 컴파일을 해야해서 굉장히 무거운 작업이다. 따라서 이런 효율적인 프로세스를 가진다.   

하지만 강제로 호출하는 경우도 있는데, .uproject나 .Bulid.cs 파일이 수정되면(프로젝트 설정, 모듈 의존성의 변화) UBT는 리플렉션 정보가 유효한지 다시 한 번 훑는다.   
또한 Intermediate 폴더를 삭제하면 기록이 다 날아가기 때문에 다시 실행한다.   

<br/>

**GameModeBase**

ActorComponent를 만들다 보니 Spawn도 자연스럽게 Actor에 붙이고 있었는데 생각해보니 굳이 Actor를 배치해야하는 비효율적인 행동을 해야했다.   
그래서 찾아봤더니 `GameModeBase`라는걸 이용하면 된다고 한다.   

근데 결국 기본 큐브만 소환가능한 상태라서 Cube 클래스에 ActionComponent를 만들어서 넣어줬다.   

계속 오류나서 빌드가 꼬였나해서 폴더 4개 삭제하고 다시 실행했는데 디버그 하면 VS가 터져버리고 에디터로 가서 실행해도 터져버린다. 하 인생...   
프로젝트 새로 만들어야겠다.   


  </p>
</details>

#### <!-- 26.04.13 -->
<details> 
  <summary>26.04.13</summary>
  <p>

OOP 다시 한 번 정리

OOP에 대해서 설명해 보세요. (중요!)

객체 지향 프로그래밍은 데이터와 그 데이터를 처리하는 함수를 묶어서 하나의 객체로 두고 관리하는 방식입니다.(패러다임)
객체지향 프로그래밍(OPP)의 4대 핵심 요소는 다음과 같습니다.   
캡슐화, 상속, 다형성, 추상화입니다   

캡슐화 (Encapsulation): 데이터와 기능을 하나로 묶고 외부로 부터 보호합니다. 객체가 외부에서 변경되는것을 막기 위함입니다.
상속 (Inheritance): 기존 클래스의 기능을 물려받아 재사용하고 확장하는 것. 계층 구조가 된다. (사람은 동물이다.)
다형성 (Polymorphism): 하나의 인터페이스나 함수가 상황에 따라 다르게 동작하는 것. 오버라이딩과 오버로딩이 있다.    
추상화 (Abstraction): 복잡한 내부 구현은 숨기고, 사용자에게 필요한 최소한의 인터페이스(기능)만 노출하는 것

<br/>

**<대기업 공채>**

8월 펄어비스   
9월 넥슨   
10월 NC   

<br/>

**<TArray 사용>**

GameModeBase에 게임 시작시 다양한 액터를 스폰하려고 하는데 생각없이 변수를 만들다가보니 배열을(TArray)쓰면 되겠다 싶어서 수정했다.   

```cpp
// GameModeBase.h
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Spawn")
TArray<TSubclassOf<class AMyActor>> SpawnActor;

//GameModeBase.cpp
for (auto& MovingActor : SpawnActor) 
{
	if (MovingActor)
	{
		for (int32 i = 0; i < SpawnCount; ++i)
		{
			FVector SpawnLocation = FVector(FMath::RandRange(-500.f, 500.f), FMath::RandRange(-500.f, 500.f), FMath::RandRange(-500.f, 500.f));
			FRotator SpawnRotation = FRotator::ZeroRotator;

			GetWorld()->SpawnActor<AMyActor>(MovingActor, SpawnLocation, SpawnRotation);
		}
	}
}
```

  </p>
</details>

#### <!-- 26.04.14 -->
<details> 
  <summary>26.04.14</summary>
  <p>

**<Static Class 사용>**

객체를 생성하지 않고 정적으로 U클래스 타입(리플렉션 시스템이 관리하는)으로 정보를 준다.

```cpp
DefaultPawnClass = ASpartaCharacter::StaticClass();
```
  </p>
</details>