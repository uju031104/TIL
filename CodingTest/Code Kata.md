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


