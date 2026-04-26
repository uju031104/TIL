# C++ 코테 정복 강의

<br/>

### bitset   

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

### 스택
```cpp
/* 
이 문제를 스택으로 풀어야 한다고 생각하고 접근했는데도 어떻게 해야할지 감도 안잡혔음. 이중 반복문으로 풀면 너무 쉬운 문제지만 시간복잡도 제한이 걸리면 이렇게 다른 방식으로 풀어야함.

특히 스택을 활용하면서 index 값을 넣는 방식을 쓴 것이 엄청 참신했음. 

현재값과 이전값을 비교할때 스택의 top()을 이전 값으로 활용
*/
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

### 예상 대진표

```cpp
/* 
코드가 너무 간단해서 놀랐음
트리를 꼭 사용해야한다고 생각해서 억지로 트리 구조 벡터를 만들고, 부모 노드로 합쳐지는부분을 도대체 어떻게 구현하나 했는데 실제 트리 구조가 아니고 논리적인 트리 구조로 푸는 문제였음

결론 : 단순하게 부모 노드로 합쳐지는 식만 만들면 된다. + 트리처럼 보인다고 그걸 꼭 실제 트리 구조로 구현해야하는건 아니다.
*/
int solution(int n, int a, int b)
{
    int answer = 0;

    do {
        a = (a + 1) / 2;
        b = (b + 1) / 2;
        ++answer;
    } while (a != b);

    return answer;
}
```

<br/> 

***

<br/>

### 다단계 칫솔 판매

```cpp
/* 
이 문제도 어떻게 트리로 풀지? 라고 생각하다가 아무리 봐도 map을 쓰는게 좋겠다고 생각했음
근데 unordered_map은 써본적이 없어서 사용법만 따로 공부한 후 적용을 해봤다.

진짜 문제는... 시간복잡도를 생각하는건 좋은데 너무 과하게 반응하는 내 자신이었다.
입력 크기가 10000이 넘어가면 '이거 O(n^2)은 안되잖아?' 라고 생각해버려서 단순하게 이중 반복문을 피해버린다.

결론 : 시간복잡도 감각을 더 기르자.

*/
#include <iostream>
#include <vector>
#include <unordered_map>
#include <iterator>

void print(std::vector<int> vec)
{
    copy(vec.begin(), vec.end(), std::ostream_iterator<int>(std::cout, " "));
    std::cout << std::endl;
}

std::vector<int> solution(std::vector<std::string> enroll, std::vector<std::string> referral, std::vector<std::string> seller, std::vector<int> amount)
{
    std::vector<int> result;
    std::unordered_map<std::string, std::string> name_referral;
    std::unordered_map<std::string, int> name_money;

    for (int i = 0; i < enroll.size(); ++i)
    {
        name_referral[enroll[i]] = referral[i];
        name_money[enroll[i]] = 0;
    }

    for (int i = 0; i < seller.size(); ++i)
    {

        int money = 100 * amount[i];
        std::string str = seller[i];

        while (money > 0 && str != "-")
        {
            name_money[str] += (money - (money / 10));

            str = name_referral[str];

            money /= 10;
        }
    }

    for (const std::string &name : enroll)
    {
        result.push_back(name_money[name]);
    }

    return result;
}

int main()
{
    print(solution({"john", "mary", "edward", "sam", "emily", "jaimie", "tod", "young"},
                   {"-", "-", "mary", "edward", "mary", "mary", "jaimie", "edward"},
                   {"young", "john", "tod", "emily", "mary"},
                   {12, 4, 2, 5, 10})); // 출력값 : 360 958 108 0 450 18 180 1080

    print(solution({"john", "mary", "edward", "sam", "emily", "jaimie", "tod", "young"},
                   {"-", "-", "mary", "edward", "mary", "mary", "jaimie", "edward"},
                   {"sam", "emily", "jaimie", "edward"},
                   {2, 3, 5, 4})); // 출력값 : 0 110 378 180 270 450 0 0
    return 0;
}

```

<br/> 

***

<br/>