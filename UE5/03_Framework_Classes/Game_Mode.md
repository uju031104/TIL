# Game_Mode

<br/>

### GameMode 구조

GameMode - Character(Default Pawn Class), Player Controller   
Character를 만들고 GameMode에 연결해서 월드에 스폰   
PlayerController(캐릭터의 빙의)   
  

게임의 기본 설정을 한다.   
보통 서버전용 로직, 규칙등을 담는다.(멀티게임)   

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

<br/>

***

<br/>