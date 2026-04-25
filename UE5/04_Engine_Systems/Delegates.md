# Delegates

<br/>

https://dev.epicgames.com/documentation/unreal-engine/delegates-and-lambda-functions-in-unreal-engine

### Delegate 함수 인자 

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

