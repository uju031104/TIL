# TroubleShooting

<br/>

## 8th-Team11-CH3-Project

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

# 8th-Team11-CH4-Project

### Anim Montage와 Gameplay Ability가 연동이 안되는 현상

**1. 발생한 현상**   
키 입력을 받고 GA를 실행할 때 몽타주가 연동이 안되는 현상   

**2. 원인**   
단순하게 기존 몽타주 재생 로직을 실행하려고 해서 발생   

**3. 해결방법**    
GAS를 사용할 땐 Montage를 플레이하기 위한 Ability_Task를 이용해야했다.   
참고로 Ability_Task는 비동기(Asynchronous)로 동작해서 시간이 걸리는 이벤트들을 기다렸다가 브로드캐스트한다.   
나는 `PlayMontageAndWait`와 `WaitGameplayEvent`, 그리고 ANS에서 `SendGameplayEventToActor`를 사용해서 Montage 이벤트를 구현하여 해결하였다.  

<br/>

**첫 번째: `AbilityTask_PlayMontageAndWait`**   

이 Task는 `OnCompleted`, `OnBlendedOut`, `OnInterrupted`, `OnCancelled` 같은 멀티캐스트 델리게이트를 제공한다. 몽타주가 정상적으로 끝났을 때와 중간에 구르기 등으로 캔슬되었을 때의 후속 처리를 분기할 때 반드시 활용해야한다.   

```cpp
// PlayMontageAndWait 기능을 사용하기위한 헤더
#include "Abilities/Tasks/AbilityTask_PlayMontageAndWait.h"

// 어빌리티가 실행되는 동안 캐릭터의 애니메이션 몽타주를 재생하고, 그 몽타주가 끝날 때까지 대기하는 Task
UAbilityTask_PlayMontageAndWait* PlayMontageTask = UAbilityTask_PlayMontageAndWait::CreatePlayMontageAndWaitProxy(
	this,            // OwningAbility: 이 Task를 소유하고 실행하는 Gameplay Ability (보통 this)
	NAME_None,       // TaskInstanceName: 이 Task의 고유 식별 이름 (보통 디버깅용이 아니면 NAME_None)
	MontageToPlay,   // MontageToPlay: 재생할 UAnimMontage
	1.0f,            // Rate: 애니메이션 재생 속도 배율 (1.0f는 기본 속도)
	NAME_None,       // SectionName: 몽타주 내에서 특정 섹션부터 시작하고 싶을 때 섹션 이름 지정
	true             // bStopWhenAbilityEnds: 어빌리티가 중간에 강제 종료(Cancel)되면 몽타주 재생도 즉시 멈출지 여부
);

if (PlayMontageTask)
{
	// 몽타주가 끝나는 다양한 상황에 대한 델리게이트 
    PlayMontageTask->OnCompleted.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
    PlayMontageTask->OnBlendOut.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
    PlayMontageTask->OnInterrupted.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
    PlayMontageTask->OnCancelled.AddDynamic(this, &UGA_SG_Kick::K2_EndAbility);
	// 이 코드를 적어줘야 실행준비완료
    PlayMontageTask->ReadyForActivation();
}
```

<br/>


**두 번째: `AbilityTask_WaitGameplayEvent`**   

이 Task는 `Gameplay Tag`를 가진 이벤트가 발생(Send)할 때까지 대기하다가, 이벤트가 감지되면 바인딩된 함수를 실행하는 통신형 Task이다. 주로 애니메이션 몽타주 도중 "공격 판정이 발생하는 타이밍(Anim Notify)"에 이벤트를 쏘아 받아낼 때 사용한다.   

```cpp
// 
#include "Abilities/Tasks/AbilityTask_WaitGameplayEvent.h"

// ANS에서 SendGameplayEventToActor를 실행할때 확인하는 태그 세팅 
FGameplayTagContainer AssetTagsContainer = GetAssetTags();
FGameplayTag MyAbilityTag = AssetTagsContainer.Num() > 0 ? AssetTagsContainer.GetByIndex(0) : FGameplayTag::EmptyTag;

// 태그 이벤트를 기다리는 Task를 만들고
UAbilityTask_WaitGameplayEvent* WaitEventTask = UAbilityTask_WaitGameplayEvent::WaitGameplayEvent(
	this, 
	MyAbilityTag,     // 에디터에서 설정한 GA_SG_Kick의 Tag
	nullptr,          // Optional External Optional Actor
	false             // bOnlyTriggerOnce (한 번만 트리거할지 여부)
);

// 조건에 맞으면 실행
if (WaitEventTask)
{
	// 이벤트가 들어오면(SendGameplayEventToActor) 실행할 함수 바인딩
	WaitEventTask->EventReceived.AddDynamic(this, &UGA_SG_Kick::OnGameplayEventReceived);
	WaitEventTask->ReadyForActivation();
}
```

<br/>

**세 번째: `SendGameplayEventToActor`**   

ANS에서 이벤트를 발생시키는 내장 라이브러리이다.(위에 WaitGameplayEvent를 실행시키는 전조 이벤트)   

```cpp
// ANS 내부의 NotifyTick
void UANS_SG_Kick::NotifyTick(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation, float FrameDeltaTime, const FAnimNotifyEventReference& EventReference)
{
    Super::NotifyTick(MeshComp, Animation, FrameDeltaTime, EventReference);
	
	// 충돌 감지 로직...

	// 충돌이 감지되었을 때 GAS Gameplay Event 전송
	if (bHit && HitResult.GetActor())
	{
		AActor* HitEnemy = HitResult.GetActor();
        
		// ANS 구간이 끝날 때까지 연타 버그 방지
		HitActors.Add(HitEnemy);

		// GAS 이벤트 전송용 데이터(Payload)
		FGameplayEventData Payload;
		Payload.Instigator = MyCharacter; // 공격자
		Payload.Target = HitEnemy;        // 피격자

		// GAS 내장 라이브러리를 통해 캐릭터 어빌리티 시스템에 무전 송신
		FGameplayTag HitTag = FGameplayTag::RequestGameplayTag(TEXT("Character.Skill.Kick"));
		UAbilitySystemBlueprintLibrary::SendGameplayEventToActor(MyCharacter, HitTag, Payload);
	}
}
```

<br/>

---

<br/>

## 네트워크 환경에서 축구공의 물리 구현 R&D

BP로 제작하고 기본 물리만 적용한 테스트용 축구공은 네트워크 환경에서 부자연스러운 움직임을 보여준다.      
이를 해결하기 위해 축구공을 C++로 전환하고, 기본적인 네트워크 및 물리 세팅을 적용한 뒤 테스트를 진행했다.   

### 초기 세팅 
    
```cpp
// --- 축구공 RnD Default Setting ---
// 네트워크 설정. 축구공의 움직임도 복제한다.   
bReplicates = true;
SetReplicateMovement(true);

// 물리 및 콜리전 설정 추가
SoccerBallMesh->SetSimulatePhysics(true);
SoccerBallMesh->SetCollisionProfileName(TEXT("PhysicsBody"));

// 서버가 더 자주 공 위치를 브로드캐스트 하도록 설정
NetUpdateFrequency = 100.0f;
MinNetUpdateFrequency = 33.0f;
```

<br/>

**1. 발생한 현상(1)**   
C++로 전환하고 움직임 복제, 브로드캐스트 빈도를 높였지만 여전히 공이 부드럽게 굴러가지 않고 뚝뚝 끊기거나 순간 이동(Jittering)하는 현상 발생했다.   

**2. 원인**   
- `Replicated Movement`의 자체 최적화 스로틀링   
언리얼 엔진의 `AActor::ReplicateMovement` 시스템은 성능 최적화를 위해 내부적으로 엄청난 `스로틀링(제한)`을 건다.      
공이 굴러갈 때 위치가 소수점 단위로 바뀐다고 해서 서버가 매 프레임 위치를 보내지 않는다.   
내부적으로 이전 위치와 현재 위치의 차이(Threshold)를 계산하여, 일정 기준치 이상 변하지 않으면 `NetUpdateFrequency`가 100이든 1000이든 데이터 전송 자체를 스킵해 버린다.   

- 물리 시뮬레이션의 비결정성(`Non-deterministic`)   
축구공처럼 `Simulate Physics`가 켜진 액터는 서버와 클라이언트의 물리 엔진(Chaos Physics)이 각각 따로 계산한다.   
서버가 현재 공의 정보(위치, 속도)가 담긴 패킷을 보내도, 클라이언트는 패킷을 받는 순간 이미 자기 화면에서 자기만의 물리 연산을 한다.   
결국 서버 데이터가 도착할 때마다 `클라이언트의 공이 강제로 워프`(텔레포트)하면서 뚝뚝 끊기는 `고무줄(Jittering)현상`이 발생한다. 빈도를 100으로 올리면 이 뚝뚝 끊기는 주기가 더 줄어들뿐 근본적인 해결은 안된다.      

**3. 해결을 위해 시도한 방법**    
`네트워크 물리 공 보간(Interpolation)`을 사용해서 서버와 클라를 자연스럽게 연결하는 방법을 시도했다.   
클라에서도 공을 차는 GA를 실행 하고 적절히 서버와 클라를 보간하는 방식을 구현했다.     

<br/>

```cpp
// 공을 차는 순간 클라에서 서버와의 동기화를 잠깐 끊고 클라에서 재생을 해준다. 그리고 일정 시간 이후 동기화를 한다.
if (!HasAuthority())
{
    if (KickPredictionTimer > 0.0f)
    {
        KickPredictionTimer -= DeltaTime;
            
        // 0.4초동안은 서버와 동기화 하지않음
        SoccerBallMesh->bReplicatePhysicsToAutonomousProxy = false;
    }
    else
    {
        // 타이머가 끝나면 다시 서버의 물리 상태 동기화
        SoccerBallMesh->bReplicatePhysicsToAutonomousProxy = true;
    }
}

// 축구공은 서버 기준으로 자연스럽게 보간하도록 설정
FVector NewLoc = FMath::VInterpTo(CurrentLoc, TargetLoc, DeltaTime, InterpolationSpeed);
SoccerBallMesh->SetWorldLocationAndRotation(NewLoc, NewRot);
```

<br/>

**1. 발생한 현상(2)**   
네트워크 레이턴시로 인해 공을 찼을 때 반응이 느린 문제를 해결하고자 `클라이언트에서 즉시 펄스(Impulse)`를 주고 0.4초간 서버 동기화를 차단(bReplicatePhysicsToAutonomousProxy = false)하는 로직을 구현했다.   
그러나 0.4초 타이머가 만료되는 순간 공이 서버의 과거 위치로 뚝 끊기듯 `되감기(Rewind)`된 후 다시 날아가는 현상 발생했다.   

**2. 원인**   
- `bReplicatePhysicsToAutonomousProxy`를 꺼두어도 서버가 보내는 리플리케이션 데이터는 클라이언트 네트워크 큐에 계속 쌓인다.   
옵션이 다시 활성화되는 순간 누적된 서버 데이터가 한 번에 덮어씌워지며 텔레포트가 발생한다.   

- `Simulate Physics`가 활성화된 상태에서 `FMath::VInterpTo`와 `SetWorldLocation`을 사용해 `좌표를 강제로 보간`하려다 보니 물리 엔진의 속도(Velocity) 벡터와 서버의 타겟 좌표가 꼬이면서 공이 뒤로 감겼다 튕겨 나가는 오동작을 유발한다.      

**3. 해결을 위해 시도한 방법**    
클라이언트가 공을 찬 직후, 서버 패킷이 도달하여 클라이언트의 위치를 덮어쓰는 데 걸리는 시간(네트워크 렉 환경 약 150ms)을 계산했다.      
공을 차는 순간 로컬 클라이언트에서 `HandleLocalPredictionKick()`을 호출하여 약 0.25초 동안 `PredictionInterpCooldown` 타이머를 가동, 이 시간 동안은 축구공 Tick 내부의 보간 로직을 return;으로 강제 패스하여 서버 데이터로 인한 되감기 현상을 원천 차단했다.    

<br/>

```cpp
// 1. 축구공 헤더파일에 보간을 잠깐 끄는 코드를 작성해준다.

public:
	// 외부에 오픈할 킥 반응 함수
	void HandleLocalPredictionKick();
	
private:
	// 로컬 예측 진행 중인 남은 시간 (이 시간이 0보다 크면 서버 동기화를 무시함)
	float PredictionInterpCooldown = 0.0f;


// 2. 축구공 cpp의 Tick함수에서 보간을 패스하는 코드를 추가해준다.

// 쿨다운 타이머가 작동 중이라면 감소시키고 보간을 패스
if (PredictionInterpCooldown > 0.0f)
{
	PredictionInterpCooldown -= DeltaTime;
	return; // 공이 서버 위치로 바뀌어서 생기는 현상 차단
}

// 외부에 오픈할 킥 반응 함수 내부 구현
void ASG_SoccerBall::HandleLocalPredictionKick()
{
    // 렉 환경(150ms)을 고려하여 약 0.25초 동안 서버 패킷 보간을 차단
    PredictionInterpCooldown = 0.25f; 
}

// 3. 기존 AddImpulse 밑에 로컬인경우 서버를 잠시 차단하게 위에서 만든 함수를 호출해준다.
BallMesh->AddImpulse(PushDirection * CachedFinalKickPower, NAME_None, true);
					
if (HasAuthority(&CurrentActivationInfo))
{
	UE_LOG(LogTemp, Warning, TEXT("🔴 [SERVER] 서버 물리 적용 완료!"));
}
else
{
	SoccerBall->HandleLocalPredictionKick();
	UE_LOG(LogTemp, Warning, TEXT("🟢 [CLIENT] 로컬 예측 중... 잠시 서버 동기화 차단"));
}
```

<br/>

**1. 발생한 현상(3)**   
0.25초 동안은 되감기가 방지되는 듯했으나 타이머가 만료되는 순간 공이 이전보다 더 크게 튀거나 서버 위치로 `강제 스냅(Snap)`되는 현상이 발생했다.   

**2. 원인**   
- 엔진 내부 복제 시스템의 한계   
C++ Tick에서 보간을 막더라도, 언리얼 엔진 내부의 리플리케이션 시스템은 서버로부터 받은 위치 데이터를 액터 변수에 계속 업데이트하고 있었다.   

- 오차의 누적 및 폭발   
0.25초 동안 클라이언트가 예측한 공의 위치와 서버가 계산한 공의 실제 위치 간의 오차가 극대화된 상태에서, 타이머가 끝나자마자 보간 로직이 재개되면서 쌓여있던 오차가 한 번에 반영되어 더 심한 고무줄 현상을 유발한다.   

**3. 해결을 위해 시도한 방법**    
단순하게 공 위치를 복제하는것은 한계가 있다고 느끼고 축구공의 완전한 물리 상태를 동기화하기 위해 `위치(Location)`, `회전(Rotation)`, `선속도(LinearVelocity)`, `각속도(AngularVelocity)`를 포함하는 `FBallPhysicsState` 구조체를 커스텀 정의했다.      
해당 구조체를 `ReplicatedUsing = OnRep_ServerPhysicsState로 설정`하여, 서버에서 물리 값이 변할 때마다 클라이언트가 변위와 운동 상태(속도)를 통째로 전달받아 동기화하도록 유도했다.      

<br/>

```cpp
// 축구공의 정보를 저장하는 구조체를 생성

// 축구공의 물리 상태 저장용 구조체(Server)
USTRUCT(BlueprintType)
struct FBallPhysicsState
{
	GENERATED_BODY()

	UPROPERTY()
	FVector Location = FVector::ZeroVector;

	UPROPERTY()
	FRotator Rotation = FRotator::ZeroRotator;

	UPROPERTY()
	FVector LinearVelocity = FVector::ZeroVector;

	UPROPERTY()
	FVector AngularVelocity = FVector::ZeroVector;
};

// 서버의 물리 상태 동기화 (ReplicatedUsing 설정)
UPROPERTY(ReplicatedUsing = OnRep_ServerPhysicsState)
FBallPhysicsState ServerPhysicsState;

UFUNCTION()
void OnRep_ServerPhysicsState();
```

<br/>

**1. 발생한 현상(4)**   
이전 방식보다 미세하게 나아지는듯 했으나 패킷이 도달할 때마다 공이 미세하게 떨리거나 뚝뚝 끊기는 현상(Jittering)은 근본적으로 잡히지 않았다.      

**2. 원인**   
- 네트워크 레이턴시의 누락   
OnRep으로 수신한 서버의 물리 데이터는 이미 네트워크 핑만큼 과거의 정보이므로 이를 클라이언트 물리 엔진에 그대로 대입하면 현재 타임라인과 오차가 발생했다.   

- 보간(Interpolation) 로직의 부족   
데이터를 수신은 완벽했으나 과거(서버)의 위치와 클라(현재)의 위치 사이를 매끄럽게 이어주는 예측 보간 로직이 부족해서 시각적인 끊김을 해결할 수 없었다.    

**3. 해결을 위해 시도한 방법**    
물리 연산의 주도권이 서버에 고정되어 있는 한 레이턴시를 완벽히 극복하는 복제는 불가능하다는 판단했다.     
이를 해결하기 위해 공을 차거나 접촉하는 순간 해당 클라이언트에게 공의 네트워크 소유권을 일시적으로 위임하여 클라이언트가 물리를 계산하고 서버로 역복제하는 `소유권(OwnerShip)기반 예측 구조`로의 전환했다.      

<br/>

```cpp
// OwnerShip 관련 코드
void ASG_SoccerBall::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
    
    // 서버권한으로 소유권 관리(공이 멈추면)
    if (HasAuthority())
    {
        // 주인이 있는 상태인데 공이 거의 멈췄다면 (속력이 5 이하)
        if (GetOwner() != nullptr && SoccerBallMesh->GetPhysicsLinearVelocity().Size() < 5.0f)
        {
            // 안전하게 소유권을 반납하고 타이머를 취소
            SetOwner(nullptr);
            GetWorld()->GetTimerManager().ClearTimer(OwnerReleaseTimerHandle);
            UE_LOG(LogTemp, Log, TEXT("🔴 [SERVER] 공이 정지하여 소유권을 반납"));
        }
    }
    
    // ... 동기화 코드
    
    // 화면 좌측 상단에 현재 오너 상태 실시간 디버깅 출력
    if (GEngine)
    {
        AActor* CurrentOwner = GetOwner();
        FString OwnerName = CurrentOwner ? CurrentOwner->GetName() : TEXT("No Owner (NULL)");
        FString NetMode = HasAuthority() ? TEXT("서버") : TEXT("클라이언트");
        FColor DisplayColor = HasAuthority() ? FColor::Red : FColor::Green;

        GEngine->AddOnScreenDebugMessage(
            1, 0.0f, DisplayColor, 
            FString::Printf(TEXT("[%s] 공의 현재 Owner: %s"), *NetMode, *OwnerName)
        );
    }
}

void ASG_SoccerBall::NotifyHit(
    UPrimitiveComponent* MyComp, 
    AActor* Other, 
    UPrimitiveComponent* OtherComp, 
    bool bSelfMoved, 
    FVector HitLocation, 
    FVector HitNormal, 
    FVector NormalImpulse,
    const FHitResult& Hit
)
{
    Super::NotifyHit(MyComp, Other, OtherComp, bSelfMoved, HitLocation, HitNormal, NormalImpulse, Hit);

    ACharacter* HittingCharacter = Cast<ACharacter>(Other);
    
    // 소유권 변경 조작은 오직 서버 권한
    if (HittingCharacter && HasAuthority())
    {
        // 만약 소유권 전환 락(0.1초)이 걸려있다면
        if (GetWorld()->GetTimerManager().IsTimerActive(OwnerCooldownTimerHandle))
        {
            // 락이 걸려있더라도 현재 이 공의 주인인 플레이어가 계속 비비고 있는 거라면
            if (GetOwner() == HittingCharacter)
            {
                // 소유권 반납 타이머를 계속 3초 뒤로 (드리블 유지)
                float ReleaseDelay = 3.0f; 
                GetWorld()->GetTimerManager().SetTimer(OwnerReleaseTimerHandle, this, &ASG_SoccerBall::ReleaseOwner, ReleaseDelay, false);
            }
            return;
        }

        // 소유권 변경
        if (GetOwner() != HittingCharacter)
        {
            SetOwner(HittingCharacter);
            
            // 0.1초 동안은 짧게 소유권이 또 바뀌지 않도록 락
            float OwnerLockTime = 0.1f; 
            GetWorld()->GetTimerManager().SetTimer(OwnerCooldownTimerHandle, this, &ASG_SoccerBall::ResetOwnerCooldown, OwnerLockTime, false);
        }
        
        // 공을 건드린 시점부터 1초 동안 안 건드리면 소유권을 해제하는 타이머 예약/갱신
        float ReleaseDelay = 3.0f; 
        GetWorld()->GetTimerManager().SetTimer(OwnerReleaseTimerHandle, this, &ASG_SoccerBall::ReleaseOwner, ReleaseDelay, false);
    }
}

void ASG_SoccerBall::ReleaseOwner()
{
    if (HasAuthority())
    {
        // 공에서 발을 떼고 0.5초가 지나면 오너를 다시 날려버려 서버 공으로 만듭니다.
        SetOwner(nullptr);
        UE_LOG(LogTemp, Warning, TEXT("🔴 [SERVER] 소유권 회수 (NULL)"));
    }
}

void ASG_SoccerBall::IgnoreServerPhysicsForDuration(float Duration)
{
    if (!HasAuthority())
    {
        KickPredictionTimer = Duration;
    }
}

void ASG_SoccerBall::ResetOwnerCooldown()
{
    // 타이머 구동용 빈 함수
}
```

<br/>

**1. 발생한 현상(5)**   
소유권 이전을 위해 엔진의 기본 복제 기능을 끄자마자 서버와 클라이언트의 공이 아예 다른 위치에서 따로 노는 치명적인 현상과 물리 버그들이 동시다발적으로 터졌다.      
- 공이 영원히 멈추지 않는 현상   
- 시작점과 속도는 같으나 최종 위치가 다른 현상   
- OwnerShip 부여 이후 공의 동기화가 안되는 현상   

**2. 원인**   
- 마찰력과 제동력을 세팅했음에도 공이 감속되지 않고 `무한히` 굴러간다. 분석 결과 서버에서 클라이언트로 위치와 속도를 복제해 주는 패킷 함수가 과거의 동일한 속도 데이터를 지속적으로 덮어쓰면서 `감속 연산을 초기화`하고 있었다.         
- 공의 속도 위주로만 복제하다 보니, `프레임 타임(DeltaSeconds)의 미세한 차이`와 네트워크 지터로 인해 감속이 돼서 멈추기 직전의 클라이언트와 서버의 최종 위치가 수 미터씩 어긋난다.    
- `if (MyPawn && MyPawn->IsLocallyControlled()) return;` 이 코드로 과하게 보호하고 있었다.     
공을 터치하여 소유권을 얻은 뒤, 공이 내 몸에서 떨어져 저 멀리 날아가거나 서버와 물리 오차가 크게 벌어졌을 때도 무조건 서버 패킷을 튕겨내 버리니 공이 아예 동기화 궤도를 이탈한다.     

**3. 해결을 위해 시도한 방법**    
- `SetReplicateMovement(false)`를 명확히 굳히고 서버 측의 무분별한 물리 복제 간섭 코드를 차단하여 물리 엔진 고유의 마찰력이 작동하도록 수정한다.      
- `OnRep_ServerPhysicsState` 내부에서 공의 현재 속력(CurrentSpeed)과 오차 거리(Distance)를 매 프레임 체크한다.   
시속이 낮아져 거의 멈춰가거나(CurrentSpeed < 100.0f) 오차가 너무 클 때만 작동하도록 제한했다.      
완전히 정지했을 때는 서버 위치로 즉시 이동(`SetWorldLocation`)시키고, 굴러가는 중일 때는 `VInterpTo`를 이용해 유저 눈에 띄지 않게 은근슬쩍 `서버 타임라인으로 보정(Blending)`하는 정밀 제어 코드를 구축했다.      
- `NotifyHit` 컴포넌트 충돌 시점을 개편한다. 쿨다운(0.1초) 중이라도 현재 공을 계속 치며 달리는 주인이 나라면 `ReleaseOwner`타이머를 0.5초로 계속 연장(드리블 유지)시켜 로컬 연산권을 보장했다.      
하지만 발에서 공이 떨어져 0.5초 동안 터치가 없으면 즉시 `ReleaseOwner()`를 호출하여 소유권을 서버에 안전하게 반납하도록 설계함. 공이 내 소유를 떠나는 순간 다시 서버의 정상적인 동기화 흐름 안으로 복귀시켰다.      

<br/>

**1. 발생한 현상(6)**   
소유권은 잘 전달되지만 가장 중요한 공의 동기화 문제가 해결되지 않고있다.      

**2. 원인**   
`SetReplicateMovement(false)`라서 공의 위치를 아무도 주도하지 않았다. 소유권만 가지고 있지 모든 서버와 클라에서 각자 재생을 해버려서 위치 차이가 극심해졌다.    

**3. 해결방법**    
기존 로직과 합쳐서 소유권, 물리 주도권 부여 방식 + 제3자 클라이언트는 예측 보간하는 방식을 채용했다.   
- 물리를 켜고 끄는 로직을 추가하여 소유권을 가진 클라이언트와 서버만 물리를 켜고 그걸 지켜보는 제 3자는 소유권과 물리 모두 가지고 있지 않게 한다.   
- 소유권을 가진 캐릭터는 물리 연산을 주도하여 서버에게 State를 전달하고 서버는 타클라에 브로드캐스트 한다.   
- 제 3자는 서버로 부터 받은 State로 예측 보간을 한다.   


```cpp
// Tick() 함수에서는 항상 소유권 체크
void ASG_SoccerBall::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
    
    if (IsLocallyControlledOwner())
    {
        UpdateOwnedBall(DeltaTime);
    }
    else if (HasAuthority())
    {
        UpdateServerBall(DeltaTime);
    }
    else
    {
        UpdateRemoteBall(DeltaTime);
    }
    
    if (HasAuthority())
    {
        if (HasBallOwner())
        {
            if (UWorld* World = GetWorld())
            {
                // Owner를 가지는 최소한의 시간 보장 (0.35초)
                if (World->GetTimeSeconds() > LastOwnerChangeTime + OwnershipDuration)
                {
                    float MinKeepOwnerTime = 0.5f; 
    
                    // Kick을 한 후 Onwer를 가지는 최소한의 시간 보장 (0.5초)
                    if (World->GetTimeSeconds() > LastOwnerChangeTime + MinKeepOwnerTime)
                    {
                        // 공의 속도가 거의 멈췄을 때만 Owner를 nullptr로 회수
                        if (BallMesh->GetPhysicsLinearVelocity().SizeSquared() < (50.f * 50.f)) // 50cm/s 이하
                        {
                            SetBallOwner(nullptr);
                        }
                    }
                }
            }
        }
    }
}

// 조건을 만족하면 SetBallOwner()를 서버권한으로 실행
void ASG_SoccerBall::SetBallOwner(APawn* NewOwner)
{
    // Owner는 서버에서만 실행
    if (!HasAuthority())
    {
        return;
    }
    
    SetOwner(NewOwner);
    RefreshPhysicsSimulation();
    ForceNetUpdate();
    
    LastOwnerChangeTime =GetWorld()->TimeSeconds;
}

// SetReplicateMovement()를 관리하는 함수, 관찰자인 Remote들은 물리를 꺼버린다.
void ASG_SoccerBall::RefreshPhysicsSimulation()
{
    // Server 혹은 Owner Client 일 경우에만 True
    bool bShouldSimulate = HasAuthority() || IsLocallyControlledOwner();
    
    // Remote Client는 Physics를 OFF 해준다.
    BallMesh->SetSimulatePhysics(bShouldSimulate);
    if (!bShouldSimulate)
    {
        BallMesh->SetPhysicsLinearVelocity(FVector::ZeroVector);
        BallMesh->SetPhysicsAngularVelocityInDegrees(FVector::ZeroVector);
    }
}

```

<br/>

### 네트워크 환경에서 축구공의 물리 구현 R&D(결과 요약)   

---
<br/>

서버가 독점하는 구조를 택하지않고 공과 상호작용하는 캐릭터가 일시적으로 공의 주인이 되어 연산을 주도하고 서버로 역복제하는 구조를 자체적으로 구축하여 문제를 최종 해결   

### 핵심 메커니즘 및 예외 처리
1. **역할별 틱(Tick) 제어 및 물리 시뮬레이션 On/Off (`RefreshPhysicsSimulation`)**
   * **로컬 오너(소유자 클라이언트):** 공의 소유권을 쥐는 순간 로컬 물리 시뮬레이션을 켜고(`SetSimulatePhysics(true)`), 초당 30회(`StateSendInterval`) 주기로 자신의 완벽한 로컬 물리 데이터를 서버로 역복제(`Server_SendBallState`)함.(체감 레이턴시 0ms)   
   * **제3자 플레이어(리모트 클라이언트):** 불필요한 연산 낭비 및 충돌 꼬임을 막기 위해 물리를 끄고(`SetSimulatePhysics(false)`), 서버가 브로드캐스트해 주는 데이터를 기반으로 미래 위치를 예측하는 **데드 레코닝(Dead Reckoning)** 보간 로직을 수행하여 타인 화면에서도 공이 부드럽게 흐르도록 구현   
2. **충격량 기반의 소유권 즉시 강탈 (`OnBallHit`)**
   * 다수의 플레이어가 난전을 벌일 때 소유권이 마구 흔들리는 것을 막기 위해 최소 유지 시간(`OwnershipDuration = 0.35초`)을 두었으나, 그냥 공에 비비는 것이 아닌 강한 킥(`ImpactForce > 1000.f`)이 들어올 경우 쿨다운을 무시하고 즉시 소유권을 넘겨받도록 예외 처리   
3. **안정적인 소유권 서버 반환 조건 세팅**
   * 공을 차서 발을 떠난 뒤에도 무작정 소유권을 쥐고 있으면 안 되므로, 최소 킥 유지 시간(0.5초)이 지난 후 공의 선속도가 거의 멈춘 상태(`50cm/s` 이하)가 되었을 때 안전하게 소유권을 서버(`nullptr`)로 회수하여 맵 전체의 정적 동기화 밸런스를 맞춤   
4. **연속 충돌 안정성 확보 (`SetUseCCD(true)`)**
   * 소유권이 급격하게 바뀌며 강한 물리 속도가 가해질 때 공이 벽이나 바닥을 뚫고 맵 밑으로 추락하는 물리 버그를 방지하기 위해 연속 충돌 감지(CCD)를 활성화하여 예외 상황을 원천 차단   

<br/>

### 최종 구현까지 오면서 얻은 성과    
- 서버가 주도적으로 통제하는 물리 복제를 통해서 보간하는 방식은 한계가 명확하다.   
- 주도권과 물리 계산을 클라이언트에게 동적으로 위임하고 회수하는 방식을 사용하고 Remote는 예측 보간을 사용하는 방식이 훨씬 자연스러운 구현이 가능하다.   

<br/>

### 네트워크 환경에서 축구공의 물리 구현 R&D(자세한 로직)
---   

1. **게임 실행 시 공이 스폰**   

   - **BeginPlay() 실행**   
`RefreshPhysicsSimulation()` 호출   
서버는 `bShouldSimulate`가 `true`라서 물리가 켜짐   
Owner가 아직 없는 상태라서 클라이언트들은 모두 물리가 꺼져있는 상태   

   - **충돌 이벤트 등록(Server)**   
서버는 `BallMesh->OnComponentHit`에 `OnBallHit` 함수를 바인딩해서 축구공의 충돌을 감시하기 시작   

2. **클라이언트가 공을 건드림(소유권 획득)**   

   - **`OnBallHit()` 발동(Server)**   
	공에 접촉이 발생해서 `OnBallHit()`를 호출   
	`CanChangeOwner()` 조건을 만족하면 서버는 `SetBallOwner()`를 호출   

   - **SetBallOwner() 처리(Server)**   
	SetBallOwner()를 호출하여 서버 권한으로 `SetOwner`를 통해 Owner를 부여   
	`LastOwnerChangeTime`을 기록하여 최소 소유 시간(OwnershipDuration = 0.35s) 타이머를 가동   
	`ForceNetUpdate()`를 날려 Replication을 액터 업데이트 주기와 상관없이 즉시 발생   

   - **`OnRep_Owner()` 호출(Client)**   
	`Owner` 변수가 `복제`되면서 모든 클라이언트에서 `OnRep_Owner()`가 가동되고, `RefreshPhysicsSimulation()`이 다시 실행   
	공을 찬 클라이언트는 `IsLocallyControlledOwner()`가 `true`가 되므로 그 즉시 공의 물리가 켜짐   
	해당 클라이언트의 화면에서는 지연없이 시원하게 공이 날아감   
	관전자 클라이언트는 여전히 물리가 꺼진상태   

3. **공이 움직일 때**   
   - **Owned Client**   
	Tick() -> `UpdateOwnedBall()`을 실행시킴.   
	내부 타이머(StateSendTimer)를 작동하고 약 1/30초 마다 클라 기준의 축구공 상태를 `FillCurrentBallState()`로 묶어 RPC(`Server_SendBallState`)로 통보   

   - **Server**   
	`Server_SendBallState_Implementation()`로 State를 받음.   
	서버 자신의 공 위치와 속도(`BallMesh->SetPhysicsLinearVelocity`)를 클라이언트와 똑같이 맞춰주고 물리 엔진을 깨운다(WakeRigidBody, 공이 Sleep 상태일 수 있어서).   
	이와 동시에 레플리케이션 변수인 `ReplicatedBallState`에 이 값을 저장. (이 값이 변하면서 다른 관전자들에게 복제 시작)

   - **Remote Client**   
	서버로부터 ReplicatedBallState가 복제되면 `OnRep_BallState()`가 호출   
	관전자 PC는 네트워크 지연 시간(Ping) 동안 공이 더 이동했을 것을 감안하여 `속도X예측시간`(PredictionTime)을 더한 최종 목표 위치(TargetLocation)를 계산   
	매 프레임 `UpdateRemoteBall()` 안에서 FMath::VInterpTo()와 RInterpTo()를 이용해 현재 내 화면의 공을 TargetLocation까지 부드럽게 미끄러지듯 보간   
	만약 렉 때문에 오차가 너무 크면(SnapDistance 초과), 강제로 순간 이동(SetWorldLocationAndRotation)시켜 싱크를 맞춤   

4. **공이 멈춤**   
	- 공이 마찰력(`LinearDamping = 0.5f`)에 의해 점점 느려지다가 멈추는 단계   
	서버의 Tick() 감시 조건공이 날아가는 동안 서버는 매 프레임 Tick() 하단에서 소유권을 뺏어올지 체크   
	소유권이 바뀐 지 최소 0.35초가 지났고, 킥을 한 지 최소 0.5초가 지났는지 확인   
	속도 판정 및 공의 속도의 제곱(SizeSquared())이 $50 \times 50$ (즉, 속도가 50cm/s 이하)로 떨어지면 공이 거의 멈췄다고 판단   
	- 서버는 `SetBallOwner(nullptr)`를 호출하여 소유권을 다시 회수   
	Owner가 nullptr이 되었으므로 다시 `OnRep_Owner()`가 돌며 모든 클라이언트의 공 물리가 꺼짐   
	공은 서버의 물리 연산만 켜진 채 정지(소유권을 탐색하는 상태로 대기)   

<br/>

## 네트워크 환경에서 캐릭터 래그돌 R&D

기본적인 Ragdoll 로직을 작성한 후 다양한 상황에서 테스트를 진행하였다.   

### 초기 세팅   

충격량과 충격 위치를 서버가 판단한 뒤, 모든 클라이언트에 동시에 래그돌을 켜기 위해 `멀티캐스트(NetMulticast)` 방식을 사용한다.   
    
```cpp
// Character.h

// 래그돌 실행
UFUNCTION(NetMulticast, Reliable)
void MulticastEnableRagdoll(FVector HitImpulse, FVector HitLocation);
void EnableRagdoll(FVector HitImpulse, FVector HitLocation);
	
// 래그돌 해제
UFUNCTION(NetMulticast, Reliable)
void MulticastDisableRagdoll();
void DisableRagdoll();

// Character.cpp
void ASG_Character::EnableRagdoll(FVector HitImpulse, FVector HitLocation)
{
	USkeletalMeshComponent* MeshComp = GetMesh();
	UCapsuleComponent* CapsuleComp = GetCapsuleComponent();
	UCharacterMovementComponent* MovementComp = GetCharacterMovement();

	if (!MeshComp || !CapsuleComp || !MovementComp) 
	{
		return;
	}

	// 캡슐 콜리전 비활성화
	CapsuleComp->SetCollisionEnabled(ECollisionEnabled::NoCollision);

	// 캐릭터 이동 및 입력 멈춤
	MovementComp->DisableMovement();
	MovementComp->StopMovementImmediately();

	// 메쉬의 피직스 시뮬레이션 켜기
	MeshComp->SetCollisionProfileName(TEXT("Ragdoll"));
	MeshComp->SetAllBodiesSimulatePhysics(true);
	MeshComp->SetSimulatePhysics(true);
	MeshComp->WakeAllRigidBodies();

	// 드롭킥 Impulse 전달
	MeshComp->AddImpulseAtLocation(HitImpulse, HitLocation);
}

void ASG_Character::MulticastEnableRagdoll_Implementation(FVector HitImpulse, FVector HitLocation)
{
	EnableRagdoll(HitImpulse, HitLocation);
}

void ASG_Character::DisableRagdoll()
{
    // EnableRagdoll 세팅 복구 코드 및 StandUp Montage 재생 코드
}

void ASG_Character::MulticastDisableRagdoll_Implementation()
{
    DisableRagdoll();
}
```

<br/>

**1. 발생한 현상**   
드롭킥 피격 시 캐릭터가 날아가지 않고 제자리에 주저앉는 현상이 발생했다.   

**2. 원인**   
`AddImpulseAtLocation`은 기본적으로 스켈레탈 메쉬의 질량($\text{Mass}$)을 곱해서 연산한다. 언리얼 엔진이 자동 계산한 메쉬의 기본 질량이 너무 무거워 충격량이 상쇄되어 발생한 현상이다.   
    
**3. 해결 방법**    
질량을 무시하고 순수 속도 변화량으로 밀어버리는 `bVelChange = true` 옵션을 사용한다. 이때 래그돌의 중심축인 `골반(Hips)` 본을 명시해 주어야 사지가 찢어지지 않고 자연스럽게 날아간다.   

<br/>

```cpp
// 속도 기반(Velocity Change)을 위해 세 번째 인자에 골반 본을 명시
MeshComp->AddImpulseAtLocation(HitImpulse, HitLocation, TEXT("Hips"));
```

<br/>

---

<br/>

**1. 발생한 현상**   
래그돌 상태일 때 카메라는 제자리에 멍 때리고, 기상 시 화면이 튀는 현상이 발생했다.   

**2. 원인**   
메쉬만 저 멀리 날아가고 카메라가 붙어있는 `CapsuleComponent` 자체는 피격당한 원점에 있기 때문에 발생하는 카메라 분리 현상이다.   
    
**3. 해결 방법**    
래그돌이 켜지는 순간 `CameraBoom`을 메쉬의 `Hips(골반)` 소켓에 임시 부착하고, 래그돌이 해제될 때 다시 원래대로 `CapsuleComponent`로 부착 대상을 원복 시킨다.   

```cpp
// 1. EnableRagdoll() 호출 시 골반 부착
if (CameraBoom) 
CameraBoom->AttachToComponent(GetMesh(), FAttachmentTransformRules::SnapToTargetNotIncludingScale, TEXT("Hips"));

// 2. DisableRagdoll 함수 호출 시 캡슐 원복 및 오프셋 초기화
if (CameraBoom) 
{
    CameraBoom->AttachToComponent(CapsuleComp, FAttachmentTransformRules::SnapToTargetNotIncludingScale);
    CameraBoom->SetRelativeLocation(FVector::ZeroVector);
}
```

<br/>

---

<br/>

**1. 발생한 현상**   
기상 시 서버와 클라이언트 간의 회전(Rotation) 및 위치 동기화가 튀는 현상이 발생했다.   

**2. 원인**   
물리 엔진(Chaos Physics)의 연산 오차로 인해 서버와 클라이언트가 인지하는 누워있는 메쉬의 최종 위치가 미세하게 달랐다. 클라이언트가 독단적으로 일어난 후 서버가 좌표를 덮어씌우니 뚝뚝 끊기듯 튀는 현상이 발생한 것이다.   
    
**3. 해결 방법**    
기존의 방식과 다르게 `Server`용과 `Client`용으로 `2개의 DisableRagdoll 함수`를 만들어줬다.   
서버가 래그돌이 멈춘 시점의 Hips 위치를 측정하여 최종 캡슐 위치를 확정하고, 이 좌표를 `Multicast` 파라미터로 클라이언트들에게 전파해 주면 모든 화면에서 동일한 위치에 보이게 된다.   

```cpp
// Character.h
// --- Server ---
// 서버에서 래그돌 해제 타이머 종료 시 호출
void ServerDisableRagdoll();

// 서버가 계산한 위치/회전/방향을 모든 클라이언트에 멀티캐스트
UFUNCTION(NetMulticast, Reliable)
void MulticastDisableRagdoll(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown);

// --- Server, Client ---
// 실제 래그돌 해제 및 복구 로직(기존 DisableRagdoll() 함수에서 이름만 바꿈)
void DisableRagdollInternal(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown);


// Character.cpp
// Server에서만 실행
void ASG_Character::ServerDisableRagdoll()
{
	// 서버만!
	if (!HasAuthority())
	{
		return;
	}

	USkeletalMeshComponent* MeshComp = GetMesh();
	UCapsuleComponent* CapsuleComp = GetCapsuleComponent();
	if (!MeshComp || !CapsuleComp)
	{
		return;
	}

	// 서버 기준 래그돌 Hips 위치 및 회전 수집
	FVector HipsLocation = MeshComp->GetSocketLocation(TEXT("Hips"));
	FRotator HipsRotation = MeshComp->GetSocketRotation(TEXT("Hips"));
	bool bIsFaceDown = IsRagdollFaceDown();

	// 동기화할 캡슐 위치 및 회전값 연산
	FVector NewCapsuleLocation = HipsLocation;
	NewCapsuleLocation.Z += CapsuleComp->GetScaledCapsuleHalfHeight();

	// ...

	// 계산된 완벽한 좌표 정보를 모든 클라이언트에 동기화
	MulticastDisableRagdoll(NewCapsuleLocation, NewCapsuleRotation, bIsFaceDown);
}

// 정보들을 서버에 멀티캐스트
void ASG_Character::MulticastDisableRagdoll_Implementation(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown)
{
	DisableRagdollInternal(TargetLocation, TargetRotation, bIsFaceDown);
}

// 실제 래그돌 복구 실행 함수
void ASG_Character::DisableRagdollInternal(FVector TargetLocation, FRotator TargetRotation, bool bIsFaceDown)
{
    // ...  DisableRagdoll() 로직 중 서버에 전권을 넘겨준 Hips/회전값을 제외한 기존 코드 유지
}
```

<br/>

### 네트워크 환경에서 캐릭터 래그돌 R&D(결과 요약)   

---
<br/>

네트워크 환경에서의 래그돌 시스템은 '피직스 제어권의 주체'와 '서버 중심의 위치 및 회전 값 확정'이 핵심이다.   

### 핵심 메커니즘 및 예외 처리
1. **서버 권한 중심의 3단계 복구 프로세스 (Server ➔ Multicast ➔ Internal)**
   * 각 클라이언트의 환경(프레임, 핑)에 따라 미세하게 달라지는 물리 연산 오차로 인한 기상 시 텔레포트(위치 튐) 현상을 차단한다.      
   * `Server`에서 최종 Hips 위치 기준 바닥면 검출 및 앞/뒤 방향 판정을 통해 위치 및 회전 값 확정 ➔ `Multicast`로 전파 ➔ `Client(Internal)`가 동일한 값으로 동기화 후 기상 애니메이션을 실행하는 구조를 구현했다.     
2. **질량 무시 기반의 충격량 처리(bVelChange)**
   * 에셋의 기본 질량($\text{Mass}$)으로 인해 충격량이 상쇄되어 주저앉는 현상을 `bVelChange = true` 옵션과 `Hips Bone 지정`을 통해 해결하여, `Mass`에 상관없이 자연스럽게 날아가게 물리적 처리를 했다.      
3. **카메라 제어(CameraBoom 소켓)**
   * 메쉬가 날아가는동안 기존 위치에 멈춰있는 `Capsule Component`로 인해 카메라도 멈춰있는 현상을 해결하기 위해 래그돌 	지속 시간 동안 `CameraBoom`을 메쉬의 `Hips 소켓`에 실시간으로 부착하고 래그돌이 끝나면 해제를 했다.   

<br/>

### 최종 구현까지 오면서 얻은 성과    
- 서버가 래그돌의 시작과 끝에서 `Multicast`를 해주면 `Ragdoll`의 흐물거리는 특성상 오차가 많이 발생한다.     
- 눈에 띄는 오차를 발생시키는 `캐릭터의 위치와 골반의 회전값`을 서버만 계산을 하여 `Multicast` 해주고 해당 값을 기준으로 클라이언트에서 래그돌 해제 후 일어나는 몽타주를 재생시키니 동기화가 매우 자연스럽게 진행됐다.   


   
