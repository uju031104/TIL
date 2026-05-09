# TroubleShooting

<br/>

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

<br/>

***

<br/>


### 카메라 시점 전환 문제 

<br/>

바닥에 있을땐 컨트롤러가 카메라를 제어하고 공중에 떠있으면 폰의 회전에 SpringArm/Camera가 같이 돌아가는 형태   

**1. 발생한 현상**   
바닥 -> 공중으로 갈 때 시점이 확 바껴버리는 현상   

**2. 원인**   
공중은 폰의 회전값을 기준으로 하기 때문에 바닥에서의 카메라 시점과 달라짐

**3. 해결방법**   
RInterpTo()를 사용하여 부드러운 화면 전환을 구현    

<br/>

```cpp
//RInterpTo()로 구현
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

<br/>

***

<br/>

### 카메라 시점 전환 문제2   

<br/>

**1. 발생한 현상**   
RInterpTo()가 제대로 적용되지 않는 현상   

**2. 원인**   
전환되는 순간 컨트롤러 로테이션값 -> 액터의 로테이션 값으로 바뀌는데 마우스를 조금이라도 움직이면 로직이 꼬여서 실행이 안된다.

**3. 해결방법**   
전환되는 순간 마우스 컨트롤을 못하게 막았다.   

<br/>

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
<br/>

***

<br/>

### Start 버튼을 누르기 전에 GameState가 실행되는 현상   

<br/>

**1. 발생한 현상**   
Start버튼을 누르지 않았는데 Wave가 시작됐다고 출력이 된다.   

**2. 원인**   
게임실행을 했을 때 GameState의 BeginPlay()도 바로 실행되기 때문에 발생했다.   

**3. 해결방법**   
GameInstance에 bool 변수를 하나 만들어서 Start 버튼을 눌렀을때 상태를 변화시키고 그 조건을 만족하면 BeginPlay()의 StartLevel이 실행되도록 바꿨다.   

<br/>

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

***

<br/>

### 아이템이 사라지면 디버프 효과가 사라지지 않는 현상   

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

***

<br/>


### 좀비가 스폰이 안되는 현상   

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

***

<br/>


### 스폰된 좀비가 MoveTo를 실행하지 못하는 현상   

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

<br/>

***

<br/>

