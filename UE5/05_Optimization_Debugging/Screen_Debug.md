# ScreenDebug

<br/>

### AddOnScreenDebugMessage()

<br/>

```cpp
//헤더파일
#include "Engine/Engine.h"
// GEngine이 존재하는지 확인 후 실행
if (GEngine)
{
    GEngine->AddOnScreenDebugMessage(-1, 3.0f, FColor::Red, FString::Printf(TEXT("Actor : %s"), *ActorLocation.ToString()));

    GEngine->AddOnScreenDebugMessage(
	-1,   // -1 해두면 계속 갱신해서 출력해줌
	2.f,  // 출력 유지 시간
	FColor::Green, // 글자색
	FString::Printf(TEXT("Player Gained %d points"), PointValue)); // 내용
}
```
 