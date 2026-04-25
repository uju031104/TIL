# TroubleShooting

### generated.h 파일

<br/>

```cpp
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Item.generated.h"  // 마지막에 와야함
#include "Components/AudioComponent.h"
```
<br/>

**1. 발생한 현상**   
컴파일 오류   

**2. 원인**   
generated.h 헤더파일 위치   

**3. 해결방법**    
처음 배울 때 꼭 하는 실수라고 한다. generated.h가 무조건 마지막에 와야한다.      

<br/>

***

<br/>


### 액터 배치와 생성자 호출   
   
액터를 배치하면 Constructor Log만 떠야할 것 같은데 Constructor - Destroyed - Constructor 순서로 뜨길래 뭔지 찾아봤다.      
에디터 내부에서 액터 재생성(Reconstruction) 과정을 거친다고 하는데 액터를 뷰포트에 끌어다 놓을때 생성되고 위치가 확정될 때 파괴되고 그 직후 최종 액터가 생성된다고 한다.   


<br/>

***

<br/>

### 큐브의 위치 문제   

<br/>

**1. 발생한 현상**  
큐브가 시작점에서 끝 점까지 왕복 운동을 할 때 지정해둔 정확한 위치에 오지않는 현상

**2. 원인**   
찾아보니 흔한 부동소수점의 오차로 발생하는 현상이라고 한다. `AddActorLocalOffset`을 사용하다 보니 이 오차가 계속 더해지고 빼져서 심해진다.   

**3. 해결방법**   
`SetActorLocation`을 사용하여 정확한 위치로 가게 설정해줬다. 그런데 여기서 또 문제가 발생했다.   

**4. 새로 발생한 현상**   

이동하는 Value값에 비해 터무니 없이 작은 이동거리를 보여준다.    

**5. 원인**   
프레임 독립적인 로직을 짠다고 아무 생각없이 `DeltaTime`을 쓴 것이 오히려 문제였다.   

**6. 해결방법**   
이미 `GetWorld()->GetTimeSeconds()`를 사용하고 있어서 DeltaTime을 쓴 것이 의미없이 프레임 값을 나눠준 것이 됐다. DeltaTime을 빼주니 해결이 됐다.

   




 