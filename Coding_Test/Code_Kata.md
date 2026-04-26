# 코드카타 (Code Kata)

<br/>

### 반복자 반환   

find() 함수를 사용하면 반환값이 반복자라서 int index로 받았다가 오류가 떴다.     
그래서 auto index로 받았다.  
```cpp
auto index = find(seoul.begin(), seoul.end(), "Kim") - seoul.begin();   
``` 
위와 같이 find()에서 나온 값에서 begin()을 빼줘야 나온다.   
<br/>

<참고사항>   
**type deduction(타입 추론)**   
컴파일러가 변수, 표현식 또는 템플릿 매개변수의 데이터 유형을 자동으로 추론하여 명시적인 유형 선언이 필요 없는 컴파일 타임 메커니즘   
위 메커니즘을 사용하는게 바로 auto다.

<br/>

***

<br/>

### 2차원 벡터

배열 말고 2차원 벡터는 처음 써봐서   
새로운 문법 눈에 익혀두자.

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

***

<br/>

### 자료형 확인

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

***

<br/>

### 명예의 전당(1)

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
// 벡터의 제일 오른쪽 값 3개가 크기순인걸로 풀었는데 이렇게 하면 나중에 tmp 벡터가 너무 길어져서 sort()하는 시간이 오래 걸린다. pop_back()을 활용하는게 좋다. 
// 우선순위큐를 사용하면 더 깔끔하게 가능하다. 우선순위 큐를 배우고 나서 다시 해보기
// 심지어 index는 사용하지 않았는데 적어놨네
// <set>도 안씀
// 통과만 한 레전드 코드ㅋㅋ
```

### 명예의 전당(1) 수정본

```cpp
/* 
위 코드와 비교했을때 매우매우매우 깔끔해짐
우선순위큐는 기본적으로 내림차순 정렬을 해준다.
그리고 일반 queue와 다르게 top()으로 우선순위 값을 반환한다.
기본 우선순위큐는 top()을 실행 시 가장 앞에 있으면서 가장 큰 값을 반환
위 처럼 greater를 써주면 가장 작은 값을 반환한다.
*/
#include <vector>
#include <queue>
#include <functional> // greater

using namespace std;

vector<int> solution(int k, vector<int> score)
{
    vector<int> answer;
    priority_queue<int, vector<int>, greater<int>> honor;

    for (int value : score)
    {
        honor.push(value);
        
        if(honor.size() > k)
        {
            honor.pop();
        }
        answer.push_back(honor.top());
    }

    return answer;
}
```

<br/>

***

<br/>

### 카드뭉치(큐)

```cpp
/* 오늘 코드카타로 풀었던 문제였는데 강의 듣다가 나옴. 코드카타에서 풀었을땐 직접적으로 큐를 이용하진 않고 의도치 않게 큐의 원리를 이용해서 풀었는데 마침 또 나와줘서 큐로 풀어봤음.
쉬운 문제라서 금방함. 
강의 풀이에서는 goal까지 큐에 넣어서 활용했는데 굳이? 싶긴한데 더 깔끔하긴 할듯?
*/
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

<br/>

***

<br/>

### 옹알이(2)

```cpp
/*
문제를 풀긴 했는데 좀 오래걸렸다.
테스트에서 성공하고 채점했는데 70의 정확도가 나와서 왜 그런가 이것 저것 다 뜯어 고쳐봤는데 for문 새로 시작할 때 pre_tmp 초기화를 안해서 그런거였다...

결론 : 잘 하자.
*/
#include <string>
#include <vector>

using namespace std;

int solution(vector<string> babbling) {
    int answer = 0;
    string tmp = "";
    string pre_tmp = "";
    vector<string> announce = {"aya", "ye", "woo", "ma"};
    
    for(string str : babbling)
    {
        tmp = str;
        pre_tmp = ""; // 문제의 부분
        while(tmp != "-")
        {
            if(tmp.length() == 0)
            {
                answer += 1;
                tmp = "-";
            }
            else if(tmp.length() == 1)
            {
                tmp = "-";
            }
            else if(tmp.length() == 2)
            {
                if((tmp != pre_tmp) && (tmp == announce[1] || tmp == announce[3]))
                {
                    answer += 1;
                }
                tmp = "-";
            }
            else if(tmp.length() > 2)
            {
                if((tmp.substr(0, 2) != pre_tmp) && (tmp.substr(0, 2) == announce[1]|| tmp.substr(0, 2) == announce[3]))
                {
                    pre_tmp = tmp.substr(0, 2);
                    tmp = tmp.substr(2);
                }
                else if((tmp.substr(0, 3) != pre_tmp) && (tmp.substr(0, 3) == announce[0] || tmp.substr(0, 3) == announce[2]))
                {
                    pre_tmp = tmp.substr(0, 3);
                    tmp = tmp.substr(3);
                }
                else
                {
                    tmp = "-";
                }
            }
        }      
    }
    
    return answer;
}
```

<br/>

***

<br/>

### 둘만의 암호(67번)

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

<br/>

***

<br/>

### 괄호 회전하기(84번)

```cpp
// unordered_map을 활용하면 더 좋다.
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

***

<br/>

### 연속 부분 수열 합의 개수(85번) 

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