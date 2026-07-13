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
  <summary><s>26.04.07</s></summary>
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
  <summary><s>26.04.08</s></summary>
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
  <summary><s>26.04.09</s></summary>
  <p>

구조체를 클래스가 상속 받을 수 있나?   
캡슐화 말고 객체지향의 특징은?   
구조체 new 생성가능?   
가비지 컬렉션에 대해서 더 깊이 설명?   
   

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
  <summary><s>26.04.10</s></summary>
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
  <summary><s>26.04.13</s></summary>
  <p>

OOP 다시 한 번 정리

OOP (중요!)

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
  <summary><s>26.04.14</s></summary>
  <p>

**<Static Class 사용>**

객체를 생성하지 않고 정적으로 U클래스 타입(리플렉션 시스템이 관리하는)으로 정보를 준다.

```cpp
DefaultPawnClass = ASpartaCharacter::StaticClass();
```

<br/>

***

<br/>

**<IMC와 IA>**

Input Mapping Context (IMC)   
-> IA들을 총괄해서 관리   

Input Action (IA)   
-> 추상적인 행동   
점프 - IA_Jump - Jump 함수   
마우스 회전 - IA_Look - Look 함수   
이동 - IA_Move - Move 함수   

**<IMC on off 하기>**   
2-2 강의 숙제에 있는 Tab키를 누르면 기존 IMC 작동 안하게, 다시 Tab을 누르면 작동 하게 만드는걸 해봤다.   

`SetupInputComponent`를 override해서 Tab키를 누르면 내가 구현한 로직이 동작하게 만들어줘야했다.   

```cpp
//PlayerController.h
bool bIsInventoryOpen = false;
void ToggleIMC();
virtual void SetupInputComponent() override;

//PlayerController.cpp
#include "EnhancedInputComponent.h"

void ASpartaPlayerController::SetupInputComponent()
{
	Super:: SetupInputComponent();

	if (UEnhancedInputComponent* EnhancedInputComponent = Cast<UEnhancedInputComponent>(InputComponent))
	{
		EnhancedInputComponent->BindAction(TabAction, ETriggerEvent::Started, this, &ASpartaPlayerController::ToggleIMC);
	}
}
```

ToggleIMC 함수에 MappingContext를 바꾸는 로직을 구현했는데 그 함수를 바인딩 시켜줬다. 메서드들이 엄청 낯설다.   

<br/>

***

<br/>

**<GameMode 구조 정리>**   

GameMode - Character(Default Pawn Class), Player Controller   
Character를 만들고 GameMode에 연결해서 월드에 스폰   
PlayerController(캐릭터의 빙의)   
IMC, IA 입력 매핑   
Local Player와 Local Player Subsystem을 가져와서 IMC를 활성화   
Local Player는 사용자를 말한다.   
Local Player Subsystem은 입력 매핑을 가지고 있는 클래스   

<br/>

***

<br/>

알고리즘 기초 정리   

**<시간복잡도와 알고리즘>**   
시간복잡도 : 입력크기(n)가 커질 때, 연산 횟수가 얼마나 증가하는지를 나타낸다.    
알고리즘 : 문제를 해결하기 위한 절차나 규칙의 집합    
-> 입력/출력/명확성/유한성/효율성을 가지고 있어야 알고리즘 취급    

<br/>

***

<br/>

**<벡터와 배열>**   
vector는 연속된 동적 배열이다.   
vector는 size와 capacity가 있다.    
공간이 꽉 차면 기존의 2배 크기의 capacity를 가진 새 메모리를 재할당한다.   
재할당은 O(n)의 시간복잡도   
미리 크기를 알면 reserve(n)으로 재할당 방지를 한다.   
v.reserve(100); 이런식으로 미리 공간 확보   

insert()와 erase()는 O(n)의 시간복잡도고 나머지는 O(1)   
v.insert(v.begin() + 2);    
v.erase(v.begin() + 2);   
실제 인덱스 위치(2)에 삽입/삭제   

<br/>

***

<br/>

**<stack과 queue 그리고 deque>**   
queue는 front()와 back()으로 양 쪽 다 접근 가능   
stack과 queue는 컨테이너 어댑터라고 부른다.   
둘 다 deque라는 기본 컨테이너를 감싸서 접근 방식을 제한 한 것이다.   

stack은 deque의 back만 사용, queue는 deque의 양쪽 끝 사용   

deque는 **여러 개의 고정 크기 메모리 블록(Chunk)**을 할당하고 이를 관리하는 맵(Map) 형태의 인덱스 체계를 가진다.   

메모리 불연속성: 데이터가 여러 블록에 나뉘어 저장되지만, 사용자 입장에서는 마치 하나의 연속된 배열처럼 인덱스 접근([])이 가능하다. (대신 임의 접근은 블록 계산을 해야해서 조금 느림)   
양방향 확장: 앞(Front)과 뒤(Back) 양쪽 모두에서 원소를 추가/제정하는 것이 $O(1)$ 성능으로 매우 빠르다.   

stack과 queue가 deque를 기본 컨테이너로 쓰는 이유   
메모리 재할당 효율성: vector는 용량이 꽉 차면 전체 데이터를 새로운 메모리 공간으로 복사해야 하지만, deque는 새로운 메모리 블록을 하나 더 할당하기만 하면 됩니다. 대량의 데이터를 다룰 때 훨씬 안정적이다.   
앞부분 삽입/삭제 성능: queue는 앞에서 데이터를 빼는 작업이 빈번합니다. vector는 앞에서 빼면 뒤의 모든 데이터를 당겨야($O(N)$) 하지만, deque는 앞쪽 블록만 건드리면 되므로 $O(1)$이다.   
메모리 해제: vector는 clear()를 해도 할당된 메모리(capacity)를 들고 있는 경우가 많지만, deque는 블록 단위로 메모리를 관리하므로 상대적으로 메모리 관리가 유연하다.   

<br/>

***

<br/>

**<string과 여러 함수들>**   

s.find("hello");   
hello를 찾아서 첫 인덱스를 리턴   
s.find("hello", 7);   
인덱스 7부터 검색    
없으면 string::npos를 리턴한다.   

s.substr(0, 5);
0부터 총 5개 즉 인덱스 0, 1, 2, 3, 4 이렇게 잘라서 리턴함   
s.substr(10);   
인덱스 10부터 끝까지   

replace는 원본이 바뀐다.   
s.replace(시작위치, 길이, "바꿀 문자열");   

**<stringstream은 따로 자세히 정리돼있음>**   

<br/>

***

<br/>

**<Map과 함수들>**    

m.count(key값); 으로 확인하고 접근   

insert 대신 emplace 추천   

  </p>
</details>

#### <!-- 26.04.15 -->
<details> 
  <summary>26.04.15</summary>
  <p>

기술 면접 정리   


  </p>
</details>

#### <!-- 26.04.16 -->
<details> 
  <summary><s>26.04.16</s></summary>
  <p>

**<FVector 방향 설정>**

X : 정면   
Y : 오른쪽   
Z : 위쪽   

키보드, 마우스 입력은 X부터 차례대로 들어온다.   
WASD를 구분하는게 아니라 첫 입력을 무조건 X로 지정한다.   
따라서 좌우로 움직이려면 X를 Y로 바꿔야하는데 그게 에디터의 swizzle 옵션이다. YXZ로 해주면 됨.   

**<카메라 설정 변경>**   
액터 자체를 움직이다보니 카메라 설정이 어색함.   
`AddActorLocalRotation`자체가 액터를 움직이게 하기 때문에 설정을 바꿔야한다.   

```cpp
// 컨트롤러 회전 대신 폰의 회전을 그대로 따르도록 설정
SpringArmComp->bUsePawnControlRotation = false; 
SpringArmComp->bInheritPitch = true;
SpringArmComp->bInheritYaw = true;
SpringArmComp->bInheritRoll = true;

// 카메라가 너무 흔들리는 게 싫다면 '지연(Lag)' 기능을 켠다.
SpringArmComp->bEnableCameraLag = true;
SpringArmComp->CameraLagSpeed = 3.0f; // 숫자가 낮을수록 부드럽게 따라옴
```


  </p>
</details>

#### <!-- 26.04.17 -->
<details> 
  <summary><s>26.04.17</s></summary>
  <p>

**<언리얼 심화반 정리>**   

```cpp
	// TObjectPtr 사용할때 참조 사용을 권장
	for (TObjectPtr<USceneComponent>& Component : Components)
	{

	}

	for (USceneComponent* Component : Components)
	{

	}

	// TSubclassOf는 어떤 클래스 타입을 등록할건지 설정해줄 수 있다. UClass는 불가능(모든 클래스 다보여줘서 디자이너가 실수 할 가능성이 높음)
	UPROPERTY(EditAnywhere, Category = "Class")
	UClass* MyClass;
	UPROPERTY(EditAnywhere, Category = "Class")
	TSubclassOf<UClass> MyClass2;

	TArray<int32> IntArray;

	// 공간을 하나 만들어서 거기 두고 넣기. 명시적이라서 오류의 가능성이 없음.
	IntArray.Add(5);
	// 복사 없이 바로 넣음(성능이 조금 더 좋음) 눈에 보이지 않는 변환이 있을 수 있어서 아주 조금 불안정함
	IntArray.Emplace(6);
	// UE5는 성능 쥐어짜는 경우 제외하면 Add를 권장

	// 성능 안좋아서 무조건 TSet을 쓰면 된다.
	IntArray.AddUnique(6);

	IntArray.Insert(600, 2);

	//IntArray.Num(); 그냥 이렇게 쓰면 오류남. for문 if문 사용해야함
	for (int32 i = 0; i < IntArray.Num(); ++i)
	{

	}

	if (IntArray.Num())
	{

	}

	// 함수객체
	IntArray.Sort([](int32 A, int32 B) { return A > B; });

	TArray<int32> ReturnIntArray = IntArray.FilterByPredicate([](const int32 FindValue) { return FindValue < 9; });

	int32 index = IntArray.Find(5);
	bool b = IntArray.Contains(5);

	IntArray.Remove(10); // 모든 10값을 삭제
	IntArray.RemoveSingle(10);  // 10값 중 가장 첫 번째꺼

	if (IntArray.IsValidIndex(2)) // 먼저 2번째 인덱스에 값이 있는지 확인
	{
		IntArray.RemoveAt(2);  // 2번째 인덱스 값 삭제
		IntArray.RemoveAt(2, EAllowShrinking::No);  
		// 두번째 인자는 인덱스값 삭제 했을 때 제일 뒤에 빈 공간을 없앨것이냐 그대로 둘 것이냐를 정함. 기븐온 Yes고 삭제를 함
	}
	
	// []안에 지역변수 (=, &) 클래스 내부 멤버 변수 (this)
	IntArray.RemoveAll([](int32 Value) { return Value % 3 == 0; });

	IntArray.Empty(); // 다 지우기


// 수업때 코드 짠건데 Arr.Num()을 사용안했다.
// 그리고 변수 이름도 RandonValue 이런식으로 하는게 좋다.
	TArray<int32> Arr;
	int32 count = 0;
	while (count < 30)
	{
		int32 Num = FMath::RandRange(0, 1000);
		if (Num <= 100)
		{
			Arr.Add(Num);
			++count;
		}
	}
	Arr.RemoveAll([](int32 Value) { return Value < 50; });
	Arr.Sort([](int32 A, int32 B) { return A < B; });

  // Set
  TSet<int32> IntArraySet;

IntArraySet.Add(100);

if (IntArraySet.Contains(100))
{

}

// TSet의 Find는 포인터를 반환한다.
int32* FoundPtr = IntArraySet.Find(20);

// TSet 순회하는 방법
for (TSet<int32>::TIterator It = IntArraySet.CreateIterator(); It; ++It)
{
	if (*It < 60)
	{
		It.RemoveCurrent();
	}
}

// Const로 받고 싶을때
for (TSet<int32>::TConstIterator It = IntArraySet.CreateConstIterator(); It; ++It)
{

}
// 제일 편한건 auto로 받는거지만 확실한거 아니면 안쓰는게 좋긴하다.(권장하지 않음)


TSet<int32> SetA = { 1, 2, 3 };
TSet<int32> SetB = { 3, 4, 5 };

TSet<int32> SetC = SetA.Union(SetB); // 합집합
TSet<int32> SetC = SetA.Intersect(SetB); // 교집합

SetC.Compact(); // 삭제해서 비어버린 부분을 다 뒤로 옮김
SetC.Shrink();  // 비어버린 부분 싹 다 정리

TArray<int32> MyArray = SetC.Array(); // 배열로 자동으로 넘어간다.

// Set 사용하는 곳 : 무기를 휘두룰때 그 범위에 같은 몬스터가 여러번 들어오면 Set을 이용해서 중복된 값을 없애면 몬스터에게 딱 한번만 데미지가 들어가게 된다.

// TMap

TMap<int32, FString> ItemMap;

ItemMap.Add(101, TEXT("Sword"));
ItemMap.Add(102, TEXT("Shield"));

ItemMap.Emplace(103, TEXT("Potion"));

ItemMap.Add(101, TEXT("Hello")); // 덮어씌워짐

if (ItemMap.Contains(101))
{
	FString* FoundItem = ItemMap.Find(101);
}

FString& ItemRef = ItemMap.FindOrAdd(104); // 찾지 못하면 만들어라
ItemRef = TEXT("Bow");

// 위험한 코드(바로 접근)
FString Name = ItemMap[105];
// 이렇게 해줘야함 - 기존 C++과 달리 없으면 만들지 않고 Crash 나기 때문
if (ItemMap.Contains(105))
{
	FString Name = ItemMap[105];
}

for (const TPair<int32, FString>& i : ItemMap)
{

}

// 지우면서 갈 땐 무조건 Iterator를 사용하자(정말 혹시 모를 오류 하나라도 제거) 그냥 순회하면 위험할 수도 있다.
for (TMap<int32, FString>::TIterator It = ItemMap.CreateIterator(); It; ++It)
{
	if (It.Key() == 103)
	{
		It.RemoveCurrent();
	}
}

// 삭제
ItemMap.Remove(102);
// 빈공간 뒤로 몰고 삭제하기!
ItemMap.Compact();
ItemMap.Shrink();
```

<br/>

**<심화반 1주차 수업 정리>**   
심화반 수업 카카시   

2d 좌표
수학은 우리가 알고있는 기본 x, y
코딩에서 기본 2d 좌표는 y가 반전이다.(아래로 갈수록 y값이 커짐)

점은 원점을 기준으로
벡터는 (0, 0) ~ (2, 2)나 (-2, -2) ~ (0, 0)이나 똑같은 벡터이다. 기준이 없어서 그렇다. 크기랑 방향만 가지고 있음.

점과 벡터 모두 (x, y)로 표현하는데 의미가 다르다.

B - A = v(벡터)
점 A = (2, 4), 점 B = (5, 1)
벡터 v = B - A = (5 - 2, 1 - 4) = (3, -3)

<br/>

**<벡터의 덧셈>**   
두 벡터를 더하면 두 이동을 연달아 하는 것

벡터a + 벡터b = (ax + bx, ay + by)

<br/>

**<벡터의 뺄셈과 스칼라곱>**   
뺄셈
두 점의 차이로 방향 벡터를 구할 때 사용
벡터a - 벡터b = (ax - bx, ay - by)

스칼라곱
방향은 유지, 크기만 변경
음수 곱하면 방향 반대

<br/>

**<벡터의 크기>**   
벡터의 크기 = 화살표의 길이 = "얼마나 멀리?"

피타고라스 정리와 같다.
x방향, y방향으로 직각삼각형을 만들고 빗변의 길이를 구하는것.
벡터v = (3, 4)  -> (3제곱 + 4제곱)에 루트 = 5

<br/>

**<벡터의 정규화(Normalize)>**   
방향은 유지하고 크기는 1로
벡터 (3, 4) -(정규화)-> (0.6, 0.8) 크기 1로 만듦

왜 정규화가 필요한가?
적이 3칸 떨어져 있든 100칸 떨어져 있든 캐릭터 이동속도는 같아야한다.
방향 벡터를 정규화하면 거리에 상관없이 순수한 방향 정보만 얻을 수 있고 여기에 속도를 곱하면 일정한 속도로 이동.

position += direction.normalized() x speed x dt

위의 식 해석
거리 = 속력 x 시간
여기에 방향을 주는것.

UE5에서 사용법
```cpp
FVector MyLoc = GetActorLocation();
FVector TargetLoc = Target->GetActorLocation();

FVector Dir = (TargetLoc - MyLoc).GetSafeNormal(); // 정규화로 방향 정보만 빼오기

FVector NewLoc = MyLoc + Dir * Speed * DeltaTime;
SetActorLocation(NewLoc);
```

<br/>

**<pawn이 계속 떨어지는 현상>**

Capsule Component에서 collision preset을 건드려주면 해결된다.   

<br/>

**<Line Trace 사용해보기>**   

바닥 충돌은 sweep으로 캡슐 범위로 하려고 Line Trace는 사용법만 익혀봤음   
```cpp
	// LineTrace 사용해보기
	FHitResult GroundHit;
	FVector Start = GetActorLocation();
	FVector End = Start + FVector(0, 0, -100.f);  // 밑으로 1m 레이저 발사

	// 디버깅용 눈으로 레이저 확인
	DrawDebugLine(GetWorld(), Start, End, FColor::Red, false, -1, 0, 1.f);

	if (GetWorld()->LineTraceSingleByChannel(GroundHit, Start, End, ECC_Visibility))
	{
		if (GroundHit.Distance < 50.f && VerticalVelocity < 0)
		{
			VerticalVelocity = 0.f;
		}
	}
```

<br/>

**<바닥 유무 확인(Sweep 활용)>**   
선 하나로 바닥을 확인하는건 효율이 좋지 않아서 Capsule 자체로 확인하는 방법을 찾아봤다.   

```cpp
bool AMyPawn::IsOnGround()
{
	FHitResult HitResult;

	// 시작~ 끝점 설정 (현재 위치에서 아주 살짝 아래까지)
	FVector Start = GetActorLocation();
	FVector End = Start + FVector(0.f, 0.f, -2.f);

	// 에디터의 캡슐 정보 가져오기
	FCollisionShape CapsuleShape = FCollisionShape::MakeCapsule(
		CapsuleComp->GetScaledCapsuleRadius(),
		CapsuleComp->GetScaledCapsuleHalfHeight()
	);

	FCollisionQueryParams Params;
	Params.AddIgnoredActor(this); // 나 자신은 제외

	bool bHit = GetWorld()->SweepSingleByChannel(
		HitResult,
		Start,
		End,
		FQuat::Identity,   // 회전 기본값
		ECC_Visibility,    // Visibility 채널 사용 (바닥이 막는)
		CapsuleShape,
		Params
	);

	return bHit;
}
```
<br/>

**<바닥일때와 공중일때 카메라 전환>**   

바닥일땐 PlayerController에게 카메라를 맡기고 공중일땐 pawn의 회전과 함께 움직이는 방법을 찾아서 적용해줬다.      

```cpp
// 회전을 담당하는 Look 함수를 수정해줬다.
void AMyPawn::Look(const FInputActionValue& Value)
{
	FVector LookValue = Value.Get<FVector>();

	// 바닥에 있을 땐 카메라만 회전, 공중에 뜨면 폰이 회전(공중에서 카메라는 폰 회전에 맞게 움직임)
	if (IsOnGround())
	{
		AddControllerYawInput(LookValue.X * RotationSpeed * GetWorld()->GetDeltaSeconds());
		AddControllerPitchInput(LookValue.Y * RotationSpeed * GetWorld()->GetDeltaSeconds());
	}
	else
	{
		LookInput = LookValue;
	}
}
```
<br/>

bool 변수 2개를 이용해서 상태 변환을 체크하는 로직을 적용해봤다.   
물론 아직 문제점이 많다...   
카메라가 끊기는 것과 바닥에서 폰이 중심을 못 잡고 통통 튀는 현상도 있다.   

```cpp
// 바닥 -> 공중 or 공중 -> 바닥 즉, 상태가 변했을 때만 실행
if (bGrounded != bWasOnGround)
{
	if (bGrounded)
	{
		// 카메라를 컨트롤러가 제어
		SpringArmComp->bUsePawnControlRotation = true;
		// 착륙 시 폰의 회전값(공중에선 폰에 회전과 함께 카메라가 움직임)을 카메라 컨트롤러와 일치시킴
		if (APlayerController* PC = Cast<APlayerController>(GetController()))
		{
			PC->SetControlRotation(GetActorRotation());
		}
	}
	else
	{
		
		// 공중에선 다시 카메라를 pawn에 고정
		SpringArmComp->bUsePawnControlRotation = false;
	}
	bWasOnGround = bGrounded;
}
```

<br/>

**<GetControlRotation()을 굳이 캐스팅 이후 불러오는 이유?>**   

공부하다 보니 굳이 
```cpp
APlayerController* PC = Cast<APlayerController>(GetController());
```
이렇게 캐스팅하고 `PC->GetControlRotation();`를 쓰길래 의문점이 생겨서 찾아봄     

두 방식은 약간의 차이가 있는데 캐스팅하면 무조건 명시적으로 컨트롤러의 로테이션을 가져온다고 보여주기도 하고 실제로도 그렇게 가져옴.   
캐스팅 안하고 그냥 가져오면 pawn의 빙의 유무에 따라 다른데 빙의하고 있으면 컨트롤러가 있기 때문에 캐스팅 하는 방식과 똑같지만 빙의하지 않으면 pawn 자체의 회전값을 가져옴.   

간단히 말하면 pawn을 possese하고 있으면 둘 다 결과값은 같긴함.   

**정리**   
명확한 의도를 표현하기 위함   
PlayerController의 추가적인 기능을 사용할 수도 있어서 확장성이 좋음   
캐스팅 안하고 그냥 쓰면 유효성 검사에서 플레이어 컨트롤러인지 AI 컨트롤러인지 확인이 불가능함   

  </p>
</details>

#### <!-- 26.04.18 -->
<details> 
  <summary><s>26.04.18</s></summary>
  <p>

**<카메라 시점 전환 문제1>**  

바닥에 있을땐 컨트롤러가 카메라를 제어   
공중에 떠있으면 폰의 회전과 같이 카메라가 돌아감   

문제는 공중에 뜨는 순간 컨트롤러 회전값과 폰의 회전값이 동일하지 않을 확률이 99.9999%이기 때문에 화면이 갑자기 폰 기준으로 확 바뀐다.   

그래서 공중에 뜨는 순간 일정 시간동안 마우스 제어를 못하게 막고 시점이 부드럽게 전환되게 구현하려고 찾아봤음   

일단 화면을 부드럽게 전환하려면 RInterpTo()를 사용하면 된다고 함   

```cpp
// 1차적으로 이렇게 구현
FRotator CurrentRotation = PC->GetControlRotation();
FRotator TargetRotation = GetActorRotation();

FRotator DelayRotation = FMath::RInterpTo(
	CurrentRotation,
	TargetRotation,
	DeltaTime,
	CameraRotationInterpSpeed
);

PC->SetControlRotation(DelayRotation);
```

**<카메라 시점 전환 문제2>**  

화면전환 로직을 컨트롤러 회전값 -> 폰의 회전값으로 서서히 다가가게 하였는데 문제는 그 사이에 마우스를 움직이면 두 값이 같아지지 않았다.   
그래서 잠깐 마우스 회전을 못하게 막고 전환이 완료되면 움직일 수 있게 하였다.   

완성된 코드

```cpp
	if (bGrounded != bWasOnGround)
	{
		if (bGrounded)
		{
			// 카메라를 컨트롤러가 제어
			SpringArmComp->bUsePawnControlRotation = true;
			// 착륙 시 폰의 회전값(공중에선 폰에 회전과 함께 카메라가 움직임)을 카메라 컨트롤러와 일치시킴
			if (PC)
			{
				PC->SetControlRotation(GetActorRotation());
			}				
			// 플레이어가 카메라 제어
			bIsNotRotate = false;
		}
		else
		{
			// 플레이어가 제어하지 못함
			bIsNotRotate = true;
		}
		bWasOnGround = bGrounded;
	}

	if (bIsNotRotate && PC)
	{

		FRotator CurrentRotation = PC->GetControlRotation();
		FRotator TargetRotation = GetActorRotation();

		FRotator DelayRotation = FMath::RInterpTo(
			CurrentRotation,
			TargetRotation,
			DeltaTime,
			CameraRotationInterpSpeed
		);

		PC->SetControlRotation(DelayRotation);

		if (CurrentRotation.Equals(TargetRotation, 0.1f))
		{
			bIsNotRotate = false;
			SpringArmComp->bUsePawnControlRotation = false;
		}
	}
```

이제 이륙할때 화면이 부드럽게 넘어간다!   

<br/>

**<폰이 바닥에 지멋대로 있음>**

폰이 착륙할 때 공중에 있던 회전값 그대로 떨어지는데 지 멋대로 넘어져있다.   
이 문제를 고치기 위해 바닥에 닿았을 때 회전값을 조정하여 균형을 잡아주기로 했다.   

```cpp
// 바닥에서 폰이 오뚜기처럼 서있게
if (bGrounded && VerticalVelocity == 0.f)
{
	FRotator CurrentRotation = GetActorRotation();
	FRotator DesiredRotation = FRotator(0.f, CurrentRotation.Yaw, 0.f);

	FRotator DelayRotation = FMath::RInterpTo(
		CurrentRotation,
		DesiredRotation,
		DeltaTime,
		5.f
	);

	SetActorRotation(DelayRotation);
}
```
직접 구현을 해봤는데 일단 오뚜기처럼 돌아가긴한다.   
하지만 또 문제가 발생했다.   

<br/>

**<바닥에서 폰이 오뚜기처럼 되돌아갈때 카메라는 안돌아가는 현상>**   

폰은 되돌아가지만 카메라는 그대로 누워있다.   
이건 금방 고칠 수 있을 것 같다.  

```cpp
// 바닥에서 폰이 오뚜기처럼 서있게 + 카메라도 같이 수정
if (bGrounded && VerticalVelocity == 0.f)
{
	FRotator CurrentRotation = GetActorRotation();
	FRotator DesiredRotation = FRotator(0.f, CurrentRotation.Yaw, 0.f);

	FRotator DelayRotation = FMath::RInterpTo(
		CurrentRotation,
		DesiredRotation,
		DeltaTime,
		5.f
	);

	SetActorRotation(DelayRotation);

	if (PC)
	{
		FRotator CurrentCameraRotation = PC->GetControlRotation();
		FRotator DesiredCameraRotation = FRotator(CurrentCameraRotation.Pitch, CurrentCameraRotation.Yaw, 0.f);

		FRotator DelayCameraRotation = FMath::RInterpTo(
			CurrentCameraRotation,
			DesiredCameraRotation,
			DeltaTime,
			5.f
		);
		PC->SetControlRotation(DelayCameraRotation);
	}
}
```
간단하게 카메라도 회전값을 바꿔줬더니 바로 해결!   

**<폰이 일어선 후 특정 방향으로 가다가 바닥에 걸리는 현상>**   

이건 아마 폰이 아주 미세하게 수평이 아니라서 나타나는 현상같다.   

알아보니 범인은 바로 `RInterpTo()`였다.   
얘는 설정한 값으로 정확히 변환되는게 아니라 아주아주 근사치까지 간다고 한다.   
그래서 아주아주 근사치까지 갔을 때 값을 고정해주면 해결된다.   

```cpp
// 오류를 수정한 최종 코드

	// 바닥에서 폰이 오뚜기처럼 서있게 + 카메라도 같이 수정
	if (bGrounded && VerticalVelocity == 0.f)
	{
		
		FRotator CurrentRotation = GetActorRotation();
		FRotator DesiredRotation = FRotator(0.f, CurrentRotation.Yaw, 0.f);

		if (FMath::IsNearlyEqual(CurrentRotation.Pitch, 0.f, 0.01f) && FMath::IsNearlyEqual(CurrentRotation.Roll, 0.f, 0.01f))
		{
			SetActorRotation(DesiredRotation);
		}
		else
		{
			FRotator DelayRotation = FMath::RInterpTo(
				CurrentRotation,
				DesiredRotation,
				DeltaTime,
				5.f
			);

			SetActorRotation(DelayRotation);
		}
		
		if (PC)
		{
			FRotator CurrentCameraRotation = PC->GetControlRotation();
			FRotator DesiredCameraRotation = FRotator(CurrentCameraRotation.Pitch, CurrentCameraRotation.Yaw, 0.f);

			if (FMath::IsNearlyEqual(CurrentCameraRotation.Roll, 0.f, 0.01f))
			{
				PC->SetControlRotation(DesiredCameraRotation);
			}
			else
			{
				FRotator DelayCameraRotation = FMath::RInterpTo(
					CurrentCameraRotation,
					DesiredCameraRotation,
					DeltaTime,
					5.f
				);
				PC->SetControlRotation(DelayCameraRotation);
			}
		}
	}
```

**<인터페이스 클래스>**

```cpp
// 인터페이스 헤더파일
#pragma once

#include "CoreMinimal.h"
#include "UObject/Interface.h"
#include "ItemInterface.generated.h"

// 인터페이스를 리플렉션 시스템에 등록하기 위한 코드다. 수정할필요 없음.
UINTERFACE(MinimalAPI)
class UItemInterface : public UInterface
{
	GENERATED_BODY()
};

// 순수 가상함수 구현은 여기에 하면 된다.
class SPARTAPROJECT_API IItemInterface
{
	GENERATED_BODY()

public:
};
인터페이스 클래스는 cpp는 필요가 없는데 삭제하지말고 놔둬야 한다.   
언리얼 엔진 코드 컨벤션에 그냥 헤더와 cpp 파일은 쌍으로 있어야 한다고 하기 때문에 건드리지 말것.   

```

  </p>
</details>

#### <!-- 26.04.19 -->
<details> 
  <summary><s>26.04.19</s></summary>
  <p>

**<콜리젼 프리셋 종류>**   

`NoCollision`: 충돌 끄기(하늘 등 상호작용 안할것들)   
`BlockAll`: 모두 막음(보통 벽, 바닥 등)   
`OverlapAll`: 모두 감지함(센서, 트리거 등)   
`BlockAllDynamic`: 움직이는 객체만 막음(플레이어랑 상호작용 하는 문 등)   
`OverlapAllDynamic`: 움직이는 객체만 감지(센서, 트리거 등)   
`Pawn`: Pawn타입 대상으로 충돌 감지 

<br/>

**<콜리전 커스텀 세팅>**   

`Collision Enabled(Query and Physics)`: 충돌, 물리적 반응 모두 활성화   
`Query Only`: 충돌(Overlap과 Hit)만 감지   
`Physics Only`: 물리적 반응만 감지   

<br/>

**<스크린에 출력>**   

```cpp
GEngine->AddOnScreenDebugMessage(
	-1,   // -1 해두면 계속 갱신해서 출력해줌
	2.f,  // 출력 유지 시간
	FColor::Green, // 글자색
	FString::Printf(TEXT("Player Gained %d points"), PointValue)); // 내용
```

<br/>

**<스폰 범위 설정하기>**

간단하게 Actor 블루프린트 하나 만들어서  CollisonComponent를 추가하고 스폰 범위만큼 스케일을 조정해주면 된다.(스폰 볼륨이라고 함)      
이렇게 하면 간단하기도 하고 플레이어의 위치를 체크하기 쉬워서 좋다.(콜리전 컴포넌트 자체가 가볍기도 함)   

<br/>

**<데이터 테이블>**   

보통 기획자들이 많이 사용하는데 엑셀이나 JSON 파일로 데이터를 모아서 엔진에 임포트한 후 이 데이터들을 쉽게 사용함   
그 데이터들을 다룰 구조체를 구현해줘야함   

None으로 class하나 만들어주고 구조체를 구현해준다. (cpp파일은 안쓰니 #include 부분을 제외하고 다 지우기)   
```cpp
// 데이터 테이블을 위한 구조체 구현 예시
#pragma once

#include "CoreMinimal.h"
#include "ItemSpawnRow.generated.h"

USTRUCT(BlueprintType)
struct FItemSpawnRow : public FTableRowBase
{
	GENERATED_BODY()

public:
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	FName ItemName;
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	TSubclassOf<AActor> ItemClass;
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	float SpawnChance;

};

```

<br/>

**<TSubclassOf에 대해서>**   

포인터라기 보다 클래스를 참조하기 위한 템플릿 데이터 구조   

`TSubclassOf`: 하드 레퍼런스   
클래스가 항상 메모리에 로드 된 상태에서 바로 접근   
`TSoftClassPtr`: 소프트 레퍼런스   
클래스의 경로만 유지하고 필요한 상황에 메모리에 로드   

**<누적값으로 랜덤 뽑기>**  

6번 과제할때 써봤던건데 다시 복습   

```cpp
// A, B, C가 있고 각 0.5 0.3 0.2 확률이면
// 0~ 1사이 랜덤값을 뽑고
// 랜덤값이 0.5보다 작으면 A
// 아니면 0.3을 더해주고 다시 비교
// 랜덤값이 0.8보다 작으면 B
// 아니면 0.2를 더해주고 다시 비교
// 마지막이니 무조건 C
	const float RandValue = FMath::FRandRange(0.f, TotalChance);

	float AccumulateChance = 0.f;

	for (FItemSpawnRow* Row : AllRows)
	{
		AccumulateChance += Row->SpawnChance;
		if (RandValue <= AccumulateChance)
		{
			return Row;
		}
	}
```

**<데미지 입히고 받기>**   

데미지 관련해서 이미 구현되어있는 기능을 사용하면 된다.(TakeDamage, ApplyDamage)   

**데미지 받기**   
```cpp
// 헤더파일에 메서드를 override 해줌
virtual float TakeDamage(
	float DamageAmount,						 // 데미지를 얼마나 입었나.
	struct FDamageEvent const& DamageEvent,  // 데미지 유형(이벤트) 특정 스킬이라던지 뭐 그런 정보
	AController* EventInstigator,			 // 데미지를 발생시킨 주체 (ex. 파이어볼을 쏜 놈)
	AActor* DamageCauser) override;			 // 데미지를 일으킨 오브젝트 (ex. 파이어볼) 

// cpp 파일에 구현
float ASpartaCharacter::TakeDamage(float DamageAmount, FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser)
{
	// ActualDamage는 데미지 계산(방어력, 관통 등등)이 끝나고 실제로 들어온 데미지
	float AcutalDamage = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	Health = FMath::Clamp(Health - DamageAmount, 0.0f, MaxHealth);
	UE_LOG(LogTemp, Warning, TEXT("Health decreased to: %f"), Health);

	if (Health <= 0.f)
	{
		OnDeath();
	}

	return AcutalDamage;
}
```

<br/>

**데미지 입히기**

```cpp
// cpp파일에서 간단하게 구현가능
#include "Kismet/GameplayStatics.h"

UGameplayStatics::ApplyDamage(
	Actor,                     // 데미지 받는 액터
	ExplosionDamage,           // 데미지 값
	nullptr,				   // 데미지 유발자
	this,					   // 데미지를 입힌 오브젝트
	UDamageType::StaticClass() // 데미지 타입
);
```
**<게임 흐름 구현>**

GameState   
게임의 전역 상태를 담는 클래스   
싱글플레이라 여기서 구현하는게 좋음   

GameMode   
보통 서버전용 로직, 규칙을 담음   
멀티게임은 여기서   

**<IsA() 사용법>**   

IsA()는 하위 클래스까지 다 확인해준다.   
```cpp
// CoinItem을 상속받은 Big, SmallCoinItem 둘 다 확인
SpawnedActor && SpawnedActor->IsA(ACoinItem::StaticClass())
```

  </p>
</details>

#### <!-- 26.04.20 -->
<details> 
  <summary><s>26.04.20</s></summary>
  <p>

**<C++의 4대 캐스팅 방법>**   

**static_cast**   
가장 많이 사용하고 컴파일 타임에 결정된다.   
기본적인 데이터 타입 변환에 많이 사용된다.   
부모, 자식 클래스간의 변환도 되는데 안전성 검사는 없다.   
*void를 구체적인 타입으로 변환
런타임 오버헤드가 없지만, 안전성은 100% 보장하지 않는다.   
```cpp
float FloatValue = 3.14f;
// 실수에서 정수로 변환 (데이터 손실을 인지하고 있음을 명시)
int IntValue = static_cast<int>(FloatValue);

// 상속 관계에서의 업캐스팅 (자식 -> 부모)
// MyPawn은 APawn의 자식이므로 항상 안전함
APawn* BasePawn = static_cast<APawn*>(MyPawnInstance);
```

<br/>

**dynamic_cast**    
런타임에 상속관계에 있는 클래스간의 안전한 변환을 보장한다.   
주로 부모 클래스 포인터를 자식 클래스 타입으로 변환(다운캐스팅)할때 사용한다.   
RTTI(Runtime Type Information)을 사용하여 변환 가능 여부를 확인한다.   
변환이 불가능할 경우 포인터는 nullptr를 반환하고 참조형은 예외를 발생시킨다.   
반드시 하나 이상의 가상함수가 포함된 다형성 클래스여야 사용 가능하다.   
```cpp
// 가상 함수가 하나라도 있는 클래스여야 함
class Animal { virtual void Speak() {} };
class Dog : public Animal { void Speak() override { /* 멍멍 */ } };

Animal* MyAnimal = new Dog();

// MyAnimal이 실제 Dog인지 확인하며 캐스팅
Dog* MyDog = dynamic_cast<Dog*>(MyAnimal);

if (MyDog) {
    // 변환 성공 시에만 안전하게 접근
}
```

<br/>

**const_cast**   
객체의 const나 volatile 속성을 제거하거나 추가할 때 사용한다.   
주로 상수 포인터나 참조자를 비상수 포인터/참조자로 잠시 바꿔야 하는 경우에 사용한다.   
원래 const로 선언된 상수의 값을 이 연산자로 강제 변경하는 것은 정의되지 않은 동작(Undefined Behavior)을 유발할 수 있어서 주의해야한다.   

```cpp
void ModifyValue(const int* ReadOnlyValue) {
    // ReadOnlyValue의 const를 강제로 제거
    int* WritableValue = const_cast<int*>(ReadOnlyValue);
    *WritableValue = 100;
}
```

<br/>

**reinterpret_cast**      
서로 전혀 관계없는 타입 간의 비트 단위 재해석을 수행하는 강력하고 위험한 캐스팅이다.   
포인터를 정수형으로 변환하거나 반대의 상황에 사용   
서로 연관없는 클래스 포인터 간의 변환 
컴파일러는 어떠한 논리적 검사도 하지 않는다.   
하드웨어 제어나 특정 네트워크 프로토콜 처리 등 특수한 상황에서만 사용한다.  
```cpp
int Value = 65;
// 정수 65를 메모리 주소 0x41(65의 16진수)로 간주하고 포인터로 변환
int* Address = reinterpret_cast<int*>(Value);

// 특정 객체를 바이트 단위(char*)로 쪼개서 전송하거나 읽을 때
MyStruct Data;
char* RawData = reinterpret_cast<char*>(&Data);
```

<br/>

UE5에서는 dynamic_cast 대신 Cast를 사용한다. 언리얼 환경에 맞게 더 좋은 성능을 보여주기 때문이다.   
RTTI대신 리플렉션 시스템이 기반 시스템이다.
그리고 UObject를 상속받은 클래스에서 사용 가능하다.

**<언리얼엔진의 HUD>**   

Canvas 기반 HUD(예전방식)   
UMG(Unreal Motion Graphics)   
-> 요즘 씀 (Widget Blueprint 사용)   
프로젝트이름.Build.cs 파일에 들어가서 UMG 등록을 해줘야 한다.(C# 코드)   
```c#
PublicDependencyModuleNames.AddRange(new string[] { 
	"Core", 
	"CoreUObject", 
	"Engine", 
	"InputCore", 
	"EnhancedInput",
	"UMG" // 여기 이부분 추가
  });
```

**<버튼 2개 구현하기>**   
4-2 강의 숙제에 있어서 구현해봤다.   
`SetVisibility`에 계속 빨간줄이 그어져서 문제를 찾아봤는데 그냥 빌드도 되고 에디터에서 정상적으로 실행이 된다.   

```cpp
// 헤더파일에 #include "Components/Button.h"

// Widget의 버튼을 찾아서 각각 캐스팅해준다.
UButton* StartButton = Cast<UButton>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("StartButton")));
UButton* RestartButton = Cast<UButton>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("RestartButton")));
		
if (StartButton && RestartButton)
{
	if (bIsRestart)
	{
    // Restart일때 StartButton은 사라지게 하고 RestartButton만 보이게 한다.
		StartButton->SetVisibility(ESlateVisibility::Collapsed);
		RestartButton->SetVisibility(ESlateVisibility::Visible);

		if (UTextBlock* ButtonText = Cast<UTextBlock>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("RestartButtonText"))))
		{
			ButtonText->SetText(FText::FromString(TEXT("Restart")));

		}
	}
	else
	{
    // 위와 반대로
		StartButton->SetVisibility(ESlateVisibility::Visible);
		RestartButton->SetVisibility(ESlateVisibility::Collapsed);

		if (UTextBlock* ButtonText = Cast<UTextBlock>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("StartButtonText"))))
		{
			ButtonText->SetText(FText::FromString(TEXT("Start")));
		}
	}
}
```

**<Animation 실행 코드>**

```cpp
// 에디터에서 만든 PlayGameOverAnim을 실행
UFunction* PlayAnimFunc = MainMenuWidgetInstance->FindFunction(FName("PlayGameOverAnim"));
if (PlayAnimFunc)
{
				MainMenuWidgetInstance->ProcessEvent(PlayAnimFunc, nullptr);
}
```
  </p>
</details>

#### <!-- 26.04.21 -->
<details> 
  <summary><s>26.04.21</s></summary>
  <p>

```cpp
// 코드카타 84번 unordered_map 활용
#include <string>
#include <vector>
#include <stack>
#include <unordered_map>

using namespace std;

bool isValid(string s)
{
    stack<char> sstack;
    unordered_map<char, char> s_map{
        {')', '('},
        {'}', '{'},
        {']', '['}
    };
    
    for(char chr : s)
    {
        if(s_map.count(chr))
        {
            if(sstack.empty() || s_map[chr] != sstack.top())
            {
                return false;
            }
            else
            {
                sstack.pop();
            }
        }
        else
        {
            sstack.push(chr);
        }
    }
    return sstack.empty();
}

int solution(string s) {
    int answer = 0;
    
    for(int i = 0; i < s.length(); ++i)
    {
        if(isValid(s))
        {
            answer ++;
        }
        
        char sf = s[0];
        s = s.substr(1) + sf;
    }
    
    return answer;
}
```

<br/>

**<과제 8번 시작 전 처음부터 싹 다 복습>**   

과제 8번이 챕터 2~ 4에 했던거에 더 보충하는 느낌인데 이미 해놓은거에 덮어씌우는거보단 최대한 보지않고 직접 다시 구현해보는게 좋을 것 같다고 판단했다.   

1.클래스간 구조 파악 다시 한번 더 해보고 정리   
2.추가로 스마트포인터를 사용하면서 코딩  
3.UPROPERTY, UFUNCTION 같은 언리얼 리플렉션 매크로의 설정을 최대한 보수적으로(VisibleAnywhere 등등) 잡아서 감각 늘리기 

<br/>

**캐릭터**   

Character   
Camera, SpringArm   

```cpp
// 카메라와 스프링암

#include "Camera/CameraComponent.h" // 카메라 헤더
#include "GameFramework/SpringArmComponent.h" // 스프링암 헤더

PrimaryActorTick.bCanEverTick = false;

SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArm"));
// RootComponent(Character는 자동으로 캡슐이 루트)
SpringArm->SetupAttachment(RootComponent);
// 스프링암 길이 설정
SpringArm->TargetArmLength = 500.f;
// Pawn(Character)의 회전과 스프링암 회전을 같게 할 것인지
SpringArm->bUsePawnControlRotation = true;

Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("Camera"));
// 카메라가 붙는 SpringArm 맨 끝이 SocketName이다 
// 그냥 Camera->SetupAttachment(SpringArm)이라고 해도 되지만 SocketName을 명시해주면 더 명확해진다.
Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);
// 카메라는 어차피 스프링암에 붙어있기 때문에 false
Camera->bUsePawnControlRotation = false;
```

<br/>

PlayerController   
IA, IMC   
BeginPlay() -> IMC 연결   

```cpp
// IMC 등록하기

// Subsystem을 불러오기 위해 필요한 헤더
#include "EnhancedInputSubsystems.h"

void AMyPlayerController::BeginPlay()
{
	Super::BeginPlay();

	// 1.LocalPlayer를 가져온다.
	if (TObjectPtr<ULocalPlayer> LocalPlayer = GetLocalPlayer())
	{
		// 2.LocalPlayer의 Subsystem을 가져온다.
		if (TObjectPtr<UEnhancedInputLocalPlayerSubsystem> Subsystem = LocalPlayer->GetSubsystem<UEnhancedInputLocalPlayerSubsystem>())
		{
			if (InputMappingContext) // IMC가 있다면
			{
				// 3.LocalPlayer의 Subsystem에 IMC를 등록해준다. 0은 제일 높은 우선순위.
				Subsystem->AddMappingContext(InputMappingContext, 0);
			}
		}
	}
}
```

GameMode   
기본 설정을 한다.   
<br/>

```cpp
#include "MyGameMode.h"
#include "MyCharacter.h"
#include "MyPlayerController.h"

AMyGameMode::AMyGameMode()
{
	// 클래스의 객체를 전달하는게 아니라 클래스 자체(설계도)를 넘겨준다.
	DefaultPawnClass = AMyCharacter::StaticClass();
	PlayerControllerClass = AMyPlayerController::StaticClass();
}
```

**<VisibleAnywhere 이해하기>**   

VisibleAnywhere를 써도 수정 가능한 상황이 많이 나와서 찾아봤다.   

컴포넌트, 서브객체인 경우 이런 상황이 나온다.   
컴포넌트의 경우 컴포넌트 자체는 고정하고 세부 값만 건드리라는 뜻이다.   
즉, EditAnywhere로 바꾸면 컴포넌트 자체를 바꾸거나 비워버릴 수 있다는 것   

변수(메모리 주소) 자체를 수정할 수 있으면 Edit, 없으면 Visible 이란 뜻이다.   

  </p>
</details>

#### <!-- 26.04.22 -->
<details> 
  <summary><s>26.04.22</s></summary>
  <p>

**<코드카타 85번>**   

3중 for문 안쓰고 2중으로 쓰는 방법
```cpp
#include <vector>
#include <unordered_set>

using namespace std;

int solution(vector<int> elements) {
    int n = elements.size();
    // 원형 수열 처리를 위해 배열 확장
    vector<int> extended = elements;
    extended.insert(extended.end(), elements.begin(), elements.end());

    unordered_set<int> unique_sums;

    // 부분 수열의 길이 len을 1부터 n까지 순회
    for (int len = 1; len <= n; ++len) {
        int current_sum = 0;

        // 1. 첫 번째 윈도우의 합을 구함 (0번 인덱스부터 len 길이만큼)
        for (int i = 0; i < len; ++i) {
            current_sum += extended[i];
        }
        unique_sums.insert(current_sum);

        // 2. 윈도우를 한 칸씩 밀면서 합을 업데이트 (슬라이딩)
        // 시작 지점(i)을 1부터 n-1까지 이동
        for (int i = 1; i < n; ++i) {
            // 이전 원소(extended[i-1])는 빼고, 새 원소(extended[i + len - 1])는 더함
            current_sum -= extended[i - 1];
            current_sum += extended[i + len - 1];
            unique_sums.insert(current_sum);
        }
    }

    return unique_sums.size();
}
```

<br/>

**<실제 캐릭터 움직임 바인딩하기>**   

컨트롤러가 IA, IMC를 가지고 있고 캐릭터는 실제 움직임을 가지고 있는데 이 두가지를 연결해야한다.   

```cpp
// Character.h

// 전방선언
struct FInputActionValue;

// 리플렉션 시스템에 등록한다.
// BindAction을 할 때 리플렉션 시스템에 등록됐는지 확인을 하기 때문이다.
// 또한 함수 이름으로 호출도 가능해진다.
// 델리게이트 시스템에도 연동이 된다.   
UFUNCTION()
// 인자는 IA의 값을 넣어준다.   
void Move(const FInputActionValue& Value);



// Character.cpp
// 밑에 코드를 위해서는 #include "InputActionValue.h"를 써도 되는데 결국 바인딩도 하기 때문에 더 넓은 범위의 헤더파일을 가져옴
#include "EnhancedInputComponent.h"

void AMyCharacter::Move(const FInputActionValue& Value)
{
	// 캐릭터가 Possess 되어야 로직을 처리할 수 있어서 체크
	if (!GetController()) return;

	// 에디터에서 IA의 Value Type을 FVector2D 값으로 설정해뒀기 때문
	FVector2D const MoveInput = Value.Get<FVector2D>();
	
	// Input Value의 X값이 0이 아닐때(X축으로 움직일때만)
	if (!FMath::IsNearlyZero(MoveInput.X))
	{
		// GetActorForwardVector()는 액터의 정면 "방향"을 가져온다.
		AddMovementInput(GetActorForwardVector(), MoveInput.X);
	}
	// Input Value의 Y값이 0이 아닐때(Y축으로 움직일때만)
	if (!FMath::IsNearlyZero(MoveInput.Y))
	{
		// GetActorForwardVector()는 액터의 오른쪽 "방향"을 가져온다.
		AddMovementInput(GetActorRightVector(), MoveInput.Y);
	}
}
```


<br/>

**<Enhanced Input 관련 헤더들>**   

```cpp
//컴포넌트 및 바인딩 관련
#include "EnhancedInputComponent.h"
//IMC 추가/제거 관련
#include "EnhancedInputSubsystems.h" 
//입력 값 추출 관련
#include "InputActionValue.h" 
```

  </p>
</details>

#### <!-- 26.04.23 -->
<details> 
  <summary><s>26.04.23</s></summary>
  <p>

마스터 과제 제출 완료   
UE5 강의 챕터3 부분 다시 복습하며 구현중      

**<RTTI와 RAII의 차이점>**   

Run-Time Type Information   
RTTI는 프로그램 실행 중에 객체의 실제 타입을 확인하는 기능입니다.   
클래스에 가상함수가 하나 이상 있어야 하고 주로 dynamic_cast를 사용합니다.(다운캐스팅중 사용한다. 부모 포인터 -> 자식 포인터)   
(typeid도 있긴함 객체의 타입 정보를 반환)   

RAII   
Resource Acquisition Is Initialization   
객체의 생명 주기(Scope)와 자원의 관리 주기를 같게 하여 메모리를 안전하게 관리하는 방법입니다.   
메모리 누수를 방지 할 수 있고 이를 사용하는 도구는 소멸자, 스마트 포인터등이 있습니다.   

  </p>
</details>

#### <!-- 26.04.24 -->
<details> 
  <summary><s>26.04.24</s></summary>
  <p>

**<오버래핑한 Actor들을 배열에 저장>**   

```cpp
TArray<AActor*> OverlappingActors;
ExplosionCollision->GetOverlappingActors(OverlappingActors);
// 참고로 GetOverlappingActors는 TArray<AACtor*>& 형식으로 받기때문에 OverlappingActors를 TObjectPtr로 구현하면 오류가 난다.
```

<br/>

**<TObjectPtr 가이드라인>**   

언리얼엔진에서는 클래스의 멤버 변수에는 `TObjectPtr`을 쓰고 함수의 매개변수, 지역변수에는 기존 포인터를 쓰는 게 가이드라인이라고 한다.   

<br/>

**<언리얼 심화 정리>**   

오늘 배운건 아래 3가지   
하나만 인식하는 트레이스   
여러개를 인식하는 트레이스   
비동기 트레이스   

Trace 쓰는 방법은 2가지, 블루프린트(Kismet)와 C++ (GetWorld()->...)   
평소에 블루프린트로 쓰다가(디버깅이 매우 쉬워서) 출시 직전엔 GetWorld()방식   
C++ 방식이 미세하게 더 가볍다.   

**콜리전 프리셋**   
나만의 콜리전 프리셋을 만들 수 있음      
project setting -> engine -> collision
Object Channels에 하나 만들어주고      
여기서 Preset-New Profile에 추가하고 설정해주면 된다.   

**큐브**   
큐브를 하나 꺼내보면 Block처리 되는데 큐브의 StaticMeshComponent에 있는 Collision이 Default로 되어있음   
이 뜻이 이 메시 자체에 있는 Collision 프리셋을 그대로 따르겠다는 뜻   
메시에 들어가서 콜리전을 직접 수정할 수 있는데 단순/복합이 있음    
심플은 가볍지만 정밀하지 않고 복합은 거의 폴리곤 단위로 콜리전이 있지만 부하가 심함    
여기서 Collision Complexity 들어가면 여러가지가 있는데 그중 Simple And Complex 는 평소엔 심플하게 하다가 충돌이 있을때 컴플렉스로 바꿈   

**<싱글 트레이스>**   
```cpp
 //싱글 트레이스(UKismetSystemLibrary 사용)
 //싱글은 Block에만 막힘
void AMyActor::StartSingleTrace()
{
	TArray<AActor*> ActorsToIgnore;
	ActorsToIgnore.Add(this);
	FHitResult HitResult;

	// 첫 인자는 this 넣어도 작동함
	// .Add(this)를 해줬지만 한번 더 true로 해준다.
	// 이래야 버그가 안생김(가끔 다른 컴포넌트가 액터에 붙으면 검출되는 상황이 있음)
	UKismetSystemLibrary::LineTraceSingle(
    // this로 넣어줘도 됨
		GetWorld(), 
    // 시작지점
		GetActorLocation(),
    // 끝지점(액터의 방향벡터와 길이에 시작지점을 더해줘서 구함) 
		GetActorForwardVector() * 1000.f + GetActorLocation(), 
    // TraceType을 Visibility로 설정
		UEngineTypes::ConvertToTraceType(ECC_Visibility),
    // Complex 설정(false로 하면 simple이 됨)
		false,
    // 무시할 엑터를 모아둔 배열
		ActorsToIgnore,
    // 디버깅 얼마동안 할지(밑에 설정은 1프레임)
		EDrawDebugTrace::ForOneFrame,
    // 충돌 결과
		HitResult,
    // 나 자신을 무시할지 결정하는건데, 위에 이미 무시한다고 넣어놨지만 여기도 true로 해줘야 확실하게 무시하게 됨(버그 방지)
		true,
    // 트레이스 색깔
		FLinearColor::Red,
    // 트레이스 충돌 시 색깔
		FLinearColor::Green
	);
}
```
<br/>

**<멀티 트레이스>**

```cpp
// 멀티 트레이스(UKismetSystemLibrary 사용)
// Overlap은 다 뚫으면서 지나가고 Block에서 막히는데 Block만 있으면 싱글과 같은 기능을 함
// 싱글과 거의 같지만 충돌을 다중으로 하기 때문에 FHitResult만 TArray로 감싸주면 된다.
void AMyActor::StartSingleTrace()
{
	TArray<AActor*> ActorsToIgnore;
	ActorsToIgnore.Add(this);
	TArray<FHitResult> HitResult;

	UKismetSystemLibrary::LineTraceMulti(
		GetWorld(),
		GetActorLocation(),
		GetActorForwardVector() * 1000.f + GetActorLocation(),
		UEngineTypes::ConvertToTraceType(ECC_Visibility),
		false,
		ActorsToIgnore,
		EDrawDebugTrace::ForOneFrame,
		HitResult,
		true,
		FLinearColor::Red,
		FLinearColor::Green
	);
}
```

<br/>

**<비동기 방식>**   

위 2개는 블루프린트 방식으로 구현했으니 마지막 비동기는 C++ 방식으로 구현   

```cpp
// 비동기 방식
// 메인 스레드에서 다른 스레드한테 일을 짬때림. 그 스레드는 일을 끝내고 다시 결과물을 메인에 줌
void AMyActor::StartAsycnTrace()
{
	// AsyncLineTraceByChannel에 쓸 Delegate 함수 바인딩
	FTraceDelegate TraceDelegate;
	TraceDelegate.BindUObject(this, &AMyActor::OnAsyncTraceCompleted);

	// UWorld() 방식은 이렇게 쿼리를 직접 가져와서 세팅
	FCollisionQueryParams QueryParams;
	FCollisionResponseParams ResponseParams;

	QueryParams.AddIgnoredActor(this);
	QueryParams.bTraceComplex = false;

	// 이 액터랑 부딪히는 오브젝트의 타입이 WorldDynamic이면 콜리전 타입을 강제로 오버랩으로 바꿔버리는 기능
	// 근데 Ignore > Overlap > Block 순으로 약해져서
	// Ignore로 설정해뒀으면 밑에 코드에서 Block으로 바꿔도 안바꿔진다.
	// Block으로 해둔걸 Ignore나 Overlap으로 바꾸거나 Overlap을 Ignore로 바꾸는 용도
	ResponseParams.CollisionResponse.WorldDynamic = ECR_Block;

	// EAsyncTraceType::Test 는 bool 처럼 인식 했냐 안했냐만 체크를 하기때문에 매우 가볍다
	// 예를 들어 눈이 먼 몬스터처럼 인식만 가능한 경우 사용  
	GetWorld()->AsyncLineTraceByChannel(
		// TraceType을 Multi로
		EAsyncTraceType::Multi,
		// Trace 시작점
		GetActorLocation(),
		// Trace 끝점
		GetActorForwardVector() * 1000.f + GetActorLocation(),
		// TraceType
		ECC_Visibility,
		// 위에 설정해둔 QueryParams
		QueryParams,
		ResponseParams,
		// Delegate 함수
		&TraceDelegate
	);
}

// AsyncLineTraceByChannel을 위한 Delegate 함수
void AMyActor::OnAsyncTraceCompleted(const FTraceHandle& Handle, FTraceDatum& Data)
{
	for (const FHitResult& Hit : Data.OutHits)
	{
		AActor* HitActor = Hit.GetActor();

		if (!IsValid(HitActor)) return;

		GEngine->AddOnScreenDebugMessage(-1, 0.f, FColor::Green, FString::Printf(TEXT("Multi Hit Actor : %s"), *HitActor->GetName()));

		// 블루프린트 형식과 다르게 Debug를 알아서 해줘야한다.
		DrawDebugSphere(GetWorld(), Hit.ImpactPoint, 20.f, 12, FColor::Green, false, 2.f);

		// #include "Kismet/KismetSystemLibrary.h" 있어야함
		UGameplayStatics::ApplyPointDamage(
			// 데미지 받는 액터
			HitActor,
			// 기본 데미지 값
			50.f,
			// 데미지 방향
			GetActorForwardVector(),
			// 충돌 결과
			Hit,
			// 때린 놈의 컨트롤러
			GetInstigatorController(),
			// 때린 놈
			this,
			// UDamageType 클래스
			UMyFireDamageType::StaticClass()
		);
	}
}
```

<br/>

**<DamageType과 커스텀>**

DamageType이라는 클래스가 있는데 내용을 보면 진짜 별거 없는 베이스 클래스이다.   

```cpp
// 실제 UDamageType 내부 모습
// 데미지 관련 변수들만 가득하다.
UCLASS(MinimalAPI, const, Blueprintable, BlueprintType)
class UDamageType : public UObject
{
	GENERATED_UCLASS_BODY()

	/** True if this damagetype is caused by the world (falling off level, into lava, etc). */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=DamageType)
	uint32 bCausedByWorld:1;

	/** True to scale imparted momentum by the receiving pawn's mass for pawns using character movement */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=DamageType)
	uint32 bScaleMomentumByMass:1;

	/** When applying radial impulses, whether to treat as impulse or velocity change. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = RigidBody)
	uint32 bRadialDamageVelChange : 1;

	/** The magnitude of impulse to apply to the Actors damaged by this type. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=RigidBody)
	float DamageImpulse;

	/** How large the impulse should be applied to destructible meshes */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Destruction)
	float DestructibleImpulse;

	/** How much the damage spreads on a destructible mesh */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Destruction)
	float DestructibleDamageSpreadScale;

	/** Damage fall-off for radius damage (exponent).  Default 1.0=linear, 2.0=square of distance, etc. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=DamageType)
	float DamageFalloff;
};
```

<br/>

**<기본 DamageType>**   

기본 타입을 쓰면 어떻게 될까?

```cpp
UGameplayStatics::ApplyPointDamage(
			HitActor,
			50.f,
			GetActorForwardVector(),
			Hit,
			GetInstigatorController(),
			this,
			// 기본 UDamageType 쓰기
			UDamageType::StaticClass()
		);
```

아무런 로직이 없기 때문에 순수하게 데미지만 전달된다.   

<br/>

**<DamageType 커스텀하기>**

```cpp
// UDamageType을 상속받은 커스텀 데미지 타입을 만든다. 
// MyFireDamageType.h
UCLASS()
class MYPROJECT_API UMyFireDamageType : public UDamageType
{
	GENERATED_BODY()
	
public:

	UMyFireDamageType();
	
	// 화상 지속시간
	UPROPERTY(EditAnywhere, BlueprintReadOnly)
	float BurnDuration;
	// 방어구 관통
	UPROPERTY(EditAnywhere, BlueprintReadOnly)
	float ArmorPenetration;
};

// MyFireDamageType.cpp
UMyFireDamageType::UMyFireDamageType()
{
	// 화상 지속시간
	BurnDuration = 5.f;
	// 방어력 관통
	ArmorPenetration = 0.2f;
}
```

<br/>

**<커스텀 데이터타입 사용해보기>**   

```cpp
// 실제 데미지를 입는 Actor에 TakeDamage 함수를 오버라이드해서 사용해보았다.  
// ACharacter 사용

float AMyProjectCharacter::TakeDamage(float DamageAmount, FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser)
{
	float ActualDamage = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	
  // 이부분은 기본 데이터타입 사용
	// #include "Engine/DamageEvents.h" 필요
	// 헤더에 있는 UDamageType으로 사용
	//const UDamageType* DT = DamageEvent.DamageTypeClass->GetDefaultObject<UDamageType>();
	
	//if (DT && DT->bCausedByWorld)
	//{
	//	// 낙사, 트랩...

	//	UE_LOG(LogTemp, Warning, TEXT("ByWorld Damage Received"));
	//}

	//if (EventInstigator)
	//{
	//	UE_LOG(LogTemp, Warning, TEXT("Im Enemy"));
	//}


	// 내가 만든 데미지 타입으로 커스텀
	const UMyFireDamageType* FireDamage = DamageEvent.DamageTypeClass->GetDefaultObject<UMyFireDamageType>();

	if (FireDamage)
	{
    // 커스텀 해준 값들 실제로 사용
		ActualDamage *= (1.f + FireDamage->ArmorPenetration);

		// 화상효과, 이펙트, 사운드 설정 추가 가능

		UE_LOG(LogTemp, Warning, TEXT("Fire Damage Received"));
	}

	// HP -= ActualDamage; 

	return ActualDamage;
}
```

  </p>
</details>

#### <!-- 26.04.25 -->
<details> 
  <summary><s>26.04.25</s></summary>
  <p>

**<알고리즘 레벨2 복습>**

정렬 특징들 간단히 정리   

버블
인접한 애 비교하고 스왑함   
최대값/최소값을 맨 뒤로가게 하는 원리   
비교, 스왑 횟수가 1씩 줄어듦(최대길이 - 1 씩)   
비교횟수 == 교환횟수 O(n^2)   
최선 : O(n^2)   

선택   
시작 시 맨 앞 값을 최대값/최소값으로 설정   
뒤로 쭉 비교해서 조건에 맞으면 스왑함   
비교횟수O(n^2) > 교환횟수O(n)   
최선 : O(n^2)   

삽입   
시작 시 맨 앞 값은 정렬된 값으로 취급   
정렬 안된 첫 값을 key로 두고 정렬된 곳과 비교해서 적절한 위치에 삽입   
비교횟수 == 교환횟수 O(n^2)   
최선 : O(n) -> C++ sort()에서 크기가 16 이하이면 삽입정렬을 실행함   

c++ sort()는 퀵 정렬 기반에 안전장치가 달린 Introsort 하이브리드 알고리즘이다   
-> 안전장치 : 16개 이하면 삽입 정렬, 최악의 경우가 감지되면 힙 정렬   

<br/>

버블, 선택, 삽입 정렬 안보고 직접 구현해봄   

```cpp
// 버블 정렬
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> bubble_array = {5, 4 ,1, 3, 2};

    for(int i = 0; i < bubble_array.size() - 1; ++i)
    {
        for(int j = 0; j < bubble_array.size() - 1 - i; ++j)
        {
            if(bubble_array[j] > bubble_array[j + 1])
            {
                swap(bubble_array[j], bubble_array[j + 1]);
            }
        }
    }

    for(const int& num : bubble_array)
    {
        cout << num << " ";
    }

    return 0;
}
```

```cpp
// 선택 정렬
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> selection_array = {5, 4, 1, 3, 2};
    int min;

    for (int i = 0; i < selection_array.size() - 1; ++i)
    {
        min = i;
        for (int j = i; j < selection_array.size(); ++j)
        {
            if (selection_array[min] > selection_array[j])
            {
                min = j;
            }
        }
        if (min != i)
        {
            swap(selection_array[i], selection_array[min]);
        }
    }

    for (const int &num : selection_array)
    {
        cout << num << " ";
    }

    return 0;
}
```

```cpp
// 삽입 정렬
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> insertion_array = {5, 4, 1, 3, 2};

    for (int i = 1; i < insertion_array.size(); ++i)
    {
        int key = insertion_array[i];
        int j = i - 1;
        while (j >= 0 && insertion_array[j] > key)
        {
            insertion_array[j + 1] = insertion_array[j];
            --j;
        }
        insertion_array[j + 1] = key;
    }

    for (const int &num : insertion_array)
    {
        cout << num << " ";
    }

    return 0;
}
```

<br/>

병합정렬 문제 풀기1

단순하기만 할 줄 알았는데 배열을 딱 2개만 써야해서 시간이 좀 걸렸다.   
큰 값을 뒤부터 채워넣으면 된다.   
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        // nums1 index: 0 ... m - 1
        // nums2 indes: m ... m + n - 1
        int nums1_index = m - 1;
        int nums2_index = n - 1;

        for(int i = m + n - 1; i >= 0; --i)
        {
            if(nums1_index == -1)
            {
                nums1[i] = nums2[nums2_index--];
                continue;
            }
            
            if(nums2_index == -1)
            {
                nums1[i] = nums1[nums1_index--];
                continue;
            }

            if(nums1[nums1_index] >= nums2[nums2_index])
            {
                nums1[i] = nums1[nums1_index--];
            }
            else
            {
                nums1[i] = nums2[nums2_index--];
            }      
        }
    }
};
```

<br/>

병합정렬 문제 풀기2   

굉장히 복잡하다. 직접 구현은 못하였고 코드를 보며 병합 정렬의 방식을 이해하였다.   
정렬된 두 배열을 합치면서 새 배열을 만들어내기 때문에 정렬에는 O(n)만 걸린다.(각각의 최솟값만 비교하면 됨)      
분할은 계속 반으로 쪼개기 때문에 O(logn)이다.   


```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }
    
    void mergeSort(vector<int>& nums, int left, int right) {
        if (left >= right) return;

        int mid = left + (right - left) / 2;

        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);

        merge(nums, left, mid, right);
    }

    void merge(vector<int>& nums, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        vector<int> L(n1), R(n2);

        for (int i = 0; i < n1; i++) 
        {
            L[i] = nums[left + i];
        }
        for (int j = 0; j < n2; j++) 
        {
            R[j] = nums[mid + 1 + j];
        }

        int i = 0, j = 0, k = left;

        while (i < n1 && j < n2) 
        {
            if (L[i] <= R[j]) 
            {
                nums[k++] = L[i++];
            } 
            else 
            {
                nums[k++] = R[j++];
            }
        }

        while (i < n1) 
        {
            nums[k++] = L[i++];
        }
        while (j < n2)
        {
            nums[k++] = R[j++];
        } 
    }
};
```
  </p>
</details>

#### <!-- 26.04.26 -->
<details> 
  <summary>26.04.26</summary>
  <p>

3주치 TIL 정리 완료   

심화 2주차 도강   

**<삼각함수>**   

반지름이 1인 원 = 단위원
단위원의 좌표는 (x, y) = (cosθ, sinθ) 

단위원: 반지름1
단위벡터 : 크기가 1인 벡터
단위 방향 벡터: 각도 θ에 해당하는 단위원 위 점 (cosθ, sinθ)
단위 방향 벡터에 속도크키(스칼라)를 곱하면 속도 벡터가 나온다


각도를 라디안(radian, rad)으로 계산한다.
한바퀴 = 2π rad
FMath::Sin 같은 곳에선 라디안

에디터에선 도(degree)단위

**<벡터의 내적>**   

두 벡터의 성분끼리 곱하고 더한다.
벡터 a = (3, 4) 벡터 b = (5, 0)
a . b = 3 * 5 + 4 * 0 = 15

단위벡터로 비교를 해보면 내적값에 따라 `방향 정렬도`가 나온다.
(1, 0) (1, 0) 내적1  내적 최댓값이면 같은방향
(1, 0) (0, 1) 내적0  내적 0이면 수직
(1, 0) (-1, 0) 내적-1 내적 최솟값이면 반대방향

두 벡터의 내적은 ||a|| ||b|| cosθ 이다. ||x||는 벡터 x의 크기를 나타낸다 (norm이라고 함)
내적 = 길이 x 길이 x 정렬도

실제로 단위벡터로 만들고 계산을 하기 때문에 cosθ에 따라서 달라진다고 생각하면 된다.
0도면 1, 90도면 0, 180도면 -1 이니까 각각 같은 방향, 수직, 반대방향이다.
이를 활용하면 0 초과면 같은방향(앞쪽) 0 미만이면 반대방향(뒤쪽)이 나온다

시야각 판정은 절반을 비교
시야각 90 -> 좌 45 우 45
시야각 120 -> 좌 60 우 60 

시야각에 따른 임계값(cos)   
각각 시야각의 절반과 임계값이다.     
30도 0.866    
45도 0.707   
60도 0.500   
90도 0.000   

**<벡터의 외적>**   

내적은 얼마나 같은 방향인지만 알려주고 좌우는 방향은 알려주지 않는다.(부호가 없음)
그래서 외적도 필요하다.   
성분을 크로스해서 곱하고 빼준다.
벡터 a = (3, 4) 벡터 b = (5, 0)
a X b = 3 * 0 + 4 * 5 = 20

두 벡터의 외적은 ||a|| ||b|| sinθ 이다.
벡터a X 벡터b -> a 크로스 b
2d에선 스칼라 하나, 3d에선 벡터가 나온다

3d
두 벡터는 한 평면을 이루고, 그 평면에 수직인 축이 하나 생긴다. 외적의 결과가 그 법선(normal) 벡터이다.
법선은 3d 게임의 핵심 : 조명 계산(빛이 면에 얼마나 닿나), 벽이 어느쪽을 보나 판정 등등

외적의 부호(벡터 a X 벡터 b)      
0 초과면 벡터b가 벡터a의 왼쪽(반시계)   
0 이면 평행(같은 방향 혹은 아예 반대)   
0 미만이면 벡터b가 벡터a의 오른쪽(시계)   

포탑이 목표 방향을 향해 돌 때   
외적 부호 양수 -> 반시계(왼쪽)로 돌면 빠름   
외족 부호 음수 -> 시계(오른쪽)로 돌면 빠름   

부호 하나로 바로 결정할 수 있음   



외적의 절댓값 = 평행사변형 넓이   

두 벡터가 만드는 평행사변형의 넓이가 외적의 절댓값   
2로 나누면 삼각형의 넓이   
각도 90도 일 때 최대넓이(sin이니까)
각도 0도 일 대 넓이 0

삼각 측량
점 P가 삼각형 안에 있는지 확인하는 방법   
벡터 AB X 벡터 AP -> P가 AB의 왼쪽인가?   
벡터 BC X 벡터 BP -> P가 BC의 왼쪽인가?   
벡터 CA X 벡터 CP -> P가 CA의 왼쪽인가?   
세 부호가 모두 같으면 P는 삼각형 안.   

메쉬 충돌, 경계선 내부 판정, 레벨 지역 체크에 자주 쓰이는 패턴   

**<UE5에서 쓰는 법>**   

```cpp
float d = FVector::DotProduct(A, B);
FVector c = FVector::CrossProduct(A, B);

float s = FMath::Sin(AngRad);
float r = FMath::DegreesToRadians(Deg);
```

  </p>
</details>

#### <!-- 26.04.27 -->
<details> 
  <summary>26.04.27</summary>
  <p>

**`FTableRowBase`**   
언리얼 엔진에서 “이 구조체는 데이터 테이블로 쓸 수 있다”라고 인식하게 해주는 베이스 구조체입니다.   

**`TSoftClassPtr<AActor>`**   
소프트 레퍼런스로, 클래스를 바로 로드하지 않고도 경로만 기억해둘 수 있습니다.   
필요할 때 `Get()`을 통해 실제 `UClass*`를 얻어 인스턴스를 생성할 수 있습니다.

언리얼 엔진에서 **GameMode**와 **GameState**는 게임의 전역 정보를 유지하고, 필요할 경우 멀티플레이어 환경에서 해당 정보를 **서버**와 **클라이언트** 간에 동기화하는 역할을 합니다.   

**GameMode**   
“게임의 규칙(룰)”을 정의하고 관리합니다.   
어떤 캐릭터를 스폰할지, 플레이어가 사망했을 때 어떻게 처리할지를 결정합니다.   
멀티플레이에서는 **서버 전용**으로 동작합니다(클라이언트에는 존재하지 않음).   
  

**GameState**   
게임 플레이 전반에서 “공유되어야 하는 전역 상태”를 저장합니다. `GameState`는 기본적으로 “레벨당 1개” 존재하며, 엔진 내부에서 데이터 동기화를 고려해 설계되었기에 전역 데이터 관리용으로 적합합니다.   
대표적으로 점수, 남은 시간, 현재 게임 단계(Phase), 스폰된 오브젝트의 총 개수 등을 저장합니다.   
멀티플레이에서는 서버가 관리하고, 클라이언트는 이를 **자동으로 동기화** 받아볼 수 있습니다.   

**싱글 플레이**에서도 `GameState`가 굳이 필요 없을 것 같지만, “전역적으로 공유해야 할 정보”를 한 군데서 관리하면 유지보수가 더 편해집니다. “몇 개의 아이템이 스폰되었는지”, “현재 게임 진행도는 어느 정도인지” 같은 데이터를 `GameState`에서 일괄 관리할 수 있기 때문입니다.   

**Game Instance**  
프로젝트가 시작될 때 (에디터에서 게임 실행을 누른 시점)부터 애플리케이션이 완전히 종료될 때까지 **유일하게 계속 살아있는 객체**입니다.   
맵이 전환되어도 **파괴되지 않으므로**, 여기서 전역 데이터를 유지할 수 있습니다.

**Seamless Travel**   
멀티플레이 환경에서 주로 사용되는 레벨 전환 방식으로, `GameState`/`PlayerController` 등을 **파괴하지 않고** 그대로 다음 맵으로 넘어가는 기능입니다.   
Seamless Travel을 사용하면 대부분의 객체를 유지할 수 있지만, 설정과 로직이 조금 더 복잡하므로, 싱글 플레이 전용 간단 프로젝트라면 `GameInstance`를 사용하기가 쉽습니다.   

**<폰 움직이게 하기>**   

Character 처럼 AddMovementInput으로 하려고 했는데 폰은 다르다고 해서 찾아봤다.   

```cpp
class UFloatingPawnMovement;

UCLASS()
class ABaseGun : public APawn
{
    // ... 기존 코드 ...

protected:
    UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Movement")
    TObjectPtr<UFloatingPawnMovement> MovementComp;
};


#include "GameFramework/FloatingPawnMovement.h" // 헤더 포함 필수!

ABaseGun::ABaseGun()
{
    // ... 기존 컴포넌트 생성 코드 ...

    // FloatingPawnMovement 생성
    // 이 컴포넌트는 생성만 해두면 내부적으로 AddMovementInput을 감지해서 작동합니다.
    MovementComp = CreateDefaultSubobject<UFloatingPawnMovement>(TEXT("MovementComp"));
}
```

하지만 움직이지 않아서 찾아봤더니

```cpp
// 무브먼트 컴포넌트가 루트 컴포넌트를 움직이게 명시적으로 설정
MovementComp->UpdatedComponent = CapsuleComp;
// 이렇게 안하면 안움직이는 경우가 있다고 한다.
```

  </p>
</details>

#### <!-- 26.04.28 -->
<details> 
  <summary>26.04.28</summary>
  <p>

**<OpenLevel 로직>**   

```cpp
// 레벨을 오픈하면(OpenLevel) BeginPlay()가 다시 실행된다.
if (LevelMapNames.IsValidIndex(CurrentLevelIndex))
{
	UGameplayStatics::OpenLevel(GetWorld(), LevelMapNames[CurrentLevelIndex]);
}
```

**<게임종료 구현>**   

```cpp
#include "Kismet/KismetSystemLibrary.h"

void AMyPlayerController::ExitGame()
{
    // 1. 월드 컨텍스트 가져오기 (현재 게임 세상)
    UWorld* World = GetWorld();
    if (!World) return;

    // 2. 종료 함수 호출
    // - World: 현재 월드
    // - Target: 특정 플레이어 (보통 GetFirstPlayerController)
    // - QuitPreference: 종료 방식 (보통 Quit)
    // - bIgnorePlatformRestrictions: 플랫폼 제한 무시 여부 (보통 false)
    UKismetSystemLibrary::QuitGame(
        World, 
        World->GetFirstPlayerController(), 
        EQuitPreference::Quit, 
        false
    );
}
```

**<Start버튼을 누르기 전에 GameState가 실행되는 현상>**   

발생현상: Start버튼을 누르지 않았는데 Wave가 시작됐다고 출력이 된다.   
원인: 게임실행을 했을 때 GameState의 BeginPlay()도 바로 실행되기 때문에 발생했다.   
해결방법: GameInstance에 bool 변수를 하나 만들어서 Start 버튼을 눌렀을때 상태를 변화시키고 그 조건을 만족하면 BeginPlay()의 StartLevel이 실행되도록 바꿨다.   

```cpp
// GameState의 BeginPlay()에 조건 추가
if (UMyGameInstance* GameInstance = Cast<UMyGameInstance>(GetGameInstance()))
{
	if (GameInstance->bShouldStartRightNow)
	{
		StartLevel();
	}
}

// PlayerController의 StartGame()에 조건 추가
if (UMyGameInstance* MyGameInstance = Cast<UMyGameInstance>(UGameplayStatics::GetGameInstance(this)))
{
	MyGameInstance->CurrentLevelIndex = 0;
	MyGameInstance->TotalScore = 0;
	MyGameInstance->bShouldStartRightNow = true;
}

UGameplayStatics::OpenLevel(GetWorld(), FName("BasicLevel"));
```

<br/>

**<Timer는 매개변수 없는 함수를 써야한다>**   

늘 매개변수 없는 함수를 넣다보니 UFUNCTION()으로 등록하고 이름만 전달하면 되는줄 알았는데 아니었다.   

람다식으로 바꿔서 하거나 매개변수를 없애야했다.   

```cpp
// 1.오류가 난 코드
void AMySlowingItem::StartSlowing(AMyCharacter* Actor)
{
	Actor->SetPlayerSlow(0.5f);

	GetWorld()->GetTimerManager().SetTimer(
		SlowTimerHandle,
		this,
		&AMySlowingItem::StopSlowing,
		5.f,
		false
	);
}

void AMySlowingItem::StopSlowing(AMyCharacter* Actor)
{
	Actor->SetPlayerNormal();
}


// 2.람다식을 사용해서 수정
void AMySlowingItem::StartSlowing(AMyCharacter* Actor)
{
    Actor->SetPlayerSlow(0.5f);

    // 람다를 사용하여 Actor를 캡처함
    GetWorld()->GetTimerManager().SetTimer(
        SlowTimerHandle,
        [Actor]() // Actor 포인터를 람다 내부로 전달
        {
            if (Actor) // 안전을 위해 유효성 검사
            {
                Actor->SetPlayerNormal();
            }
        },
        5.f,
        false
    );
}


// 3.매개변수를 멤버 변수로 저장해서 사용
// 헤더 파일 (.h)에 추가
TWeakObjectPtr<AMyCharacter> SlowedPlayer; // weak_ptr 활용

// 소스 파일 (.cpp)
void AMySlowingItem::StartSlowing(AMyCharacter* Actor)
{
    SlowedPlayer = Actor; // 멤버 변수에 저장
    Actor->SetPlayerSlow(0.5f);

    GetWorld()->GetTimerManager().SetTimer(
        SlowTimerHandle,
        this,
        &AMySlowingItem::StopSlowing, // 인자 없는 함수로 호출
        5.f,
        false
    );
}

void AMySlowingItem::StopSlowing() // 인자를 없앰
{
    if (SlowedPlayer.IsValid()) // weak_ptr이 살아있는지 확인
    {
        SlowedPlayer->SetPlayerNormal();
    }
}
```

3번째 수정본에서 약한 참조를 사용한 이유는 아이템 효과가 지속되는 5초 동안 플레이어가 게임을 나가거나, 다른 이유로 캐릭터 객체가 파괴될 수도 있기 때문이다.   
5초동안 그냥 지켜보는 느낌   

<br/>

**<아이템이 사라지면 디버프 효과가 사라지지 않는 현상>**   

**1. 발생한 현상**   
아이템을 먹으면 아이템이 사라지는데 이때 아이템이 준 디버프 효과가 계속 지속됨   

**2. 원인**   
느려지는 아이템을 먹고 Destroy()를 해주면 아이템 클래스에 있는 Timer()가 사라져버린다.   

**3. 해결방법**   
Character 클래스 내에서 느려지는 효과를 구현하고 아이템은 그 명령만 내려주게 바꾸면 된다.   

```cpp
// 타이머를 Character의 메서드에 넣어준다. 
void AMyCharacter::SetPlayerSlow(float Amount)
{
	NormalSpeed *= Amount;
	WalkSpeed = NormalSpeed * 0.5f;
	SprintSpeed = NormalSpeed * 2.0f;
	GetCharacterMovement()->MaxWalkSpeed = NormalSpeed;
	GetCharacterMovement()->GravityScale /= Amount;

	GetWorld()->GetTimerManager().SetTimer(
		SlowTimerHandle,
		this,
		&AMyCharacter::SetPlayerNormal,
		5.f,
		false
	);
}

void AMyCharacter::SetPlayerNormal()
{
	NormalSpeed = 600.f;
	WalkSpeed = NormalSpeed * 0.5f;
	SprintSpeed = NormalSpeed * 2.0f;
	GetCharacterMovement()->MaxWalkSpeed = NormalSpeed;
	GetCharacterMovement()->GravityScale = 1.5f;
}

// 아이템에선 불러오기만 하면 된다.
void AMySlowingItem::ActivateItem(AActor* Activator)
{
	if (Activator && Activator->ActorHasTag("Player"))
	{
		if (AMyCharacter* PlayerCharacter = Cast<AMyCharacter>(Activator))
		{
			PlayerCharacter->SetPlayerSlow(SlowingAmount);
		}
	}
	DestroyItem();
}
```

<br/>

**<블러처리 하는 방법>**  

WBP에 background blur라는 속성이 있다.   
이걸 기존 HUD에 넣거나 따로 만들어서 레이어를 쌓아주면 된다.   

```cpp
// Blur 세팅값 변경하는 방법
// 헤더파일 필요
#include "Components/BackgroundBlur.h"

// 블러 강도를 변경하는 함수
void AMyPlayerController::SetBlurAmount(float Intensity)
{
	if (BlurWidgetInstance)
	{
		UBackgroundBlur* BlurComp = Cast<UBackgroundBlur>(BlurWidgetInstance->GetWidgetFromName(TEXT("Blur")));
		if (BlurComp)
		{
			BlurComp->SetBlurStrength(Intensity);
		}
	}
}

void AMyPlayerController::BlurOn()
{
	SetBlurAmount(10.0f);
	GetWorld()->GetTimerManager().SetTimer(
		BlurTimerHandle,
		[this]()
		{
			this->SetBlurAmount(0.0f);
		},
		3.0f,
		false
	);
}

// BlindItem.cpp
#include "MyBlindItem.h"
#include "MyPlayerController.h"
#include "Kismet/GameplayStatics.h" // Controller를 가져오기 위해서

void AMyBlindItem::ActivateItem(AActor* Activator)
{
	if (APlayerController* PC = UGameplayStatics::GetPlayerController(GetWorld(), 0))
	{
		if (AMyPlayerController* PlayerController = Cast<AMyPlayerController>(PC))
		{
			PlayerController->BlurOn();
			DestroyItem();
		}
	}
}
```

<br/>

**<UPROPERTY(meta = (BindWidget))>**   

이 키워드를 사용해서 실제 WBP내의 컴포넌트 이름 자체를 C++ Class에서 변수로 사용할 수 있다.(GetWidgetFromName 사용 안해도 됨)   
하지만 WBP에 들어가서 UUserWidget을 상속받은 클래스로 세팅을 해줘야한다.   
현재 프로젝트는 PlayerController에서 UI를 세팅하고 있어서 불가능하다.   

```cpp
UPROPERTY(meta = (BindWidget))
UBackgroundBlur* Blur;
```

  </p>
</details>

#### <!-- 26.04.29 -->
<details> 
  <summary>26.04.29</summary>
  <p>

**<코드카타 90번>**

각 a, b, c ,d 개의 가능한 모든 조합의 경우의 수는 (a + 1) * (b + 1) * (c + 1) * (d + 1) - 1이다.   
마지막 -1은 모두 0개일 경우의 수를 빼주는것   

```cpp
#include <string>
#include <vector>
#include <unordered_map>

using namespace std;

int solution(vector<vector<string>> clothes) {
    int answer = 1;
    unordered_map<string, int> clothes_num;
    
    for(const vector<string>& str : clothes)
    {
        clothes_num[str[1]]++;
    }
    
    for(const auto& c : clothes_num)
    {
        answer = answer * (c.second + 1);
    }
    return answer - 1;
}
```

**<맵이 바뀔때 GetWorld()에서 크래쉬가 나느 현상>**   

tick을 쓰면 더 간단한데 이상하게 적용이 안돼서 BeginPlay로 구현했는데 레벨이 바뀌고 월드가 바뀌는순간 nullptr 역참조로 오류가 난다.   

```cpp
// 억지 BeginPlay() 구현
void AMyCoinItem::BeginPlay()
{
	Super::BeginPlay();

	GetWorldTimerManager().SetTimer(
		CoinRotateTimerHandle,
		[this]()
		{
			UWorld* World = GetWorld();
			if (World && IsValid(this))
			{
				SetActorRotation(FRotator(0.f, 70.f * GetWorld()->GetTimeSeconds(), 0.f));
			}
		},
		0.01f,
		true
	);
}

// 근데 다시 해보니 Tick()이 잘 된다. 뻘짓했다...
void AMyCoinItem::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

	AddActorLocalRotation(FRotator(0.f, 70.f * DeltaTime, 0.f));
}
```


**<웨이브가 바뀔때 스폰된 액터가 누적되는 현상>**   

레벨은 OpenLevel()로 깔끔하게 밀어줘서 문제가 안생기는데 웨이브는 계속 누적된다.   

배열을 새로 만들어서 거기에 스폰된 액터들을 집어넣었다가 웨이브가 끝나면 없애주면 된다.   

```cpp
// 헤더파일
UPROPERTY()
TArray<AActor*> SpawnedItems;

// 웨이브가 시작되고 스폰될때
AActor* SpawnedActor = SpawnVolume->SpawnRandomItem();
if (SpawnedActor)
{
    SpawnedItems.Add(SpawnedActor); // 리스트에 추가
}

// 웨이브가 끝날때
for (AActor* Item : SpawnedItems)
    {
        if (Item && Item->IsValidLowLevel())
        {
            Item->Destroy();
        }
    }
    SpawnedItems.Empty();
```

  </p>
</details>

#### <!-- 26.04.30 -->
<details> 
  <summary>26.04.30</summary>
  <p>

**<전위/후위 증가 연산자>**   

전위 증가   
값 증가 -> 증가된 값 반환   
자기 자신의 참조(Reference)를 반환하므로 불필요한 객체 복사가 발생하지 않습니다.   

후위 증가   
기존 값의 복사본 생성 -> 값 증가 -> 복사본 반환   
이전 값을 임시 객체로 보관해야 하므로 메모리 복사 비용이 발생합니다.   

```cpp
// 전위 증가 연산자 (++it)
Iterator& operator++() {
    this->ptr += 1; // 1. 값을 먼저 증가시키고
    return *this;   // 2. 자기 자신의 참조를 반환합니다.
}

// 후위 증가 연산자 (it++)
Iterator operator++(int) {
    Iterator temp = *this; // 1. 현재 상태의 복사본을 만들고
    this->ptr += 1;        // 2. 값을 증가시킨 뒤,
    return temp;           // 3. 복사본(이전 상태)을 반환합니다.
}
```

<br/>


**<총기 반동 카메라 연출하기>**   

먼저 블루프린트 클래스를 하나 만들어서 카메라 흔들림 정도를 설정한 후 이걸 C++에 가서 연결만 해주면 된다.   

<br/>

1.CameraShakeBase 클래스를 상속받은 BP를 하나 만들어준다.   
2.Camera Shake Pattern 칸에 들어가서 Wave Oscillator Camera Shake Pattern을 클릭 후 하위 메뉴로 들어간다.   
3.Location, Rotation 등 흔들림을 주고싶은 곳으로 가서 값을 적절히 설정해준다.   
4.Duration으로 가서 시간을 설정해준다.   

설정 값 설명   
1.Amplitude: 진폭, 흔들리는 크기   
2.Frequency: 주파수, 흔들리는 속도   
3.Duration: 흔들리는 시간   
4.Blend In Time: 흔들림이 부드럽게 시작되는 시간   
5.Blend Out Time: 흔들림이 부드럽게 끝나는 시간   

이렇게 설정 후 C++ 코드를 작성해주면 끗.   

<br/>

```cpp
// 1. Build.cs에 추가해주기
// UMG 추가하던 것 처럼 추가해준다.
PublicDependencyModuleNames.AddRange(new string[] { 
    "Core", 
    "CoreUObject", 
    "Engine", 
    "InputCore", 
    "EnhancedInput", 
    "GameplayCameras" // 모듈 추가
});

// 2. 헤더파일
class UCameraShakeBase;
// 총기 반동을 위한 클래스 타입
UPROPERTY(EditDefaultsOnly, Category = "Combat")
TSubclassOf<UCameraShakeBase> FireShakeClass;

// 3. C++ 파일
// 컨트롤러 -> 카메라 매니저 -> BP 클래스 실행
if (GetWorld())
{
	APlayerController* PC = Cast<APlayerController>(GetController());
	if (PC && PC->PlayerCameraManager && FireShakeClass)
	{
		PC->PlayerCameraManager->StartCameraShake(FireShakeClass);
	}
}
```
  </p>
</details>

#### <!-- 26.05.01 -->
<details> 
  <summary>26.05.01</summary>
  <p>

**<코드카타 92번>**   

별 생각없이 코드를 짰는데 시간초과가 떴다.(솔직히 실행 직전에 뜰 줄 알긴했음)   

```cpp
// 매우 비효율적인 코드
// 모든 루프를 다 돌아야함
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<int> priorities, int location) {

    int answer = 0;
    vector<int> temp_vec;
    priority_queue<int> priority_process;

    for(const int& i : priorities)
    {
        priority_process.push(i);
    }

    while(!priority_process.empty())
    {
        for(int i = 0; i < priorities.size(); ++i)
        {
            if(priorities[i] == priority_process.top())
            {
                priority_process.pop();
                temp_vec.push_back(i);
            }
        }
    }
    
    for(int i = 0; i < temp_vec.size(); ++i)
    {
        if(location == temp_vec[i])
        {
            answer = i + 1;
        }
    }
    return answer;
}
```

<br/>

`queue`를 사용하면서 인덱스 값도 확인을 해야하는 상황인데 `pair<>`의 존재가 이때 생각났다.   
싹 지우고 다시 구현했다.   

```cpp
// 수정 후 코드
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<int> priorities, int location) {
    int answer = 0;
    queue<pair<int, int>> que;
    priority_queue<int> pri_que;

    for (int i = 0; i < priorities.size(); ++i) {
        que.push({i, priorities[i]});
        pri_que.push(priorities[i]);
    }
    
    while(!pri_que.empty())
    {
        if(que.front().second < pri_que.top())
        {
            que.push(que.front());
            que.pop();
        }
        else if(que.front().second == pri_que.top())
        {
            ++answer;
            if(que.front().first == location)
            {
                return answer;
            }
            que.pop();
            pri_que.pop();
        }
    }
    return answer;
}
```

**<팀프로젝트 준비하기>**   

내가 맡은 곳은 몬스터 AI, 보스 몬스터   

AI관련이랑 Behavior Tree 공부   

  </p>
</details>

#### <!-- 26.05.02 -->
<details> 
  <summary>26.05.02</summary>
  <p>

**<NavMeshBoundsVolume 사용하기>**   

ACharacter로 만든 액터가 이동할 수 있는 범위를 자동으로 만들어준다.   
P를 눌러보면 녹색으로 범위가 나타난다.   

<br/>

**<Behavior Tree와 Black Board>**   

`Behavior Tree`는 기본적으로 위에서 아래, 왼쪽에서 오른쪽으로 순서가 매겨진다.   

`Selector`에서 행동을 선택할 수 있다.   

`Sequence`에서 순서를 정한다(왼쪽 -> 오른쪽 순)   

`Task`는 기본으로 정해주는 것을 쓸 수도 있고 위쪽에 `NewTask`를 입력해서 새로운 Task를 만들어줄 수 있다.   

<br/>

**<Task 만들기>**   

`BTTask_taskname`에 들어오면 EventGraph가 있는데 왼쪽 Functions의 Override를 눌러서 나오는 기본 메서드를 사용할 수 있다.   

기본 메서드중 `Execute AI`는 `BeginPlay`와 같은 역할을 하고 `Finish Execute`로 끝맺음을 해야한다.    

<br/>

**<언리얼에서 권장하는 BT사용방식>**   

BT/BB: 에디터에서 사용(시각적 이점이 매우 높음)   
BTTask/BTService/BTDecorator: 이 노드들은 복잡한 로직을 다룰 수 있게 C++ 클래스로 상속받아 작성   

커스텀 AIController: C++ 클래스로 부모를 만들고 블루프린트로 상속하는 방식   

<br/>

**<GetRandomReachablePointInRadius 사용하기>**   

`GetRandomReachablePointInRadius`는 특정 위치에서 정해준 범위 내의 랜덤한 포인트를 반환한다.   

먼저 `"NavigationSystem"`을 Build.cs 파일에 추가해준다.   
`#include "NavigationSystem.h"`은 C++ 파일에 추가해준다.   
`UNavigationSystemV1` 클래스의 멤버함수인 `GetRandomReachablePointInRadius`를 호출해서 사용하면 된다.   
GetRandomReachablePointInRadius(현재위치, 반경, 다음위치)   

```cpp
// BTTask 코드

// .h 파일
#pragma once

#include "CoreMinimal.h"
#include "BehaviorTree/BTTaskNode.h"
#include "BTTask_ZombieRoam.generated.h"

UCLASS()
class MONSTER_AI_PROJECT_API UBTTask_ZombieRoam : public UBTTaskNode
{
	GENERATED_BODY()
	
public:
	UBTTask_ZombieRoam();

	// 태스크가 실행될 때 호출되는 핵심 함수
	virtual EBTNodeResult::Type ExecuteTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory) override;

protected:
	// 노드 이름을 에디터에서 식별하기 좋게 설정
	virtual FString GetStaticDescription() const override;

	// 에디터에서 조절 가능한 탐색 범위 변수
	UPROPERTY(EditAnywhere, Category = "AI")
	float SearchRadius = 1000.0f;
};

// .cpp 파일
#include "BTTask_ZombieRoam.h"
#include "Zombie.h"
#include "ZombieAIController.h"
#include "NavigationSystem.h"
#include "Blueprint//AIBlueprintHelperLibrary.h"

UBTTask_ZombieRoam::UBTTask_ZombieRoam()
{
	NodeName = TEXT("Zombie Roam"); // BT 에디터에 표시될 이름
}

EBTNodeResult::Type UBTTask_ZombieRoam::ExecuteTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory)
{
	AZombieAIController* ZombieAIController = Cast<AZombieAIController>(OwnerComp.GetAIOwner());
	if (!ZombieAIController) return EBTNodeResult::Failed;

	AZombie* Zombie = Cast<AZombie>(ZombieAIController->GetPawn());
	if (!Zombie) return EBTNodeResult::Failed;

	// 1. 좀비의 현재 위치
	FVector Origin = Zombie->GetActorLocation();

	// 2. 내비게이션 시스템 가져오기
	UNavigationSystemV1* NavSystem = UNavigationSystemV1::GetCurrent(GetWorld());

	// 3. 반경 내 랜덤 위치 찾기
	FNavLocation NextLocation;
	if (NavSystem->GetRandomReachablePointInRadius(Origin, SearchRadius, NextLocation))
	{
		// 4. 찾은 위치로 이동 명령 (AI Move To)
		ZombieAIController->MoveToLocation(NextLocation.Location);

		// 5. 성공 반환
		return EBTNodeResult::Succeeded;
	}
	
	return EBTNodeResult::Failed;
}

FString UBTTask_ZombieRoam::GetStaticDescription() const
{
	return TEXT("Zombie performs roam");
}
```

**<위 코드에서의 문제점>**   

에디터의 BT에 위의 Task 옆에 `Wait`를 걸어놨다. 근데 문제는 Task를 실행하는 순간 바로 `Succeeded`를 반환하기 때문에 이동이 끝나고 `Wait`를 하는게 아니라 이동하는 순간 `Wait`가 시작된다.(이동하다 멈추지는 않고 `Wait`의 시간이 이동하는 순간부터 줄어든다.)   
그래서 실제 이동이 다 끝나고 나면 `Succeeded`가 반환되게 만들어야한다.   

```cpp
// 수정 후 코드
// 많이 복잡하다...
// Build.cs에 "AIModule" 추가!

// .h 파일
#pragma once

#include "CoreMinimal.h"
#include "BehaviorTree/BTTaskNode.h"
#include "BTTask_ZombieRoam.generated.h"

UCLASS()
class MONSTER_AI_PROJECT_API UBTTask_ZombieRoam : public UBTTaskNode
{
	GENERATED_BODY()
	
public:
	UBTTask_ZombieRoam();

	// 태스크가 실행될 때 호출되는 핵심 함수
	virtual EBTNodeResult::Type ExecuteTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory) override;

protected:
	// 태스크 중단 시 처리
	virtual EBTNodeResult::Type AbortTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory) override;

	// 이동이 완료되었을 때 호출될 커스텀 함수
	void OnMoveCompleted(struct FAIRequestID RequestID, const struct FPathFollowingResult& Result);

	// 노드 이름을 에디터에서 식별하기 좋게 설정
	virtual FString GetStaticDescription() const override;

	// 에디터에서 조절 가능한 탐색 범위 변수
	UPROPERTY(EditAnywhere, Category = "AI")
	float SearchRadius = 1000.0f;

private:
	// 나중에 이벤트를 끄기 위해 저장해두는 컴포넌트 포인터
	UBehaviorTreeComponent* MyOwnerComp;
};


// .cpp 파일
#include "BTTask_ZombieRoam.h"
#include "Zombie.h"
#include "ZombieAIController.h"
#include "NavigationSystem.h"
#include "Navigation/PathFollowingComponent.h"
#include "Blueprint/AIBlueprintHelperLibrary.h"

UBTTask_ZombieRoam::UBTTask_ZombieRoam()
{
	NodeName = TEXT("Zombie Roam"); // BT 에디터에 표시될 이름
	// 이 태스크는 Tick이나 이벤트를 기다려야 하므로 latent(지연) 태스크임을 명시할 수 있음
	bNotifyTick = false;
	MyOwnerComp = nullptr;
}

EBTNodeResult::Type UBTTask_ZombieRoam::ExecuteTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory)
{
	AZombieAIController* ZombieAIController = Cast<AZombieAIController>(OwnerComp.GetAIOwner());
	if (!ZombieAIController) return EBTNodeResult::Failed;

	AZombie* Zombie = Cast<AZombie>(ZombieAIController->GetPawn());
	if (!Zombie) return EBTNodeResult::Failed;

	// 1. 좀비의 현재 위치
	FVector Origin = Zombie->GetActorLocation();

	// 2. 내비게이션 시스템 가져오기
	UNavigationSystemV1* NavSystem = UNavigationSystemV1::GetCurrent(GetWorld());
	if (!NavSystem) return EBTNodeResult::Failed;

	// 3. 반경 내 랜덤 위치 찾기
	FNavLocation NextLocation;
	if (NavSystem->GetRandomReachablePointInRadius(Origin, SearchRadius, NextLocation))
	{
		// 4. 이동 완료 이벤트를 수신하기 위해 델리게이트 연결
		UPathFollowingComponent* PFollowComp = ZombieAIController->GetPathFollowingComponent();
		if (PFollowComp)
		{
			MyOwnerComp = &OwnerComp;
			PFollowComp->OnRequestFinished.AddUObject(this, &UBTTask_ZombieRoam::OnMoveCompleted);
		}

		// 5. 찾은 위치로 이동 명령 (AI Move To)
		ZombieAIController->MoveToLocation(NextLocation.Location);

		// 6. 아직 끝나지 않았음을 반환
		return EBTNodeResult::InProgress;
	}
	
	return EBTNodeResult::Failed;
}

void UBTTask_ZombieRoam::OnMoveCompleted(FAIRequestID RequestID, const FPathFollowingResult& Result)
{
	if (MyOwnerComp)
	{
		// 4. 델리게이트 연결 해제 (중요: 메모리 누수 및 중복 실행 방지)
		AZombieAIController* ZombieAIController = Cast<AZombieAIController>(MyOwnerComp->GetAIOwner());
		if (ZombieAIController && ZombieAIController->GetPathFollowingComponent())
		{
			ZombieAIController->GetPathFollowingComponent()->OnRequestFinished.RemoveAll(this);
		}

		// 5. 비헤이비어 트리에 이 태스크가 성공적으로 끝났음을 알림
		FinishLatentTask(*MyOwnerComp, EBTNodeResult::Succeeded);
	}
}

EBTNodeResult::Type UBTTask_ZombieRoam::AbortTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory)
{
	// 태스크가 도중에 강제 중단될 경우 (예: 상위 우선순위 노드 실행) 이동을 멈춤
	AZombieAIController* ZombieAIController = Cast<AZombieAIController>(OwnerComp.GetAIOwner());
	if (ZombieAIController)
	{
		ZombieAIController->StopMovement();
		if (ZombieAIController->GetPathFollowingComponent())
		{
			ZombieAIController->GetPathFollowingComponent()->OnRequestFinished.RemoveAll(this);
		}
	}
	return Super::AbortTask(OwnerComp, NodeMemory);
}

FString UBTTask_ZombieRoam::GetStaticDescription() const
{
	return TEXT("Zombie performs roam");
}
```

<br/>

**<위 코드에서 나온 또 하나의 문제점>**   

액터를 여러개 배치했을때 시작하면 다같이 움직이지만 그 후로는 하나의 액터만 움직인다..!   

문제점을 찾아보니 세마리가 하나의 자원을 공유하다 보니 처음에는 동시에 움직였다가 그 후론 한놈만 해당 자원을 활용해서 움직이는거였다.   

바로 `MyOwnerComp` 요놈을 다른 객체들도 똑같이 사용하고 있었던것.   
`MyOwnerComp`를 담을 변수나 구조체를 생성하고 거기로 관리를 해줘야한다.   

```cpp
// .h 파일
#pragma once

#include "CoreMinimal.h"
#include "BehaviorTree/BTTaskNode.h"
#include "Navigation/PathFollowingComponent.h"
#include "BTTask_ZombieRoam.generated.h"

// Task 실행 시 각 인스턴스마다 별도로 저장할 데이터 구조체
struct FZombieRoamTaskMemory
{
	// 약한 참조를 사용하여 메모리 안전성을 높입니다.
	TWeakObjectPtr<UBehaviorTreeComponent> OwnerComp;
};

UCLASS()
class MONSTER_AI_PROJECT_API UBTTask_ZombieRoam : public UBTTaskNode
{
	GENERATED_BODY()

public:
	UBTTask_ZombieRoam();

	// 태스크가 실행될 때 호출되는 핵심 함수
	virtual EBTNodeResult::Type ExecuteTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory) override;

protected:
	// 태스크 중단 시 처리
	virtual EBTNodeResult::Type AbortTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory) override;

	// 인스턴스별 메모리 크기를 반환하여 엔진이 할당하게 함
	virtual uint16 GetInstanceMemorySize() const override { return sizeof(FZombieRoamTaskMemory); }

	// 이동 완료 콜백
	void OnMoveCompleted(struct FAIRequestID RequestID, const struct FPathFollowingResult& Result, UBehaviorTreeComponent* OwnerComp);

	// 노드 이름을 에디터에서 식별하기 좋게 설정
	virtual FString GetStaticDescription() const override;

	// 에디터에서 조절 가능한 탐색 범위 변수
	UPROPERTY(EditAnywhere, Category = "AI")
	float SearchRadius = 1000.0f;

	// 주의: 클래스 멤버 변수(예: MyOwnerComp)를 상태 저장용으로 사용하지 않습니다.
};

// .cpp 파일
#include "BTTask_ZombieRoam.h"
#include "Zombie.h"
#include "ZombieAIController.h"
#include "NavigationSystem.h"
#include "Navigation/PathFollowingComponent.h"
#include "Blueprint/AIBlueprintHelperLibrary.h"

UBTTask_ZombieRoam::UBTTask_ZombieRoam()
{
	NodeName = TEXT("Zombie Roam");
	bNotifyTick = false;
	// 멤버 변수인 MyOwnerComp를 초기화하던 로직을 제거합니다.
}

EBTNodeResult::Type UBTTask_ZombieRoam::ExecuteTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory)
{
	AZombieAIController* ZombieAIController = Cast<AZombieAIController>(OwnerComp.GetAIOwner());
	if (!ZombieAIController) return EBTNodeResult::Failed;

	AZombie* Zombie = Cast<AZombie>(ZombieAIController->GetPawn());
	if (!Zombie) return EBTNodeResult::Failed;

	UNavigationSystemV1* NavSystem = UNavigationSystemV1::GetCurrent(GetWorld());
	if (!NavSystem) return EBTNodeResult::Failed;

	// 1. 노드 전용 메모리에 현재 OwnerComp 저장 (구조체 활용)
	FZombieRoamTaskMemory* MyMemory = reinterpret_cast<FZombieRoamTaskMemory*>(NodeMemory);
	MyMemory->OwnerComp = &OwnerComp;

	FVector Origin = Zombie->GetActorLocation();
	FNavLocation NextLocation;

	if (NavSystem->GetRandomReachablePointInRadius(Origin, SearchRadius, NextLocation))
	{
		UPathFollowingComponent* PFollowComp = ZombieAIController->GetPathFollowingComponent();
		if (PFollowComp)
		{
			// 2. 델리게이트에 람다를 사용하여 현재 실행 중인 OwnerComp를 안전하게 전달
			// 캡처 리스트에 &OwnerComp를 사용하지 않고 포인터로 전달하여 안전성을 높임
			UBehaviorTreeComponent* OwnerCompPtr = &OwnerComp;
			PFollowComp->OnRequestFinished.AddLambda([this, OwnerCompPtr](FAIRequestID ReqID, const FPathFollowingResult& Res)
				{
					this->OnMoveCompleted(ReqID, Res, OwnerCompPtr);
				});
		}

		ZombieAIController->MoveToLocation(NextLocation.Location);
		return EBTNodeResult::InProgress;
	}

	return EBTNodeResult::Failed;
}

void UBTTask_ZombieRoam::OnMoveCompleted(FAIRequestID RequestID, const FPathFollowingResult& Result, UBehaviorTreeComponent* OwnerComp)
{
	if (OwnerComp)
	{
		AZombieAIController* ZombieAIController = Cast<AZombieAIController>(OwnerComp->GetAIOwner());
		if (ZombieAIController && ZombieAIController->GetPathFollowingComponent())
		{
			// 작업 완료 후 해당 인스턴스의 델리게이트 제거
			ZombieAIController->GetPathFollowingComponent()->OnRequestFinished.RemoveAll(this);
		}

		// 해당 OwnerComp에 대해 성공 보고
		FinishLatentTask(*OwnerComp, EBTNodeResult::Succeeded);
	}
}

EBTNodeResult::Type UBTTask_ZombieRoam::AbortTask(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory)
{
	AZombieAIController* ZombieAIController = Cast<AZombieAIController>(OwnerComp.GetAIOwner());
	if (ZombieAIController)
	{
		ZombieAIController->StopMovement();
		if (ZombieAIController->GetPathFollowingComponent())
		{
			ZombieAIController->GetPathFollowingComponent()->OnRequestFinished.RemoveAll(this);
		}
	}
	return Super::AbortTask(OwnerComp, NodeMemory);
}

FString UBTTask_ZombieRoam::GetStaticDescription() const
{
	return FString::Printf(TEXT("Zombie performs roam within %.1f radius (Multi-AI Safe)"), SearchRadius);
}
```

<br/>

**1.AbortTask()**   

위에서 `EBTNodeResult::Type UBTTask_ZombieRoam::AbortTask` 함수는 분명 `EBTNodeResult::Type`을 반환하는데 왜 부모 함수를 불러서 리턴하는지 궁금했다.   

 `AbortTask`함수를 호출하면 부모인 `UBTTaskNode`는 내부 상태를 변경하는 시스템적인 처리를 수행한다고 한다.   
즉, 그냥 함수를 실행만 하는게 아니라 엔진이 기대하는 최종 상태 값을 반환하기 때문에 이를 관리하는 부모 함수를 호출해서 결과값을 리턴해준다고 한다.   

**2.메모리 리턴 함수**   

```cpp
virtual uint16 GetInstanceMemorySize() const override { return sizeof(FZombieRoamTaskMemory); }
```
이 함수는 호출을 하지않아서 어떤 구조로 작동하는지 궁금해서 찾아봤다.   

`Behavior Tree 시스템`이 작동할때 알아서 호출을 한다고 한다. 그리고 여기서 받아낸 메모리 값이 바로 `ExecuteTask()`나 `AbortTask()`의 매개변수에 있는 `NodeMemory` 값이라고 한다.   

**3.OwnerComp를 TArray로 쓰면 안될까?**   

사실상 엔진 자체가 메모리를 활용한 구조체 방식을 강제한다고 한다.   
배열을 쓰면 이동 로직이 끝날 때 마다 인덱스 값을 찾아야하고 좀비를 Destroy할 때도 일일이 지워줘야 해서 매우 비효율적이다.   

구조체가 확장성도 훨씬 좋고 `NodeMemory`와 연동하고 `TWeakObjectPtr`를 사용하기 때문에 안전한 메모리 관리와 즉각적인 접근이 가능하다.   

**4.현재 구현 방식의 문제점**   

쭉 수정해온 코드들은 매번 델리게이트 바인딩과 해제를 해야하는데 수많은 좀비가 생기면 성능 저하가 온다.   

따라서, 초반에 구현했던 단순한 이동만 코드로 구현을 하고(단순 Succeeded 반환) 그 이후의 상태 체크는 `Service`/`Decorator`가 하도록 해야한다.    
-> `Decorator` 조건문의 역할   
-> `Service` Tick함수의 역할   
위 코드에서 `Decorator`로 좀비가 목표 지점에 도착했는지를 확인하고 추가로 플레이어를 추적한다고 하면 `Service`로 플레이어와의 거리를 설정한 주기마다 체크하는 식으로 사용.   


  </p>
</details>

#### <!-- 26.05.03 -->
<details> 
  <summary>26.05.03</summary>
  <p>

**<Mixamo에서 받은 애니메이션을 UE5로 옮기는 방법>**    

온 갖 뻘짓(컨버터 써보기, 스켈레탈 직접 수정 등등)을 해봤는데 다 실패하다가 3분짜리 영상에서 드디어 방법을 찾았음.   

Import를 하고나서 Retarget Animations를 누르고 언리얼 엔진의 뼈대로 자동으로 바꾸는 기능을 사용하면 너무 편리함.   

<br/>

**<좀비 AI가 먹통>**   

프로젝트 새로 만들고 계속 비교해봤는데 아무리 찾아봐도 틀린점이 없었는데 알고보니 커스텀 `AIController`의 `OnPossess` 함수에서 부모를 안불러와서 그랬음(Super::)   
이거때매 3시간 날림   

<br/>

**<좀비의 yaw 회전이 너무 부자연스러운 현상>**   

좀비가 플레이어를 추적하다 보니 수시로 움직이는데 엄청 부자연스러움   

+좀비끼리 너무 부비부비 해댐   
  
이걸 다 해결해준 코드가 있음   
```cpp
UCharacterMovementComponent* MoveComp = GetCharacterMovement();
if (MoveComp)
{
	MoveComp->MaxWalkSpeed = 50.f;

	// 회전 속도 (Yaw) 조절 - 뚝뚝 끊기는 현상 방지
	MoveComp->RotationRate = FRotator(0.0f, 180.0f, 0.0f); // 수치가 낮을수록 회전이 부드러워짐

	// 이동 방향으로 자동 회전 설정
	MoveComp->bOrientRotationToMovement = true;

	// 컨트롤러 회전 사용 안 함 (캐릭터가 휙 돌아가는 것 방지)
	bUseControllerRotationYaw = false;

	// 군중 회피(RVO Avoidance) 활성화 - 좀비끼리 겹치는 현상 방지
	MoveComp->bUseRVOAvoidance = true;
	// 1.0은 이동에만 신경쓰고
	// 0.0은 회피에만 신경쓰고
	// 0.5은 딱 밸런스
	// 좀비끼리 잘 엉켜서 0.3으로 세팅
	MoveComp->AvoidanceWeight = 0.3f;
}
```

<br/>

**<좀비 애니메이션 끊기는 문제>**   

mixamo에서 받을 때 InPlace를 체크하지 않아서 생긴 문제였음.   

<br/>

**<AI Perception(감지) 설정>**   

내 좀비 블루프린트 클래스에는 AI Perception이 없어서 추가를 해줬다.   

```cpp
// .h
// AIPerception 컴포넌트 선언
UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "AI")
class UAIPerceptionComponent* PerceptionComp;

// .cpp
PerceptionComp = CreateDefaultSubobject<UAIPerceptionComponent>(TEXT("PerceptionComponent"));
```

여기서 Senses Config 항목으로 시야 상실 후 유지시간을 설정할 수 있다.   
근데 현재 프로젝트와는 맞지 않아서 이런 기능이 있다는거만 체크하고 넘어감.   

  </p>
</details>

#### <!-- 26.05.04 -->
<details> 
  <summary>26.05.04</summary>
  <p>

**<코드카타 93번>**   

완전 탐색 문제인데 처음 접해봐서 접근 방법을 찾아봤다.   
순열을 이용한 완전 탐색과 DPS와 백트래킹을 이용한 방법이 있었다.   

<algorithm>에 포함된 `next_permutation`이라는 함수가 있는데 얘가 순열을 알아서 뽑아내준다.(단, 컨테이너가 오름차순 정렬이 되어있어야함)   

조합을 뽑을 때는 `prev_permutation`을 사용하면 된다.   
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int k, vector<vector<int>> dungeons) {
    int max_dungeons = 0;
    
    // 순열을 사용하기 위해 인덱스 배열 생성 (0, 1, 2, ... N-1)
    vector<int> indices(dungeons.size());
    for (int i = 0; i < dungeons.size(); i++) {
        indices[i] = i;
    }
    
    // 가능한 모든 순서에 대해 반복
    // (std::next_permutation은 오름차순 정렬된 배열에서 시작해야 모든 순열을 탐색합니다.)
    sort(indices.begin(), indices.end());
    
    do {
        int current_k = k;
        int cnt = 0;
        
        for (int i = 0; i < indices.size(); i++) {
            int idx = indices[i];
            // 최소 필요 피로도 확인
            if (current_k >= dungeons[idx][0]) {
                current_k -= dungeons[idx][1]; // 소모 피로도 차감
                cnt++;
            } else {
                break; // 피로도가 부족하면 탐험 중단
            }
        }
        
        // 최대 방문 던전 수 갱신
        max_dungeons = max(max_dungeons, cnt);
        
    } while (next_permutation(indices.begin(), indices.end()));
    
    return max_dungeons;
}
```

<br/>

**DFS를 사용한 풀이**   
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int max_d = 0;
vector<bool> visited;

void dfs(int k, int cnt, const vector<vector<int>>& dungeons) {
    max_d = max(max_d, cnt);
    
    for (int i = 0; i < dungeons.size(); i++) {
        // 방문하지 않았고, 최소 필요 피로도 조건을 만족할 때
        if (!visited[i] && k >= dungeons[i][0]) {
            visited[i] = true;
            dfs(k - dungeons[i][1], cnt + 1, dungeons);
            visited[i] = false; // 백트래킹 (원상복구)
        }
    }
}

int solution_dfs(int k, vector<vector<int>> dungeons) {
    max_d = 0;
    visited.assign(dungeons.size(), false);
    
    dfs(k, 0, dungeons);
    
    return max_d;
}
```

**<BlackBoard 변수 사용하기>**   

구하려는 값이 플레이어와 좀비의 거리라서 `AI Controller`의 Tick()함수에 추가를 해준다.   

```cpp
void AZombieAIController::Tick(float DeltaSeconds)
{
    Super::Tick(DeltaSeconds);

	ACharacter* PlayerCharacter = UGameplayStatics::GetPlayerCharacter(GetWorld(), 0);
	if (PlayerCharacter != nullptr)
	{
		FVector PlayerLocation = PlayerCharacter->GetActorLocation();

		// 좀비와 플레이어 사이의 거리 계산
		AZombie* CurrentZombie = Cast<AZombie>(GetPawn());
		if (CurrentZombie != nullptr)
		{
			float Distance = FVector::Dist(CurrentZombie->GetActorLocation(), PlayerLocation);

			// 블랙보드에 거리 값 저장
			Blackboard->SetValueAsFloat(TEXT("DistanceToPlayer"), Distance);
		}
	}
}
```

<br/>

**<애니메이션 몽타주가 실행이 안되는 현상>**   

좀비가 플레이어한테 왔을 때 계속 멍때리길래 뭔가 했더니 애니메이션을 실행하는 함수는 실행하자마자 종료를 해버려서(속도가 너무 빠름) 그런거였음.   
뒤에 `wait`를 달아주거나 `Attack Task`를 `InProgress` 상태로 유지하다가 실제 애니메이션이 끝나는 순간 `Succeeded`로 반환을 해줘야 한다.   

  </p>
</details>

#### <!-- 26.05.05 -->
<details> 
  <summary>26.05.05</summary>
  <p>

**<애니메이션이 끊겨 보이는 현상>**  

<s>이거때문에 미치겠네 어케 하는거지 blend 조절하고 다 해봤는데 안되네;</s>    

최대한 간단하게 ABP를 만들었는데 결국 세부적으로 다 나눠서 구현했다. 이러니까 아주 잘 된다...    

간편하게 Idle과 Walk를 BlendSpace로 만들어서 연결했었는데 앞으로는 직접 statmachine을 만들어서 세부적으로 나누는게 제일 좋을 것 같다.   

<br/>

**<Damage 파이프라인>**   

`TakeDamage`랑 `ApplyDamage`는 한쌍인데 서로 다른 곳에 들어가있다.   
`TakeDamage`는 `AActor`에 들어가있는 메서드고 `ApplyDamage`는 `GameplayStatics`에 들어가있다.   

<br/>

**<내적 사용해서 공격범위안에 적이 있는지 확인하기>**   

심화반 수업 도강한게 여기서 도움이 됐다.   

바로 내적, cos이 떠올랐다.   

```cpp
// 직접 짠 만족스러운 코드(나중에 보면 아니겠지?)
bool AZombieAIController::IsCanAttackSight()
{
	if (!PlayerCharacter || !Zombie)
	{
		return false;
	}
	// 좀비의 정면 단위 방향 벡터
	FVector ZombieFowardDirection = Zombie->GetActorForwardVector();
	ZombieFowardDirection.Z = 0.f;
	ZombieFowardDirection.Normalize();
	// 좀비 - 플레이어 단위 방향 벡터
	FVector ZombieLocation = Zombie->GetActorLocation();
	FVector PlayerLocation = PlayerCharacter->GetActorLocation();
	FVector ZombieToPlayerDirection = PlayerLocation - ZombieLocation;
	ZombieToPlayerDirection.Z = 0.f;
	ZombieToPlayerDirection.Normalize();

	float DotValue = FVector::DotProduct(ZombieFowardDirection, ZombieToPlayerDirection);
	// 위와 같은 기능
	// float DotValue = ZombieFowardDirection | ZombieToPlayerDirection; 
	
	return DotValue >= 0.866f;
}
```

<br/>

**<공격 애니메이션이 실행되는 동안 플레이어의 위치를 향해 회전하는 현상>**   

플레이어가 공격유무값을 저장할 부울 변수를 만들어서 공격하는 도중엔(true) 회전을 못하게 막고 공격 이후 공격유무값을 false로 지정하게 만들어줬다.   
Timer를 만들어서 해결했다.   

지연값은 몽타주 실행 시간(공격 애니메이션 실행 시간)동안으로 정해줬다.   
몽타주 실행 시간은 커스텀 Task에서 몽타주를 실행하는데 그 때 ZombieAIController에 새로 만든 MontageTime 변수에 저장을 따로 해주고 아래의 함수가 실행될 때 사용했다.   ㄹ
```cpp
bool AZombieAIController::IsCanAttackSight()
{
	if (!PlayerCharacter || !Zombie)
	{
		return false;
	}

	// 좀비의 정면 단위 방향 벡터
	FVector ZombieFowardDirection = Zombie->GetActorForwardVector();
	ZombieFowardDirection.Z = 0.f;
	ZombieFowardDirection.Normalize();
	// 좀비 - 플레이어 단위 방향 벡터
	FVector ZombieLocation = Zombie->GetActorLocation();
	FVector PlayerLocation = PlayerCharacter->GetActorLocation();
	FVector ZombieToPlayerDirection = PlayerLocation - ZombieLocation;
	ZombieToPlayerDirection.Z = 0.f;
	ZombieToPlayerDirection.Normalize();

	float DotValue = FVector::DotProduct(ZombieFowardDirection, ZombieToPlayerDirection);
	// 위와 같은 기능
	// float DotValue = ZombieFowardDirection | ZombieToPlayerDirection; 
	
	// 시야안에 들어왔으면 공격중으로 상태를 바꾸고(bIsAttaking) 애니메이션 재생 시간 뒤에 공격이 끝났다고 바꿔줌
	if (DotValue >= 0.999f)
	{
		bIsAttaking = true;
		UE_LOG(LogTemp, Warning, TEXT("%f"), MontageTime);
		GetWorldTimerManager().SetTimer(
			AttackTimer,
			[this]() 
			{
				bIsAttaking = false;
			},	
			MontageTime,
			false
			);
		return true;
	}
	return false;
}
```

  </p>
</details>

#### <!-- 26.05.06 -->
<details> 
  <summary>26.05.06</summary>
  <p>

**<코드카타 94번>**   

깊이 우선 탐색을 사용하는 문제다.   
재귀함수를 사용하는데 +, - 두가지 선택지가 있어서 다음단계로 넘어가는 재귀함수가 2개.   
깊이(배열의 인덱스)가 배열의 길이와 같으면 탐색이 끝난다.(탈출 조건 달성)   
-> 깊이가 n일 때 n - 1 인덱스의 배열 값을 합계에 더해주기 때문에 깊이가 1 더 크다.   

```cpp
#include <string>
#include <vector>

using namespace std;

void DFS(int Depth, int Sum, const vector<int>& numbers, const int& target, int& answer)
{
    if(Depth == numbers.size())
    {
        if(Sum == target)
        {
            ++answer;     
        }
        return;
    }
    DFS(Depth + 1, Sum + numbers[Depth], numbers, target, answer);
    DFS(Depth + 1, Sum - numbers[Depth], numbers, target, answer);
}

int solution(vector<int> numbers, int target) {
    int answer = 0;
    
    DFS(0, 0, numbers, target, answer);
    
    return answer;
}
```

<br/>

**<블루프린트 AI Move To 사용했을때 문제점>**   

플레이어가 대각선으로 좀비에게 접근하면 좀비가 플레이어를 놓치고(정확히는 내적값은 true 처리가 되고 거리값은 false가 되는 기이한 현상) 약 2~ 3초 멍때리다가 다시 Chase 하는 문제가 생겼다.   
BT도 수정하고 이것저것 건드려봤지만 해결되지 않아서 결국 해당 Task를 C++코드로 만들어서 간단하게 `MoveToActor`를 사용했는데 이 현상이 해결됐다. 분명 같은 원리긴한데 내부 지연의 차이가 조금 있다던데 앞으로 그냥 C++로 써야겠다.   

<br/>

**<MoveToActor를 사용했을때 Radius 계산>**   

AIMoveTo를 사용했을땐 범위를 150으로 설정하면 정확히 Distance가 150이 됐을 때 동작을 했는데 C++에서는 조금 달랐다.   
좀비의 캡슐 컴포넌트의 반지름 값과 플레이어의 반지름 값도 생각을 해야한다.   
예를 들어 Radius를 150으로 설정했다면 실제로 둘 사이의 값 150에 두명의 반지름 값을 더한 70정도가 더해져서 220정도의 거리에서 Chase를 멈추지만 멈추지않는(?) 이상한 현상이 발생했다.   
아마 Velocity는 살아있어서 움직이는 애니메이션은 계속 실행되지만 더이상 플레이어한테 다가가지 못해서 가만히 러닝머신을 타는 현상이 나타난듯하다.   

그래서 `AcceptanceRadius = 70.f`정도로 해주니 공격 범위의 150에 근접해서 애니메이션이 아주 자연스럽게 잘 나오게 됐다.   

  </p>
</details>

#### <!-- 26.05.07 -->
<details> 
  <summary>26.05.07</summary>
  <p>

**<코드카타 95번>**   

`reverse(str.begin(), str.end())`를 생각하지 못했다. 스택으로 넣고 다시 문자열로 넣으려고 했는데 `reverse`를 쓴 방식이 간결하다.   


```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <cmath>

using namespace std;

bool bIsPrime(long long n)
{
    if (n < 2) 
    {
        return false;
    }
    for (long long i = 2; i <= sqrt(n); i++) 
    {
        if (n % i == 0)
        {
            return false;
        }
    }
    return true;
}

int solution(int n, int k) {
    int answer = 0;
    string str = "";
    string sum = "";
    
    while(n > 0)
    {
        str += to_string(n % k);
        n /= k;
    }
    reverse(str.begin(), str.end());
    
    for(char c : str)
    {
        if(c == '0')
        {
            if(!sum.empty() && bIsPrime(stoll(sum)))
            {
                ++answer;
            }
            sum = "";
        }
        else
        {
            sum += c;
        }
    }
    
    if(!sum.empty() && bIsPrime(stoll(sum)))
    {
        ++answer;
    }
    
    return answer;
}
```

<br/>

**<원형으로 탄 퍼지게 하는 법>**   

저번주 언리얼 심화시간에 블루프린트로 배웠는데 이번에 과제하면서 코드로 작성해봤다.   
저번에 작성했던 방식보다 훨씬 자연스럽게 퍼져나간다.   

```cpp
void ATemplateWeapon_Shotgun::StartTrace()
{
	int32 PelletCount = 8; // 탄 개수
	float SpreadAngle = 20.0f; // 탄 퍼짐

	FCollisionQueryParams QueryParams;
	QueryParams.AddIgnoredActor(this);
	QueryParams.AddIgnoredActor(GetOwner());


	// 수업에서 블루프린트로 배운 원형으로 퍼지는 방식
	FVector StartLocation = GetActorLocation();
	FVector MuzzleForward = GetActorForwardVector();
	float SpreadRadius = FMath::DegreesToRadians(SpreadAngle); // 각도를 라디안으로 변환

	for (int32 i = 0; i < PelletCount; ++i)
	{
		// MuzzleForward를 중심으로 SpreadRadius(라디안)만큼 원형으로 퍼진 랜덤 벡터 생성
		FVector PelletDirection = FMath::VRandCone(MuzzleForward, SpreadRadius);

		FVector EndLocation = StartLocation + (PelletDirection * Range);

		FHitResult HitResult;
		bool bIsHit = GetWorld()->LineTraceSingleByChannel(
			HitResult,
			GetActorLocation(),
			EndLocation,
			ECC_Visibility,
			QueryParams
		);

		DrawDebugLine(GetWorld(), GetActorLocation(), EndLocation, FColor::Green);

		if (bIsHit)
		{
			AActor* HitActor = HitResult.GetActor();
			if (HitActor)
			{
				GEngine->AddOnScreenDebugMessage(-1, 2.f, FColor::Red, FString::Printf(TEXT("Number%d Pellet Hits %s!!!"), i + 1, *HitActor->GetName()));
				DrawDebugSphere(GetWorld(), HitResult.ImpactPoint, 20.f, 12, FColor::Red, false, 2.f);
			}
		}
	}
}
```

<br/>

**<Tick 함수>**   

부모 클래스의 Tick을 켜놓고 자식 Tick을 껐는데(`PrimaryActorTick.bCanEverTick = false;`) Tick이 계속 호출된다.   

알고보니 True 상태에서 BP를 만들어놨는데 코드에서 수정을 해도 BP의 Tick 옵션이 켜져있는거였다.   

  </p>
</details>

#### <!-- 26.05.08 -->
<details> 
  <summary>26.05.08</summary>
  <p>

**<코드카타 96번>**   

풀고나서 실행했는데 틀려서 봤더니 하루치 주차시간을 다 더하고 요금을 계산하는거였다.   
문제를 잘 읽자...   
근데 저렇게 계산하는 곳이 어딨음;   

<br/>

**<Interface 사용법>**  

기본적으로 순수 가상 함수를 만들고 인터페이스를 상속시켜서 사용한다.   

하지만 블루프린트가 엮이면 달라진다.   

```cpp
// 인터페이스 클래스
// 헤더파일만 작성
#pragma once

#include "CoreMinimal.h"
#include "UObject/Interface.h"
#include "TestMyInterface.generated.h"

UINTERFACE(MinimalAPI)
class UTestMyInterface : public UInterface
{
	GENERATED_BODY()
};

class MYPROJECT_API ITestMyInterface
{
	GENERATED_BODY()

public:
	// 이러면 블루프린트에서 못씀
	//virtual void OnFireDetected(float Temperature, FVector HitLocation) = 0;

	// 블루프린트는 virtual을 쓰지 못해서 이렇게 리플렉션에 등록해준다.
	// C++ 처럼 구현하지 않아도 된다.
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent, Category = "Interface")
	void OnFireDetected(float Temperature, FVector HitLocation);
};
```

<br/>

```cpp
// 인터페이스의 함수를 사용하는 클래스에 상속한다.
// 헤더파일
#pragma once

#include "CoreMinimal.h"
#include "ItemBase.h"
#include "TestMyInterface.h"
#include "ItemCloth.generated.h"

UCLASS()
class MYPROJECT_API AItemCloth : public AItemBase, public ITestMyInterface
{
	GENERATED_BODY()
	
public:
	// C++ 방식
	//virtual void OnFireDetected(float Temperature, FVector HitLocation) override;
	// 블루프린트 방식
	// _Implementation을 붙여줘야함
	virtual void OnFireDetected_Implementation(float Temperature, FVector HitLocation) override;

protected:
	UPROPERTY(EditAnywhere, Category = "Effects")
	TObjectPtr<class UParticleSystem> FireEffect;
};

// C++ 파일
#include "ItemCloth.h"
#include "Kismet/GameplayStatics.h"
#include "Particles/ParticleSystem.h"

void AItemCloth::OnFireDetected_Implementation(float Temperature, FVector HitLocation)
{
	if (FireEffect)
	{
		UGameplayStatics::SpawnEmitterAtLocation(
			GetWorld(),
			FireEffect,
			GetActorLocation(),
			GetActorRotation(),
			FVector(1.f)
		);
	}
}
```

<br/>

```cpp
// C++과 블루프린트에서 사용하는 방법들
for (const TWeakObjectPtr<AActor>& Item : Items)
{
	// 이렇게 작성하면 C++에서만 사용가능하다. 블루프린트는 다중상속을 지원안함
	// 약한 참조라서 Get()을 사용 가능
	/*ITestMyInterface* MyInterface = Cast<ITestMyInterface>(Item.Get());

	if (MyInterface)
	{
		MyInterface->OnFireDetected(100.f, FVector::ZeroVector);
	}*/

	// 블루프린트로 사용하려고 리플렉션에 등록된 클래스를 확인하는 과정이라서 UTestMyInterface로 가져온다.
	// UTestMyInterface 클래스에 인터페이스가 있는지 체크
	if (UKismetSystemLibrary::DoesImplementInterface(Item.Get(), UTestMyInterface::StaticClass()))
	{
		// 메서드 앞에 Execute_ 를 붙여줘야한다.
		ITestMyInterface::Execute_OnFireDetected(Item.Get(), 100.f, FVector::ZeroVector);
	}
}
```

<br/>

**<delegate 사용해보기>**   

기본 델리게이트 문법   

```cpp
// *** DELEGATE 선언 ***

// C++ 형태로 1대1만 지원
// DECLARE_DELEGATE

// C++ 1대 다수
// DECLARE_MULTICAST_DELEGATE

// 1대1 형태로 블루프린트까지
// DECLARE_DYNAMIC_DELEGATE

// 1대 다수로 블루프린트까지
// DECLARE_DYNAMIC_MULTICAST_DELEGATE

// 바인드 되기 전까지 1바이트도 차지하지 않는다, 하지만 사용시 느려짐 -> 거의 바인딩 되지 않으면 효율적
// 아아아아주 가끔 쓰임
// DECLARE_SPARSE_DELEGATE


// *** 반환값, 매개변수 추가 ***

// 반환값이 하나고 매개변수가 없다면
// DECLARE_DELEGATE_OneParam

// 반환값이 3개고 매개변수가 있다면
// DECLARE_DELEGATE_RetVal_ThreeParams

// (주의!) MULTICAST는 반환값을 지원하지 않는다.

// ------------------------------------------------------------ //

// *** 바인딩 ***
// 기다리겠다는 뜻. 호출되면 함수 실행시켜줘!

// C++ 전용 바인딩, 함수 포인터를 참조해서 매우 빠름
// AddUObject, BindUObject

// 블루프린트까지, 리플렉션 시스템을 이용해서 함수 이름을 찾기 때문에 조금 더 오래걸림
// AddDynamic, BindDynamic

// 싱글 -> Bind로 시작
// 멀티(1대 다수) -> Add로 시작



// *** 바인딩하는 기본 양식 ***
// 오브젝트, 스마트포인터(SharedPtr, ...), Lamda, Static, UFUNCTION


// 오브젝트
// 델리게이트.BindUObject(객체, &UMyObject::함수);

// 스마트포인터
// 델리게이트.BindSP(객체, &UMyObject::함수);

// 람다
// 델리게이트.BindLamda([](){});

// 스태틱
// 델리게이트.BindStatic(객체, &UMyObject::함수);

// UFUNCTION
// 델리게이트.BindUFunction(객체, TEXT("함수이름"));


// 블루프린트와 연동하는 다이나믹 -> 연동되는 함수는 무조건 UFUNCTION() 붙여줘야한다.



// ------------------------------------------------------------ //

// *** 델리게이트 실행 ***
// 싱글
// Execute();

// 멀티(1대 다수)
// Broadcast();

// 싱글은 바인딩 안되면 크래시가 난다.
// 그래서 IsBound로 검사를 꼭 해줘야한다.
// MySingleDelegate.IsBound()

// 블루프린트로 받아올경우
// 이쪽에서 객체로 만들고 그 객체를 통해서 블루프린트 델리게이트를 만들어줌
// UPROPERTY(BlueprintAssignable)
// 이렇게 해야 블루프린트에서 쓸 수 있다.
```

<br/>

```cpp
// 델리게이트 정의
// 1대 다수로 블루프린트까지 지원하는 델리게이트(죽었을때)
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FHealthDeadSignature, AController*, Instigator);
// 1대 다수로 블루프린트까지 지원하는 델리게이트(데미지 입었을때)
DECLARE_DYNAMIC_MULTICAST_DELEGATE_ThreeParams(FHealthDamagedSignature, float, NewHealth, float, MaxHealth, float, HealthChange);

// 클래스 내부에 이런식으로 정의해준다.
UPROPERTY(BlueprintAssignable)
FHealthDeadSignature OnHealthDead;
UPROPERTY(BlueprintAssignable)
FHealthDamagedSignature OnHealthDamaged;
```

<br/>

```cpp
// 다른 클래스에서 HealthManager의 델리게이트를 사용하여 아이템 파괴와 연동 
void AItemBase::BeginPlay()
{
	Super::BeginPlay();
	ACharacter* Player = UGameplayStatics::GetPlayerCharacter(GetWorld(), 0);
	if (Player)
	{
		UHealthManager* Manager = Player->FindComponentByClass<UHealthManager>();
		if (Manager)
		{
			Manager->OnHealthDead.AddDynamic(this, &AItemBase::ItemDestroy);
		}
		else
		{
			// fail
		}
	}
}

void AItemBase::ItemDestroy(AController* InstigatorController)
{
	Destroy();
}
```

  </p>
</details>

#### <!-- 26.05.09 -->
<details> 
  <summary>26.05.09</summary>
  <p>

**<좀비가 스폰이 안되는 현상>**   

**1. 발생한 현상**   
에디터에서 끌어서 배치를 하면 정상적으로 되는데 스폰 볼륨에서 좀비를 스폰하면 애가 움직이지 못하고 Idle 상태로 가만히 있는다.   


**2. 원인**   
먼저, `BT`를 확인해보니 돌아가는게 보이는데 `Distance`가 측정이 안되고 있다.   
`AIController`에서 여기저기 로그를 집어넣어 봤더니 원인이 나왔다. AIController가 `ZombieCharacter`에 `Possess`가 안된건지 로직 순서가 꼬인건지 정확히는 모르겠지만 `GetPawn()`을 해서 ZombieCharacter를 불러오지 못한다.   
```cpp
// 여기 로그가 출력된다.
if (!ZombieCharacter)
{
	UE_LOG(LogTemp, Warning, TEXT("No ZombieCharacter"));
	return;
}
```

`BeginPlay()`에서 `Player`와 `Zombie`를 가져오고 있었는데 좀비가 스폰되는 순서와 `OnPossess()`가 실행되는 순서가 안맞아서 발생하는 현상이었다.   

**3. 해결 방법**   
`OnPossess()`보다 `BeginPlay()`가 먼저 실행 될 수 있기 때문에 `OnPossess()`에서 `GetPawn()`으로 `ZombieCharacter`를 초기화해주면 해결된다.   

<br/>

**<스폰된 좀비가 MoveTo를 실행하지 못하는 현상>**   

**1. 발생한 현상**
BT를 보면 `MoveTo`를 실행하고 있지만 실제로 좀비가 움직이지 않는다. 다가가면 공격 Task는 실행한다. `NavMesh` 문제 같기도 한데 분명 깔아놓았고 혹시 몰라서 좀비 스폰도 시작하고 1초뒤에 하게 했는데도 이런 현상이 발생한다.   

**2. 원인**   
`MoveTo`가 있는 Task에서 `Blackboard`의 `TargetActor`를 불러오는데 값이 비어있다.   
찾아보니 `BeginPlay()`에서 값을 넣어주는게 문제였다. `Spawn`을 시키면 `BeginPlay()`가 먼저 실행되기 때문에 아직 `BehaviorTree`가 `Controller`에 연결이 안된 상태에서 `BlackBoard` 값을 넣어주는게 됐다.   

**3. 해결 방법**   
`OnPossess()`에서 BT를 연결 한 이후에 BB에 값을 넣어주면 된다!   

```cpp
void AZombieAIController::OnPossess(APawn* InPawn)
{
	Super::OnPossess(InPawn);

	// Possess할 때 
	ZombieCharacter = Cast<AZombieCharacter>(GetPawn());
	
	// BP 자식 클래스에서 에셋을 할당했는지 확인 후 실행
	if (BTAsset)
	{
		// UseBlackboard는 내부적으로 Blackboard 데이터 에셋을 기반으로 초기화합니다.
		if (BTAsset->BlackboardAsset)
		{
			Blackboard->InitializeBlackboard(*(BTAsset->BlackboardAsset));
		}
		RunBehaviorTree(BTAsset);
	}

	// BeginPlay()에 넣으면 좀비를 직접 배치할 땐 되지만 스폰할 땐 안된다.
	// BTTask_MoveAndFaceTarget에서 쓸 BB 오브젝트 변수에 값 넣어줌
	Blackboard->SetValueAsObject(BBKeys::TargetActor, PlayerCharacter);
}
```

  </p>
</details>

#### <!-- 26.05.11 -->
<details> 
  <summary>26.05.11</summary>
  <p>

코드카타 97번   

탐색 부분부터 확실히 어려워진다.   

```cpp
// 수학적 접근으로 푼 방법
// 난이도 높음
#include <string>
#include <vector>
#include <cmath>

using namespace std;

int solution(string word) {
    int answer = word.length(); // 각 글자가 존재함에 따른 기본 순위 (+1씩)
    int weight[] = {781, 156, 31, 6, 1}; // 각 자리수별 가중치
    string vowels = "AEIOU";

    for (int i = 0; i < word.length(); i++) {
        for (int j = 0; j < 5; j++) {
            if (word[i] == vowels[j]) {
                answer += j * weight[i];
                break;
            }
        }
    }

    return answer;
}
```

```cpp
// 재귀를 이용한 DFS
// 난이도 보통
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<string> dict;
string vowels = "AEIOU";

void dfs(string current) {
    if (current.length() > 5) return;
    if (current.length() > 0) dict.push_back(current);

    for (int i = 0; i < 5; i++) {
        dfs(current + vowels[i]);
    }
}

int solution(string word) {
    dfs("");
    sort(dict.begin(), dict.end()); // 사전순 정렬
    
    // find를 사용하거나 인덱스를 직접 반환
    return find(dict.begin(), dict.end(), word) - dict.begin() + 1;
}
```
  </p>
</details>

#### <!-- 26.05.13 -->
<details> 
  <summary>26.05.13</summary>
  <p>

알고리즘 수업 코테문제(https://leetcode.com/problems/powx-n/)   

단순한 문제지만 시간복잡도 때문에 생각을 해봐야함   

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        long long N = n;
        if(n < 0)
        {
            x = 1 / x;
            N = - N;
        }
        double value = x;
        double result = 1.0;
        while(N > 0)
        {
            if(N % 2 == 1)
            {
                result *= value;
            }
            N /= 2;
            value *= value;
        }
        return result;
    }
};
```

<br/>

**<다른 클래스의 함수 델리게이트에 Add하기>**   

```cpp
if (UWorld* World = GetWorld())
{
	// GameMode 가져오기
	ANBC_GameMode* MyGM = Cast<ANBC_GameMode>(World->GetAuthGameMode());

	if (MyGM)
	{
		HealthComponent->OnDeath.AddDynamic(MyGM, &ANBC_GameMode::OnMonsterKilled);
	}
}
```

<br/>

**<웨이브 스폰 매니저>**   

데이터 테이블, 스폰 볼륨을 웨이브 스폰 매니저를 만들어서 활용하기로 했다.   
GameMode에 부착해서 사용할 수 있어서 좋다.   

`ZombieSpawnRow (Data)`: "1웨이브에는 일반 좀비 10마리, 5초 뒤에 스피드 좀비 5마리" 같은 기획 데이터를 담는다.

`ZombieSpawnVolume (Worker)`: 매니저가 "여기서 좀비 A 스폰해!"라고 명령하면 실제 좌표를 계산해 SpawnActor를 실행

`WaveSpawnManager (Brain)`: DataTable을 읽고, 시간을 재고, 볼륨에게 스폰 명령을 내림   

  </p>
</details>

#### <!-- 26.05.14 -->
<details> 
  <summary>26.05.14</summary>
  <p>

**<vector에 push_back과 emplace_back의 차이점>**   

push_back은 함수 인자로 이미 생성된 객체를 받습니다.   
인자로 전달된 객체를 벡터의 끝에 추가하기 위해 복사 생성자(Copy Constructor) 또는 이동 생성자(Move Constructor)를 호출합니다.   
임시 객체를 전달하면 임시 객체 생성 -> 복사/이동 수행 -> 임시 객체 소멸이라는 단계를 거친다.   

```cpp
std::vector<std::string> vec;
std::string str = "Hello";

vec.push_back(str);           // 복사 생성자 호출 (str은 그대로 남음)
vec.push_back("World");       // "World"라는 임시 객체 생성 후 이동 생성자 호출
```

emplace_back은 객체를 직접 받는 대신, 객체를 생성하는데 필요한 인자들을 받습니다.   
가변 인자 템플릿(Variadic Templates)을 사용하여, 벡터가 관리하는 메모리 공간 내부에서 객체를 직접 생성(Forwarding)합니다.   
불필요한 복사나 이동 과정이 생략되므로 성능상 이점이 있습니다.   
객체의 구조가 복잡하거나 생성자에 전달해야 할 인자가 여러 개일 때 유용합니다.   

```cpp
std::vector<std::string> vec;

// "Hello"를 만들기 위한 인자만 전달 -> 벡터 내부 메모리에서 직접 string 객체 생성
vec.emplace_back("Hello");
```

<br/>

복사생성자    
기존 객체의 내용을 그대로 복사해서 새로운 객체를 만들어서 성능 부하가 크다.   

이동생성자   
기존 객체가 가진 자원(메모리 주소 등)을 새 객체가 받아서 빠르다.   

가변 인자 템플릿(Variadic Templates)   
함수가 개수와 타입에 상관없이 인자를 받을 수 있게 해주는 문법이다.   
...(Ellipsis) 기호를 사용한다.   

std::forward(완벽한 전달, Perfect Forwarding)   
가변 인자로 받은 재료들을 "원래 성질 그대로" 생성자에게 전달하는 기술이다.   
함수 인자로 이름을 붙여 받는 순간 시스템상에서 '이름이 있는 변수(L-value)'가 되어버려 '임시 값(R-value)'특성을 잃어 버릴 수 있는데 원래 성질을 기억해서 그대로 넘겨주게 해준다.   

<br/>

해시 테이블(Hash Table)   
key 를 사용하여 해시값으로 변환 후 저장
Key-Value로 저장하며 임의의 크기를 가진 데이터를 고정된 크기의 고유한 숫자(해시 값)로 변환하여 저장하는 자료구조입니다.
해시 함수(Hash Function)에 Key를 넣으면 저장할 인덱스를 반환하고 버킷(Bucket)에서 인덱스에 실제 데이터를 저장합니다.   

해시 충돌(Hash Collision)   
서로 다른 키가 같은 인덱스를 가리키는 현상입니다.   
해결법으론 체이닝(Chaining)으로 같은 칸에 여러 데이터를 연결 리스트로 줄 세우는 방법이 있고   
개방 주소법(Open Addressing)으로 비어있는 근처 칸을 찾아 저장하는 방법이 있습니다.   

힙(Heap)   
완전 이진 트리(Complete Binary Tree)이며 마지막 레벨을 제외하고 모든 노드가 채워져있습니다.   
최대 힙(Max Heap) 부모 노드가 자식 노드보다 항상 큼(루트가 최댓값)   
최소 힙(Min Heap) 부모 노드가 자식 노드보다 항상 작음(루트가 최솟값)   
데이터 삽입 및 최우선 순위 데이터 삭제 시 O(log n)의 시간 복잡도입니다.   

Red-Black Tree   
일반적인 이진 탐색 트리와 다르게 균형을 맞춰서 높이를 O(log n)으로 강제하여 빠른 성능을 유지합니다.

  </p>
</details>

#### <!-- 26.05.17 -->
<details> 
  <summary>26.05.17</summary>
  <p>


**<State Tree 사용>**   

Player가 계속 안불러와져서(아마 스폰 로직 순서 꼬인 것 같기도) 플레이어를 불러오는 Task를 따로 만들기로 했다.   

ST에서 `Evaluators`(StateTreeEvaluatorBlueprintBase로 만든 Blueprint Class)를 Add해서 Task를 추가해서 `TargetActor`라는 변수를 만들고 플레이어를 가져오는 `Tick`으로 `Set`해준다.   
일단 Player 가져오는건 성공.   

하지만 Move To가 제대로 실행이 안되는중   


**<보스와 플레이어 거리 측정의 오류>**   

분명 플레이어가 멀어지는데 특정 위치로 가면 보스와의 거리가 0으로 수렴하는 이상한 현상이 있다.   
Z축이 서로 다른 문제였던 것 같은데 일단 서로의 다른 중심축을 연결하는 방식을 사용하기로 했다.   

**<Task에서 Move To 하지 말자>**   

기본적으로 AIController에서 Move To를 만들고 해당 함수를 블루프린트에서 불러오는 방식이 훨씬 쉽고 간단하다.   

```cpp
// 정말 간단...
void ABossAIController::MoveToTarget()
{
	this->MoveToActor(PlayerCharacter, 100.f);
}
```

  </p>
</details>

#### <!-- 26.05.18 -->
<details> 
  <summary>26.05.18</summary>
  <p>

**<Tick함수의 매개변수 이름 차이>**   

팀플 하다보니 `Actor`와 `AIController`의 Tick 함수의 매개변수가 달라서 궁금해서 찾아봄   

각각 `DeltaTime`, `DeltaSeconds`인데 똑같은 값을 전달하고 변수명만 다르다고 함.   
이유는 언리얼 엔진이 20년이 넘는 세월동안 개발되면서 나온 코딩 스타일 규칙(Naming Convention) 차이에서 온 해프닝이라고 함.   

실제로 `UUserWidget(UI)`의 Tick 함수는 또 `InDeltaTime`으로 되어있다고 한다.   

팁: 오버라이드해서 구현할 때 매개변수의 이름은 바꿔도 상관은 없음. 즉, `AIController`에서 `DeltaTime`이라고 써도 무방하다는 뜻이다.(타입만 맞으면 됨)   

<br/>

**<ST에서 BT의 Wait와 비슷한 동작을 하는 방법>**   

`Chase`에서 `MeleeAttack`으로 넘어갈때 이전 BT처럼 Attack이 너무 빠르게 끝나버려서 꼬이는 현상을 발견했다.   

AI한테 물어봐서 2시간동안 이것 저것 다 해봤는데 결국 내가 해답을 찾았다. 분명 AI가 `ST`에선 `Wait`같은 기능이 없으니 `Task` 자체를 뭐 뜯어 고쳐야 한다느니 뭐라뭐라 했는데 알고보니 Wait와 같은 기능을 하는 `Delay`라는 놈이 있었다. 진짜 어이없다. AI성능 레전드   


<br/>

**<보스가 플레이어를 Chase하는 속도 갱신에 대한 문제>**   

보스랑 플레이어의 거리에 비례해서 보스의 속도를 높이고 싶은데 `Move To`가 매번 실행되는게 아니라 실행 시켜놓고 `Attack`으로 넘어갈지 안갈지 체크하는 상태라서 처음 `Move To`한 속도가 그냥 고정되는 상태다.    

Tick을 이용해서 Move To를 계속 불러오는 방식을 사용해야 하는 것 같다.   
이 부분은 아직 중요하진 않아서 추후에   

<br/>

**<Root Motion 사용해보기>**   

보스가 점프 공격을 하는데 캡슐은 원래 자리에 있어서 뒤로 돌아가버리는 현상이 생겼다.   
언리얼 공식 문서를 검색해서 공부를 해보았따.   

... 답이 안나온다. 내일 튜터님께 여쭤봐야겠다.   


  </p>
</details>

#### <!-- 26.05.19 -->
<details> 
  <summary>26.05.19</summary>
  <p>

**<프로세스와 스레드의 차이점>**   

프로세스는 프로그램이 메모리에 올라가서 실행되고 있는 것을 말합니다. (운영체제로부터 자원을 할당받는 작업의 단위)
이 메모리 공간은 크게 Code, Data, Heap, Stack 영역으로 나뉩니다.
프로세스는 서로 독립적이라 직접 접근할 수 없고 프로세스 하나에서 에러가 나도 다른 프로세스엔 영향을 미치지 않습니다.
두 프로세스가 데이터를 주고 받으려면 통신 비용이 많이 듭니다.
(IPC(Inter-Process-Communication)라는 복잡한 파이프라인이나 소켓 통신을 거쳐야해서)
IPC 종류는?
프로세스는 캐싱 히트율이 매우 낮다(메모리 공유를 하지 않아서)

스레드는 프로세스 내에서 실제로 일을 합니다. (프로세스가 할당받은 자원을 이용하는 실행 흐름의 단위, CPU가 처리하는 최소 작업 단위)
프로세스의 Code, Data, Heap 영역을 공용으로 사용하고 각자 독립된 Stack 영역을 가집니다.
메모리 일부를 공유하기 때문에 스레드끼리 데이터를 주고 받을때는 메모리 주소만 넘기면 돼서 통신 비용이 저렴하지만 스레드 하나가 에러가 나면 다른 스레드에도 영향을 미칩니다.
Context Switching(스레드에서 스레드로 넘어가는것, 현재 상태를 저장하고 다른 스레드 상태를 불러와서 작업) 비용이 저렴합니다.
하나의 메모리공간에 여러 스레드가 동시에 접근하는 경쟁 상태(Race Condition)을 조심해야합니다.
메모리를 공유하기 때문에 캐싱이 될 가능성이 높아서 엄청 빠르다. 캐시 히트율이 매우 높다.

Code 컴파일된 기계어를 저장(Read Only)
Data  전역변수, 정적변수
Heap 동적 할당한 변수
Stack 지역변수, 메서드, 함수 리턴 주소


1코어
코어 하나가 돌아가면서 작업을 함(동시성, Concurrency)

멀티코어
여러 코어가 각자 스레드를 맡아서 함(병렬성, Parallelism) 패럴렐리즘

<br/>

**<Root Motion 해결>**   

튜터님께 갔더니 구글링 해서 방법을 알려주셔서 그 영상 따라서 해서 드디어 해결했드아ㅏㅏㅏㅏ    

Blender에 github에서 받은 mixamo 애니메이션에 Root를 추가해주는 변환기를 애드온 한 후 변환을 하면 해결된다...   

<br/>

**<Enum값 출력 하기>**   

```cpp
EMovementMode MovementMode = GetCharacterMovement()->MovementMode;
UE_LOG(LogTemp, Warning, TEXT("MovementMode: %s"), *UEnum::GetValueAsString(MovementMode));
```

<br/>

**<점프 하는순간 착지 판정이 나버리는 현상>**   

AI들한테 다 물어봐도 도저히 이상한 대답만 내놔서 이것 저것 삽질하면서 생각하다보니 원인을 찾은 것 같다.   
점프 직전에 미세하게 웅크리는 모션을 취하고 점프를 하는데 이때 Velocity.Z 값이 마이너스가 되고 Location.Z값도 미세하게 떨어졌다가 올라간다.   
즉, Location.Z값이 원래 상태로 복구되는 순간 점프가 끝났다고 착각하는 것 같다는게 내 결론이다.   
물론 아직 증명은 안됐다. 고쳐봐야지...   

->Movement를 Flying으로 바꿔주면 해결된다..!!!!!   
(MoveTo에서 다시 Walking으로 바꾸면 됨)   

  </p>
</details>

#### <!-- 26.05.20 -->
<details> 
  <summary>26.05.20</summary>
  <p>

**<스마트 포인터의 크기>**   

1. std::unique_ptr ➔ 기본 크기: 8바이트
std::unique_ptr은 독점 소유권을 가지는 스마트 포인터입니다. 내부적으로 실제 객체를 가리키는 포인터 딱 하나만 가지고 있습니다.

크기: 8바이트 (일반 포인터와 동일)

특징: 성능 오버헤드가 전혀 없습니다. 일반 포인터와 크기가 같으므로 메모리나 속도 측면에서 수동 delete를 쓰는 것과 동일한 효율을 냅니다.

예외: 만약 사용자 정의 삭제자(Custom Deleter)를 상태(State)가 있는 함수 객체 형태로 넘기면, 그 삭제자의 크기만큼 스마트 포인터의 크기가 커질 수 있습니다. (람다에 캡처가 있는 경우 등)

2. std::shared_ptr ➔ 기본 크기: 16바이트
std::shared_ptr은 공동 소유권을 가지는 스마트 포인터입니다. 내부적으로 2개의 포인터를 가지고 있기 때문에 크기가 일반 포인터의 2배입니다.

크기: 16바이트

내부 구조:

자원 포인터 (8바이트): 실제 관리하는 객체를 가리키는 포인터

제어 블록 포인터 (8바이트): 참조 횟수(Reference Count), 약한 참조 횟수(Weak Count), 삭제자 등을 관리하는 메모리 공간(Control Block)을 가리키는 포인터

Tip (std::make_shared를 써야 하는 이유)
std::shared_ptr을 사용할 때 new로 객체를 생성해 넘기면 '실제 객체'와 '제어 블록'이 메모리에 각각 따로 할당되어 파편화가 생깁니다. 반면 std::make_shared를 사용하면 이 두 개를 하나의 메모리 블록에 묶어서 한 번에 할당하므로 성능과 메모리 효율이 훨씬 좋아집니다.

3. std::weak_ptr ➔ 기본 크기: 16바이트
std::weak_ptr은 std::shared_ptr이 가리키는 객체를 참조하지만, 참조 횟수(Ref Count)를 늘리지 않아 순환 참조를 방지할 때 씁니다.

크기: 16바이트

내부 구조: shared_ptr과 동일하게 자원 포인터와 제어 블록 포인터 2개를 가집니다. 제어 블록에 접근해서 "이 객체가 아직 살아있는지" 확인해야 하기 때문입니다.

<br/>

**<점프 거리를 조절하기 위한 모션 워핑 사용하기>**   

1. `meta = (AllowPrivateAccess = "true")` 쓰는 이유   
   private으로 정해놓으면 블루프린트에서 편집이 불가능한데 이걸 풀어주는 역할
2. `FORCEINLINE`
   언리얼엔진에서 함수를 인라인 함수로 등록하는 역할을 한다.   

Scale을 조절하는게 제일 편하다.


<br/>

**<플레이어가 세팅되는 순서차이>**   

플레이어가 계속 잡히지 않아서 뭔가 했더니 MoveTo가 BeginPlay()보다 빨리 실행돼서 생기는 오류였따.   

```cpp
void ABossAIController::BeginPlay()
{
	Super::BeginPlay();

	UE_LOG(LogTemp, Warning, TEXT("PC Setting"));
	PlayerCharacter = UGameplayStatics::GetPlayerCharacter(GetWorld(), 0);
	
}

void ABossAIController::BossMoveToActor()
{
	if (PlayerCharacter == nullptr)
	{
		UE_LOG(LogTemp, Warning, TEXT("NO PC"));
		return;
	}

	UE_LOG(LogTemp, Warning, TEXT("MoveTo 함수 실행 시작"));
	MoveToActor(PlayerCharacter, 150.f);
}
```
이런 경우가 생각보다 빈번해서 진짜 골치아프다.   

OnPossess가 제일 빠른 것 같은데 문제는 일반 좀비 몬스터를 할 때는 이런 문제가 없었던건데 이유를 알아냈다.   

좀비에선 ZombieCharacter에서 MoveTo를 실행했기때문에 이미 Player를 받고 실행했지만 이번 보스 좀비에서는 BossAIController에서 바로 실행하도록 바꿨기때문에 이런 차이가 발생했다.   

  </p>
</details>

#### <!-- 26.05.21 -->
<details> 
  <summary>26.05.21</summary>
  <p>

**<State Tree 연동 성공!>**   

페이즈가 바뀔 때 `OnEvent`를 시작해줘야하는데 그 과정이 생각보다 복잡하다.   

```cpp
void ABossAIController::TriggerPhaseTransition()
{
	// 1. 월드 및 기본 방어
	if (!GetWorld()) return;

	// 2. StateTreeAIComponent 클래스 동적 로드
	UClass* TargetClass = StaticLoadClass(UActorComponent::StaticClass(), nullptr, TEXT("/Script/GameplayStateTreeModule.StateTreeAIComponent"));
	if (!TargetClass)
	{
		UE_LOG(LogTemp, Error, TEXT("[PhaseTransition] StateTreeAIComponent 클래스를 로드하지 못했습니다!"));
		return;
	}

	// 3. 컨트롤러에 해당 컴포넌트가 실제로 붙어있는지 확인
	UActorComponent* FoundComponent = GetComponentByClass(TargetClass);
	if (!FoundComponent)
	{
		UE_LOG(LogTemp, Error, TEXT("[PhaseTransition] 이 컨트롤러에 StateTreeAIComponent가 배치되지 않았습니다. 블루프린트를 확인하세요!"));
		return;
	}

	// 4. 컴포넌트의 클래스 정보가 안전한지 한 번 더 확인
	UClass* ComponentClass = FoundComponent->GetClass();
	if (!ComponentClass) return;

	// 5. "SendStateTreeEvent" 함수가 실제로 존재하는지 확인
	UFunction* SendEventFunc = ComponentClass->FindFunctionByName(TEXT("SendStateTreeEvent"));
	if (!SendEventFunc)
	{
		UE_LOG(LogTemp, Error, TEXT("[PhaseTransition] SendStateTreeEvent 함수를 찾을 수 없습니다!"));
		return;
	}

	// 6. 모든 게 안전함이 확인되었으니 실행
	FGameplayTag TransitionTag = FGameplayTag::RequestGameplayTag(FName("Boss.Event.PhaseTransition"));

	// FStateTreeEvent 메모리 정렬에 맞춘 구조체 (태그 + 오리진)
	struct FDynamicStateTreeEvent
	{
		FGameplayTag Tag;
		FName Origin;
	};

	FDynamicStateTreeEvent Params;
	Params.Tag = TransitionTag;
	Params.Origin = NAME_None;

	// 최종 실행
	FoundComponent->ProcessEvent(SendEventFunc, &Params);

	UE_LOG(LogTemp, Warning, TEXT("[PhaseTransition] 페이즈 태그를 안전하게 전달했습니다."));
}
```

  </p>
</details>

#### <!-- 26.05.22 -->
<details> 
  <summary>26.05.22</summary>
  <p>

**<좀비들 끼리 튕겨내는 현상>**   

이것 저것 다 건드려봤는데 단순하게 mesh의 collision pawn이 block이라서 서로 밀어내고 난리나는거였다. ignore로 바꾸니까 바로 해결   

<br/>

**<보스 공격 판정 구현>**   

```cpp
// 헤더 파일
#pragma once

#include "CoreMinimal.h"
#include "Components/ActorComponent.h"
#include "BossAttackComponent.generated.h"


UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )
class NBC_CH3_TEAMPROJECT_API UBossAttackComponent : public UActorComponent
{
	GENERATED_BODY()

public:	
	UBossAttackComponent();

protected:
	virtual void BeginPlay() override;

public:	
	virtual void TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction) override;

	// 공격 시작 (ANS_Begin에서 호출)
	UFUNCTION(BlueprintCallable, Category = "Boss | Attack")
	void StartMeleeTrace(FName InSocketName, float InRadius);

	// 공격 추적 연산을 수행
	UFUNCTION(BlueprintCallable, Category = "Boss | Attack")
	void ExecuteMeleeTrace();

	// 공격 종료 (ANS_End에서 호출)
	UFUNCTION(BlueprintCallable, Category = "Boss | Attack")
	void EndMeleeTrace();

private:

	UPROPERTY()
	TObjectPtr<ACharacter> BossCharacter;

	// 현재 공격 추적 중인지 여부
	bool bIsAttacking;

	// 추적 타겟 소켓 이름 및 반경
	FName TargetSocketName;
	float TraceRadius;

	// 지난 프레임의 소켓 위치 기록 (궤적을 그리기 위함)
	FVector LastSocketLocation;

	// 한 번의 공격 콤보 내에서 이미 대미지를 입은 액터들의 목록 (중복 피격 방지)
	UPROPERTY()
	TArray<TObjectPtr<AActor>> AlreadyHitActors;
};


// C++ 파일
#include "AI/BossAttackComponent.h"
#include "GameFramework/Character.h"
#include "Kismet/GameplayStatics.h"


UBossAttackComponent::UBossAttackComponent()
{
	PrimaryComponentTick.bCanEverTick = false;

	bIsAttacking = false;
	TargetSocketName = NAME_None;
	TraceRadius = 50.f;
	LastSocketLocation = FVector::ZeroVector;
}

void UBossAttackComponent::BeginPlay()
{
	Super::BeginPlay();

	BossCharacter = Cast<ACharacter>(GetOwner());
}

void UBossAttackComponent::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction)
{
	Super::TickComponent(DeltaTime, TickType, ThisTickFunction);
}

void UBossAttackComponent::StartMeleeTrace(FName InSocketName, float InRadius)
{
	if (!BossCharacter || !BossCharacter->GetMesh()) return;

	bIsAttacking = true;
	TargetSocketName = InSocketName;
	TraceRadius = InRadius;

	// 공격 시작 시점에 이미 맞았던 액터 리스트를 초기화
	AlreadyHitActors.Empty();

	LastSocketLocation = BossCharacter->GetMesh()->GetSocketLocation(TargetSocketName);
}

void UBossAttackComponent::EndMeleeTrace()
{
	bIsAttacking = false;
	AlreadyHitActors.Empty();
}

// NotifyState에서 매 프레임 호출
void UBossAttackComponent::ExecuteMeleeTrace()
{
	if (!bIsAttacking || !BossCharacter || !BossCharacter->GetMesh()) return;

	UWorld* World = GetWorld();
	if (!World) return;

	// 현재 프레임의 소켓 위치
	FVector CurrentSocketLocation = BossCharacter->GetMesh()->GetSocketLocation(TargetSocketName);

	// 중복 프레임 제거
	if (CurrentSocketLocation.Equals(LastSocketLocation, 0.1f)) return;

	TArray<FHitResult> HitResults;
	FCollisionShape SphereShape = FCollisionShape::MakeSphere(TraceRadius);

	FCollisionQueryParams QueryParams;
	QueryParams.AddIgnoredActor(BossCharacter); // 보스 자신은 제외

	// 이미 맞은 애들도 트레이스 계산에서 제외
	for (AActor* HitActor : AlreadyHitActors)
	{
		if (HitActor)
		{
			QueryParams.AddIgnoredActor(HitActor);
		}
	}

	// 플레이어 판정을 위해 ECC_Pawn을 기본 사용
	// 추후 플레이어 피격용 전역 커스텀 채널 만들 예정(예: ECC_GameTraceChannel2)
	FCollisionObjectQueryParams ObjectParams;
	ObjectParams.AddObjectTypesToQuery(ECC_Pawn);

	bool bHit = World->SweepMultiByObjectType(
		HitResults,
		LastSocketLocation,
		CurrentSocketLocation,
		FQuat::Identity,
		ObjectParams,
		SphereShape,
		QueryParams
	);

	// 디버그 라인
	 DrawDebugSphere(World, CurrentSocketLocation, TraceRadius, 8, FColor::Red, false, 1.0f);

	if (bHit)
	{
		for (const FHitResult& Hit : HitResults)
		{
			AActor* HitActor = Hit.GetActor();
			if (HitActor && !AlreadyHitActors.Contains(HitActor))
			{
				// 중복 타격 리스트에 추가
				AlreadyHitActors.Add(HitActor);

				// 플레이어의 TakeDamage / HealthComponent에게 전달
				UGameplayStatics::ApplyDamage(
					HitActor,
					50.f, // 대미지 값 
					BossCharacter->GetController(),
					BossCharacter,
					UDamageType::StaticClass()
				);
			}
		}
	}

	// 다음 틱 연산을 위해 현재 소켓 위치를 지난 프레임 위치로 갱신
	LastSocketLocation = CurrentSocketLocation;
}


```


  </p>
</details>

#### <!-- 26.05.23 -->
<details> 
  <summary>26.05.23</summary>
  <p>

**<보스 크기가 커서 정면을 바라보고 공격하면 플레이어한테 닿지 않는 문제>**   

보스가 크기가 크다보니 공격들이 대부분 플레이어가 앞에서 가만히 있어도 맞지 않는다.   


1. ABP에서 `LookAt` 노드 사용해보기
   보스가 플레이어 쪽으로 꺾여버림...   공격 몽타주를 실행할때만 발동하고 싶은데 일단 다른 방법을 찾아보기로 함.   

2. C++코드에서 `FindLookAtRotation` 사용해보기   
    비추천
   
보스의 공격 범위 자체를 키우는게 낫다.   

  </p>
</details>

#### <!-- 26.05.26 -->
<details> 
  <summary>26.05.26</summary>
  <p>

**<팀 프로젝트 정리>**   

AI 기능 명세서 (Project 8th Team11 CH3)

발표 자료용 요약본

---

1. 보스 AI 시스템 (Boss AI)   
스테이트 트리(State Tree)를 기반으로 동작하며, 보스는 체력에 따라 총 3단계의 페이즈로 변화하고 각 페이즈마다 고유한 공격 패턴을 실행하도록 설계

**핵심 구성 요소**   
- **BossCharacter**: 보스의 체력 관리, 페이즈 전환 로직, 애니메이션 몽타주 재생을 담당
- **BossAIController**: 플레이어 추적, 회전 처리, 페이즈별 공격 판단(근접/점프 공격) 및 StateTree 이벤트 전송을 관리
- **BossAttackComponent**: 보스의 공격 판정 로직을 컴포넌트화하여 관리
- **StateTree**: 보스의 페이즈 조건과 페이즈별 상태의 로직을 트리로 구현 
- **AnimNotifyState**: 몽타주의 특정 구간동안 활성화 하여 정확한 공격 범위를 생성
- **RootMotion**: 루트 모션을 활성화하여 점프 공격 애니메이션 몽타주를 구현
- **MotionWarping**: 모션 워핑을 이용하여 점프 공격 애니메이션의 Scale을 자연스럽게 조정

**주요 기능**   
- **페이즈 시스템 (3-Phase System)**
  - **Phase 1 (체력 100% ~ 70%)**: 기본적인 추적 및 근접 공격을 수행
  - **Phase 2 (체력 70% ~ 30%)**: 이동 속도가 증가하며, 일정 확률로 강력한 **점프 공격**을 시도
  - **Phase 3 (체력 30% 이하)**: 이동 속도가 대폭 증가(광폭화)하고 점프 공격 빈도 상승
- **공격 시스템**
  - **Melee Trace**: 무기 소켓 위치를 추적(Sweep)하여 정밀한 근접 공격 판정을 수행
  - **Jump Attack (Radial Slam)**: 플레이어와의 거리에 따라 4단계의 도약 거리(Animation Montage)를 선택하여 점프하며, 착지 시 일정 범위 내 플레이어에게 방사형 데미지(Radial Damage)를 
  - **Interpolation Turn**: 플레이어를 부드럽게 바라보도록 보간 회전(RInterpTo) 처리

---

2. 일반 좀비 AI 시스템 (Zombie AI)   
비헤이비어 트리(Behavior Tree)를 기반으로 동작하며, 대량의 적이 효율적으로 동작하도록 설계

**핵심 구성 요소**   
- **ZombieCharacter**: 좀비의 기본 속성(공격력, 사거리 등) 정의 및 피격/사망 로직을 포함
- **ZombieAIController**: 비헤이비어 트리 구동 및 블랙보드 데이터(TargetActor, Distance 등)를 갱신
- **BehaviorTree**: 좀비의 기본 행동 사이클

**비헤이비어 트리 주요 태스크 (BTTasks)**   
- **BTTask_Move**: 플레이어를 목표로 이동하며 적정 사거리를 유지
- **BTTask_Attack**: 플레이어가 공격 사거리 및 각도 내에 있는지 판별하여 실행 (Dot Product 활용)

**최적화 및 편의 기능**   
- **RVO Avoidance**: 좀비들끼리 서로 겹치지 않고 자연스럽게 길을 찾아가도록 회피 시스템이 적용
- **Random Animation**: 공격, 피격, 사망 시 여러 애니메이션 중 하나를 랜덤하게 재생하여 단조로움을 방지

---

3. 스폰 및 웨이브 시스템 (Wave System)   
데이터 테이블(DataTable)을 기반으로 웨이브 진행에 따른 적 스폰을 자동화

**주요 기능**   
- **WaveSpawnManager**: 게임 상태(GameState)의 현재 웨이브 정보를 읽어 데이터 테이블에 정의된 적 종류와 숫자를 스폰
- **DataTable Driven**: 코드 수정 없이 데이터 테이블 편집만으로 웨이브 구성(적 종류, 스폰 수량 등)을 변경
- **Spawn Volume**: 지정된 구역(Box Component) 내에서 적절한 위치를 계산하여 좀비와 보스를 생성

---

4. 공통 전투 시스템에 연동   
- **HealthComponent**: 보스와 좀비 모두 공통된 체력 컴포넌트를 사용하여 데미지 처리 및 사망 이벤트를 관리
- **HitReactComponent**: 피격 시 물리적인 반응(Hit Reaction)을 처리하여 타격감을 강화
- **GameMode**: 적 처치 시 게임 모드에 알림을 보내어 점수 산정 및 다음 웨이브 트리거로 활용

  </p>
</details>

#### <!-- 26.05.27 -->
<details> 
  <summary>26.05.27</summary>
  <p>

팀 프로젝트 회고록 작성      

팀 프로젝트간 발생한 트러블 슈팅 정리   

---
- 문제: 좀비가 플레이어를 추적(MoveTo)할 때 회전이 부자연스럽고 서로 겹치는 현상
- 과정: 회전 관련 설정을 확인해보았고 겹치지 않게 하는 옵션이 있는지 검색
- 결과: MovementComponent의 RotationRate를 이용해 부드러운 회전을 만들었고 bUseRVOAvoidance를 true로 하여 군중 회피를 활성화   
---
- 문제: 몬스터를 직접 배치하면 문제없지만 스폰을 하면 로직이 작동하지 않는 현상
- 과정: 스폰을 하면 AIController의 BeginPlay가 OnPossess보다 더 빠르게 작동하는걸 로그로 확인
- 결과: Pawn을 Possess하기전에 Pawn과 관련된 로직을 BeginPlay에 넣지말고 OnPossess에 넣으면 해결
---
- 문제: 몬스터가 공격을 실행할 때 제자리가 아니라 플레이어에게 미끄러지듯 오는 현상
- 과정: StopMovement 등을 사용하여 움직임을 멈춰보려고 했지만 멈추는 순간 MoveTo가 발생해서 소용이 없었고 MoveTo를 Task 자체를 멈출 방법이 필요
- 결과: BT같은 경우 Wait노드를 공격 몽타주 시간만큼 실행을 해주고 ST의 경우 같은 방법으로 Delay를 걸어주면 해결
---
- 문제: Mixamo에서 가져온 애니메이션과 Skeleton에 Root Motion을 사용할 수 없는 현상
- 과정: AI를 참고하여 정말 이것저것 다 건드려 봤는데 결론은 Mixamo의 애니메이션은 Root가 없어서 Root Motion을 못 쓰는 거였다.
- 결과: 튜터님의 도움을 받아서 Blender에서 Root를 추가시켜주는 기능을 애드온 하는 법을 알게 됐고 변환을 통해 해결
---
- 문제: 보스의 점프 공격의 Z축이 막히는 현상
- 과정: 여러 부분을 디버깅하면서 캡슐 컴포넌트가 바닥에 붙어있는 것(Location.Z도 고정, Velocity도 고정)을 확인하고 Z축 관련된 모든 옵션을 확인했는데 보스의 점프 준비자세에서 z축이 잠깐 아래로 갔다가 올라오는데 이때 엔진은 보스가 착지했다고 판단(그래서 Jump , Falling 옵션은 불가능)
- 결과: 정말 많은 시도 끝에 공중에 있는 동안만 Movement를 Flying으로 바꿔서 해결
---
- 문제: Motion Warping을 사용해서 점프 거리를 늘릴 때 보스가 뒤로 튀어 나갔다가 다시 앞으로 튀어나가는 현상
- 과정: 보스가 점프 할 때 양 팔을 뒤로 젖히는데 이 때 미세하게 보스의 특정부분이 뒤로간다고 판단해서 거리를 늘린 만큼 순간적으로 뒤로 튀어갔다가 양팔을 젖히는 모션이 끝나면 앞으로 튀어 나감
- 결과: 이 부분은 애니메이션을 직접 수정해야해서 Scale 옵션을 X, Y, Z축을 각자 조절하여 적절한 점프 높이, 거리를 만들어내서 해결
---

  </p>
</details>


#### <!-- 26.05.28 -->
<details> 
  <summary>26.05.28</summary>
  <p>

브로셔 내 파트 내용 간단 정리

핵심 기능   
1. 좀비 AI
   
    Behavior Tree와 BTTask, AIController내에서 회전값 조정을 이용하여 기본적인 추적, 공격, 회전 등을 구현
    
    좀비마다 필요한 정보가 다르지 않아서 독립적인 메모리는 생성하지 않고 단순하게 인스턴스를 찍어내는 방식을 사용하고 최소한의 Tick으로 플레이어의 위치정보 등을 BlackBoard로 관리하여 수십마리의 좀비가 등장해도 성능이 크게 떨어지지 않도록 함
2. 보스 AI
   
    State Tree와 STTask, BossAIController내의 로직을 사용해서 추적, 공격, 페이즈 변화, 거리에 따른 점프 공격 변화, 광폭화 등을 구현
3. 다양한 모션
   
    몽타주를 적극 활용하여 단조롭지 않게 하였고 보스의 경우 공격 모션과 같은 공격 범위를 구현

핵심 기술   
1. Behavior Tree
   
    Behavior Tree, BTT, BB를 사용하여 좀비의 단순한 AI 로직을 구현
2. State Tree
   
    StateTree, STTask를 이용하여 페이즈 별 패턴 구분

3. Root Motion
    
    Root Motion을 이용하여 캡슐 컴포넌트를 움직이고 Motion Warping을 이용해서 애니메이션 Scale을 조절

3.트러블 슈팅   

- 문제 상황: 좀비가 플레이어를 추적(MoveTo)할 때 회전이 부자연스럽고 서로 겹치는 현상
- 원인: 회전 관련 설정이 디폴트 상태이고 Pawn끼리 겹치지 않게 하는 옵션이 비활성화
- 해결방법: MovementComponent의 RotationRate를 이용해 부드러운 회전을 만들었고 bUseRVOAvoidance를 true로 하여 군중 회피를 활성화
- 배운 점: 움직임을 자연스럽게 만드는게 생각보다 더 난이도가 높다는걸 느낌

<br/>

- 문제 상황: 몬스터를 직접 배치하면 문제없지만 스폰을 하면 로직이 작동하지 않는 현상
- 원인: 스폰을 하면 AIController의 BeginPlay가 OnPossess보다 더 빠르게 작동하는걸 로그로 확인
- 해결방법: Pawn을 Possess하기전에 Pawn과 관련된 로직을 BeginPlay에 넣지말고 OnPossess에 넣으면 해결
- 배운 점: 상황에 따라 함수의 실행 순서가 조금씩 달라지고 디버깅의 중요성을 느낌

<br/>

- 문제 상황: 몬스터가 공격을 실행할 때 제자리가 아니라 플레이어에게 미끄러지듯 오는 현상
- 원인: StopMovement 등을 사용하여 움직임을 멈춰보려고 했지만 멈추는 순간 MoveTo가 발생
- 해결방법: BT같은 경우 Wait노드를 공격 몽타주 시간만큼 실행을 해주고 ST의 경우 같은 방법으로 Delay를 걸어주면 해결
- 배운 점: BT, ST에서 기본으로 제공되는 몇 안되는 Task인데 그 이유가 있었음

<br/>

- 문제 상황: Mixamo에서 가져온 애니메이션과 Skeleton에 Root Motion을 사용할 수 없는 현상
- 원인:  Mixamo의 애니메이션은 Root가 없음
- 해결방법: 튜터님의 도움을 받아서 Blender에서 Root를 추가시켜주는 기능을 애드온 하는 법을 알게 됐고 변환을 통해 해결
- 배운 점: 앞으로 Mixamo의 애니메이션 만큼은 기본적으로 다룰 수 있게 돼서 애니메이션 선택 폭이 넓어짐

<br/>

- 문제 상황: 보스의 점프 공격의 Z축이 막히는 현상
- 원인: 여러 부분을 디버깅하면서 캡슐 컴포넌트가 바닥에 붙어있는 것(Location.Z도 고정, Velocity도 고정)을 확인하고 Z축 관련된 모든 옵션을 확인했는데 보스의 점프 준비자세에서 z축이 잠깐 아래로 갔다가 올라오는데 이때 엔진은 보스가 착지했다고 판단(그래서 Jump , Falling 옵션은 불가능)
- 해결방법: 정말 많은 시도 끝에 공중에 있는 동안만 Movement를 Flying으로 바꿔서 해결
- 배운 점: 눈에 보이지 않는 부분이지만 이러한 미세한 차이가 엔진에서는 전혀 다르게 동작을 한다는 걸 알았고 조금 더 시야가 넓어짐

<br/>

- 문제 상황: Motion Warping을 사용해서 점프 거리를 늘릴 때 보스가 뒤로 튀어 나갔다가 다시 앞으로 튀어나가는 현상
- 원인: 보스가 점프 할 때 양 팔을 뒤로 젖히는데 이 때 미세하게 보스의 특정부분이 뒤로간다고 판단해서 거리를 늘린 만큼 순간적으로 뒤로 튀어갔다가 양팔을 젖히는 모션이 끝나면 앞으로 튀어 나가게 됨
- 해결방법: 이 부분은 애니메이션을 직접 수정해야해서 Scale 옵션을 X, Y, Z축을 각자 조절하여 적절한 점프 높이, 거리를 만들어내서 해결
- 배운 점: 위와 같은 느낌으로 미세한 부분에서 비정상적인 동작이 만들어짐을 또 느꼈고 프로그래머라서 부드러운 애니메이션에 대한 욕심은 좀 포기해야겠음


4.기술적 의사 결정   

**상황**

프로젝트 후반부에 플레이어 피격 기능, 몬스터의 공격기능이 없는 걸 확인 후 전투 담당인원과 추가할지 말지 결정

**선택지**

1. 한명이 좀비, 보스 부분을 다 맡기
2. 서로 나눠서 하기

**선택한 방법과 이유**

나는 보스를 계속 구현했기 때문에 보스의 공격 애니메이션과 플레이어 피격 기능을 합치고 일반 좀비는 전투 담당이 맡음

**결과**

생각보다 더 빠르게 구현이 완료됨

<br/>

챕터3 개인 회고 작성 완료   


  </p>
</details>

#### <!-- 26.05.29 -->
<details> 
  <summary>26.05.29</summary>
  <p>

에이타니 퀴즈 정리   

UnrealBuildTool(UBT)은 C++ 코드를 바이트코드로 변환하지 않습니다. 언리얼 C++는 네이티브 코드로 컴파일되며, 가상 머신에서 실행되지 않습니다.

**<오브젝트 풀링이란?>**   

오브젝트 생성, 파괴를 한꺼번에 할 때면 CPU에 부담이 엄청 가게된다.   

모든 기능을 다 끄고(Tick, Visible 등등) 총알 수백발을 미리 생성해둔다.(추적 컴포넌트는 부착하지 않은 상태)   

쓰는 순간 기능을 켜주고(컴포넌트도 부착) 총알이 사라져야할때 다시 기능을 다 끄고 원래 총알 모아둔곳에 다시 보관을 해줘서 생성, 소멸 자체를 하지 않아 부하를 없앤다.    

구조   
MyObjectPool -> Actor ( Manager )   
PooledObject -> Component ( 추적용도 )   
PooledObjectData -> None ( 파라미터용 )   

```cpp
// 오브젝트 생성하는 코드
void AMyObjectPool::BeginPlay()
{
	Super::BeginPlay();
	
	FActorSpawnParameters SpawnParams;

	// 액터의 종류
	for (int32 PoolIndex = 0; PoolIndex < PooledObjectData.Num(); ++PoolIndex)
	{
		// 실제 컴포넌트가 들어갈 공간
		FSingleObjectPool CurrentpoolIndex;

		// 이름 정해주기
		SpawnParams.Name = FName(FString::Printf(TEXT("%s"), *PooledObjectData[PoolIndex].ActorName));

		// 내가 직접 생성한 이름을 최대한 사용해달라(규칙 만들기)
		SpawnParams.NameMode = FActorSpawnParameters::ESpawnActorNameMode::Requested;
		SpawnParams.SpawnCollisionHandlingOverride = ESpawnActorCollisionHandlingMethod::AlwaysSpawn;

		// 액터 하나당 몇개를 만들어줄지
		for (int32 ObjectIndex = 0; ObjectIndex < PooledObjectData[PoolIndex].PoolSize; ++ObjectIndex)
		{
			// 스폰
			AActor* SpawnedActor = GetWorld()->SpawnActor(
				PooledObjectData[PoolIndex].ActorTemplate,
				&FVector::ZeroVector,
				&FRotator::ZeroRotator,
				SpawnParams
			);

			// 외부 이름 재설정
			SpawnedActor->SetActorLabel(SpawnedActor->GetName());

			// UObject 타입은 NewObject로
			UPooledObject* PoolComp = NewObject<UPooledObject>(SpawnedActor);
			// 기능적 컴포넌트를 등록
			PoolComp->RegisterComponent();
			// 특정 액터의 소유 확정(컴포넌트 붙이기)
			SpawnedActor->AddInstanceComponent(PoolComp);
			// MyObjectPool을 넘겨줌
			PoolComp->Init(this);

			// 방금 만들어준 컴포넌트를 저장
			CurrentpoolIndex.PooledObjects.Add(PoolComp);

			// 이제 액터를 안보이게 만들어줄차례
			SpawnedActor->SetActorHiddenInGame(true);
			SpawnedActor->SetActorEnableCollision(false);
			SpawnedActor->SetActorTickEnabled(false);
			SpawnedActor->AttachToActor(this, FAttachmentTransformRules::SnapToTargetNotIncludingScale);

		}

		// 컴포넌트 뭉치 저장
		Pools.Add(CurrentpoolIndex);
	}
}
```

  </p>
</details>

#### <!-- 26.06.01 -->
<details> 
  <summary>26.06.01</summary>
  <p>

BindWidget   
순수 가상함수처럼 강제로 정의하게 만드는 키워드   
키워드가 붙은 UPROPERTY 변수가 자식 블루프린트에 강제로 존재하게 함    

```cpp
// 이게 붙으면 자식 위젯 블루프린트에 똑같은 UEditableTextBox가 강제됨
// 이 상태로 에디터에 가서 WBP를 만들면 컴파일에 '!'가 떠있음.   
// EditableTextBox를 만들어서 EditableTextBox_ChatInput라고 이름을 바꾸고 IsVariable 체크하고 컴파일하면 끝
UPROPERTY(meta = (BindWidget))
TObjectPtr<UEditableTextBox> EditableTextBox_ChatInput;
```

<br/>

UI 델리게이트 바인드 하기   

```cpp
if (EditableTextBox_ChatInput->OnTextCommitted.IsAlreadyBound(this, &ThisClass::OnChatInputTextCommitted) == false)
{
	EditableTextBox_ChatInput->OnTextCommitted.AddDynamic(this, &ThisClass::OnChatInputTextCommitted);
}
```

<br/>

채팅창 Enter 기능

```cpp
void UCXChatInput::OnChatInputTextCommitted(const FText& Text, ETextCommit::Type CommitMethod)
{
	if (CommitMethod == ETextCommit::OnEnter)
	{
		// 엔터를 친 플레이어를 가져옴 GetOwningPlayer()
		APlayerController* OwningPlayerController = GetOwningPlayer();
		if (IsValid(OwningPlayerController) == true)
		{
			ACXPlayerController* OwningCXPlayerController = Cast<ACXPlayerController>(OwningPlayerController);
			if (IsValid(OwningCXPlayerController) == true)
			{
				OwningCXPlayerController->SetChatMessageString(Text.ToString());

				// 빈 텍스트로 밀어주기
				EditableTextBox_ChatInput->SetText(FText());
			}
		}
	}
}
```

<br/>

채팅/로그 동시 출력   

```cpp
#include "Kismet/KismetSystemLibrary.h"

UKismetSystemLibrary::PrintString(this, ChatMessageString, true, true, FLinearColor::Red, 5.0f);
```

<br/>

서버의 구조   

1.P2P(Peer To Peer Server)   
다크소울, 토렌트같은 서버   
각각의 컴퓨터가 클라이언트이자 서버인 구조   

2.Listen Server   
클라이언트이자 서버인 방장(Host)이 있고, 나머지 참가자(Guest)는 모두 클라이언트 역할만 맡는 형태   
P2P의 일종이라고도 볼 수 있고 마크, 어몽어스 등이 있음   

3.Dedicated Server   
서버를 담당하는 컴퓨터가 따로 있다.   
대부분의 한국온라인 게임들이 가지고 있는 형태   

**서버 프로세스의 실행**   
PIE(Play In Editor)를 했거나, Server.exe를 수동으로 실행하는 식으로 서버 프로세스 실행   
실행할 때 Open {Level이름}?Listen  명령어가 인자로 전달된다. 그리고 해당 Level을 열어둔다.   
이때 Socket이 생성되며 다른 PC가 접속 가능하게끔 한다. Listen 명령어가 없다면 싱글플레이다.   

**서버와 GameMode**   
Level에는 WorldSettings 속성이 있고, WorldSettings에는 GameMode와 GameState 정보가 있다.   
이를 통해 GameMode와 GameState 액터를 생성한다.   
중요한 것은 GameMode 액터는 전체 컴퓨터에서 딱 한 곳(Server)에만 존재한다는 것.   
그래서 GameMode와 Server를 동일시해도 된다.   

**클라이언트와 서버**   
클라이언트는 서버의 IP주소와 포트번호로 접속 시도. 서버는 접속 시도하는 클라이언트에게 Level 정보를 넘긴다.   
클라이언트도 해당 Level을 열고, Level을 여는데 성공했다고 데디 서버에게 알린다.   

Level을 여는데 성공한 클라이언트(Client1) 전용 PlayerState, PlayerController, PlayerCharacter가 서버에 생성된다.   
이것이 다시 Client1에 복제된다. GameState도 복제된다.

**여러 클라이언트와 서버**   
또 다른 클라이언트도 접속. 마찬가지로 서버는 접속 시도하는 또 다른 클라이언트에게 Level 정보를 넘긴다.   
클라이언트도 해당 Level을 열고, Level을 여는데 성공했다고 데디 서버에게 알린다.   

Client2 전용 PlayerState, PlayerController, PlayerCharacter가 서버에 생성된다.   
이것이 다시 Client2에 복제된다. GameState도 복제된다.    
이때, 클라이언트 간의 PlayerState와 PlayerCharacter도 복제되면서 서로가 보이게 된.   

<br/>

Visual Studio에서 코드 베이스가 엄청 많아지면 Ctrl + T로 찾으면 된다.   
자동완성 사라지면 Ctrl + SpaceBar   

<br/>

멀티 세팅을 안해줬는데 타 클라이언트에서 채팅이 보이는 현상   
-> 마치 온라인 게임에서 남이 죽었는데 내 UI에 죽었다고 뜨는 것과 같음   

```cpp
// 위젯 객체는 Owning Client에서만 생성되면 됨
// Owning == Local 이라고 보면 된다.
// 이렇게 IsLocalController를 호출해서 Owning Client를 판별한다.
if (IsLocalController() == false)
	{
		return;
	}

```

<br/>

**NetMode**   
로직이 서버에서 돌고 있는지 클라에서 돌고 있는지 알아야 하는데 그때 필요한 것이 `NetMode`이다.   

**NetConnection 이란?**   
- 다른 PC와의 연결이 발생하면 그에 대응하는 `UNetConnection` 객체도 생성   
- 서버에 클라이언트가 접속하면 서버에는 `ClientConnection` 객체 추가   
- 클라이언트에는 `ServerConnection` 객체 생성
- 두 PC는 `UNetConnection` 객체를 통해 통신
- `UNetDriver`는 생성된 `UNetConnection` 객체를 소유하고 관리
- 서버 PC에 생성된 `UNetDriver`는 접속한 클라이언트의 수 만큼 `UNetConnection`을 관리
- 클라이언트 PC에 생성된 `UNetDriver`는 `ServerConnection` 단 하나만을 관리

**NetDriver**   
- 언리얼 네트워크 통신에서 로우레벨 동작들을 관리하는 클래스
- 싱글플레이에서는 `UNetDriver` 객체가 생성되지 않음
- 멀티플레이에서만 `UWorld::Listen()` 함수를 통해 `UNetDriver` 객체 생성
- 멀티플레이에 참여하는 각 PC마다 `UNetDriver` 객체 생성

<br/>

```cpp
// UNetDriver.h

UCLASS(...)
class UNetDriver : public UObject, public FExec
{
	...
	
	/** Connection to the server (this net driver is a client) */
	UPROPERTY()
	TObjectPtr<class UNetConnection> ServerConnection;
	// ServerConnection는 딱 하나

	/** Array of connections to clients (this net driver is a host) - unsorted, and ordering changes depending on actor replication */
	UPROPERTY()
	TArray<TObjectPtr<UNetConnection>> ClientConnections;
	// ClientConnections 복수형이다. 클라는 여러개라서
	...

}

// ServerConnection이 nullptr이고 ClientConnections만 가지고 있다면?
// -> 해당 NetMode는 서버
```

<br/>

**언리얼에서의 OwnerShip**   

- 하나의 `ClientConnection`은 하나의 `PlayerController`를 소유
- `PlayerController`의 **Owning Connection**은 `ClientConnection`
- `PlayerController`가 빙의하는 폰의 `Owner` 속성은 해당 `PlayerController`로 설정
- 폰에 무기 액터가 생성되고, 무기 액터의 `Owner` 속성에 해당 폰을 설정할 수도 있다.
- `ClientConnection`에서부터 무기 액터에 이르는 소유 관계를 패밀리라고도 부른다.
- 소유 관계 속에 있는 액터가 본인의 **Owning Connection**을 얻으려면 
`AActor::GetNetConnection()` 함수를 호출하면 됩니다.
- 이 소유 관계가 후에 배울 **RPC**와 **Property Replication**과 관련됨

<br/>

멀티플레이 디버깅용 나만의 출력 만들기(모듈)   

```cpp
// ChatX.h

#pragma once

#include "CoreMinimal.h"

class ChatXFunctionLibrary
{
public:
	// static이라서 ChatXFunctionLibrary 객체가 없어도 호출 가능
	// InWorldContextActor 가져올 월드에 있는 어떤 액터를 넣어도 알아서 월드를 찾아줌 단, nullptr이면 안됨
	static void MyPrintString(const AActor* InWorldContextActor, const FString& InString, float InTimeToDisplay = 1.f, FColor InColor = FColor::Cyan)
	{
		if (IsValid(GEngine) == true && IsValid(InWorldContextActor) == true)
		{
			// 클라나 ListenServer를 위한 출력
			if (InWorldContextActor->GetNetMode() == NM_Client || InWorldContextActor->GetNetMode() == NM_ListenServer)
			{
				GEngine->AddOnScreenDebugMessage(-1, InTimeToDisplay, InColor, InString);
			}
			else // dedicated server를 위한 로그(콘솔창이라 로그만 가능)
			{
				UE_LOG(LogTemp, Log, TEXT("%s"), *InString);
			}
		}
	}
	// static이라서 ChatXFunctionLibrary 객체가 없어도 호출 가능
	static FString GetNetModeString(const AActor* InWorldContextActor)
	{
		FString NetModeString = TEXT("None");

		if (IsValid(InWorldContextActor) == true)
		{
			ENetMode NetMode = InWorldContextActor->GetNetMode();
			if (NetMode == NM_Client)
			{
				NetModeString = TEXT("Client");
			}
			else
			{
				if (NetMode == NM_Standalone)
				{
					NetModeString = TEXT("StandAlone");
				}
				else // Listen or Dedicated Server(지금 배우고있는 DedicatedServer일 때 출력) 
				{
					NetModeString = TEXT("Server");
				}
			}
		}

		return NetModeString;
	}
};


// 로그 찍을 곳에 헤더 추가
#include "ChatX.h"

void ACXPlayerController::PrintChatMessageString(const FString& InChatMessageString)
{
	//UKismetSystemLibrary::PrintString(this, ChatMessageString, true, true, FLinearColor::Red, 5.0f);
	
	FString NetModeString = ChatXFunctionLibrary::GetNetModeString(this);
	FString CombinedMessageString = FString::Printf(TEXT("%s: %s"), *NetModeString, *InChatMessageString);
	ChatXFunctionLibrary::MyPrintString(this, CombinedMessageString, 10.f);
	// 문제 상황이 생기면, 위와 같은 로깅 함수로 다양한 변수의 값들과 함수이름을 확인해서 
	// 문제의 원인을 적극적으로 찾아보세요!
}

// 서버/클라에 맞게 출력이 됨
```

<br/>

**Authority와 Proxy**   

서버에 스폰 된 액터가 가진 **`NetRole`** 속성 값은 언제나 **`Authority`**다.
다시 말해, 서버에 스폰 된 액터에서 수행될 로직은 **“권한을 가지고 있다”**를 뜻한다.
그러니 게임에 중대한 영향을 끼치는 로직은 `NetRole`이 `Authority`일 때 수행해야 한다.   

`NetRole`이 `Authority`인 액터가 클라이언트로 복제되었을 때(`Replicated`),
클라이언트에 복제된 액터의 `NetRole` 속성 값은 `Proxy`다.
"**허상**"이라는 뜻이다.

여기서는 중요한 로직을 수행하면 안 된다.   

<br/>

**Local Role과 Remote Role**   

게임에 중대한 영향을 끼치는 로직을 작성하기 위해, 
해당 액터가 현재 어느 PC에 스폰 되어서 로직이 돌고 있는지 구분해야 한다.   

이를 구분하기 위해 현재 동작하는 컴퓨터에서의 롤을 **로컬 롤(Local Role)**,
커넥션으로 연결된, 반대편 컴퓨터에서의 롤을 **리모트 롤(Remote Role)**이라고 한다.   

`Server`의 Actor가 `Authority`라는 `Local Role`을 가지고 있고 `Autonomous`라는 `Remote Role`을 가지고 있으면 `Client`는 반대로 `Autonomous`라는 `Local Role`을 가지고 있고 `Authority`라는 `Remote Role`을 가지고 있다.

<br/>

**NetRole 종류**   

**None**

- 보통의 경우, 레플리케이션 되지 않는 액터를 뜻한다. 다만, 무조건적이진 않다.
- ex) LocalRole은 Authority이고 RemoteRole이 None이라면
서버에서 스폰 되고, 클라쪽으로 레플리케이션 되지 않는 액터라고 볼 수 있다.

**Authority**

- 게임에 중대한 영향을 끼칠 수 있는 권한을 가진 액터를 뜻한다.
- 서버에서 스폰된 액터가 LocalRole으로 Authority를 가질 수 있다.
- **ex)** `GameMode`

**Autonomous Proxy**

- Authority 액터의 복제본이다.
서버로부터 데이터를 수신 받아서 동기화도 되면서, 서버로 송신도 가능하다.
- **ex)** `PlayerController`

**Simulated Proxy**

- Authority 액터의 복제본이다.
서버로부터 수신 받아서 동기화 당하기만 한다.
- **ex)** 내 화면에 보이는 친구의 `PlayerCharacter`


<br/>

**Role 디버깅**   

아까 만들었던 디버깅 모듈에 추가해주면 된다.   
```cpp
static FString GetRoleString(const AActor* InActor)
{
	FString RoleString = TEXT("None");

	if (IsValid(InActor) == true)
	{
		FString LocalRoleString = UEnum::GetValueAsString(TEXT("Engine.ENetRole"), InActor->GetLocalRole());
		FString RemoteRoleString = UEnum::GetValueAsString(TEXT("Engine.ENetRole"), InActor->GetRemoteRole());

		RoleString = FString::Printf(TEXT("%s / %s"), *LocalRoleString, *RemoteRoleString);
	}

	return RoleString;
}
```

<br/>

**폰의 소유에 따른 서버 로그 변화**   

```cpp
[2026.06.01-11.31.04:144][ 56]LogTemp: CXPawn::BeginPlay() Server [ROLE_Authority / ROLE_SimulatedProxy]
[2026.06.01-11.31.04:144][ 56]LogTemp: CXPawn::PossessedBy() Server [ROLE_Authority / ROLE_AutonomousProxy]
```

`Pawn`이 `빙의(Possessed)`가 된 후에 `Ownership`이 설정되고 특정 `Controller`의 소유가 되고 또 컨트롤러는 `Connection`의 소유가 됨. 즉, 하나의 `패밀리`가 됐다는걸 알 수 있음.   
마지막으로 이 패밀리에 액터가 들어가면 `Autonomous Proxy`가 된다.   

<br/>

**서버에서 스폰 된 캐릭터 B관련 설명 중...**   

궁금한 점
1. Possessed가 안된다고 했는데 AIController를 OnPossessed() 할 수 있지 않나?
2. 서버에서 스폰된 캐릭터가 클라이언트에서 접속한 내 눈에 보이려면 Replicated가 되어야 하는거 아닐까?


  </p>
</details>

#### <!-- 26.06.02 -->
<details> 
  <summary>26.06.02</summary>
  <p>

언리얼 사운드   
SoundBase는 언리얼 엔진에서 모든 사운드 에셋의 기본 클래스다. SoundWave는 단일 오디오 파일(.wav)로 간단한 짧은 효과음이나 UI 사운드에 적합하며, SoundQueue(또는 SoundCue)는 여러 사운드 조합, 페이드, 블렌딩 등 동적 처리가 필요한 상황에 적합하다.

<br/>

**Remote Procedure Call(RPC)**   

함수를 호출하는 PC와 실행하는 PC가 달라도 되게끔 해주는 통신 기법   

**Call과 Invoke**   

Call   
- 정적인 의미를 가진다.
- 컴파일 타임에 어떤 함수인지, 호출하는 곳과 실행하는 곳이 정해져야 한다.
- 지금까지 정의했던 일반적인 전역 함수와 멤버 함수가 이에 해당된다.
즉, **직접적으로** 함수를 **호출하고 실행**해야 한다. (Direct)   

Invoke   
- 동적인 의미를 가진다.
- 런타임에 어떤 함수인지, 호출하는 곳과 실행하는 곳이 어딘지 정해진다.
- 예를 들어, 함수 포인터, 동적 바인딩, RPC 같은 개념들이 이에 해당된다.
- 즉, **간접적으로** 함수를 **호출하고 실행**해야 한다. (Indirect)
RPC도 마찬가지로 "**RPC를 Invoke**"라고 표현한다.   

<br/>

**NetMulticast**   
"서버를 포함한 모든 클라이언트에서 해당 RPC를 실행시켜야"한다 라는 요청을 나타내야 한다.   

**Server**   
"서버에서 해당 RPC를 실행시켜야 한다"라는 요청을 나타내야 한다.

**Client**   
"클라이언트에서 해당 RPC를 실행시켜야 한다"라는 요청을 나타내야 한다.   

<br/>

**RPC가 클라이언트에서 호출되고 서버에서 실행되어야 하는 경우에는 `Server` 키워드를 사용해야 한다.**   

- `ClientConnection`이 소유하고 있는 액터(Client-Owned)에서 RPC가 호출되어야 한다.
- `_Validate()` 함수에서 RPC를 실행할지 말지 결정된다.


**RPC가 서버와 모든 클라이언트에서 실행되어야 하는 경우에는 `NetMulticast` 키워드를 사용해야 한다.**

- 서버에서 호출해야 한다.
- 부하가 심하므로, 빈번하게 호출되게끔 코드를 작성하는 건 권장되지 않는다.
ex) Tick() 함수 내에서 NetMulticast RPC 호출.

**RPC가 서버에서 호출되고 클라이언트에서 실행되어야 하는 경우에는 `Client` 키워드를 사용해야 한다.**

- 서버에서 호출해야 한다.

**WithValidation**   

`UFUNCTION()` 매크로와 함께 사용되는 키워드다.
서버에서 실행되는 RPC의 경우에 해당 키워드를 작성하는 것이 권장된다.

이 키워드가 붙은 RPC를 구현 할때는 `_Implementation()` 함수와 `_Validate()` 함수로 나뉘어 진다.

`_Validate()` 함수는 해당 RPC가 서버에서 실제로 실행할지 말지를 결정한다.

서버 실행 로직은 무조건적으로 신뢰되기 때문에, 위변조를 막기 위한 방어막 역할을 한다.

<br/>

**Unreliable VS Reliable**    

`UFUNCTION()` 매크로와 함께 사용되는 키워드다.

RPC는 기본적으로 **Unreliable** 키워드를 기준으로 동작한다. 아무것도 안쓰면 Unreliable이다.

**Unreliable**은 원격 PC에서 무조건 실행되리라는 보장은 없다.

반면, 원격 PC에서 무조건 실행되어야 하는 로직이라면 **Reliable** 키워드를 작성한다.


**Unreliable**의 활용 예시

- 코스메틱(이펙트, 사운드 등)처럼 게임에 큰 영향이 없는 로직.

**Reliable**의 활용 예시

- 충돌, 데미지, 스폰처럼 게임에 큰 영향을 끼치는 로직.


  </p>
</details>

#### <!-- 26.06.04 -->
<details> 
  <summary>26.06.04</summary>
  <p>

**TCP와 UDP**   

TCP (Transmission Control Protocol)   
"정확하고 안전하게, 순서대로 전달한다." (연결 지향형)

TCP는 데이터의 신뢰성을 최우선으로 생각하는 프로토콜입니다. 데이터를 보내기 전에 송신측과 수신측이 서로 연결을 확인하는 과정을 거칩니다.

- 연결 지향 (3-Way Handshake): 데이터를 보내기 전, "보내도 돼?", "응 준비됐어", "그럼 보낸다!"라는 3번의 신호 교환을 통해 안전한 연결을 먼저 수립합니다.

- 높은 신뢰성과 순서 보장: 데이터가 중간에 유실되면 다시 재전송(ARQ)을 요청하고, 데이터가 뒤죽박죽 도착해도 원래 순서대로 조립해 줍니다.

- 흐름 제어 및 혼잡 제어: 수신자가 처리할 수 있는 속도에 맞춰 데이터 양을 조절(흐름 제어)하고, 네트워크가 혼잡하면 전송 속도를 늦춥니다(혼잡 제어).

단점: 안전장치가 많은 만큼 UDP에 비해 속도가 느리고 오버헤드(추가적인 부담)가 큽니다.

주요 사용처
- 웹 서핑 (HTTP/HTTPS)

- 파일 전송 (FTP)
  
- 이메일 (SMTP)

텍스트 데이터나 파일처럼 단 1비트의 데이터 손실도 용납되지 않는 곳에 사용됩니다.

UDP (User Datagram Protocol)   
"안전한 건 모르겠고, 일단 빠르게 던진다!" (비연결 지향형)

UDP는 신뢰성보다는 속도와 실시간성을 최우선으로 생각하는 프로토콜입니다. 일방적으로 데이터를 던지는 방식을 취합니다.

- 비연결 지향: 사전 연결 수립 과정(Handshake)이 없습니다. 그냥 상대방의 주소만 알고 있으면 데이터를 바로 보냅니다.

- 신뢰성 없음 (Handshake 없음, 재전송 없음): 데이터가 중간에 사라지거나 순서가 뒤바뀌어도 신경 쓰지 않습니다. 확인 작업(ACK)도 하지 않습니다.

- 가볍고 빠름: 기능이 단순한 만큼 헤더가 가볍고, 지연 시간(Latency)이 거의 없어 속도가 매우 빠릅니다.

- 1:N 통신 가능: 일대일(Unicast)뿐만 아니라, 일대다(Multicast), 전체 방송(Broadcast) 통신이 가능합니다.

주요 사용처
- 실시간 스트리밍 (유튜브 라이브, 넷플릭스 등)

- 온라인 게임 (실시간 위치 동기화 등)

- 보이스톡 / 영상통화 (VoIP)

- DNS (Domain Name System) 조회

영상이나 음성처럼 데이터가 아주 약간 깨지거나 유실되더라도(끊김 현상 등) 실시간 흐름이 더 중요한 곳에 사용됩니다.

<br/>

**스택과 힙 공부**   

굉장히 기초적이지만 중요한 내용이라서 쭉 정리해서 한 번 공부를 해봤다.   

스택(Stack)   
스택은 지역변수, 매개변수, 리턴값 등이 저장되는 공간입니다. 구조적으로 후입선출방식(LIFO)을 따릅니다.   
메모리가 자동으로 관리되고 메모리 할당, 해제 속도가 매우 빠릅니다.(CPU가 Stack Pointer Register를 사용)   
컴파일 시점에 크기가 결정되며(정적 크기) 공간이 그리 크지 않아서 함수 호출이 너무 깊어지거나 공간을 초과하면 Stack Overflow가 발생합니다.

힙(Heap)   
힙은 개발자가 필요에 따라 동적으로 메모리를 할당하는 공간입니다.(new, malloc)   
개발자가 직접 데이터의 생명 주기를 제어합니다.(할당 이후엔 반드시 해제를 해줘야합니다. 하지 않으면 Memory Leak(메모리 누수)발생)   
빈 메모리 공간을 찾고 할당하는 과정(할당 알고리즘)이 필요하고 포인터를 거쳐 접근해야 하므로 스택보다 속도가 느립니다.   
런타임에 크기가 결정되며(동적) 스택에 비해 큰 메모리 공간을 사용할 수 있지만 메모리 단편화(Fragmentation)가 될 수 있다는 단점이 있습니다.   

스택은 메모리의 높은 주소 -> 낮은 주소 / 힙은 낮은 주소 -> 높은 주소 방향으로 채워집니다.   

스택 포인터 레지스터(Stack Pointer Register, SP)   
현재 스택 영역에서 가장 최근에 데이터가 쌓인 위치(꼭대기, Top)의 메모리 주소를 가리키고 있습니다.   
데이터를 Push하면 SP의 주소 값을 감소합니다.(스택은 높은주소 -> 낮은 주소 방향으로 채워지기 때문)   

힙의 빈 메모리 공간 찾기 및 할당 과정   
힙은 크기가 제각각인 데이터가 중구난방으로 들어옵니다. 따라서 운영체제(OS)와 메모리 할당자(Allocator)는 힙 영역 내의 사용중인 블록과 비어 있는 블록(Free Block)을 관리하는 리스트(Free List)를 유지합니다.   
최초 적합(First Fit)   
힙의 처음부터 탐색하다가, 요청한 크기보다 크거나 같은 빈 공간을 발견하는 순간 바로 할당합니다.(탐색속도가 빠름)   
최적 적합(Best Fit)   
힙 전체를 싹 다 뒤져서, 요청한 크기와 차이가 가장 적은 빈 공간을 찾아 할당합니다.   
내부 파편화를 최소화 할 수 있지만 시간이 오래 걸립니다.   
최악 적합(Worst Fit)   
힙에서 가장 크기가 큰 빈공간에 할당하고 남은 큰 공간을 다시 Free List에 넣습니다.   
데이터 재활용에 좋지만 느립니다.    

메모리 단편화(Memory Fragmentation)   
힙에서 메모리를 할당, 해제를 반복하다보니 메모리 공간은 남아있는데 할당을 하지 못하는 비효율적인 상태를 말합니다.   
외부 단편화(External Fragmentation)   
중간중간 비어있는 공간의 총 합은 큰데, 그 비어있는 공간들이 새로운 메모리를 할당하기엔 크기가 충분하지 않아서 할당을 못하는 상태입니다.   
예시) 총 10mb의 공간이 있지만 2mb씩 쪼개져있다고 한다면 5mb짜리 큰 메모리는 할당하지 못합니다.   
내부 단편화(Internal Fragmentation)   
메모리 할당자가 고정된 블록 단위(예: 8, 16바이트)로 메모리를 건네주다 보니, 실제 요청한 크기보다 더 큰 메모리가 할당되어 낭비되는 공간이 생기는 상태입니다.   
예시) 내부적으로 16바이트 단위로만 할당하는데 개발자가 12바이트만 요청하면 남은 4바이트는 낭비되는 공간이 됩니다.   


  </p>
</details>

#### <!-- 26.06.05 -->
<details> 
  <summary>26.06.05</summary>
  <p>

마스터 과제 중 좀비 100킬 퀘스트를 같은 파티원이랑 할 수 있게 하는 기능이 있는데 이걸 위해 PlayerState를 알아봤다.   

```cpp
//PlayerState.h
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/PlayerState.h"
#include "MyPlayerState.generated.h"

UCLASS()
class ZOMBIEPRACTICE_API AMyPlayerState : public APlayerState
{
	GENERATED_BODY()
	
public:
	AMyPlayerState();

	void SetPartyID(int32 NewPartyID);
	int32 GetPartyID() const;

private:
	// 기본값은 -1
	UPROPERTY(VisibleAnywhere, Category = "Party")
	int32 PartyID = -1;
};

//PlayerState.cpp
#include "MyPlayerState.h"

AMyPlayerState::AMyPlayerState()
{
}

void AMyPlayerState::SetPartyID(int32 NewPartyID) 
{ 
	PartyID = NewPartyID;
}

int32 AMyPlayerState::GetPartyID() const 
{ 
	return PartyID; 
}
```

간단하게 PartyID를 관리하고 캐릭터 생성 시 각 캐릭터마다 PartyID를 설정(이 부분은 캐릭터에서 해줌)    

<br/>

**레플리케이션(Replication)**   

생성된 액터의 정보를 네트워크 내 다른 클라이언트에게 복제하는 작업을 레플리케이션이라고 한다.   

서버-클라이언트 모델에서는 서버에서 클라이언트로 복제되는 것이 기본 규칙이다.   

레플리케이션의 두가지 방법   
- RPC(Remote Procedure Call)
- Property Replication
  

Property Replication   

우리가 원하는 속성만 다른 클라이언트에게 복제하는 것을 `Property Replication`라고 한다.   
항상 `Authority`에서 `Proxy`로만 복제가 가능하다.   

**Property Replication 설정 방법**   

1. 액터의 `bReplicates` 속성을 true로 설정한다.
2. `UPROPERTY()`에 `Replicated` 키워드를 추가한다.
3. `GetLifetimeReplicatedProps()` 함수에 네트워크로 복제할 속성을 추가한다.
   - `#include “Net/UnrealNetwork.h”` 헤더파일 추가한다.
   - `DOREPLIFETIME` 매크로를 사용해 복제할 속성을 명시한다.

<br/>

Ctrl + M O   
VS에서 함수 다 닫기   



  </p>
</details>

#### <!-- 26.06.09 -->
<details> 
  <summary>26.06.09</summary>
  <p>

**Property Replication 설정 방법**   

저번에 공부했던 부분 실제 적용 코드   

```cpp
// .h
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/PlayerState.h"
#include "CXPlayerState.generated.h"

UCLASS()
class CHATX_API ACXPlayerState : public APlayerState
{
	GENERATED_BODY()

public:
	ACXPlayerState();

	virtual void GetLifetimeReplicatedProps(TArray<class FLifetimeProperty>& OutLifetimeProps) const override;

	UPROPERTY(Replicated)
	FString PlayerNameString;

};


// .cpp
#include "CXPlayerState.h"
#include "Net/UnrealNetwork.h" // 추가

ACXPlayerState::ACXPlayerState()
{
	bReplicates = true;
}

void ACXPlayerState::GetLifetimeReplicatedProps(TArray<class FLifetimeProperty>& OutLifetimeProps) const
{
	Super::GetLifetimeReplicatedProps(OutLifetimeProps);

	DOREPLIFETIME(ThisClass, PlayerNameString);
	// ThisClass == ACXPlayerState
}
```

<br/>

**Stack Overflow에 관한 고찰**   

`Stack Overflow`가 왜 발생하는지, 어떻게 해결해야 하는지 여러방면에서 알아봤다.   

1. 원인   
    `Stack Overflow`는 기본적으로 스택 메모리 용량의 부족으로 나타나는 현상이다.   
	무한루프에 빠진 재귀함수, 너무 깊은 함수호출(`Deep Call Stack`), 크기가 너무 큰 지역변수를 Stack 영역에 할당하면 `Stack Overflow`가 발생한다.
2. 해결법   
	재귀 함수의 경우 `Base Case`를 작성하여 무한루프에 빠지지 않게 하고 너무 큰 지역변수는 `Heap`영역에 동적할당을 해준다.   
	`TCO`(Tail Call Optimization, 꼬리 물기 최적화)를 이용해서 무한루프를 원천 차단하는 방법도 있다.   
	마지막으로 `IDE` 설정을 들어가서 `Stack` 크기 자체를 키울 수 있다.   

<br/>

위에서 나온 `TCO`와 `Stack` 크기를 키우는 방법에 대해서 좀 더 자세히 알아봤다.   

1. TCO란?   
	`Tail Call Optimization`(꼬리 물기 최적화)라고 하며 재귀호출시 필요한 연산을 매개변수로 넣어서 오직 호출, 반환만 이뤄지게 하는 방법이다. 이렇게 하면 컴파일러가 스택 프레임을 새로 쌓지 않고 하나의 스택 프레임내에서 변수만 바꾸며 계산을 한다. (내부적으로 While문으로 계산) 따라서 Stack Overflow 자체를 원천 차단할 수 있다.   
	단, 언리얼 엔진에선 스마트 포인터의 경우 함수 반환 시 소멸자를 자동으로 호출해버려 TCO 조건에 맞지 않고 리플렉션 시스템, 가비지 컬렉션 등과 시스템적으로 맞지 않아서 사용하지 않는다.(중간에 다른 함수 호출 없이 반환만 해야하는데 중간에 시스템적으로 개입이 많음)
2. Stack 크기 키우기   
   `Solution Explorer`에서 `ToolChain`을 검색하면 여러 OS 전용 `ToolChain.cs` 파일이 나온다.   
   여기서 내 환경은 MSVC를 사용하기 때문에 `VCToolChain.cs`로 들어가서 `DefaultStackSize`를 찾아서 고쳐준다.   

```cpp
// VCToolChain.cs 원래 코드
// Set the default stack size.
if (LinkEnvironment.Platform.IsInGroup(UnrealPlatformGroup.Microsoft))
{
	if (LinkEnvironment.DefaultStackSize > 0)
	{
		if (LinkEnvironment.DefaultStackSizeCommit > 0)
		{
			Arguments.Add("/STACK:" + LinkEnvironment.DefaultStackSize + "," + LinkEnvironment.DefaultStackSizeCommit);
		}
		else
		{
			Arguments.Add("/STACK:" + LinkEnvironment.DefaultStackSize);
		}
	}
}

// 아래와 같이 수정해서 직접 크기를 지정할 수 있다!
// 10MB로 지정
Arguments.Add("/STACK:10485760");

// 스택 크기 팁
// 5 MB: 5242880 (언리얼 기본값보다 약간 더 여유로운 수준)
// 10 MB: 10485760 (일반적으로 깊은 알고리즘이나 스택 오버플로우 회피용으로 가장 추천)
// 20 MB: 20971520 (정말 대규모 데이터나 비정상적으로 깊은 호출 스택이 필요할 때)
```

<br/>

하.지.만. 중요한건 현재 저렇게 스택 크기를 바꿔도 실제로 적용이 안된다는 것 이다.  

이유는?   
에픽게임즈 런처를 통해 다운받은 언리얼 엔진은 소스코드가 아니라 컴파일이 끝난 바이너리 상태인 실행파일(.exe) 및 DLL(Dynamic Link Library) 파일이다.   
따라서, 나중에 배포를 할 때 풀 패키징 상태에서 가능하다.   
(물론, 간접적으로 바꾸는 방법이 존재한다.)   

```cpp
// 간접적으로 Stack 크기 바꾸는 방법
// Config/DefaultEngine.ini

[/Script/WindowsTargetPlatform.WindowsTargetSettings]
DefaultStackSize=10485760
DefaultStackSizeCommit=10485760
```

<br/>

DLL(Dynamic Link Library)이란?   

런타임중에 `.dll` 파일에 분리해둔 기능이 필요한 순간에만 메모리에 올려서 연결(Link)하는 방법이다.   
메모리를 절약할 수 있고 기능을 나누기 때문에 부분적으로 업데이트가 가능하다.   


  </p>
</details>

#### <!-- 26.06.10 -->
<details> 
  <summary>26.06.10</summary>
  <p>

**DP의 4단계 프레임**   

1. 상태 정의   
   DP가 무엇을 뜻하는지 한 문장으로
2. 점화식   
   작은 DP들로 큰 DP를 표현
3. 초기값   
   가장 작은 경우를 직접 정함
4. 답   
   어디서 정답을 꺼낼지

**LCS와 편집거리**   

LCS(Longest Common Subsequence)   
최장 공통 부분 수열   
같으면 대각선 + 1   
다르면 max(위, 왼쪽)   
선택지 2개   

편집 거리(Edit Distance)   
문자열 A를 문자열 B로 바꾸기 위해 필요한 최소 연산 횟수를 구하는 알고리즘   
같으면 대각선 그대로   
다르면 1 + min(위, 왼쪽, 대각선)   
선택지 3개 (삭제, 삽입, 교체)   

`LCS`가 같은문자면 +1   
`편집 거리`는 다른문자면 +1   
구조는 형제처럼 닮음   

LIS (Longest Increasing Subsequence)   
최장 증가 부분 수열   
이전 전부 훑어서 확인, "나보다 앞에 있고 작은것중 제일 큰 것"   
시간복잡도 O(n^2)   

<br/>

프로세스와 스레드 관련해서 찾다보니 컨텍스트 스위칭(Context Switching)이 나와서 찾아봤다.   

**컨텍스트 스위칭(Context Switching)이란?**   
CPU가 한 프로세스(또는 스레드)에서 다른 프로세스로 전환하여 실행할 때, 기존의 상태를 저장하고 새로운 상태를 불러오는 과정을 말합니다.   

**그러면 여기서 `Context`란 무엇을 의미하는걸까?**   
컨텍스트(문맥)는 "CPU가 해당 프로세스를 실행하기 위해 필요한 모든 제어 정보"를 의미합니다. CPU는 다른일을 하러 가기전에 무슨 작업을 했는지 저장을 해놓아야합니다.   
이 정보들은 PCB(Process Control Block)라는 공간에 저장됩니다.   
- PC(Program Counter): 다음번에 실행할 코드의 주소
  
- CPU 레지스터 상태: 현재 연산 중이던 데이터값들
  
- 메모리 관리 정보: 페이지 테이블, 세그먼트 테이블 정보 등
  
- 프로세스 상태: 실행(Running), 준비(Ready), 대기(Waiting) 등

**컨텍스트 스위칭의 작동 과정**   
1. A의 상태 저장: CPU 레지스터에 있던 프로세스 A의 작업 데이터를 A의 PCB에 저장합니다.

2. 스케줄러 작동: OS의 스케줄러가 다음에 실행할 프로세스로 B를 선택합니다.

3. B의 상태 복원: B의 PCB에 저장되어 있던 이전 작업 데이터를 CPU 레지스터로 불러옵니다.

4. 실행: CPU는 프로세스 B가 마지막으로 멈췄던 지점(PC 주소)부터 다시 실행합니다.

컨텍스트 스위칭은 비용이 발생합니다. 이는 프로세스와 스레드에서 다르게 나타납니다.   

**프로세스 컨텍스트 스위칭(비용 높음)**   
서로 독립적인 메모리 공간을 가지고 있어서 CPU 캐시 메모리를 비워야하는 캐시 플러시(Cache Flush)가 일어납니다. 또한 가상 메모리 주소를 물리 주소로 바꾸는 TLB(Translation Lookaside Buffer) 캐시도 초기화 되어 속도가 느려집니다.   

**스레드 컨텍스트 스위칭(비용 낮음)**   
Stack을 제외한 메모리 공간을 공유하기 때문에 속도가 빠릅니다.   

**정리**   
컨텍스트 스위칭은 우리에게 부드러운 멀티태스킹 환경을 제공해 주는 고마운 기능이지만, 자주 발생하면 (잦은 스레드/프로세스 교체) 오버헤드가 커져서 컴퓨터 전체의 성능이 떨어지는 시스탬 병목 현상(Thrashing)이 발생할 수 있습니다.   


  </p>
</details>

#### <!-- 26.06.11 -->
<details> 
  <summary>26.06.11</summary>
  <p>

어제 컨텍스트 스위칭을 알아보면서 예전에 배운 `Cache`를 복습하고 컨텍스트 스위칭에 적용하고 조금 더 깊게 살펴봤다.      

1. CPU는 Ram에서 데이터를 뭉탱이로 긁어와서 Cache에 저장한다.(`Cache Line`)   
2. Cache에서 필요한 값을 레지스터로 복사해온다.(`Load`)   
3. CPU 내부의 연산장치(`Arithmetic Logic Unit, ALU`)가 연산을 하고 다른 레지스터에 저장을 한다.(`Execute`)   
4. 레지스터에 있는 결과값을 캐시나 메모리로 보낸다.(`Store`)   
   
위 처럼 CPU는 Cache에서 자주 쓰는 데이터를 가져다 쓰는데(`Cache Hit`) 이게 제대로 되지 않으면 다시 `Ram`까지 가서 데이터를 긁어와야한다.(`Cache Miss`)   

프로세스의 스위칭 같은 경우 서로다른 가상 메모리 공간을 사용하기 때문에 기존 캐시 메모리가 쓸모가 없다. 따라서 기존 캐시 메모리를 비우고(`Cache Flush`) 새로운 캐시 메모리에 다시 긁어와야해서 `Cache Miss`가 대량으로 발생한다. 이때 데이터가 캐시에 다 차기전에 CPU가 버벅이는데 이를 Cache `Cold Start`라고 한다.   

스레드의 스위칭은 Stack을 제외한 메모리를 공유하기 때문에 TLB(Translation Lookaside Buffer) 캐시도 유지되고 Cache Hit도 높게 유지된다.   

일반적인 IPC (Pipe, Message Queue, Socket 등)   
프로세스 A가 프로세스 B에게 데이터를 주려면, 자기 메모리 영역에 있는 데이터를 커널 공간(Kernel Space)으로 복사(Copy)한 뒤, 커널이 이를 다시 프로세스 B의 메모리 공간으로 복사해 줘야 한다.   

비용 폭발 원인   
이 과정에서 시스템 콜(System Call)이 발생하여 유저 모드와 커널 모드 간의 모드 스위칭(Mode Switching)이 일어나고, CPU 캐시에 있던 데이터들을 계속 다른 메모리 공간으로 복사하고 옮겨 적느라 캐시 오염(Cache Pollution)이 발생하며 캐시 히트율이 떨어진다.   

<br/>

계속 공부를 하다보니 궁금한게 더 생겼다.         
1. 왜 굳이 가상메모리르 쓸까? TLB 캐시를 사용해서 메모리 오버헤드가 발생할텐데   
2. 프로세스에서 공유메모리 방식은 정확히 어떤 메모리를 공유하는걸까?   

<br/>

**가상메모리를 쓰는 이유**   

1. 메모리 고갈 문제 해결    
   가상메모리가 없다면 16GB RAM에서 20GB짜리 최신 게임을 돌릴수가 없다.   
   필요한 부분만 물리 메모리(RAM)에 올려서 실행해서 RAM 용량 한계 이상으로 개발/실행이 가능하다.    
2. 메모리 단편화(Fragmentation) 해결   
   프로그램을 껐다 켰다하면 물리 메모리에 빈공간이 생기는데 이를 가상 메모리가 마치 연속된 메모리처럼 보이게 관리를 해서(Page 단위로 관리, 보통 4KB) 단편화를 해결한다.   
3. 완벽한 격리와 보안 (Memory Protection)   
   가상 메모리 체제에서 모든 프로세스가 자신만의 독립적인 가상 주소 공간을 가진다. 따라서 보안성이 높아진다. 이러한 장점때문에 제조사들은 **TLB**라는 칩을 내장시켜서 주소변환 오버헤드를 0에 가깝게 줄이는 방식으로 타협을 봤다.   

<br/>

**공유 메모리는 실제로 어디에 있을까?**   

실제 물리 메모리의 특정 구역을 공유 메모리 구역으로 지정을 한다. 그리고 프로세스 A와 B의 가상 메모리 공간에 각각 연결을 해서 통신을 하게 만든다.   

<br/>

추가로 찾아본 커널과 인터럽트!   

**커널(Kernel)**   

OS는 덩치가 꽤 큰데 컴퓨터가 켜질 때 메모리(RAM)에 가장 먼저 상주하여 컴퓨터가 꺼질 때까지 하드웨어를 관리하고 통제하는 핵심 프로그램을 `커널(Kernel)`이라고 한다.   

**유저 모드(User Mode) vs 커널 모드(Kernel Mode)**    

컴퓨터는 보안을 위해 메모리와 CPU 권한을 두 가지 모드로 분리한다.   
- 유저 모드(User Mode)   
  유저가 만든 프로그램이 실행되는 곳. 하드웨어(모니터, 키보드 등)나 다른 프로세스의 메모리에 접근할 수 있는 권한이 없다.
- 커널 모드(Kernel Mode)   
  CPU의 모든 명령어를 실행할 수 있고, 모든 하드웨어와 메모리에 무제한으로 접근할 수 있는 최고 권한을 가진다.

**시스템 콜(System Call)**   

유저모드의 프로그램이 하드웨어 제어가 필요하다면 직접 건드리지 못하고 Kernel에게 대신 부탁해야한다. 이를 시스템 콜(System Call)이라고 한다. 이때 유저 모드에서 커널 모드로의 전환(Mode Switching)이 일어난다.   

<br/>

**Interrput**   

CPU가 일을 처리하느라 바쁠 때 급하게 처리해야할 일이 있으면 CPU에게 신호를 보내는데 이게 인터럽트다.   

1. 하드웨어 인터럽트(External / Hardware Interrupt)   
   - 타이머 인터럽트   
	 OS가 멀티태스킹을 구현하는 핵심이다. 주기적으로 컨텍스트 스위칭을 하도록 강제한다.   
   - I/O 인터럽트   
	 키보드, 마우스, 디스크 읽기/쓰기 등   

2. 소프트웨어 인터럽트(Internal / Software Interrupt / Trap)   
   - 예외(Exception)   
	 숫자를 0으로 나누거나 메모리 주소에 잘 못 접근했을 때 CPU 스스로 인터럽트를 발생시켜 커널에게 넘긴다.(보통 프로그램 강제종료)   
   - 트랩(Trap)/시스템콜(SystemCall)   
	 
결론적으로 운영체제(`Operating System, OS`)는 커널(`Kernel`)이 끊임없이 컨텍스트 스위칭(`Context Switching`)을 하는 거대한 시스템이다. 인터럽트에 의해 구동되는 프로그램(`Interrupt-Driven Program`)이라고 부르는 이유다.   

  </p>
</details>

#### <!-- 26.06.12 -->
<details> 
  <summary>26.06.12</summary>
  <p>

에이타니   

`COND_OwnerOnly`는 해당 변수를 소유한 클라이언트에게만 복제하는 조건이다. Health(체력)과 같은 민감한 정보는 소유자에게만 전달하는 것이 일반적이다.   
`COND_AutonomousOnly`는 자율 프록시에만 복제하고, `COND_SimulatedOnly`는 시뮬레이티드 프록시에만 복제한다.   
`COND_None`은 모든 클라이언트에게 복제하는 기본 조건이다.   

`RepNotify` 함수는 복제된 변수의 값이 변경될 때 클라이언트에서 자동으로 호출되는 콜백 함수다. 주로 변수 변경에 따른 시각적 효과(애니메이션, 파티클 등)나 사운드 재생 등을 처리하는 데 사용된다.   

<br/>

**GamePlayAbility**   

에셋 태그
이름이 붙어있음   
소유 태그   
스킬을 사용했을 때 태그가 붙었다가 끝나면 떼어짐(포스트잇 느낌)   
필수 태그   
이 태그가 있어야 스킬이 발동됨   
차단된 태그   
태그 있으면 차단   

소스 필수 태그   
특정 태그가

타깃 필수 태그   
상대방이 이 태그가 있어야 발동   
타깃 차단됨 태그   
상대방이 이 태그가 있으면 스킬 발동 안함   

인스턴싱 정책(Instancing Policy)   
함수처럼 실행하고 끝나고 실행하고 끝나는 방식(No Instanced)   
캐릭터마다 인스턴스를 만들어줌, 상태를 기억해야할때 필요함(PerActor)   
스킬버튼을 누를 때 마다 새로운 인스턴스가 생성됨(InstancedPerExecution)    


  </p>
</details>

#### <!-- 26.06.15 -->
<details> 
  <summary>26.06.15</summary>
  <p>

에이타니   

인터페이스   
인터페이스는 상속이 아닌 계약(Contract)의 개념이다. 부모 클래스의 기능을 자동으로 상속받지 않으며, 각 클래스가 인터페이스의 함수를 직접 구현해야 한다.   

A*(A-Star) 알고리즘   
A* 알고리즘의 핵심 비용 함수는 f(n) = g(n) + h(n)이다. 여기서 g(n)은 시작점부터 현재 노드 n까지의 실제 이동 비용이고, h(n)은 현재 노드에서 목표 지점까지의 추정 비용(휴리스틱)이다.   

<br/>

과제 9번을 하는 중 시도횟수가 잘 못 출력되는 현상이 발생했다.   

원인은 카운팅을 하기 전에 클라이언트에서 미리 문자열을 만들고 검증(3자리 숫자인지) 후 결과값을 서버로 올려보내기 때문이었다.   

클라에서는 단순하게 값을 올려보내고 서버에서 검증을 하면서 카운팅을 해주는 방식으로 바꿔보았다.   

```cpp
// ----------- 기존 코드 -----------
// 로컬(PlayerController)
void ACXPlayerController::SetChatMessageString(const FString& InChatMessageString)
{
    // ...
    ACXPlayerState* CXPS = GetPlayerState<ACXPlayerState>();
    if (IsValid(CXPS) == true)
    {
        // 카운팅을 하지 않았는데 문자열을 만들어버린다.
        FString CombinedMessageString = CXPS->GetPlayerInfoString() + TEXT(": ") + InChatMessageString;

        // 카운팅이 안된 문자열을 서버로 보낸다.
        ServerRPCPrintChatMessageString(CombinedMessageString);
    }
}
// 서버(GameModeBase)
void ACXGameModeBase::PrintChatMessageString(ACXPlayerController* InChattingPlayerController, const FString& InChatMessageString)
{
    // ...
    if (IsGuessNumberString(GuessNumberString) == true)
    {
        // 결과를 만들어낸 후
        // 카운트는 여기서 뒤늦게 올라간다.
        IncreaseGuessCount(InChattingPlayerController); 
        
        // 모든 클라이언트에게 카운팅이 잘못 된 결과값을 전송한다.
    }
}

// ----------- 수정한 코드 -----------
// 로컬(PlayerController)
void ACXPlayerController::SetChatMessageString(const FString& InChatMessageString)
{
	ChatMessageString = InChatMessageString;

	if (IsLocalController() == true)
	{
		// 카운팅이 안되는 현상 때문에 로컬에서는 순수 텍스트만 서버로 옮기게 수정!!! 
		ServerRPCPrintChatMessageString(InChatMessageString);
	}
}

// 서버(GameModeBase)
void ACXGameModeBase::PrintChatMessageString(ACXPlayerController* InChattingPlayerController, const FString& InChatMessageString)
{
	// PlayerState 가져오기
	ACXPlayerState* CXPS = InChattingPlayerController->GetPlayerState<ACXPlayerState>();
	if (IsValid(CXPS) == false)
	{
		return;
	}

	// ...

	if (IsGuessNumberString(GuessNumberString) == true)
	{
		// 카운트를 한 후 최신 플레이어 정보를 가져온다.
		IncreaseGuessCount(InChattingPlayerController);
		FString PlayerInfoString = CXPS->GetPlayerInfoString();
		
		// ...

		// 서버에서 문자열 완성
		FString CombinedMessageString = FString::Printf(TEXT("%s: %s -> %s"), *PlayerInfoString, *InChatMessageString, *JudgeResultString);
		for (TActorIterator<ACXPlayerController> It(GetWorld()); It; ++It)
		{
			ACXPlayerController* CXPlayerController = *It;
			if (IsValid(CXPlayerController) == true)
			{
				// 완성한 문자열 보내기
				CXPlayerController->ClientRPCPrintChatMessageString(CombinedMessageString);
				// ...
			}
		}
	}
	else
	{
		// 일반 채팅도 최신 카운트 정보 반영
		FString PlayerInfoString = CXPS->GetPlayerInfoString();
		FString CombinedMessageString = FString::Printf(TEXT("%s: %s"), *PlayerInfoString, *InChatMessageString);

		// ...
	}
}
```

<br/>

**ReplicatedUsing**   

서버가 값을 바꿨을 때 클라이언트에서 특정 함수(OnRep_...)가 자동으로 실행되므로, UI 위젯의 텍스트를 즉각 갱신하기에 매우 좋다.   

```cpp
// ReplicatedUsing 예시
public:
    // 현재 턴을 진행 중인 플레이어의 컨트롤러 (누구 턴인지 판별용)
    UPROPERTY(ReplicatedUsing = OnRep_CurrentTurnPlayer)
    class ACXPlayerController* CurrentTurnPlayer;

    // 현재 턴의 남은 시간 (초 단위)
    UPROPERTY(ReplicatedUsing = OnRep_RemainingTime)
    int32 RemainingTime;

protected:
    UFUNCTION()
    void OnRep_CurrentTurnPlayer();

    UFUNCTION()
    void OnRep_RemainingTime();

```


<br/>

플레이어의 턴이 맞지 않는 현상   

턴을 저장하는 CurrentTurnPlayer가 로그인 전에 값을 넣으려고 해서 nullptr로 저장되는게 원인이었다.   

그래서 먼저 로그인 된 컨트롤러에게 첫 턴을 넘겨주는 방식을 택했다.   

```cpp
void ACXGameModeBase::OnPostLogin(AController* NewPlayer)
{
	Super::OnPostLogin(NewPlayer);

	ACXPlayerController* CXPlayerController = Cast<ACXPlayerController>(NewPlayer);
	if (IsValid(CXPlayerController))
	{
		// ... 기존 로직 ...
		AllPlayerControllers.Add(CXPlayerController);

		// 방금 들어온 플레이어가 첫 번째 플레이어라면 바로 턴을 부여함
		ACXGameStateBase* CXGS = GetGameState<ACXGameStateBase>();
		if (IsValid(CXGS) && CXGS->CurrentTurnPlayer == nullptr)
		{
			CXGS->CurrentTurnPlayer = CXPlayerController;
			StartTurnTimer();
		}
	}
}
```

<br/>


  </p>
</details>

#### <!-- 26.06.16 -->
<details> 
  <summary>26.06.16</summary>
  <p>

에이타니   
BT에서 Service 노드는 주기적으로 정보를 수집하고 Blackboard를 업데이트하는 역할을 하며 백그라운드에서 지속적으로 동작한다.   
행동의 흐름에 영향을 끼치지 않는다.   
영향을 끼치고 성공/실패를 반환하는건 Decorator이다.   

AI Perception을 위한 컴포넌트 조합   
AI Perception 시스템은 AI Controller에 AI Perception Component를 추가하고, 감지될 타겟(플레이어 등)에 AI Stimulus Component를 추가하여 구성한다.   

<br/>

**백트래킹 문제 풀이**   

```cpp
// leetcode 39번 Combination Sum
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> currentCombination;

        sort(candidates.begin(), candidates.end());
        backtrack(candidates, target, 0, currentCombination, result);

        return result;
    }

private:
    void backtrack(const vector<int>& candidates, int remainTarget, int start, vector<int>& current, vector<vector<int>>& result)
    {
        // 성공 조건: target을 정확히 채운 경우
        if (remainTarget == 0) {
            result.push_back(current);
            return;
        }

        // 탐색 진행
        for (int i = start; i < candidates.size(); ++i) {
            // 가지치기: 현재 숫자가 남은 target보다 크다면, 
            // 정렬되어 있으므로 이후의 숫자들도 모두 target보다 크다. 따라서 탐색 중단(break).
            if (remainTarget - candidates[i] < 0) {
                break;
            }

            // 1. 선택: 현재 숫자를 조합에 추가
            current.push_back(candidates[i]);

            // 2. 재귀 호출: 동일한 숫자를 또 쓸 수 있으므로 start 인덱스를 i로 넘김
            backtrack(candidates, remainTarget - candidates[i], i, current, result);

            // 3. 복원(백트래킹): 다음 경우의 수를 위해 넣었던 숫자를 다시 빼줌
            current.pop_back();
        }
    }
};
```

<br/>

```cpp
// leetcode 51번 4-Queen 문제
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> result;
        // 빈 체스판 초기화 (모두 '.'으로 채움)
        vector<string> board(n, string(n, '.'));

        // 공격 경로 체크용 플래그 배열 (체크 속도 최적화)
        vector<bool> cols(n, false);
        vector<bool> diag1(2 * n - 1, false); // / 방향 대각선
        vector<bool> diag2(2 * n - 1, false); // \ 방향 대각선

        // 0번 행부터 백트래킹 시작
        backtrack(0, n, board, cols, diag1, diag2, result);

        return result;
    }

private:
    void backtrack(int row, int n, vector<string>& board, vector<bool>& cols, vector<bool>& diag1, vector<bool>& diag2, vector<vector<string>>& result) {
        
        // 성공 조건: 모든 행에 퀸을 배치 완료한 경우
        if (row == n) {
            result.push_back(board);
            return;
        }

        // 현재 행(row)에서 각 열(col)을 하나씩 시도
        for (int col = 0; col < n; ++col) {
            int d1 = row + col;
            int d2 = row - col + n - 1;

            // 가지치기: 현재 자리가 공격 경로 상에 있다면 놓지 못하고 패스
            if (cols[col] || diag1[d1] || diag2[d2]) {
                continue;
            }

            // 1. 선택: 퀸 배치 및 공격 경로 마킹
            board[row][col] = 'Q';
            cols[col] = diag1[d1] = diag2[d2] = true;

            // 2. 재귀 호출: 다음 행으로 이동
            backtrack(row + 1, n, board, cols, diag1, diag2, result);

            // 3. 복원(백트래킹): 다음 경우의 수를 위해 퀸을 치우고 마킹 해제
            board[row][col] = '.';
            cols[col] = diag1[d1] = diag2[d2] = false;
        }
    }
};
```

<br/>

**Greedy 알고리즘 관련 문제**

```cpp
// leetcode 455번 Assign Cookies
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());

        int g_index = 0;
        int s_index = 0;

        while(g_index < g.size() && s_index < s.size())
        {
            if(g[g_index] <= s[s_index])
            {
                g_index++;
            }
            s_index++;
        }

        return g_index;
    }
};
```

<br/>

```cpp
// leetcode 134번 Gas Station
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int total_tank = 0;   // 전체 주유량 - 전체 소모량
        int current_tank = 0; // 현재 시작점부터 누적된 가솔린 잔여량
        int start_index = 0;  // 가정하는 시작 주유소 위치

        for (int i = 0; i < gas.size(); ++i) {
            int fuel_gain = gas[i] - cost[i];
            total_tank += fuel_gain;
            current_tank += fuel_gain;

            // 만약 현재까지 모은 기름으로 다음 주유소로 갈 수 없다면 (기름 바닥)
            if (current_tank < 0) {
                // i번까지의 주유소는 전부 시작점이 될 수 없음.
                // 다음 주유소인 i + 1을 새로운 시작점으로 가정하고 탱크를 비운다.
                start_index = i + 1;
                current_tank = 0;
            }
        }

        // 전체 한 바퀴를 돌았을 때 total_tank가 음수라면 완주할 기름이 부족
        if (total_tank < 0) {
            return -1;
        }

        // 그것이 아니라면 마지막으로 살아남은 start_index가 유일한 정답
        return start_index;
    }
};
```

  </p>
</details>

#### <!-- 26.06.17 -->
<details> 
  <summary>26.06.17</summary>
  <p>

에이타니   

`Spawn System Attached` 노드는 `Niagara` 파티클 시스템을 특정 컴포넌트(예: 스켈레탈 메시, 무기 등)에 부착하여 생성하며, 생성과 동시에 자동으로 활성화되어 재생된다. 이는 발사 효과, 충돌 효과 등 특정 위치나 오브젝트에 파티클을 부착해야 할 때 가장 일반적으로 사용되는 방법이다.   

유한 상태 머신(`FSM, Finite State Machine`)은 유한한 개수의 상태(State)를 가지며, 특정 시점에 하나의 상태만 활성화된다. 특정 조건(`Transition Condition`)이 만족되면 다른 상태로 전이된다.   

허브(`Hub`)는 물리 계층(`Layer 1`)에서 동작하는 가장 단순한 네트워크 장비로, 수신한 신호를 모든 포트로 `단순히 복제`하여 전송하는 역할만 한다.   

라우터(`Router`)는 네트워크 계층(`Layer 3`)에서 동작하며, 서로 다른 네트워크(예: LAN과 WAN) 간의 데이터 패킷을 `IP 주소`를 기반으로 최적의 경로로 전달하는 역할을 한다.   

스위치(`Switch`)는 데이터 링크 계층(`Layer 2`)에서 동작하며, 동일 네트워크 내에서 `MAC 주소를 기반`으로 데이터 프레임을 목적지 장치로만 전송하여 네트워크 효율성을 높인다.   

모뎀(`Modem`)은 변조(`Modulation`)와 복조(`Demodulation`)를 수행하여 컴퓨터의 디지털 신호를 전화선이나 케이블을 통해 전송 가능한 아날로그 신호로 `변환`하거나 그 반대 과정을 담당한다.   

<br/>

동적계획법((Dynamic Programming, DP)   

```cpp
// leetCode 198번 House Robber
// 점화식: dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

#include <vector>
#include <algorithm>

class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        
        // 집이 없는 경우와 1개만 있는 경우
        if (n == 0) return 0;
        if (n == 1) return nums[0];

        // 각 집까지의 최대 금액을 저장할 DP 테이블 생성
        vector<int> dp(n, 0);

        // 초기 상태 설정 (Base Cases)
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);

        // 3번째 집(인덱스 2)부터 끝까지 점화식 적용
        for (int i = 2; i < n; ++i) {
            // dp[i] = max(직전 집을 털고 이번 집은 건너뛰기, 전전 집까지 털고 이번 집도 털기)
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]);
        }
        
        // 맨 마지막 집까지 고려했을 때의 최댓값 반환
        return dp[n - 1];
	}
};


// 더 깔끔한 방식
class Solution {
public:
    int rob(vector<int>& nums) {
        int prev2 = 0; // dp[i-2] 역할 (전전 집까지의 최댓값)
        int prev1 = 0; // dp[i-1] 역할 (직전 집까지의 최댓값)
        
        // C++의 범위 기반 for 루프(Range-based for loop) 활용
        for (int money : nums) {
            // 현재 집을 고려했을 때의 최댓값 계산
            int current = max(prev1, prev2 + money);
            
            // 다음 집으로 이동하기 위해 이전 값들을 한 칸씩 밀어줌 (Slide)
            prev2 = prev1;
            prev1 = current;
        }
        
        return prev1;
    }
};
```

<br/>

```cpp
// leetCode 64번 Minimum Path Sum
// 점화식: dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]

class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        
        // m x n 크기의 DP 테이블을 0으로 초기화
        vector<vector<int>> dp(m, vector<int>(n, 0));
        
        // 시작점 초기화
        dp[0][0] = grid[0][0]; 
        
        // 맨 윗줄 초기화 (오직 왼쪽에서만 올 수 있음)
        for (int j = 1; j < n; ++j) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }
        
        // 맨 왼쪽 줄 초기화 (오직 위에서만 올 수 있음)
        for (int i = 1; i < m; ++i) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }
        
        // 나머지 칸들 채우기
        for (int i = 1; i < m; ++i) {
            for (int j = 1; j < n; ++j) {
                // 위쪽 칸과 왼쪽 칸 중 더 작은 값 + 현재 칸의 숫자
                dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }
        
        // 우측 하단 도착점의 결과 반환
        return dp[m - 1][n - 1];
    }
};

// 새로운 배열을 만들지 않고 바로 덮어쓰는 방식
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                // 시작점은 건너뜀
                if (i == 0 && j == 0) continue;
                
                if (i == 0) {
                    // 맨 윗줄인 경우: 왼쪽 칸의 누적합을 더함
                    grid[i][j] += grid[i][j - 1];
                } else if (j == 0) {
                    // 맨 왼쪽 줄인 경우: 위쪽 칸의 누적합을 더함
                    grid[i][j] += grid[i - 1][j];
                } else {
                    // 일반적인 경우: 위쪽과 왼쪽 중 최소값 + 현재 값
                    grid[i][j] += min(grid[i - 1][j], grid[i][j - 1]);
                }
            }
        }
        
        return grid[m - 1][n - 1];
    }
};
```

<br/>

```cpp
// leetCode 416번 Partition Equal Subset Sum
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        // 전체 합 계산 (std::accumulate는 배열의 총합을 구할 때 유용), #include <numeric> 헤더 필요!
        int totalSum = accumulate(nums.begin(), nums.end(), 0);
        
        // 총합이 홀수면 반으로 똑같이 나눌 수 없음
        if (totalSum % 2 != 0) return false;
        
        int target = totalSum / 2;
        
        // dp[i]는 합 i를 만들 수 있는지 여부를 저장 (초기값은 모두 false)
        vector<bool> dp(target + 1, false);
        dp[0] = true; // 합 0은 언제나 가능
        
        // 0-1 배낭 문제 로직 수행
        for (int num : nums) {
            // 중요: 역순(target부터 num까지)으로 탐색해야 
            // 현재 루프에서 같은 숫자가 중복으로 사용되는 것을 막을 수 있음.
            for (int j = target; j >= num; --j) {
                if (dp[j - num]) {
                    dp[j] = true;
                }
            }
            
            // 최적화: 만약 이미 target을 만들 수 있다면 조기 종료
            if (dp[target]) return true;
        }
        
        return dp[target];
    }
};
```

  </p>
</details>

#### <!-- 26.06.18 -->
<details> 
  <summary>26.06.18</summary>
  <p>

에이타니   

**블루프린트 통신 방식**   
`Direct Reference`는 통신할 대상을 미리 알고 직접 참조하는 방식이다. 따라서 동적으로 생성되는 액터와의 통신에는 적합하지 않다. 동적 생성 액터와의 통신에는 `Cast`나 `Interface` 방식이 더 적합하다.   
성능이 가장 빠르고, 직접 참조하여 접근하며, 참조 대상을 미리 알아야 한다.   

`Cast`는 타입 변환 과정에서 오버헤드가 발생하며, 과도하게 사용하면 성능 저하와 메모리 관리 문제를 야기할 수 있다.   
`Cast`는 실패할 수 있으므로 항상 실패 처리를 고려해야 하고, 단일 대상에게만 통신하며, 통신할 대상의 참조가 필요하다.   

`Event Dispatcher`는 일대다(One-to-Many) 통신을 위한 방식으로, 하나의 이벤트가 발생했을 때 여러 리스너에게 동시에 알림을 보낼 수 있다. `옵저버 패턴`을 구현한 것으로, 여러 객체가 특정 이벤트를 `구독(Bind)`하고 해당 이벤트 발생 시 모두 알림을 받는다. 타입에 제한이 없고, 여러 리스너 바인딩이 가능하며, `Direct Reference`보다는 오버헤드가 있습니다.   

`Blueprint Interface`의 핵심 장점은 상속 관계가 없는 서로 다른 클래스들이 같은 인터페이스를 구현하여 일관된 방식으로 통신할 수 있다는 것이다. 이는 다형성을 제공하고 결합도를 낮춘다. `Interface`는 `Cast`와 유사한 성능을 가지며, 각 클래스에서 직접 구현해야 하고, 함수 호출만 가능하며 변수 직접 접근은 불가능하다.   

<br/>

**Race Condition**   

이전에 잠깐 키워드만 확인했던 `Race Condition`에 대해서 다시 알아봤다.   

멀티스레드나 멀티프로세스 환경에서 여러 개의 프로세스/스레드가 하나의 공유 자원에 동시에 접근해 쓰기(Write) 작업을 하려고 할 때, 접근 타이밍이나 실행 순서에 따라 결과가 달라지는 현상이다.   

**Race Condition이 발생하는 예시**   

```cpp
#include <iostream>
#include <thread>
#include <vector>

int shared_counter = 0; // 공유 자원

void increase_counter() {
    for (int i = 0; i < 100000; ++i) {
        shared_counter++; // 임계 구역 (Critical Section)
    }
}

int main() {
    // 2개의 스레드가 동시에 같은 함수를 실행
    std::thread t1(increase_counter);
    std::thread t2(increase_counter);

    t1.join();
    t2.join();

    // 기대 결과: 200000
    // 실제 결과: 134232, 189431 등 실행할 때마다 엉뚱한 값이 나옴 (Race Condition)
    std::cout << "최종 결과: " << shared_counter << std::endl;
    return 0;
}
```

`shared_counter++`는 한 줄짜리 코드 같지만, CPU 레벨에서는 1) 값을 읽고, 2) 1을 더하고, 3) 다시 저장하는 3단계로 나뉜다. 스레드 1이 값을 더하기 전에 스레드 2가 옛날 값을 읽어가 버리기 때문에 데이터가 누락되는 것   

<br/>

**해결방법**   

**1.`std::mutex` 키워드 사용**   

`lock()`, `unlock()`을 사용해서 직접 열고 닫으면 `데드락(Dead Lock)`이 발생할 수 있기 때문에 `RAII(Resource Acquisition Is Information)`를 따르는 `lock_guard`나 `unique_lock`키워드를 사용하는게 좋다.   

```cpp
#include <iostream>
#include <thread>
#include <mutex>

int shared_counter = 0;
std::mutex mtx; // 자물쇠 역할을 할 뮤텍스 객체

void increase_counter() {
    for (int i = 0; i < 100000; ++i) {
        // 객체가 생성될 때 자동으로 mtx.lock()을 호출합니다.
        std::lock_guard<std::mutex> lock(mtx); 
        
        shared_counter++; 
        
        // 함수 블록(스코프)을 벗어나면 lock 객체가 소멸하면서 자동으로 mtx.unlock()이 호출됩니다.
    }
}

int main() {
    std::thread t1(increase_counter);
    std::thread t2(increase_counter);
    t1.join(); t2.join();

    std::cout << "최종 결과 (Mutex): " << shared_counter << std::endl; // 항상 200000 보장
    return 0;
}
```
   
<br/>

**2.`std::atomic` 키워드 사용**   

단순한 덧셈/뺄셈 같은 가벼운 연산 때문에 무거운 뮤텍스(컨텍스트 스위칭 비용 발생)를 쓰는 것은 비효율적이다.   
C++11부터는 CPU의 원자적 연산 명령어를 직접 사용하는 std::atomic 타입을 제공한다.   

```cpp
#include <iostream>
#include <thread>
#include <atomic> // 원자적 연산을 위한 헤더

std::atomic<int> shared_counter(0); // 원자적 변수로 선언(0으로 초기화)

void increase_counter() {
    for (int i = 0; i < 100000; ++i) {
        // CPU 레벨에서 쪼개지지 않는 하나의 연산(Atomic)으로 처리됩니다.
        shared_counter++; 
    }
}

int main() {
    std::thread t1(increase_counter);
    std::thread t2(increase_counter);
    t1.join(); t2.join();

    std::cout << "최종 결과 (Atomic): " << shared_counter << std::endl; // 항상 200000 보장
    return 0;
}
```

락을 걸지 않기 때문에(Lock-free) 뮤텍스보다 압도적으로 빠르다. 다만, 복잡한 로직이나 여러 줄의 코드 블록을 보호할 때는 사용할 수 없고, 단일 변수 연산에만 유효하다.   

<br/>

**3.`std::counting_semaphore` (C++20 표준 세마포어)**   

특정 자원의 개수를 제한하거나 스레드 간의 신호(Signal)를 주고받을 때는 C++20에 정식 도입된 세마포어를 사용한다.   

```cpp
#include <iostream>
#include <thread>
#include <semaphore> // C++20 표준 세마포어

int shared_counter = 0;
// 허용 개수를 1로 설정 (바이너리 세마포어처럼 동작)
std::counting_semaphore<1> sem(1); 

void increase_counter() {
    for (int i = 0; i < 100000; ++i) {
        sem.acquire(); // 카운트를 1 줄임 (0이 되면 다른 스레드는 대기)
        
        shared_counter++;
        
        sem.release(); // 카운트를 1 늘림 (대기 중인 다른 스레드가 깨어남)
    }
}

int main() {
    std::thread t1(increase_counter);
    std::thread t2(increase_counter);
    t1.join(); t2.join();

    std::cout << "최종 결과 (Semaphore): " << shared_counter << std::endl; // 항상 200000 보장
    return 0;
}
```

<br/>

**임계 구역(Critical Section)**   

임계 구역(`Critical Section`)은 쉽게 말해 "여러 스레드가 동시에 접근하면 난리가 나는 공유 자원(변수, 파일 등)을 다루는 코드 영역"을 말한다.    
멀티스레드 프로그램에서 스레드들은 각자의 스택 메모리를 가지고 있지만, 나머지는 공유해서 쓴다. 이때 나머지(힙, 코드, 데이터) 영역을 동시에 접근하면 문제가 생기는데 이 부분을 임계 구역이라고 한다.   

<br/>

**임계 구역을 다룰 때의 3대 원칙**   
OS 이론에서는 임계 구역을 안전하게 보호하기 위해 아래 3가지 조건이 반드시 만족되어야 한다고 말한다.   

상호 배제(`Mutual Exclusion`): 어떤 스레드가 임계 구역을 실행 중이면, 다른 스레드는 절대 들어올 수 없다. (뮤텍스, 세마포어가 해주는 일)   

진행(`Progress`): 임계 구역에 아무도 없다면, 들어가고자 하는 스레드는 바로 들어갈 수 있어야 한다. (아무도 없는데 막히면 안 됨)   

한정 대기(`Bounded Waiting`): 어떤 스레드가 임계 구역에 들어가려고 대기할 때, 무한정 기다려서는 안 된다. (언젠가는 차례가 와야 함)   

<br/>

`CRITICAL_SECTION` 과 `Mutex`의 비교   

`CRITICAL_SECTION`은 유저 모드(User Mode)에서 동작하므로 모드 전환이 이뤄지지 않아서 빠르다. 단점은 하나의 프로세스 내에 있는 스레드끼리만 가능하다는 점이다.   

`Mutex`는 커널 모드(Kernel Mode)에서 동작하고 이름을 붙일 수 있어서 서로 다른 프로세스끼리도 동기화가 가능하다. 단점으로는 모드를 바꿔야하기 때문에 비용이 든다.   

<br/>

**데드락(Deadlock)이 발생하는 4가지 조건**   
-> `Coffman conditions`(코프만 조건)이라고도 한다.   

상호 배제 (Mutual Exclusion)   
자원은 한 번에 한 스레드만 사용할 수 있어야한다.   

점유와 대기 (Hold and Wait)   
스레드가 최소한 하나의 자원을 움켜쥔 채(Hold), 다른 스레드가 가진 자원을 추가로 얻으려고 기다리는(Wait) 상태여야 한다.   

비선점 (No Preemption)   
다른 스레드가 가진 자원을 강제로 빼앗을 수 없어야 한다.   

순환 대기 (Circular Wait)   
대기하고 있는 스레드들의 관계가 둥글게 원(Cycle)을 그리며 서로를 기다려야 한다.   


  </p>
</details>

#### <!-- 26.06.19 -->
<details> 
  <summary>26.06.19</summary>
  <p>

에이타니   

`XR 콘텐츠`의 입력 시스템은 물리적 컨트롤러뿐만 아니라 핸드트래킹, 시선 추적, 음성 인식 등 다양한 입력 방식을 지원한다. 입력 구조는 일반적으로 입력 장치로부터 데이터를 수집하는 입력 계층, 데이터를 해석하고 처리하는 논리 계층, 그리고 게임 로직에 전달하는 이벤트 시스템으로 구성된다.   

`핸드트래킹`은 주로 적외선 LED와 카메라를 사용한 광학 추적 방식으로 작동한다. 적외선 LED가 손을 비추면 카메라가 반사된 빛을 감지하여 손의 형태와 위치를 3D로 재구성한다.   

<br/>

**Attribute**   

```cpp
// GAS_AttributeSetBase.h

#pragma once

#include "CoreMinimal.h"
#include "AttributeSet.h"
#include "AbilitySystemComponent.h"
#include "GAS_AttributeSetBase.generated.h"

#define ATTRIBUTE_ACCESSORS(ClassName, PropertyName) \
GAMEPLAYATTRIBUTE_PROPERTY_GETTER(ClassName, PropertyName) \
GAMEPLAYATTRIBUTE_VALUE_GETTER(PropertyName) \
GAMEPLAYATTRIBUTE_VALUE_SETTER(PropertyName) \
GAMEPLAYATTRIBUTE_VALUE_INITTER(PropertyName)

UCLASS()
class SPARTAMASTERGAS_API UGAS_AttributeSetBase : public UAttributeSet
{
	GENERATED_BODY()
	
public:
	UGAS_AttributeSetBase();
	
	ATTRIBUTE_ACCESSORS(UGAS_AttributeSetBase, Hp);
	ATTRIBUTE_ACCESSORS(UGAS_AttributeSetBase, MaxHp);
	ATTRIBUTE_ACCESSORS(UGAS_AttributeSetBase, Stamina);
	ATTRIBUTE_ACCESSORS(UGAS_AttributeSetBase, MaxStamina);
	
	// 밑에 함수 순서대로 실행됨
	// 명령을 받은 직후 // 필터링
	// 무적상태
	// 데미지 튕김
	// ...
	virtual bool PreGameplayEffectExecute(struct FGameplayEffectModCallbackData &Data) override;
	
	// 값이 바뀌기 전 호출 // 필터링
	// 체력이 maxHp를 넘지 못하게 막을 때
	// 체력이 0 밑으로 내려가지 않게 막을 때
	// 이동 속도가 너무 빨라지지않게
	// ...
	virtual void PreAttributeChange(const FGameplayAttribute& Attribute, float& NewValue) override;
	
	// 값이 바뀐 후 호출
	// 피가 깎였으니까 UI 체력바를 갱신해라
	// 피가 깎였으니 사운드를 재생해라
	// 특정 스탯이 변했으니까 캐릭터 외형을 바꿔라
	// ...
	virtual void PostAttributeChange(const FGameplayAttribute& Attribute, float OldValue, float NewValue) override;
	
	// 명령을 수행하고 난 후 // 이펙트 처리가 완전 끝난 후 실행
	// 매개변수에 Data는 사망판정과 함께 넘어오는 데이터들을 넣어줄 수 있다.
	virtual void PostGameplayEffectExecute(const struct FGameplayEffectModCallbackData &Data) override;
	
private:
	UPROPERTY()
	FGameplayAttributeData Hp;
	UPROPERTY()
	FGameplayAttributeData MaxHp;
	UPROPERTY()
	FGameplayAttributeData Stamina;
	UPROPERTY()
	FGameplayAttributeData MaxStamina;
};

// GAS_AttributeSetBase.cpp

#include "AttributeSet/GAS_AttributeSetBase.h"

UGAS_AttributeSetBase::UGAS_AttributeSetBase()
{
	// 초기화 부분만 이렇게 써야한다. 게임 도중엔 절대 이렇게 쓰면 안됨!!!(GameplayEffect에서 바꿔줌)
	InitHp(100.f);
	InitMaxHp(100.f);
	InitStamina(100.f);
	InitMaxStamina(100.f);
	
	// HP 가져오기
	// GetHp();
	
	// HP 변경하기
	// SetHp();
	
	// HP 포인터
	// GetHpAttribute();
}

bool UGAS_AttributeSetBase::PreGameplayEffectExecute(struct FGameplayEffectModCallbackData& Data)
{
	Super::PreGameplayEffectExecute(Data);
	
	GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, TEXT("PreGameplayEffectExecute"));
	
	return true;
}

void UGAS_AttributeSetBase::PreAttributeChange(const FGameplayAttribute& Attribute, float& NewValue)
{
	Super::PreAttributeChange(Attribute, NewValue);
	
	GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, TEXT("PreAttributeChange"));
}

void UGAS_AttributeSetBase::PostAttributeChange(const FGameplayAttribute& Attribute, float OldValue, float NewValue)
{
	Super::PostAttributeChange(Attribute, OldValue, NewValue);
	
	GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, TEXT("PostAttributeChange"));
}

void UGAS_AttributeSetBase::PostGameplayEffectExecute(const struct FGameplayEffectModCallbackData& Data)
{
	Super::PostGameplayEffectExecute(Data);
	
	GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, TEXT("PostGameplayEffectExecute"));
}
```

<br/>

**Character에서 SetHp 사용해보기**   

```cpp
// Character.h에 추가
public:
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "AbilitySystem")
	TObjectPtr<class UGAS_AttributeSetBase> AttributeSet;
	
	UFUNCTION(BlueprintCallable)
	void ApplyDamage(float DamageAmount);


// Character.cpp에 추가
void AGAS_CharacterBase::ApplyDamage(float DamageAmount)
{
	float NewHp = AttributeSet->GetHp() - DamageAmount;
	AttributeSet->SetHp(NewHp);
}

UAbilitySystemComponent* AGAS_CharacterBase::GetAbilitySystemComponent() const
{
	return AbilitySystemComponent;
}
```

TriggerBox 만들고 선택한 상태에서 레벨 블루프린트로 가서 ApplyDamage(내가 만든 함수 불러와야함) 불러와서 테스트 해보면 실행된다.   
SetHp를 사용했기 때문에 GAS의 반만 사용하는 느낌이다.   
디버깅하면 `PreAttributeChange`, `PostAttributeChange`만 호출됨..!

  </p>
</details>

#### <!-- 26.06.22 -->
<details> 
  <summary>26.06.22</summary>
  <p>

에이타니   

`Character Movement Component`는 네트워크 환경을 위해 설계된 컴포넌트로, 클라이언트 예측(`Client Prediction`)과 서버 조정(`Server Reconciliation`) 메커니즘을 내장하고 있다. 클라이언트는 입력을 즉시 로컬에서 시뮬레이션하여 반응성을 높이고, 동시에 서버에 이동 데이터를 전송한다. 서버는 이를 검증하고 필요시 클라이언트를 수정하며, 다른 클라이언트들에게는 자동으로 복제된다.   

<br/>

**가상 메모리**   

지난번에 컨텍스트 스위칭에 대해서 공부할 때 가상메모리가 잠깐 나왔었다.   
예전에 공부한 내용 -> `프로세스의 스위칭 같은 경우 서로다른 가상 메모리 공간을 사용하기 때문에 기존 캐시 메모리가 쓸모가 없다.`   

가상메모리란 물리적 메모리(RAM)의 한계를 극복하기 위해 하드디스크나 SSD 같은 저장 장치의 일부를 RAM처럼 사용하는 방법이다.   

내 컴퓨터의 실제 RAM이 16GB밖에 안 되더라도, 가상 메모리 덕분에 프로그램들은 마치 컴퓨터에 64GB나 128GB의 엄청나게 큰 메모리가 있는 것처럼 착각하며 작동할 수 있게 된다.   

<br/>

**가상 메모리가 필요한 이유**   

메모리 부족 해결   
RAM 용량보다 더 큰 프로세스를 실행하거나, 여러 개의 프로그램을 동시에 띄울 때 RAM이 가득 차서 컴퓨터가 멈추는(Crash) 현상을 방지   

효율적인 메모리 관리   
프로그램이 실행될 때 코드의 모든 부분이 한 번에 다 쓰이는 것은 아니다. 당장 필요한 부분만 RAM에 올리고, 나머지는 가상 메모리에 보관함으로써 실제 RAM을 아낄 수 있다.   

메모리 보호 (보안)   
각 프로세스는 자신만의 독립된 가상 주소 공간을 가진다. 따라서 하나의 프로그램이 오류를 일으켜서 다른 프로그램의 메모리 영역을 침범하거나 망가뜨리는 것을 원천적으로 차단한다.   

<br/>

**페이징(Paging)**   

가상 메모리는 관리의 효율성을 위해 메모리를 일정한 크기로 잘라서 관리한다.

페이지(Page)   
가상 메모리를 나누는 최소 단위 (보통 4KB)   
프레임(Frame)   
물리 메모리(RAM)를 나누는 최소 단위 (페이지와 크기가 같음)   
페이지 테이블(Page Table)   
가상 주소와 실제 RAM의 물리 주소를 연결해 주는 '지도' 역할을 하는 테이블이다.   

<br/>

**요구 페이징(Demand Paging) & 페이지 폴트**   

프로그램이 실행될 때 모든 데이터를 RAM에 올리지 않고, "지금 당장 필요한 페이지"만 RAM에 올리는 방식이다.   

1.CPU가 특정 메모리 주소를 요청합니다.   
2.페이지 테이블을 확인했는데, 해당 데이터가 실제 RAM(프레임)에 없고 하드디스크(가상 메모리 영역)에 있는 상태일 수 있다. 이를 `페이지 폴트(Page Fault)`라고 한다.   
3.페이지 폴트가 발생하면 운영체제(OS)는 하드디스크에서 해당 페이지를 찾아 빈 RAM 공간(프레임)에 올린다.   
4.만약 RAM이 꽉 차 있다면, 당장 쓰이지 않는 RAM의 주인을 하드디스크의 가상 공간으로 쫓아내고(스와핑 Out), 그 자리에 필요한 데이터를 들여온다.(스와핑 In)   

<br/>

**가상 메모리의 단점, 스래싱 (Thrashing)**   

하드디스크나 SSD는 RAM보다 압도적으로 느리기 때문에 데이터가 RAM과 디스크를 자주 오고 가면 성능 저하가 발생한다.   

`스래싱(Thrashing)`  
동시에 너무 많은 프로그램을 켜거나 RAM 용량이 극도로 부족해지면, CPU가 실제 연산을 하는 시간보다 하드디스크와 RAM 사이에 데이터를 주고받는(스래싱) 시간이 더 길어지는 현상이 발생한다. 이 상태가 되면 컴퓨터가 극도로 버벅거리거나 "응답 없음" 상태에 빠지게된다.   

간단하게 요약하자면,   
가상 메모리는 RAM의 한계를 넘기 위해 디스크 공간을 빌려 쓰는 기술이다.   
페이지 테이블을 통해 가상 주소를 실제 RAM 주소로 변환한다.   
당장 필요한 부분만 RAM에 올리며, RAM이 부족하면 디스크의 페이징 파일(Swap 영역)을 활용한다.   
디스크는 RAM보다 느리므로, 과도한 가상 메모리 의존은 스래싱(성능 저하)을 유발한다.   

  </p>
</details>

#### <!-- 26.06.23 -->
<details> 
  <summary>26.06.23</summary>
  <p>

어제 공부한 가상 메모리와 그전에 공부했던 부분들을 합쳐서 조금더 공부해봤다.   

**프로세스 독립성의 비밀 (컨텍스트 스위칭의 부담 완화)**

가상 메모리는 각 프로세스에게 "이 컴퓨터의 메모리(예: 4GB/8GB)는 전부 내 거야"라는 환상을 심어준다. 이를 가상 주소 공간(Virtual Address Space)이라고 한다.   

가상 메모리 덕분에 프로세스 A와 B는 물리 메모리(RAM)의 전혀 다른 위치를 가리키고 있다. OS는 컨텍스트 스위칭 시 메모리 자체를 뒤엎는 게 아니라, 가상 주소를 물리 주소로 번역해 주는 페이지 테이블(Page Table)의 기준 주소(포인터)만 슥 바꿔준다. 이 덕분에 컨텍스트 스위칭이 비약적으로 빨라진다.   

<br/>

**스레드(Thread)가 메모리를 공유하는 방식**   

스레드는 프로세스 내에서 Stack만 따로 쓰고 Code, Data, Heap 영역을 공유한다고 배웠다. 가상 메모리 관점에서 보면 이게 아주 명확해진다.   

스레드의 주소 공간: 같은 프로세스에 속한 스레드들은 동일한 가상 주소 공간(페이지 테이블)을 공유한다.   

예를 들어, 스레드 1이 가상 주소 0x1000에 있는 데이터를 수정하면, 스레드 2가 0x1000을 바라보았을 때 정확히 같은 물리 메모리의 데이터를 보게 된다.   
바로 이 공유 주소 공간 때문에, 여러 스레드가 같은 가상 주소(Heap이나 Data 영역)에 동시에 접근하려다 보니 경쟁 상태(Race Condition)가 발생하는 것이다.   

<br/>

**메모리 보호 (Memory Protection)**   

만약 가상 메모리가 없고 모든 프로세스가 물리 메모리 주소에 직접 접근한다면?   

프로세스 A(예: 악성코드나 버그가 있는 프로그램)가 포인터 연산을 잘못해서 프로세스 B의 메모리 영역 주소를 찔러버릴 수 있다. 그러면 프로세스 B가 갑자기 죽거나, 심지어 OS 영역을 건드려 블루스크린이 뜰 수 있다.   

가상 메모리의 해결책: 프로세스는 오직 자기에게 할당된 가상 주소만 볼 수 있다. OS는 페이지 테이블을 거치지 않는 물리 주소 접근을 원천 차단한다. 만약 프로세스가 허용되지 않은 가상 주소를 찌르면, CPU와 OS가 이를 감지해 그 유명한 Segmentation Fault (또는 Access Violation) 에러를 내뿜으며 해당 프로세스만 강제 종료시킨다. 다른 프로세스는 안전하게 보호된다.   

**페이지(Page)와 페이지 폴트(Page Fault)**   
가상 메모리는 메모리를 페이지(Page)라는 작은 단위(보통 4KB)로 쪼개서 관리한다.   

요청 페이징 (Demand Paging): 프로세스가 실행된다고 해서 그 프로그램의 모든 코드와 데이터를 RAM에 다 올리지 않는다. 지금 당장 실행에 필요한 페이지 몇 개만 RAM에 올린다.   

페이지 폴트 (Page Fault): 스레드가 열심히 일하다가 "어, 다음 코드를 실행해야 하는데 이 가상 주소에 매핑된 데이터가 아직 RAM(물리 메모리)에 없네?"라고 CPU에 찌르는 상황이다.   

작동 순서   
CPU가 하던 일을 멈추고 OS 인터럽트를 발생시킵니다. (컨텍스트 스위칭과 유사한 비용 발생)   
OS는 하드디스크(SSD)의 스왑 영역에서 필요한 데이터를 찾아 RAM의 빈 곳에 올린다.   
페이지 테이블을 업데이트하고, 멈췄던 스레드를 다시 실행한다.   

만약 RAM이 너무 부족하면 OS는 계속해서 하드디스크에서 페이지를 넣었다 뺐다 하는 작업만 반복하게 된다. CPU는 일은 안 하고 페이지 교체만 하느라 바빠지는데, 이 현상을 **쓰레싱(Thrashing)**이라고 한다. 시스템이 엄청나게 버벅거리는 원인이다.   

<br/>

**Build.cs 파일 구성**   

**Public Dependency**   
헤더(.h)와 소스(.cpp) 모두에서 사용하는 모듈   
**Private Dependency**   
소스(.cpp) 파일에서만 사용하는 모듈   

  </p>
</details>

#### <!-- 26.06.25 -->
<details> 
  <summary>26.06.25</summary>
  <p>

에이타니   

멀티플레이어 게임에서 클라이언트의 요청을 서버가 검증하고 모든 클라이언트에 전파하는 일반적인 패턴은 다음과 같다   

`Client → Server RPC`: 클라이언트가 `UFUNCTION(Server, Reliable, WithValidation)`으로 선언된 함수를 호출하여 서버에 요청을 보낸다.   

`Server_Validate`: 서버에서 요청의 유효성을 검증한다. 치팅 방지를 위해 필수적이다.   

`Server_Implementation`: 검증이 통과되면 실제 로직이 실행된다.   

`NetMulticast`: 서버에서 모든 클라이언트에게 결과를 전파하기 위해 `UFUNCTION(NetMulticast, Reliable)` 함수를 호출한다.   

`RPC`는 네트워크 통신을 사용하기 때문에 네트워크 지연의 영향을 받으며, `Unreliable`로 설정된 경우 신뢰성이 보장되지 않는다.   




<br/>

화요일에 이어서 가상메모리에서의 페이지 폴트 관련해서 더 알아봤다.   

운영체제는 프로그램을 일정한 크기의 조각인 페이지로 나누어 필요한 부분만 RAM에 올리는 `Demand Paging` 방식을 사용합니다.
RAM에 올라와 있는 페이지 조각을 `프레임(Frame)`이라고 하고 이를 페이지 `테이블(Page Table)`에 기록해둡니다.   

프로세스를 실행할 때 CPU는 `MMU(Memory Management Unit)`에 Virtual Address를 요청하고 `TLB(Translation Lookaside Buffer)`에서 물리주소를 알아내고 RAM으로 이동합니다.   
이때, 물리메모리가 존재하지 않으면 `Page Fault`라는 `Interrput`를 발생시키고 OS는 저장장치에서 Page를 찾아서 RAM에 업로드를 하고 CPU는 다시 Virtual Address 요청을 합니다.   

인터럽트   
CPU 내부에서 급하게 처리해야 하는 일이 발생하면, 현재 하던 일을 잠깐 멈추고 그 급한 일부터 처리하도록 하는 메커니즘   

**인터럽트 처리 과정**   

현재 상태 저장   
CPU는 하던 일을 멈추기 직전, 나중에 돌아와서 다시 이어서 할 수 있도록 현재 CPU 레지스터 값들과 프로그램 카운터(PC) 위치를 메모리의 스택(Stack) 공간에 안전하게 저장합니다.   
인터럽트 벡터(Interrupt Vector) 확인   
CPU는 발생한 인터럽트의 번호(ID)를 확인합니다. 그리고 메모리 한구석에 있는 '인터럽트 벡터 테이블'을 봐서, 이 번호일 때는 어떤 코드를 실행해야 하는지 주소를 찾습니다.   
인터럽트 서비스 루틴(ISR) 실행   
인터럽트를 해결하기 위해 OS가 미리 준비해 둔 함수(코드)인 ISR(Interrupt Service Routine) 또는 인터럽트 핸들러를 실행합니다.   

페이지 폴트라면? 디스크에서 페이지를 RAM으로 올려주는 ISR이 실행됩니다.   
처리가 끝나면, 아까 스택에 저장해 두었던 이전 상태를 CPU 레지스터에 복구하고, 멈췄던 원래 프로그램의 위치로 돌아가서 실행을 재개합니다.   

  </p>
</details>

#### <!-- 26.06.26 -->
<details> 
  <summary>26.06.26</summary>
  <p>

GAS 일부 정리   

Gameplay Effect BP 설정에서

중첩없는 즉발
Instant

쿨타임
Has Duration
Scalable Float Magnitude에 쿨타임 초 입력

Aggregate by Target
내 캐릭터 기준으로 Stack Limit Count
Stack Limit Count가 2면 적이 아무리 많아도
내 캐릭터는 최대 2중첩만 받음

Aggregate by Source
적 캐릭터 기준으로 Stack Limit Count
Stack Limit Count가 2고 적이 4마리면
플레이어는 8중첩을 받음

10초동안 3초마다 한 번씩 데미지가 들어오는 점화 예시
Stack Duration Refresh Policy
10초를 리프레시해서 10초로 다시 만듦

Stack Period Reset Policy
3초 카운팅을 하는걸 초기화 함 (1초.. 2초.. 이때 초기화하면 다시 1초부터 시작해서 점화 데미지가 늦게 들어오게 됨) 


디버깅 하는 법
Stamina에 변수이름
AbilitySystem.DebugAttribute Stamina

GE 디테일에서
Execute Periodic Effect on Application 체크 해제하면 첫 데미지 안들어감

GA에서
Wait Target Data를 Event ActivateAbility랑 연결하고
Confirmed로 Type을 User Confirmed로 설정하면 롤 스킬 스마트키 안한 상태(범위 보여주고 누르면 실행) 됨   

  </p>
</details>

#### <!-- 26.06.29 -->
<details> 
  <summary>26.06.29</summary>
  <p>

저번 프로젝트에서 Root Motion을 활용해서 AI의 캡슐 컴포넌트를 공중으로 띄웠는데 이번에 맡은 플레이어 캐릭터의 점프와 어떤 차이가 있는지 궁금해져서 찾아봤다.   

**AI의 점프**   

구동 주체: 애니메이션 에셋   
3D 맥스나 마야 같은 툴에서 애니메이터가 캐릭터의 'Root(최상위) 본'을 위로 들어 올리는 애니메이션을 만든다. 언리얼 엔진은 이 애니메이션이 재생될 때, Root 본의 위치 변화량(Delta)을 추출하여 캐릭터의 캡슐 컴포넌트 위치로 강제 전환(수행)시킨다.   
애니메이터가 의도한 정교하고 역동적인 연출(예: 벽을 짚고 점프, 공중 덤블링)을 완벽하게 표현할 수 있지만, 재생 중에는 캐릭터 무브먼트 컴포넌트의 일반적인 물리 법칙이나 플레이어의 즉각적인 조작 입력을 무시하게 된다.   

**플레이어의 점프**   

구동 주체: 캐릭터 무브먼트 컴포넌트(Character Movement Component)와 물리 엔진   
애니메이션과 상관없이, 점프 키를 누르는 순간 캐릭터의 캡슐 컴포넌트(Capsule Component)에 위쪽 방향으로 순간적인 속도(Velocity/Impulse)를 가한다.   
애니메이션은 캡슐이 허공으로 떠오르는 물리적 움직임에 맞춰 "공중에 떠 있는 것처럼 보이는 시각적 효과"만 흉내 낼 뿐이다. 애니메이션이 있든 없든 캡슐은 무조건 위로 솟구친다.   

<br/>

---

<br/>

**GAS로 플레이어 Kick 스킬 설계**   

Kick을 하는 능력을 위해서 GAS로 간단하게 설계를 해봤다.   

1. Character에 `Ability System Component`를 부착시켜서 능력을 가질 수 있게 만든다.   
2. `Gameplay Ability`로 Kick을 만든다. 입력 받으면 Kick이 실행되고 애니메이션이 재생되며 `Overlap 혹은 Trace`를 통해 축구공이 있는지 확인을 하고 판정을 내린다.   
3. Kick과 관련된 태그들을 만든다.   
`State.Character.Kicking` : 캐릭터가 Kick하는중인 상태를 나타내는 태그   
`Ability.Active.Kick` : 능력을 활성화 하는 태그   

<br/>

**GA_Kick의 내부 로직**   

1. Ability Activated    
2. Play Montage and Wait(네트워크 동기화됨)   
	애니메이션 중 공을 차는 타이밍에 AnimNotify 활용 가능   
3. Target Data / Overlap Test   
	캐릭터 앞 가상의 공간에 축구공이 있는지 검사   
4. Apply Physics Impulse(축구공을 찾았다면)   
	서버(Server) 권한으로 축구공에 Add Impulse 실행   
5. End Ability    

<br/>

---

<br/>

**메모리 단편화와 해결방법**   

이전에 메인으로 공부하진않고 관련 키워드로 본 적이 있는데 이번에 제대로 공부해보았다.   

**메모리 단편화(Memory Fragmentation)**   
힙에서 메모리를 할당, 해제를 반복하다보니 메모리 공간은 남아있는데 할당을 하지 못하는 비효율적인 상태를 말합니다.   

**외부 단편화(External Fragmentation)**   
중간중간 비어있는 공간의 총 합은 큰데, 그 비어있는 공간들이 새로운 메모리를 할당하기엔 크기가 충분하지 않아서 할당을 못하는 상태입니다.   
예시) 총 10mb의 공간이 있지만 2mb씩 쪼개져있다고 한다면 5mb짜리 큰 메모리는 할당하지 못합니다.   

**내부 단편화(Internal Fragmentation)**   
메모리 할당자가 고정된 블록 단위(예: 8, 16바이트)로 메모리를 건네주다 보니, 실제 요청한 크기보다 더 큰 메모리가 할당되어 낭비되는 공간이 생기는 상태입니다.   
예시) 내부적으로 16바이트 단위로만 할당하는데 개발자가 12바이트만 요청하면 남은 4바이트는 낭비되는 공간이 됩니다.   

그렇다면 해결방법은?   

첫번째로 지난번에 공부했던 Paging기법이 있다.   
물리 메모리를 `Frame`으로 나누고 같은 크기로 가상 메모리를 `Page`로 나눈다.   
연속되지 않은 물리 메모리(외부 단편화의 원인)를 마치 연속된 것 처럼 가상메모리에서 저장을 하므로 외부 단편화는 완전히 해결된다.   
단, 페이지도 결국 4KB 단위로 나누기 때문에 내부 단편화는 일부 남아있을 수 있다.   

두번째로 세그멘테이션(Segmentation) 기법이 있다.   
메모리를 고정된 크기가 아니라, 가변적인 크기의 `논리적 단위(Code, Data, Stack, Heap 등 세그먼트)`로 나누어 할당한다.   
딱 필요한 크기만큼만 할당하므로 내부 단편화는 발생하지 않지만, 세그먼트들의 해제와 할당이 반복되면 다시 외부 단편화가 발생할 수 있다.   

세번째로 메모리 압축(Compaction) 및 통합(Coalescing, 코얼레싱)이 있다.   
압축(디스크 조각 모음과 유사): 메모리상에 분산되어 있는 사용 중인 블록들을 한쪽으로 몰고, 빈 공간들을 하나로 모으는 방법이다.   실제 물리 주소가 바뀌기 때문에 모든 연산을 중단하고 주소록을 갱신해야한다. 따라서 메모리 오버헤드가 발생한다.   
메모리 통합 (Coalescing): 메모리가 해제될 때, 앞 뒤 주소가 비어있다면 합쳐서 하나의 메모리 블록으로 만들어서 외부 단편화를 완화한다.   

마지막으로 메모리 풀(Memory Pool)이 있다.   
필요한 크기의 메모리 블록을 미리 왕창 할당(Allocation)받아 놓고, 필요할 때마다 풀에서 꺼내 쓰고 반납하는 방식이다.   
new나 malloc을 통해 OS에 수시로 메모리를 요청하는 행위 자체를 줄이므로, 동적 할당으로 인한 외부 단편화를 원천 차단하고 성능을 크게 향상시킬 수 있다. 단, 내부 단편화는 어쩔 수 없다.     

<br/>

+추가   
세그멘테이션에 대해서 조금 더 자세히 알아보았다.   

세그멘테이션(Segmentation)은 메모리를 물리적인 고정 크기로 쪼개는 것이 아니라, 프로그래머가 바라보는 논리적인 개념(의미) 단위로 나누어 물리 메모리에 배치하는 방식이다.   

논리적 단위인 세그먼트(Segment)는 프로그램의 구조를 바탕으로 나뉜다.   
메인 함수, 서브 루틴(함수), 전역 변수(Data), 실행 코드(Code), 스택(Stack), 힙(Heap) 등이 각각 하나의 세그먼트가 된다.   

**페이징과 세그멘테이션 비교!**   

페이징   
물리적인 크기로 쪼갬   
고정된 크기   
외부 단편화 해결, 내부 발생 가능   
페이지 테이블 사용   

세그멘테이션   
논리적인 기준   
가변 크기   
내부 단편화 해결, 외부 발생 가능   
세그먼트 테이블 사용   

  </p>
</details>

#### <!-- 26.06.30 -->
<details> 
  <summary>26.06.30</summary>
  <p>

에이타니   

`NavModifierVolume`은 이미 생성된 NavMesh의 특정 영역에 속성을 부여하여 AI의 경로 탐색 행동을 제어하는 볼륨이다. 이를 통해 특정 영역의 비용(Cost)을 조정하거나, 영역을 완전히 차단하여 AI가 해당 구역을 회피하도록 만들 수 있다. 예를 들어, 위험 지역이나 장애물 주변에 `NavModifierVolume`을 배치하여 AI가 우회 경로를 선택하도록 유도할 수 있다.   

<br/>

GAS와 기존 IMC를 연결해서 스킬 입력하기   

GAS를 이용해서 축구공을 차는 간단한 스킬을 만들어봤다. 잘 동작했지만 차징을 해서 더 강하게 공을 차는 기능으로 업그레이드 할 때 문제가 발생했다.   
차징을 하는 키를 GAS와 연동시켜줘야 했다.   

Character의 `SetupPlayerInputComponent` 함수에서 평소에 IMC 등록에 아래 코드를 잘 추가해준다.   
```cpp
// 1. Character.h에 열거형으로 먼저 만들어준다.

// 현재는 Kick만 추가하여서 Kick만 등록해준상태
UENUM(BlueprintType)
enum class ESGAbilityInputID : uint8
{
	None			UMETA(DisplayName = "None"),
	Confirm			UMETA(DisplayName = "Confirm"),
	Cancel			UMETA(DisplayName = "Cancel"),
	// --- 추가 항목 ---
	Kick			UMETA(DisplayName = "Kick")
	// Dash			UMETA(DisplayName = "Dash"),
	// Jump			UMETA(DisplayName = "Jump")
};


// 2. Character.h에 함수들을 등록한다.

// 첫번째는 ASC를 캐릭터에 부착하기 위함이라 IA와 GAS 연동과는 상관없다.
// 두번째는 기존 IA 만드는 것과 동일하다.
// 세번째는 GA_Kick을 에디터에서 등록하기 위함이다.
protected:
	// ASC 세팅
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "GAS")
	TObjectPtr<UAbilitySystemComponent> AbilitySystemComponent;
	
	// Kick 버튼
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Input")
	class UInputAction* IA_Kick;
	
	// 에디터에서 할당할 발차기 GA 클래스 타입
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "GAS")
	TSubclassOf<class UGameplayAbility> KickAbilityClass;

// 3. Character.cpp
// 래핑할 함수 구현

void ASG_Character::AbilityInputPressed(int32 InputID)
{
	if (AbilitySystemComponent)
	{
		AbilitySystemComponent->AbilityLocalInputPressed(InputID);
	}
}

void ASG_Character::AbilityInputReleased(int32 InputID)
{
	if (AbilitySystemComponent)
	{
		AbilitySystemComponent->AbilityLocalInputReleased(InputID);
	}
}


// 4. Character.cpp 
// IA 바인딩 해준다.

if (AbilitySystemComponent)
		{
			FTopLevelAssetPath AbilityInputBindsAssetPath = FTopLevelAssetPath(TEXT("/Script/SoccerGame"), TEXT("ESGAbilityInputID"));
			
			AbilitySystemComponent->BindAbilityActivationToInputComponent(EnhancedInputComponent, 
			FGameplayAbilityInputBinds(
				FString("Confirm"), 
				FString("Cancel"), 
				AbilityInputBindsAssetPath, 
				static_cast<int32>(ESGAbilityInputID::Confirm), 
				static_cast<int32>(ESGAbilityInputID::Cancel)
				)
			);
			
			if (IA_Kick)
			{
				// 누르는순간 GAS에 Press 신호 전달
				EnhancedInputComponent->BindAction(IA_Kick, ETriggerEvent::Started, this, &ASG_Character::AbilityInputPressed, static_cast<int32>(ESGAbilityInputID::Kick));
            
				// 떼는 순간 GAS에 Release 신호 전달 (WaitInputRelease Task가 이 신호를 감지)
				EnhancedInputComponent->BindAction(IA_Kick, ETriggerEvent::Completed, this, &ASG_Character::AbilityInputReleased, static_cast<int32>(ESGAbilityInputID::Kick));
			}
		}
```

`BindAbilityActivationToInputComponent` 시스템을 사용하면, 내가 로컬에서 마우스를 누르고 뗐다는 신호가 내부적으로 서버(Server)까지 자동으로 리플리케이션(전달)된다. 그렇기 때문에 C++ 내부의 `WaitInputRelease` 태스크가 멀티플레이어 환경에서도 클라/서버 양쪽에서 완벽하게 싱크가 맞아떨어지며 작동할 수 있는 것이다.   

<br/>

**오늘 GAS를 사용하면서 느낀 부분**   

차징하는 시간만큼 강해지는 Kick을 GA로 구현하였는데 원래라면 타이머를 사용해서 시간을 측정했어야했다. 하지만 GAS와 EnhancedInputSystem을 사용해서 그 부분을 비동기 방식으로 구현할 수 있었다.   
퍼포먼스도 최적화 되고 지금 당장은 적용하진 않았지만 네트워크 동기화 부분에서도 내부적으로 알아서 해준다고 한다.   

비동기 상태 대기(Asynchronous State Waiting)   
WaitInputRelease Task -> OnInputReleased 순으로 진행된다.   
오늘 구현한 마우스를 누르는 순간 시간을 기록하고 마우스 떼는 Input을 기다리다가 떼는 순간 콜백함수를 호출하는 형식인것이다.   

  </p>
</details>

#### <!-- 26.07.01 -->
<details> 
  <summary>26.07.01</summary>
  <p>

에이타니   

**BT의 Service**   
Service는 Task와 달리 Success/Failure 같은 실행 결과를 반환하지 않는다. Service는 백그라운드에서 주기적으로 실행되며, 주로 Blackboard 값을 업데이트하거나 환경을 감지하는 역할을 한다. 트리의 흐름 제어는 Task, Decorator, Composite 노드의 역할이다.   

**GetStaticDescription**   
UBTNode에서 부가적인 설명을 텍스트로 노출할 수 있도록 도와주는 가상함수   
매개변수가 없고 고정된 프로퍼티 상태 표시   

이 함수를 오버라이드하여 FString을 반환하면, 해당 문자열이 에디터 화면의 노드 하단에 상시 표시되므로, 어떤 Blackboard 키가 연결되어 있는지 쉽게 파악할 수 있어 상황별 행동 설계와 디버깅 효율이 크게 향상된다.   

**GetRuntimeDescription**   
공유 인스턴스 환경에서 런타임 시 특정 AI 에이전트만의 고유 메모리 상태(예: 개별 진행률)를 노출하고 싶을 때 사용한다.   

<br/>

**AI Perception 시스템**   

1. AI Controller에 AI Perception Component 추가   
2. AIPerceptionComponent에 AISenseConfig_Sight를 추가하고 감지 반경, 시야각, 감지 팀 등을 설정   
3. On Target Perception Updated 이벤트 바인딩   

<br/>

**AI Perception 시스템에서의 청각 감지**   
AI Perception 시스템에서 청각 감지를 위해서는 소리를 발생시키는 액터에서 MakeNoise() 함수를 호출해야한다.   
이 함수는 Pawn Controller를 통해 소리 이벤트를 생성하고, AIPerceptionComponent의 AISenseConfig_Hearing이 이를 감지할 수 있게 한다.   

우리가 보통 알고 있는 PlaySound()는 그냥 소리만 재생할뿐 AI와 상관이 없다.   

<br/>

---

<br/>

GAS를 사용하는 캐릭터에서 Montage를 플레이하려는데 GA에서 AnimNotify를 불러올 수 없는 문제가 있었다.   

찾아보니 AbilityTask를 사용해서 몽타주를 실행시켜줘야했다.   

`AbilityTask_PlayMontageAndWaitForEvent`를 사용하라고 나와서 사용해보려고 했더니 이 Task는 UE5에서 기본으로 제공하는 기능이 아니라 에픽게임즈 공식샘플에 있는 커스텀 Task라고 한다.   

위 커스텀 Task는 `PlayMontageAndWait`과 `WaitGameplayEvent`의 기능을 제공한다고 보면 된다.   
그래서 나는 일단 커스텀 Task가 아닌 위 두가지를 사용하여 구현해보려고 한다.   

```cpp
// 2가지 기능을 사용하기위한 헤더들
#include "Abilities/Tasks/AbilityTask_PlayMontageAndWait.h"
#include "Abilities/Tasks/AbilityTask_WaitGameplayEvent.h"

// 몽타주를 재생하고
UAbilityTask_PlayMontageAndWait* PlayMontageTask = UAbilityTask_PlayMontageAndWait::CreatePlayMontageAndWaitProxy(
		   this,
		   NAME_None, 
		   MontageToPlay, 
		   1.0f, 
		   NAME_None, 
		   true
		);


// 태그 이벤트를 기다리는 Task를 만들고
		UAbilityTask_WaitGameplayEvent* WaitEventTask = UAbilityTask_WaitGameplayEvent::WaitGameplayEvent(
		   this, 
		   MyAbilityTag,     // 에디터에서 설정한 GA_SG_Kick의 Tag
		   nullptr,          // Optional External Optional Actor
		   false             // bOnlyTriggerOnce (한 번만 트리거할지 여부)
		);

// 조건에 맞으면 실행
if (WaitEventTask)
		{
			// 이벤트가 들어오면 실행할 함수 바인딩
			WaitEventTask->EventReceived.AddDynamic(this, &UGA_SG_Kick::OnGameplayEventReceived);
			WaitEventTask->ReadyForActivation();
		}
```

<br/>

---

<br/>

오늘 구현하면서 알게된 것들 정리

**K2_ 접두사**   
원본 `EndAbility`의 복잡한 인자들을 넘길 필요 없이, 인스턴스 기반 어빌리티에서 멤버 변수를 활용해 능력을 끝내는 `K2_EndAbility()`를 사용해봤다. 단, 마지막 두 인자가 true, false가 고정된 상태로 전달되기 때문에 다른값을 넣기 위해선 원본을 사용하거나 따로 함수를 만들어서 깔끔하게 만들 수 있다.   

**커스텀 AN을 사용하여 Event 발동**    
몽타주에서 직접 커스텀 제작한 블루프린트 노티파이(AN_SendGameplayEvent)를 사용하여 Event Tag에 맞는 Event(GA_Kick)를 발동시켰다.   

**GA C++ 파일에서 본인의 AbilityTags를 가져오기**   
`AbilityTags` 멤버 변수 직참조 방식에서 캡슐화가 적용된 `GetAssetTags()` 함수 호출 방식으로 코드를 전면 리팩토링하여 추후 버전 업데이트시 사용이 불가능할 수 있다는 경고를 해결했다.   
```cpp
// 바로 이부분..!
// 어빌리티 태그 정보가 private 일 수도 있어서 엔진이 제공하는 GetAssetTags()라는 함수를 사용하여 불러와야한다.
		FGameplayTagContainer AssetTagsContainer = GetAssetTags();
		FGameplayTag MyAbilityTag = FGameplayTag::EmptyTag;
		if (AssetTagsContainer.Num() > 0)
		{
			MyAbilityTag = AssetTagsContainer.GetByIndex(0);
		}
```

  </p>
</details>

#### <!-- 26.07.02 -->
<details> 
  <summary>26.07.02</summary>
  <p>

에이타니   

**AI Perception**   

`AIPerceptionComponent`에서 특정 액터에 대한 감지 정보를 가져오려면 `GetActorsPerception()` 함수를 사용해야 한다. 이 함수는 감지된 액터와 `FActorPerceptionBlueprintInfo` 구조체를 매개변수로 받아 해당 액터에 대한 모든 감각 정보를 반환한다.   

`Lose Sight Radius`는 `Sight Radius`보다 `크거나 같게` 설정해야 한다. 이는 `히스테리시스(hysteresis)` 개념으로, 대상이 감지 범위 경계에서 약간만 움직여도 감지/미감지가 반복되는 것을 방지한다. 예를 들어 Sight Radius가 1000이고 Lose Sight Radius가 1200이면, 대상을 1000 이내에서 감지하고 1200 밖으로 나가야 놓치게 되어 안정적인 감지 시스템을 구현할 수 있다.   

`Peripheral Vision Angle`(주변 시야각)은 AI가 전방을 기준으로 좌우 얼마만큼의 각도 내에 있는 대상을 볼 수 있는지를 정의한다. 예를 들어 90도로 설정하면 AI는 전방 180도(좌우 각 90도) 범위 내의 대상만 감지할 수 있다. 이는 시각 감지에만 적용되는 속성이며, 회전 속도나 청각 감지와는 무관하다.   

**BT**   

AI의 행동을 조건에 따라 전환하는 스테이트 머신을 구현할 때는 Blackboard와 Behavior Tree의 조합이 가장 적절하다.   
`Blackboard`는 AI의 상태 정보(플레이어 발견 여부, 타겟 위치 등)를 저장하는 공유 메모리 역할을 한다.   
`Selector` 노드는 우선순위에 따라 자식 노드를 실행하며, 조건이 만족되면 해당 분기를 선택한다.   
`Decorator`는 조건을 체크하여 특정 Sequence의 실행 여부를 결정한다.   


  </p>
</details>

#### <!-- 26.07.03 -->
<details> 
  <summary>26.07.03</summary>
  <p>

`Listen Server`로 `GA_Kick`을 실행했을 때 `Released`가 4번이나 중복해서 발생하는 현상   

현재 GA_Kick은 Enhanced Input System과 GAS 내장 RPC가 이중으로 겹쳐서 작동하는 구조이다.   
따라서, 이렇게 찍히는게 자연스러운 현상이라고 한다.   


애니메이션 몽타주가 내 클라에서만 보이고 다른곳에선 안보이는 현상   

네트워크 설정 문제일 가능성 99%

```cpp
// 일단 이걸 켜준다.
GetMesh()->SetIsReplicated(true);

// GameAbility에 내장된 함수로 바꿔줬다.   
void UGA_SG_Kick::InputReleased(const FGameplayAbilitySpecHandle Handle, const FGameplayAbilityActorInfo* ActorInfo, const FGameplayAbilityActivationInfo ActivationInfo)
{
    Super::InputReleased(Handle, ActorInfo, ActivationInfo);
	
    float CurrentTime = GetWorld() ? GetWorld()->GetTimeSeconds() : 0.0f;
    float ActualChargeTime = CurrentTime - ChargeStartTime;
	
	FString NetMode = HasAuthority(&CurrentActivationInfo) ? TEXT("서버") : TEXT("클라이언트");
    UE_LOG(LogTemp, Log, TEXT("[%s] 마우스 입력 해제, 누른 시간: %f 초"), *NetMode, ActualChargeTime);
    
    float BaseKickPower = 1000.0f;
    UAbilitySystemComponent* ASC = GetAbilitySystemComponentFromActorInfo();
    if (ASC)
    {
       const UGAS_SG_CharacterAttributeSet* AttributeSet = ASC->GetSet<UGAS_SG_CharacterAttributeSet>();
       if (AttributeSet)
       {
          BaseKickPower = AttributeSet->GetKickPower();
       }
    }
    
    float ChargeRatio = FMath::Clamp(ActualChargeTime / MaxChargeTime, 0.0f, 1.0f);
    float FinalMultiplier = FMath::Lerp(1.0f, MaxPowerMultiplier, ChargeRatio);
    CachedFinalKickPower = BaseKickPower * FinalMultiplier; 
    
    UAnimMontage* MontageToPlay = nullptr;

    if (ActualChargeTime < ActionSplitTime)
    {
       UE_LOG(LogTemp, Log, TEXT("숏 차징 (%f초) -> 패스 모션 재생"), ActualChargeTime);
       MontageToPlay = PassMontage;
    }
    else
    {
       UE_LOG(LogTemp, Log, TEXT("롱 차징 (%f초) -> 슛 모션 재생"), ActualChargeTime);
       MontageToPlay = ShootMontage;
    }

    if (MontageToPlay)
    {
       UAbilityTask_PlayMontageAndWait* PlayMontageTask = UAbilityTask_PlayMontageAndWait::CreatePlayMontageAndWaitProxy(
          this, NAME_None, MontageToPlay, 1.0f, NAME_None, true
       );
       
       if (PlayMontageTask)
       {
          PlayMontageTask->OnCompleted.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
          PlayMontageTask->OnBlendOut.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
          PlayMontageTask->OnInterrupted.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
          PlayMontageTask->OnCancelled.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
          PlayMontageTask->ReadyForActivation();
       }
       
       FGameplayTagContainer AssetTagsContainer = GetAssetTags();
       FGameplayTag MyAbilityTag = FGameplayTag::EmptyTag;
       if (AssetTagsContainer.Num() > 0)
       {
          MyAbilityTag = AssetTagsContainer.GetByIndex(0);
       }

       UAbilityTask_WaitGameplayEvent* WaitEventTask = UAbilityTask_WaitGameplayEvent::WaitGameplayEvent(
          this, MyAbilityTag, nullptr, false
       );
       
       if (WaitEventTask)
       {
          WaitEventTask->EventReceived.AddDynamic(this, &UGA_SG_Kick::OnGameplayEventReceived);
          WaitEventTask->ReadyForActivation();
       }
    }
    else
    {
       K2_EndAbility();
    }
}
```

  </p>
</details>

#### <!-- 26.07.06 -->
<details> 
  <summary>26.07.06</summary>
  <p>


에이타니   

**Event Dispatcher**    
Event Dispatcher 패턴의 핵심은 발신자(NPC A)가 수신자(NPC B)를 직접 알 필요 없이 이벤트를 브로드캐스트하는 것이다. NPC A가 NPC B의 함수를 직접 호출하면 Event Dispatcher를 사용하는 의미가 없고, 강한 결합이 발생한다. Event Dispatcher는 1:N 통신에 매우 효과적이다.   

<br/>

축구공은 인식 안되는 Collision 오류   

단순하게 Collision을 추가안해서 생겼다.
```cpp
// Pawn(플레이어/AI) 타입 감지
ObjectTypes.Add(UEngineTypes::ConvertToObjectType(ECollisionChannel::ECC_Pawn)); 
	
// 축구공(물리 액터) 감지를 위해 PhysicsBody 추가
ObjectTypes.Add(UEngineTypes::ConvertToObjectType(ECollisionChannel::ECC_PhysicsBody));
```

<br/>

지난 언리얼 마스터 수업에서 배웠던 부분을 바로 활용   

```cpp
// Hp와 Stamina를 0과 100사이로 유지시켜준다.
void UGAS_SG_CharacterAttributeSet::PreAttributeChange(const FGameplayAttribute& Attribute, float& NewValue)
{
	Super::PreAttributeChange(Attribute, NewValue);
	
	if (Attribute == GetHpAttribute())
	{
		NewValue = FMath::Clamp(NewValue, 0.0f, GetMaxHp());
	}
	else if (Attribute == GetStaminaAttribute())
	{
		NewValue = FMath::Clamp(NewValue, 0.f, GetMaxStamina());
	}
	
	// GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, TEXT("PreAttributeChange"));
}

// PreAttributeChange에서만 해주면 Base 값은 저 범위를 벗어나기 때문에 범위를 벗어나는 순간 Hp를 Set해준다.
void UGAS_SG_CharacterAttributeSet::PostGameplayEffectExecute(const struct FGameplayEffectModCallbackData& Data)
{
	Super::PostGameplayEffectExecute(Data);
	
	if (Data.EvaluatedData.Attribute == GetHpAttribute())
	{
		// SetHp는 BaseHp를 Set해준다.
		SetHp(GetHp());
	}
	else if (Data.EvaluatedData.Attribute == GetStaminaAttribute())
	{
		SetStamina(GetStamina());
	}
	
	// GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, TEXT("PostGameplayEffectExecute"));
}
```

<br/>

GAS를 사용하며 네트워크 코드도 같이(Listen Server로 개발) 추가하고 있는데 서버에 대해서 다시 한 번 공부하고 정리했다.   

**리슨 서버 (Listen Server)**      
정의: 게임을 플레이하는 플레이어 중 한 명(방장)의 PC가 '서버 역할'과 '클라이언트(화면 렌더링) 역할'을 동시에 수행하는 구조입니다.   

**특징**   
방장 플레이어는 서버 권한(HasAuthority == true)을 가짐과 동시에, 로컬 컨트롤러(IsLocallyControlled == true)로 자신의 캐릭터를 조종합니다.   
방장의 화면에서는 네트워크 레이턴시(지연 시간)가 0입니다.   
다른 참여자(Client)들은 서버 역할을 하는 방장의 PC에 접속합니다.   

**데디케이트 서버 (Dedicated Server)**   
정의: 그래픽 화면(UI, 메시 렌더링)이 전혀 없고, 오직 게임의 물리 연산, 로직 검증, 동기화만 처리하는 순수한 독립 서버 프로그램입니다.   

**특징**   
모든 플레이어가 똑같이 클라이언트가 되며, 서버에 접속합니다.   
서버에는 플레이어가 존재하지 않으므로, 서버 컴퓨터 내부의 캐릭터들은 IsLocallyControlled가 무조건 false입니다.   
모든 플레이어가 공평하게 네트워크 레이턴시를 가집니다.   

<br/>

bReplicateInputDirectly = true; (어빌리티 생성자)   
클라이언트가 인풋(마우스 클릭 등)을 입력했을 때, 이 입력 신호를 서버로 직접 복제(Replicate)하겠다는 세팅입니다.   

왜 썼는가?   
드롭킥은 누르는 순간 즉시 시전됩니다. 클라이언트 화면에서 드롭킥 인풋(Started)이 터졌을 때, 이 신호가 서버로 즉시 전달되어 서버에서도 동일한 어빌리티가 예측(Prediction) 및 실행되도록 유도합니다. 루트 모션과 모션 워핑이 서버/클라이언트 양쪽에서 싱크가 맞추어 시작되도록 돕는 핵심 기반입니다.   

if (!HasAuthority(...)) return; (서버 권한 체크)   
이 코드를 실행하는 주체가 서버(Authority)인지 확인하고, 클라이언트라면 아래 로직을 실행하지 못하게 막는 방어벽입니다.   

리슨 서버에서의 동작   
방장이 드롭킥을 차면 HasAuthority가 참이므로 통과합니다. 클라이언트가 차면, 클라이언트 화면에서는 이 조건문에서 막히고, 서버에 복제되어 실행 중인 서버 측 어빌리티에서만 이 아래 로직이 실행됩니다.

축구공에 물리적인 힘을 가하거나(PushBall), 적에게 데미지 효과(GameplayEffect)를 주는 것은 절대로 클라이언트가 마음대로 결정해서는 안 되기 때문입니다. (클라이언트가 결정하게 하면 핵/변조에 취약해집니다.)   

UFUNCTION(NetMulticast, Reliable) (멀티캐스트 래그돌)   
의미: "서버에서 이 함수를 실행하면, 접속해 있는 모든 클라이언트(방장 포함)에게 이 함수를 원격 실행(RPC) 시켜라"라는 뜻입니다.

적 캐릭터가 드롭킥을 맞고 래그돌로 전환되어 날아가는 연출은 모든 사람의 화면에 똑같이 보여야 하는 시각적 연출입니다. 서버에서 데미지 판정을 마친 뒤, Multicast_ApplyRagdollPhysics를 호출함으로써 방장 화면과 클라이언트 화면 모두에서 적이 시원하게 날아가게 동기화한 것입니다.   

  </p>
</details>

#### <!-- 26.07.07 -->
<details> 
  <summary>26.07.07</summary>
  <p>

에이타니   

**XR 핸드트래킹**   
XR 핸드트래킹 구현에서 `Get Hand Joint Transform` 노드는 손의 각 관절(Joint)에 대한 실시간 위치와 회전 정보를 직접 가져올 수 있는 표준 방식이다. 이 노드를 통해 엄지, 검지, 중지 등 각 손가락의 특정 관절(팁, 중간 관절 등)의 Transform 데이터를 정확하게 추적할 수 있어 오브젝트 그랩, 포인팅, 제스처 인식 등의 상호작용을 구현할 수 있다.(`OpenXR Hand Tracking` 플러그인 필요)   

핸드트래킹 구현의 올바른 순서는 먼저 `Get Motion Controller` 노드로 왼손 또는 오른손을 선택하고, `Get Hand Joint Transform`으로 특정 관절(엄지 끝 등)의 위치를 얻은 후, `Sphere Trace` 또는 `Box Trace`로 충돌을 감지하고, `Hit Result`를 확인하는 것이다.   

**패키징**   
언리얼 엔진에서 프로젝트를 패키징할 때 필수적으로 설정해야 하는 항목은 Default Maps(시작 맵), 타겟 플랫폼, 빌드이다.   
LOD(Level Of Detail) 최적화는 성능 향상을 위한 권장사항이지만, 패키징을 위해 반드시 설정해야 하는 필수 항목은 아니다.   

<br/>

---

<br/>

축구공 네트워크 물리적용을 위해서 테스트용 블루프린트 액터를 C++로 우선 전환하였다. (디테일한 네트워크 설정을 위함)   

```cpp
// SG_SoccerBall.h
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "SG_SoccerBall.generated.h"

UCLASS()
class SOCCERGAME_API ASG_SoccerBall : public AActor
{
	GENERATED_BODY()
	
public:
	ASG_SoccerBall();
	// Mesh 접근 Getter 함수
	FORCEINLINE UStaticMeshComponent* GetSoccerBallMesh() const { return BallMesh; }

private:
	// 리플렉션, 에디터에선 접근 가능한 private  설정 meta = (AllowPrivateAccess = "true")
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Ball", meta = (AllowPrivateAccess = "true"))
	TObjectPtr<UStaticMeshComponent> SoccerBallMesh;

};

// SG_SoccerBall.cpp

#include "Character/SG_SoccerBall.h"

ASG_SoccerBall::ASG_SoccerBall()
{
	PrimaryActorTick.bCanEverTick = true;
	
	// 네트워크 복제 활성화
	bReplicates = true;
	SetReplicateMovement(true);

	SoccerBallMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("BallMesh"));
	RootComponent = SoccerBallMesh;

	// 물리 및 콜리전 설정 추가
	SoccerBallMesh->SetSimulatePhysics(true);
	SoccerBallMesh->SetCollisionProfileName(TEXT("PhysicsBody"));
}
```

<br/>

콘솔창에 네트워크 지연을 부여하여 현재 내 공의 반응속도를 체크해보았다.   
`NetEmulation.PktLag 150`   
공을 차고 0.2~ 0.3초 뒤에 날아가는 듯한 모습을 보여준다.   
캐릭터도 미세하게 뚝뚝 끊기는 모습을 보여준다.   
캐릭터로 공을 밀면서 같이 가면 공이 동기화가 제대로 되지 않아서 캐릭터가 뒤에서 매우 부자연스럽게 따라간다.   
서버와 클라이언트의 동기화가 제대로 되지 않는 모습   

<br/>

**이런 현상들이 발생하는 원인**   

캐릭터는 공 보다는 낫지만 부자연스러운 움직임을 보여주는 현상   
-> 원인   
`CharacterMovementComponent`는 원래 네트워크 지연 환경에서도 부드럽게 움직이도록 '클라이언트 측 예측(Client-side Prediction)' 기능이 기본적으로 탑재되어 있다.   
하지만 이 예측이 맞지 않아서 서버와의 차이가 발생해 어긋나는 것이다.   

축구공은 대놓고 매우매우 느린 반응속도를 보여주는 현상   
-> 원인   
공은 클라이언트에서 예측을 전혀 하지 않기때문에 오직 서버의 물리를 받고 있다.   
왕복 지연 시간(Ping)인 300ms + 패킷 처리 시간이 합쳐져서 느리게 반응하는 것.   

<br/>

**해결하기위한 여러가지 방안들**   

첫 번째로 단순하게 서버가 확인하는 빈도를 높여보았다.   

```cpp
NetUpdateFrequency = 100.0f; // 기본값( 보통 33이나 66)보다 올려서 서버가 더 자주 공 위치를 방송하게 함
MinNetUpdateFrequency = 33.0f;
```

결과 : 지연이 높은 상황에서 큰 차이가 없었다.   

두 번째로 네트워크 물리 공 보간(Interpolation)을 사용해서 서버와 클라를 자연스럽게 연결하는 방법을 시도해보았다.   

일단, 애니메이션 몽타주의 ANS, AN의 `Trigger Setting`에서 클라에서 실행되도록 설정을 해주었다. `Trigger on Follower`를 True로 설정.   

했지만 여전히 서버에서만 실행되는 문제가 발생.   

원인을 찾아보았다.   
이유는 바로 Kick을 할 때 공을 인식하는 부분과 사람들 인식하는 부분을 나눠서 구현했는데 둘 다 서버권한이 필요한 Event 함수에 묶어놨기 때문이었다.   

```cpp
// EventReceived 함수에 두 행위가 다 묶여있다.
void UGA_SG_Kick::OnGameplayEventReceived(FGameplayEventData Payload)
{
	if (!HasAuthority(&CurrentActivationInfo))
	{
		return;
	}
	
	UE_LOG(LogTemp, Log, TEXT("FindAndPushBall Test"));
	FindAndPushBall(); // 여기있는 이 함수를 밑으로 옮기고 이건 삭제
	
	OnEnemyHitReceived(Payload);
}
```

<br/>

마우스를 떼는 순간 공 부터 체크를 해서 서버/클라 양쪽에서 빠르게 실행되게 바꿔줘야한다.   

```cpp
// InputReleased 함수에서 FindAndPushBall()를 실행시켜준다.

// ... InputReleased 기존 로직

FindAndPushBall(); // 추가 

    if (MontageToPlay)
    {
		// ... 기존 로직
	}
```


<br/>

또 다시 생긴 문제점.   
이렇게 하면 차는 순간의 딜레이는 줄어들지만 몽타주 재생 전에 이미 발차기가 실행이 되고 네트워크과 클라에서 초반엔 공이 같이 움직이다가 중간에 멈췄다가 다시 튀어오름   

첫 번째 문제부터 해결해보자.....

몽타주 재생 전에 이미 발차기가 실행되는 문제   
원인 : 클라에서 똑같이 실행시키기 위해 구조를 바꿨더니 Kick을 하는 순간 공을 차는 함수가 실행됨   

해결법 : Delay를 줘서 실제 몽타주로 타격하는 시간쯤에 Kick이 발동하게 조절해준다.   

```cpp
// Delay 추가
#include "Abilities/Tasks/AbilityTask_WaitDelay.h"

float KickSyncDelay = 0.45f; // 딜레이 시간 설정
       
    	UAbilityTask_WaitDelay* WaitDelayTask = UAbilityTask_WaitDelay::WaitDelay(this, KickSyncDelay);
    	if (WaitDelayTask)
    	{
    		// 딜레이가 끝나면 (발이 정확히 공에 배달되면) 오버랩 판정 실행
    		WaitDelayTask->OnFinish.AddDynamic(this, &UGA_SG_Kick::FindAndPushBall);
    		WaitDelayTask->ReadyForActivation();
    	}
```

공을 차는 순간 동기화는 어느정도 됐다.   

<br/>

또 새로운 문제점   

공을 차면 클라이언트에서 중간에 멈췄다가 날아가는 현상   

원인 : 축구공은 무조건 서버 위치 기준으로 보간을 하게 되어있다. 근데 위에서 몽타주 동기화 해결을 하면서 로컬과 서버를 어느정도 맞춰버리면서 서버 위치를 기준으로 업데이트를 하면 오히려 어긋나게 됐다.  

```cpp
// 원인이 된 코드(축구공 C++ 내부)
// 문제 발생: 내 화면에서 이미 잘 날아가고 있는 공의 위치(CurrentLoc)를,
   // 150ms 전의 과거 서버 위치 정보가 담긴 TargetLoc를 향해 역으로 당겨버린다.
   FVector NewLoc = FMath::VInterpTo(CurrentLoc, TargetLoc, DeltaTime, InterpolationSpeed);
   SoccerBallMesh->SetWorldLocationAndRotation(NewLoc, NewRot);
```

<br/>

해결 방법 : 공을 찬 직후(에러가 나는 부분)에는 잠시 보간(Interpolation)을 끈다.   

```cpp
// 축구공 헤더파일에 보간을 잠깐 끄는 코드를 작성해준다.

public:
	// 외부에 오픈할 킥 반응 함수
	void HandleLocalPredictionKick();
	
private:
	// 로컬 예측 진행 중인 남은 시간 (이 시간이 0보다 크면 서버 동기화를 무시함)
	float PredictionInterpCooldown = 0.0f;


// 축구공 cpp의 Tick함수에서 보간을 패스하는 코드를 추가해준다.

// 쿨다운 타이머가 작동 중이라면 감소시키고 보간을 패스
if (PredictionInterpCooldown > 0.0f)
{
	PredictionInterpCooldown -= DeltaTime;
	return; // 공이 서버 위치로 바뀌어서 생기는 현상 차단
}

// 외부에 오픈할 킥 반응 함수 내부 구현
void ASG_SoccerBall::HandleLocalPredictionKick()
{
    // 렉 환경(150ms)을 고려하여 약 0.25초 동안 서버 패킷 보간을 차단
    PredictionInterpCooldown = 0.25f; 
}
```

이제 축구공을 차는 순간 차단하는 함수를 호출하게 세팅을 해줘야한다.   

```cpp
// 기존 AddImpulse 밑에 로컬인경우 서버를 잠시 차단하게 위에서 만든 함수를 호출해준다.
BallMesh->AddImpulse(PushDirection * CachedFinalKickPower, NAME_None, true);
					
if (HasAuthority(&CurrentActivationInfo))
{
	UE_LOG(LogTemp, Warning, TEXT("🔴 [SERVER] 서버 물리 적용 완료!"));
}
else
{
	SoccerBall->HandleLocalPredictionKick();
	UE_LOG(LogTemp, Warning, TEXT("🟢 [CLIENT] 로컬 예측 중... 잠시 서버 동기화 차단"));
}
```

문제가 있던 구간은 해결이 됐는데 문제는 완전 해결이 된게 아니라 문제가 있는 구간을 뒤로 미룬 느낌이 됐다. 서버 차단을 한 구간만 정상적으로 작동하다가 그 구간이 지나면 다시 공이 서버 기준으로 롤백됐다가 날아간다.   

총제적 난국   

다시 정리해보는 현재의 문제점   

서버와 클라가 둘 다 물리엔진을 계산하다보니 조금의 오차만 나도 난리가난다.   
현재는 보간을 통해서 서버에서 공의 위치만 따와서 적용을 하는데 그렇게 하다보니 보간을 막는 타이머가 끝나면 다시 문제가 생겨버린다.   

공의 위치만 동기화할게 아니라 속도, 회전 속도 등을 동기화해서 조절을 해줘야한다.   

```cpp
// 축구공의 정보를 저장하는 구조체를 생성

// 축구공의 물리 상태 저장용 구조체(Server)
USTRUCT(BlueprintType)
struct FBallPhysicsState
{
	GENERATED_BODY()

	UPROPERTY()
	FVector Location = FVector::ZeroVector;

	UPROPERTY()
	FRotator Rotation = FRotator::ZeroRotator;

	UPROPERTY()
	FVector LinearVelocity = FVector::ZeroVector;

	UPROPERTY()
	FVector AngularVelocity = FVector::ZeroVector;
};

// 서버의 물리 상태 동기화 (ReplicatedUsing 설정)
UPROPERTY(ReplicatedUsing = OnRep_ServerPhysicsState)
FBallPhysicsState ServerPhysicsState;

UFUNCTION()
void OnRep_ServerPhysicsState();

```

이런식으로 다양한 정보를 동기화 하는 방향으로 작성해보았지만 여전히 서버와 클라이언트 차이는 좁혀지지 않았다.   

<br/>

해도해도 안되는 동기화 문제...

이 문제의 해결방법으로 공을 차거나 공에 닿는 순간 해당 캐릭터(클라)가 공을 소유하고 정보를 서버로 보내고 서버가 다시 클라에 전달만해주는 구조를 구현해보기로 했다.   
공이 이리저리 튀어서 Owner가 1초에 몇 번씩 바뀌는 상황에도 큰 부하가 없기 때문에 좋은 방법같다.   

일단 서버로부터 동기화하는 코드에 내가 Owner일 때 return을 하게 작성해줬다.   
```cpp
void ASG_SoccerBall::OnRep_ServerPhysicsState()
{
	// 공을 소유하고 있는 상태라면 서버를 무시하고 return 해준다.
	APawn* MyPawn = Cast<APawn>(GetOwner());
	if (MyPawn && MyPawn->IsLocallyControlled())
	{
		return; 
	}
	
	//... 기존 로직
}
```

<br/>

일단 Owner가 바뀌는건 확인했지만 먼저 캐릭터 자체의 Movement 문제와 공이 멈추지 않는 문제부터 고치는게 시급해졌다.   

공이 멈추지 않는 문제   
마찰력, 제동력 등을 설정해줬는데도 공이 계속 굴러가는 문제가 생겼다.   

원인을 파악해봤는데 높은 확률로 서버에서 클라로 공의 위치, 속도 등을 전송하는 함수가 문제일 것 같은 상황이다. 계속 동일한 속도를 건네주어서 공이 멈추지 않는것이다.   

해결방법    

1.SetReplicateMovement(false)로 엔진 간섭 차단   
2.서버 복제 차단코드 추가   

위 방법으로 공이 멈추지 않는 현상은 수정완료   

<br/>

현재 공의 속도만 복제를 하다보니 시작지점과 속도는 같지만 마지막에 공이 위치하는 곳이 다른 현상이 발생했다.   
공이 느려질 때 동기화를 자연스럽게 시켜주는게 필요해졌다.   

해결방법   

공의 상태에 따라서 부드럽게 움직임을 가져가서 어색하지 않게 위치를 보정시켜준다.   

```cpp
void ASG_SoccerBall::OnRep_ServerPhysicsState()
{
	// ... 기존 코드
	
	// 서버가 새 패킷을 보냈을 때 클라이언트가 처리할 로직
	if (SoccerBallMesh)
	{
		// 서버의 실제 속도와 위치 가져오기
		SoccerBallMesh->SetPhysicsLinearVelocity(ServerPhysicsState.LinearVelocity);
		SoccerBallMesh->SetPhysicsAngularVelocityInRadians(ServerPhysicsState.AngularVelocity);

		// 위치 오차 보정
		FVector CurrentLoc = SoccerBallMesh->GetComponentLocation();
		float Distance = FVector::Dist(CurrentLoc, ServerPhysicsState.Location);

		// 공의 현재 속력(크기) 계산
		float CurrentSpeed = SoccerBallMesh->GetPhysicsLinearVelocity().Size();

		// 공이 거의 멈춰가거나(시속이 낮을 때) 위치 차이가 너무 클 때 (예: 1.5미터 이상)
		if (CurrentSpeed < 100.0f || Distance > 150.0f)
		{
			// 눈에 띄지 않게 부드럽게 서버 위치로 슬쩍 이동 (Interp 느낌의 세팅)
			// 만약 완전히 정지했다면(서버 속도가 0이면) 서버 위치로 보정
			if (ServerPhysicsState.LinearVelocity.IsNearlyZero())
			{
				SoccerBallMesh->SetWorldLocationAndRotation(ServerPhysicsState.Location, ServerPhysicsState.Rotation);
			}
			else
			{
				// 완전히 멈추기 직전 굴러가는 중이라면 부드럽게
				FVector BlendedLoc = FMath::VInterpTo(CurrentLoc, ServerPhysicsState.Location, GetWorld()->GetDeltaSeconds(), 5.0f);
				SoccerBallMesh->SetWorldLocation(BlendedLoc);
			}
		}
	}
}
```

<br/>

또 발생한 문제    

공이 서버와 클라에서 아예 다른 위치에서 노는 현상   

원인   
Owner를 설정하는 코드에서 너무 과하게 방어를 해버렸다. 공의 Owner가 됐는데 공이 다른곳으로 가버렸을때도 무조건 Owner의 공으로 취급해서 동기화를 아예 안시켜버리는 문제가 생긴것.   
```cpp
// 문제를 유발한 코드
APawn* MyPawn = Cast<APawn>(GetOwner());
if (MyPawn && MyPawn->IsLocallyControlled())
{
    return; // Owner라면 서버 무시
}
```

해결방법   

공이 떨어지면 소유권을 없앤다.(일정시간)   

```cpp
void ASG_SoccerBall::NotifyHit(
	UPrimitiveComponent* MyComp, 
	AActor* Other, 
	UPrimitiveComponent* OtherComp, 
	bool bSelfMoved, 
	FVector HitLocation, 
	FVector HitNormal, 
	FVector NormalImpulse,
	const FHitResult& Hit
)
{
	Super::NotifyHit(MyComp, Other, OtherComp, bSelfMoved, HitLocation, HitNormal, NormalImpulse, Hit);

	// 우리가 설계한 플레이어간 소유권(Owner) 변경 락 체인 로직
	ACharacter* HittingCharacter = Cast<ACharacter>(Other);
	if (HittingCharacter && HasAuthority())
	{
		// 쿨이 돌고있으면 소유권 이전 불가능
		if (GetWorld()->GetTimerManager().IsTimerActive(OwnerCooldownTimerHandle))
		{
			// --- 추가 코드 1번 ---
			// 쿨다운 중이라도 지금 치고 있는 사람이 주인이라면 타이머 계속 연장(드리블 유지)
			if (GetOwner() == HittingCharacter)
			{
				float ReleaseDelay = 0.5f; // 0.5초 동안 안 건드리면 소유권 박탈
				GetWorld()->GetTimerManager().SetTimer(
					OwnerReleaseTimerHandle, 
					this, &ASG_SoccerBall::ReleaseOwner,
					ReleaseDelay, 
					false
					);
			}
			return;
		}

		if (GetOwner() != HittingCharacter)
		{
			SetOwner(HittingCharacter);
            
			// 0.1초(쿨) 동안 소유권 이전 불가능
			float OwnerLockTime = 0.1f; 
			GetWorld()->GetTimerManager().SetTimer(
				OwnerCooldownTimerHandle, 
				this, 
				&ASG_SoccerBall::ResetOwnerCooldown, 
				OwnerLockTime, 
				false
			);
		}
		
		// --- 추가 코드 2번 ---
		float ReleaseDelay = 0.5f; 
		GetWorld()->GetTimerManager().SetTimer(
			OwnerReleaseTimerHandle, 
			this, 
			&ASG_SoccerBall::ReleaseOwner, 
			ReleaseDelay, 
			false
			);
	}
}
```

<br/>

위 코드로 어느정도 잡히나 했는데 여전히 공이 미친듯이 따로 놀아서 결국 다시 SetReplicateMovement를 켜주고 코드를 수정하기로 했다.   

일단, OwnerShip 부여하는 로직으로 꽤 괜찮은 결과를 얻었다.   




  </p>
</details>

#### <!-- 26.07.08 -->
<details> 
  <summary>26.07.08</summary>
  <p>

서버는 괜찮은데 클라에서 공을 Impulse 하는 순간 뜬근없이 LobbyLevel로 이동하는 현상   

원인   
공이 비정상적으로 바닥에 쳐박히며(눈에는 안보임) KillZ에 걸려 파괴되면서 어딘가에 있는 레벨 리셋 코드를 작동시킴   

```cpp
// 공에 EndPlay를 Override하여 확인

// 로비 레벨로 나가지는 버그 확인
virtual void EndPlay(const EEndPlayReason::Type EndPlayReason) override;

void ASG_SoccerBall::EndPlay(const EEndPlayReason::Type EndPlayReason)
{
    Super::EndPlay(EndPlayReason);
    UE_LOG(LogTemp, Error, TEXT("공이 파괴되었습니다! 이유: %d"), (int32)EndPlayReason);
}
```

로그를 확인하니 `LogTemp: Error: 공이 파괴되었습니다! 이유: 2` 라고 떴다.   

해결 방법   

```cpp
// CCD 옵션을 켜준다.
SoccerBallMesh->SetUseCCD(true); 
```

<br/>

공이 캐릭터와 충돌해서 버벅이는 현상 때문에 공과 충돌을 막고 일정 거리에 들어오면 자동으로 Impulse를 주어 드리블 하는 형태로 세팅을 해보았다.   

근데, 드리블 중간 중간 캐릭터가 공을 뚫고 들어가는 현상이 발견되었다.   

원인   
드리블 하는 동안 서버의 복제를 잠깐 막는다. 다시 서버와 동기화 하는 순간 위치 차이만큼 공이 이동하는데 캐릭터의 속도가 빠르다보니 공의 위치와 캐릭터의 위치가 겹치게 된다.   

해결방법   
가상 드리블 Impulse 방식을 포기하고 다시 원래대로 바꾸고 RnD를 계속 하고있다.   

<br/>

RnD를 계속 하다보니 코드들이 섞여서 여러 옵션들이 다 켜지고 꺼지고 해서 뒤죽박죽 됐다. 기본 설계를 다시 하고 코드를 다시 작성하려고 한다.   

**기본적인 설계**   
Player -> Kick Input -> Server 승인   
 
Ball Owner를 Player로 설정   
Owner가 Ball Physics 계산(클라)   
Server로 Position / Velocity 전송   
Server가 다른 Client에게 Replicate   

Ball의 여러 조건(정지, 느린속도 등)일 경우 Owner 해제   
Server가 다시 Authority를 가져간다.   


  </p>
</details>

#### <!-- 26.07.09 -->
<details> 
  <summary>26.07.09</summary>
  <p>

네트워크 게임 구현하며 공부하다 보니 Reliable, Unreliable을 쓰는데 마치 저번에 배운 TCP, UDP 같아서 복습하는겸 조금 더 알아보았다.    

<br/>

소켓(Socket) 계열이 있다.
프로토콜(통신 규약)을 기반으로 동작하며, 로컬과 네트워크 모두 가능하다.

프로토콜이란?
정해진 통신 규약같은것.
소켓은 알맞는 프로그래밍 언어로 프로토콜을 사용할 수 있게 해준다.(연결창구 느낌)

TCP (Transmission Control Protocol)
속도보다 신뢰성이 최우선인 전송 방식이고 3-Way-Handshake 방식을 사용합니다.   
신뢰성 보장을 위해 많은 헤더(제어 정보)가 필요하고 흐름/혼잡 제어 기능이 있기 때문에 헤더 용량이 크고 상대적으로 느립니다.    
신뢰가 우선인 웹, 이메일, 파일전송 등에 사용됩니다.   

UDP (User Datagram Protocol)   
속도가 최우선이며 TCP가 가진 여러 기능들(3-Way-Handshake, 흐름/혼잡제어)이 존재하지 않아서 헤더가 가볍고 전송 속도가 빠릅니다.   
순서가 보장되지 않고 일부 유실될 수도 있습니다.   
속도가 우선인 스트리밍, 멀티 게임 등에 사용됩니다.   

3-Way-Handshake   
SYN(Synchronize) : 클라이언트에서 서버에게 Sequence Number(연결 번호)를 알려주며 요청   
SYN + ACK : 서버에서 요청을 받고 자신의 Sequence Number도 알려주며 응답   
ACK(Acknowledge) : 클라이언트가 서버의 요청을 확인(ACK)하고 통신 시작    
누락되면 재전송 요청   

네트워크에서 Header   
네트워크로 데이터를 보낼 때, 실제 전달하고 싶은 '진짜 데이터(Payload)' 앞부분에는 제어 정보가 담긴 '표지판(Header)'이 붙는다.   

TCP는 Sequence Number, Acknowledgment Number, 에러 검출, 흐름 제어 정보 등 신뢰성을 보장하기 위한 수많은 필드가 헤더에 포함돼서 크다.(최소 20바이트)   
UDP는 출발지 포트 (Source Port), 목적지 포트 (Destination Port), 전체 패킷 길이 (Length), 오류 검사용 최소 정보 (Checksum) 딱 4가지만 들어가고 딱 8바이트다.

흐름 제어 (Flow Control) & 혼잡 제어 (Congestion Control)   
TCP가 데이터 전송 속도를 스스로 조절하는 메커니즘
흐름 제어 (Flow Control)   
수신자의 처리 능력에 맞추는 기능입니다. 받는 쪽의 버퍼(대기열)가 가득 차서 넘치지 않도록, 송신자가 보내는 속도나 양을 조절합니다.   
혼잡 제어 (Congestion Control)   
네트워크 전체의 교통량에 맞추는 기능입니다. 인터넷 망에 병목 현상이 생겨 패킷 유실이 발생하면, 송신자가 전송 속도를 줄여 네트워크 부하를 줄입니다.   
UDP는?   
수신자가 받을 준비가 됐든 안 됐든, 네트워크 망이 막히든 말든 일정한 속도로 데이터를 보낸다.   

패킷(Packet)이란?   
네트워크에서 데이터를 주고받을 때 사용하는 데이터의 조각   
데이터를 송신할 때 작고 일정한 단위로 쪼개서 보내는데 이 쪼개진 데이터 한 조각을 패킷이라고 부른다.

패킷의 구성
헤더 (Header): 제어 정보(보내는 사람 IP, 받는 사람 IP, 포트 번호, 패킷 순서 번호 등)
페이로드 (Payload): 실제 데이터
트레일러 (Trailer): 패킷 끝부분에 붙어 데이터에 오류가 없는지 검사하는 정보   

스트림 소켓 (Stream Socket)   
상대방과 연결이 된 상태에서 경계가 없는 데이터를 보내는 방식입니다. 패킷 순서가 보장되고 유실되지 않습니다.     
데이터그램 소켓 (Datagram Socket)   
데이터를 Datagram 단위로 주고받는 방식입니다. 상대와 연결을 확인하지 않고 일단 전송합니다. 순서가 보장되지 않고 사라질 수도 있습니다.
   
중요!!!!
로그인 할 때는 어떤 프로토콜을 쓸지
게임 내부에서 어느 부분에서 뭘 쓸지 잘 알고있어야한다.   

  </p>
</details>

#### <!-- 26.07.10 -->
<details> 
  <summary>26.07.10</summary>
  <p>

GA_Kick이 키를 입력할때마다 계쏙 나가는 현상   

원인 : GA_Kick이 구조상 계속 실행 될 수 있음.

**해결방법1**   
GA가 발차기 중에 실행이 안되도록 여러가지 방법을 구현

CanActivateAbility(), bIsKickInProgress, Spec->IsActive() 3가지를 사용해서 온몸비틀기로 GA 중복 실행을 막아보았다.   

**CanActivateAbility()**   
CanActivateAbility()를 Override하고 bIsKickInProgress라는 변수를 만들어서 Kick이 진행중에는 false로 만들어서 실행하지 못하도록 한다.      
또한 Spec->IsActive()까지 추가하여서 더 제대로 막아보았다.   


```cpp
// 헤더에서 override해주고
public:
	// 어빌리티가 실행될 수 있는 조건인지 서버/클라 양쪽에서 미리 검사하는 GAS 핵심 함수
	virtual bool CanActivateAbility(
		const FGameplayAbilitySpecHandle Handle, 
		const FGameplayAbilityActorInfo* ActorInfo, 
		const FGameplayTagContainer* SourceTags = nullptr, 
		const FGameplayTagContainer* TargetTags = nullptr, 
		FGameplayTagContainer* OptionalRelevantTags = nullptr
	) const override;

// cpp에 구현
bool UGA_SG_Kick::CanActivateAbility(
    const FGameplayAbilitySpecHandle Handle, 
    const FGameplayAbilityActorInfo* ActorInfo, 
    const FGameplayTagContainer* SourceTags, 
    const FGameplayTagContainer* TargetTags, 
    OUT FGameplayTagContainer* OptionalRelevantTags) const
{
   // 이미 킥이 진행 중이라면 서버든 클라든 활성화 자체를 거부
   if (bIsKickInProgress)
   {
      UE_LOG(LogTemp, Warning, TEXT("킥이 이미 활성화 돼서 실패 해야해"));
      return false;
   }
   
   // 어빌리티가 이미 활성화되어서 작동 중이라면 실행 거부
   FGameplayAbilitySpec* Spec = ActorInfo->AbilitySystemComponent->FindAbilitySpecFromHandle(Handle);
   if (Spec && Spec->IsActive())
   {
      UE_LOG(LogTemp, Error, TEXT("킥이 이미 활성화 돼서 실패 해야한다고"));
      return false;
   }
   
   UE_LOG(LogTemp, Warning, TEXT("왜 자꾸 그냥 실행되냐"));

   return Super::CanActivateAbility(Handle, ActorInfo, SourceTags, TargetTags, OptionalRelevantTags);
}


// 추가로 이런 코드를 중간중간 심어뒀지만 GA가 실행중이라는 걸 씹고 Input이 들어오면 EndAbility가 실행되고 바로 다시 Activate 된다...
// 이미 발차기/차징중이면 취소
   if (bIsKickInProgress)
   {
      return;
   }
```

음... 일단 이 방법으로는 해결을 못했다. 활성화 처리가 안된건지 Input 문제인지 더 확인해야겠다.   

원인을 분석하다가 Character의 Input에 눈이 더 가서 이 부분을 수정해보기로 했다.   

<br/>

---

<br/>

**해결방법2**   
그 전에 GA_Kick의 `Retrigger Instanced Ability`가 생성자에서 false로 되어있는데 실제 BP에선 true로 되어있는걸 확인했다. 근데 체크해제를 해도 소용이 없다. Input 문제일 확률이 더 높아졌다.   

```cpp
UGA_SG_Kick::UGA_SG_Kick()
{
    InstancingPolicy = EGameplayAbilityInstancingPolicy::InstancedPerActor;
    bReplicateInputDirectly = true;
   
	// 이런 기본 세팅은 BP에 적용 안되는경우가 생각보다 많은 것 같다...!
    bRetriggerInstancedAbility = false;
   
}
```

<br/>

---

<br/>

**이상현상 추가**   
Input 확인하기 전에 한가지 현상을 발견했는데 킥 버튼을 계속 누르면 동일하게 처음부터 재생된다기보단 차징 시간이 중첩이 되는 듯한? 계속 누르다가 시행하면 차징이 된 강한 킥이 나가는 현상을 발견했다.   
이 부분이 현재 문제를 수정할 수 있는 Key가 될 것 같다.   

라고 생각하고 다시 테스트해봤는데 이번엔 그런 현상이 사라졌다. 이런...

**해결방법3**   
결국 Input이 계속 들어오면 그 순간 EndAbility가 실행된 후 ActivateAbility가 실행되는 현상이 문제라서 계속 들어오는 Input을 확인해야겠다.   


  </p>
</details>

#### <!-- 26.07.13 -->
<details> 
  <summary>26.07.13</summary>
  <p>

기존 X_Bot으로 테스트 하다가 새로운 mixamo skeltal mesh를 사용하려는데 기존 X_Bot Skeleton에 맞춰서 설정돼서 캐릭터가 매우 어색한 현상   

리타겟팅이 되지 않아서 발생하는 현상이었다.   

해결방법   

`Skeleton`에 들어가서 옵션에서 `Translation Retargeting`을 켜주고 root(Mixamo 뼈대를 쓰는중이지만 Blender로 변환을 해줘서 root가 있음)를 Skeleton으로 바꿔준다. 이러면 root밑의 모든 뼈대가 Skeleton으로 바뀐다.   
주의할점은 Hips(골반위치)는 `Animation Scaled`를 선택하여 기존 애니메이션이 어색하지 않도록 설정해야한다.   

<br/>

피격시 Ragdoll 만들기   

충격량과 충격위치만 서버로 전송하고 해당 값을 Multicast 하는 함수와 Ragdoll을 실행시키는 함수를 만들어준다.    

```cpp
// Character.h
public:
	//-------------------------------- Ragdoll --------------------------------//
	UFUNCTION(NetMulticast, Reliable)
	void MulticastEnableRagdoll(FVector HitImpulse, FVector HitLocation);

	void EnableRagdoll(FVector HitImpulse, FVector HitLocation);
	

// Character.cpp
void ASG_Character::EnableRagdoll(FVector HitImpulse, FVector HitLocation)
{
	USkeletalMeshComponent* MeshComp = GetMesh();
	UCapsuleComponent* CapsuleComp = GetCapsuleComponent();
	UCharacterMovementComponent* MovementComp = GetCharacterMovement();

	if (!MeshComp || !CapsuleComp || !MovementComp) return;

	// 캡슐 콜리전 비활성화
	CapsuleComp->SetCollisionEnabled(ECollisionEnabled::NoCollision);

	// 캐릭터 이동 및 입력 멈춤
	MovementComp->DisableMovement();
	MovementComp->StopMovementImmediately();

	// 메쉬의 피직스 시뮬레이션 켜기
	MeshComp->SetCollisionProfileName(TEXT("Ragdoll"));
	MeshComp->SetAllBodiesSimulatePhysics(true);
	MeshComp->SetSimulatePhysics(true);
	MeshComp->WakeAllRigidBodies();

	// 드롭킥 Impulse 전달
	MeshComp->AddImpulseAtLocation(HitImpulse, HitLocation);
}
```

<br/>

발생한 문제   
드롭킥을 날렸을 때 래그돌 상태가 되기는 하지만 캐릭터가 제자리에 풀썩 주저앉는다.   

원인   
AddImpulse는 캐릭터의 메쉬의 질량을 곱해서 계산하는데 스켈레탈 메쉬의 질량이 기본적으로 높게 설정돼서 제자리에 주저앉게된다.(무거워서 날아가지못함)   

해결방법   
질량을 무시하고 속도로 날려버리는 `bVelChange` 파라미터를 사용한다.   
이 파라미터는 Bone Name이 들어가게 되는데 몸의 중심인 골반을 적어주면 좀 더 자연스럽게 날아간다.   

```cpp
// Impulse 마지막 인자에 추가!
MeshComp->AddImpulseAtLocation(HitImpulse, HitLocation, TEXT("Hips"));
```

<br/>

발생한 문제   
래그돌이 된 캐릭터의 카메라가 캐릭터를 따라가지 않고 일어나는순간 화면이 전환되는 현상   

원인   
맞은 순간 캡슐 자체는 제자리에 서있기 때문에 카메라가 가만히 멍 때리는 것이다.   

해결방법   
맞을때 Hips를 중심으로 날아가는데 거기에 카메라를 잠시 달아주고 Ragdoll이 끝나면 다시 원상복구 시켜준다.   

```cpp
// EnableRagdoll 함수
// SpringArm을 Mesh의 골반(Hips) 소켓에 부착
if (CameraBoom) 
{
	CameraBoom->AttachToComponent(GetMesh(), FAttachmentTransformRules::SnapToTargetNotIncludingScale, TEXT("Hips"));
}

// DisableRagdoll 함수
if (CameraBoom)
{
	CameraBoom->AttachToComponent(GetCapsuleComponent(), FAttachmentTransformRules::SnapToTargetNotIncludingScale);
	CameraBoom->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f)); // 기존 SpringArm의 RelativeLocation 기본값으로 원복
}
```

<br/>

날아가고나서 다시 일어설때 서버와 클라이언트의 캐릭터 Rotation이 달라서 어색하게 동기화되는 현상이 발생했다.   

원인   
클라에서 알아서 일어나는 모션을 실행 후 서버에서 동기화를 시켜줘서 Rotation이 튀는거였다.   

해결방법   
기존의 방식과 다르게 Server용 Client용으로 2개의 DisableRagdoll 함수를 만들어줬다.   
서버가 래그돌이 멈춘 시점의 Hips 위치를 측정하여 최종 캡슐 위치를 확정하고, 이 좌표를 Multicast 파라미터로 클라이언트들에게 전파해 주면 모든 화면에서 동일한 위치에 보이게 된다.

```cpp
// Character.h

// --- Server ---
// 서버에서 래그돌 해제 타이머 종료 시 호출
void ServerDisableRagdoll();

// 서버가 계산한 위치/회전/방향을 모든 클라이언트에 멀티캐스트
UFUNCTION(NetMulticast, Reliable)
void MulticastDisableRagdoll(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown);

// --- Server, Client ---
// 실제 래그돌 해제 및 복구 로직(기존 DisableRagdoll() 함수에서 이름만 바꿈)
void DisableRagdollInternal(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown);

// Character.cpp

// Server에서만 실행
void ASG_Character::ServerDisableRagdoll()
{
	// 서버만!
	if (!HasAuthority())
	{
		return;
	}

	USkeletalMeshComponent* MeshComp = GetMesh();
	UCapsuleComponent* CapsuleComp = GetCapsuleComponent();
	if (!MeshComp || !CapsuleComp)
	{
		return;
	}

	// 서버 기준 래그돌 Hips 위치 및 회전 수집
	FVector HipsLocation = MeshComp->GetSocketLocation(TEXT("Hips"));
	FRotator HipsRotation = MeshComp->GetSocketRotation(TEXT("Hips"));
	bool bIsFaceDown = IsRagdollFaceDown();

	// 동기화할 캡슐 위치 및 회전값 연산
	FVector NewCapsuleLocation = HipsLocation;
	NewCapsuleLocation.Z += CapsuleComp->GetScaledCapsuleHalfHeight();

	FRotator NewCapsuleRotation = FRotator(0.0f, HipsRotation.Yaw, 0.0f);
	if (bIsFaceDown)
	{
		NewCapsuleRotation.Yaw += 180.0f;
	}

	// 계산된 완벽한 좌표 정보를 모든 클라이언트에 동기화
	MulticastDisableRagdoll(NewCapsuleLocation, NewCapsuleRotation, bIsFaceDown);
}

// 정보들을 서버에 멀티캐스트
void ASG_Character::MulticastDisableRagdoll_Implementation(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown)
{
	DisableRagdollInternal(TargetLocation, TargetRotation, bIsFaceDown);
}

// 실제 래그돌 실행 함수
void ASG_Character::DisableRagdollInternal(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown)
{
    // ... 기존에 있던 통합된 로직 실행
}
```



  </p>
</details>