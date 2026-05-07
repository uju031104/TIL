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

<br/>

***

<br/>

### 해시(90번)

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
<br/>

***

<br/>

### 프로세스 (92번)  

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

### 피로도 (93번)   

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


### k진수에서 소수 개수 구하기 (95번)  

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