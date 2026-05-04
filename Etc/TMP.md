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