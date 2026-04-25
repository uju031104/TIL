# CPP_Unreal_Engine

<br/>

### HLOD(Hierarchical Level of Detail)폴더    
성능을 위해 엔진이 자동으로 만든 데이터 보관소   
알아서 최적화 해주는데 용량도 좀 차지해서 상황에 따라 켜거나 끄는거 추천   


<br/>

***

<br/>

### FString

```cpp
//헤더파일
#include "Engine/Engine.h"
// GEngine이 존재하는지 확인 후 실행
if (GEngine)
{
    GEngine->AddOnScreenDebugMessage(-1, 3.0f, FColor::Red, FString::Printf(TEXT("Actor : %s"), *ActorLocation.ToString()));
}
```

보통 C++에서 * 는 포인터가 가리키는 실제 값을 가져오는 '역참조' 연산자이다. 하지만 언리얼의 FString 클래스는 이 * 연산자를 특별하게 재정의(Overloading) 해두었다.   
FString 앞에 * 를 붙이면?  
"가방(객체) 안에 들어있는 실제 문자열 데이터(TCHAR*)의 시작 주소를 반환해라!"라는 뜻이 된다.   

<br/>

***

<br/>


### Component Setting 

```cpp
AItem::AItem()
{
    SceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneRoot"));
    // 루트 컴포넌트로 설정해주기(+루트는 자동으로 리플렉션 시스템에 등록)
    SetRootComponent(SceneRoot);

    StaticMeshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("StaticMesh"));
    // 컴포넌트 붙이기
    StaticMeshComp->SetupAttachment(SceneRoot);

    static ConstructorHelpers::FObjectFinder<UStaticMesh> MeshAsset(TEXT("/Game/Resources/Props/SM_Chair.SM_Chair"));
    if (MeshAsset.Succeeded())
    {
        StaticMeshComp->SetStaticMesh(MeshAsset.Object);
    }

    // Metarial은 여러개가 될 수 있어서 아래처럼 (0, 머터리얼 변수명.Object)로 1개만 쓴다고 알려줘야함
    static ConstructorHelpers::FObjectFinder<UMaterial> MaterialAsset(TEXT("Game/Resources/Materials/M_Metal_Gold.M_Metal_Gold"));
    if (MaterialAsset.Succeeded())
    {
        StaticMeshComp->SetMaterial(0, MaterialAsset.Object);
    }
}
```

<br/>

***

<br/>

### Audio Component  

<br/>

```cpp
// 오디오 컴포넌트를 쓰기 위한 헤더파일
#include "Components/AudioComponent.h"

static ConstructorHelpers::FObjectFinder<USoundBase> SoundAsset(TEXT("/Game/Resources/Audio/Fire01_Cue.Fire01_Cue"));
if (SoundAsset.Succeeded())
{
    // 사운드 세팅
    AudioComp->SetSound(SoundAsset.Object);

    // 사운드 자동재생 세팅
    AudioComp->bAutoActivate = true;
}
```

<br/>

***

<br/>

### Actor의 Life Cycle  

콜백 함수를 순서대로 호출한다.   

생성자   
-> 메모리에 생김. 딱 한번 호출

PostInitializeComponents()   
-> 컴포넌트가 완성된 직후 호출. 컴포넌트끼리 데이터 주고받기, 상호작용   

BeginPlay()   
-> 배치(Spawn) 직후   

Tick(float DeltaTime)   
-> 매 프레임마다 호출됨   

Destroyed()   
-> 삭제되기 직전에 호출된다(리소스 정리하면 좋음)   

EndPlay()   
-> 게임 종료, 파괴(Destroyed()), 레벨 전환   

Destroyed()를 부르면 EndPlay()도 호출된다.   
근데 게임을 그냥 종료해버는 상황이라면 EndPlay()만 호출   

팁 : 로그 찍을 때 Destroyed()와 EndPlay()는 Super::~ 부분 위에 하는게 좋다.   

<br/>

***

<br/>

### Actor Transform  

<br/>

```cpp
void AItem::BeginPlay()
{
    Super::BeginPlay();
    
    SetActorLocation(FVector(300.0f, 200.0f, 100.0f));
    SetActorRotation(FRotator(0.0f, 90.0f, 0.0f)); // pitch, yaw, roll 
    SetActorScale3D(FVector(2.0f)); // 하나만 적으면 전체가 다 2배된다.

    // 3가지를 한 번에 관리하는 방법
    FVector NewLocation(300.0f, 200.0f, 100.0f);
    FRotator NewRotation(0.0f, 90.0f, 0.0f);
    FVector NewScale(2.0f);
    FTransform NewTransform(NewRotation, NewLocation, NewScale);

    SetActorTransform(NewTransform);
}
```

<br/>

***

<br/>

### DeltaTime   

<br/>

```cpp
void AItem::Tick(float DeltaTime)
{
    // 120프레임 - 1초 / 120 = DeltaTime
    //  30프레임 - 1초 /  30 = DeltaTime 
    // 1초에 90도씩 회전
    // 90도 / 120 ,  90도 / 30
    Super::Tick(DeltaTime);

    if (!FMath::IsNearlyZero(RotationSpeed))
    {
        AddActorLocalRotation(FRotator(0.0f, RotationSpeed * DeltaTime, 0.0f));
    }

    //AddActorLocalRotation(FRotator(0.0f, RotationSpeed, 0.0f));  // 컴퓨터 마다 프레임이 달라서 이런 방식은 안된다.  

}
```
컴퓨터마다 프레임이 다르기 때문에 DeltaTime을 사용해야한다.   
DeltaTime은 1프레임당 시간이다. 따라서, 프레임이 높을수록 DeltaTime은 작아진다.   
회전하는 값에 DeltaTime을 곱해주면 프레임에 상관없이 같은 시간에 같은 값만큼 회전하게 된다.    

<br/>

***

<br/>

### IsNearlyZero()    

<br/>

 부동소수점은 정확한 0인지 판단하기 어렵기 때문에 `FMath::IsNearlyZero()`를 사용해준다.   


<br/>

***

<br/>

### SetActorScale3D()   

<br/>

```cpp
void ASquare::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

    // 현재 흐르는 시간(초단위)
	float Time = GetWorld()->GetTimeSeconds();
    // 2.0f 스케일에서 -1 ~ 1 범위로 변동
	float ScaleSpeed = 2.0f + FMath::Sin(Time);

	SetActorScale3D(FVector(ScaleSpeed));
}
```

<br/>

***

<br/>

### FMath::Sin() 사용법 

<br/>

```cpp
// 시간 세팅
float Time = GetWorld()->GetTimeSeconds();

// 기본적인 -1 ~ 1의 범위
float S = FMath::Sin(Time);
// 5.0f는 속도이다. 높을수록 빨라진다.
float S = FMath::Sin(Time * 5.0f);
// 50.0f는 범위이다. 높을수록 범위가 크다.
float S = FMath::Sin(Time * 5.0f) * 50.0f;
```

<br/>

***

<br/>

### UActorComponent 사용   

다양한 움직임을 가진 큐브들을 만들때 클래스를 하나하나 만들어야 하진 않을테고 방법을 찾아봤다.   
UActorComponent를 상속받은 클래스를 하나 만들어서 해당 클래스에 다양한 움직임들을 구현한 후 에디터에서 Actor의 Detail 창에서 Add하면 된다.   

```cpp
// 헤더파일에 열거형 클래스를 하나 만들어주고
UENUM(BlueprintType)
enum class EMoveAction : uint8 {
	Idle UMETA(DisplayName = "Idle"),
	UpDown UMETA(DiaplayName = "UpDown"),
	LeftRight UMETA(DisplayName = "LeftRight"),
	Scale UMETA(DisplayName = "Scale"),
	Rotate UMETA(DisplayName = "Rotate")
};

// Switch문으로 나눠준다.

	switch (SeletedAction)
	{
	case EMoveAction::UpDown:
		Owner->AddActorLocalOffset(FVector(0, 0, Range * Value * DeltaTime));
		break;
	case EMoveAction::LeftRight:
		Owner->AddActorLocalOffset(FVector(0, Range * Value * DeltaTime, 0));
		break;
	case EMoveAction::Scale:
		Owner->SetActorScale3D(FVector(1.0f + (Range + 1) / 2));
		break;
	case EMoveAction::Rotate:
		Owner->AddActorLocalRotation(FRotator(0, Speed * DeltaTime, 0));
		break;
	}
```

<br/>

***

<br/>

### Actor에서 ActorComponent에 접근

<br/>

참고로 이런 로직을 Tick()에 구현하면 최적화에 안좋은 영향을 끼치기 때문에 헤더파일에 멤버 변수를 하나 선언하고 BeginPlay()에서 값을 불러온 후 Tick()에서는 해당 멤버 변수를 사용하면 된다. 

```cpp
// 접근할 컴포넌트관련 헤더를 추가
#include "Components/StaticMeshComponent.h"

// StaticMeshComponent에 접근한다.
UStaticMeshComponent* StaticMesh = GetOwner()->FindComponentByClass<UStaticMeshComponent>();
if (StaticMesh)
{
	StaticMesh->AddLocalRotation(FRotator(0, -Speed * DeltaTime, 0));
}
break;
```

<br/>

***

<br/>

### 짐벌락(Gimbal Lock)  

3차원 공간 회전을 계산할 때 사용하는 오일러 각도(Euler Angles) 방식(Roll, Pitch, Yaw)의 구조적 결함   
세 개의 회전축 중 두 개의 축이 겹쳐지면서 한 방향의 자유도를 완전히 잃게됨   

언리얼의 `AddActorLocalRotation`은 이를 어느정도 보정을 해주는데, 아주 정교한 작업을 할 때는 `FQuat`를 써야한다.   

FQuat 예시   
```cpp
// 1. 원하는 회전량을 FRotator로 만듦
    FRotator DeltaRotation(0, Speed * DeltaTime, 0);

    // 2. 이를 쿼터니언(FQuat)으로 변환하여 적용 (짐벌락 방지)
    Owner->AddActorLocalRotation(DeltaRotation.Quaternion());
    break;
```

<br/>

***

<br/>

### 열거형   
`enum class EnumName : uint8`   
enum class를 사용하면 EnumName::Name 처럼 호출하기 때문에 이름이 겹치는 오류에서 안전하다.   
그리고 강제로 `static_cast`를 써서 숫자와 계산을 하게 만들기 때문에 안정성이 높아진다.   
또한 `uint8(1바이트)`를 사용해서 메모리를 아낄 수 있고 uint8은 언리얼의 리플렉션 시스템이랑 제일 잘 맞는다.   

<br/>

***

<br/>

### 열거형을 uint8로 설정하는 이유

열거형으로 설정하는 상태값들(상태 머신, 아이템 등) 255가지를 넘지 않으며(1Byte) 최적화에 매우 좋다.   
네트워크 최적화의 과정엔 4Byte를 1Byte로 변환하는 과정이 필수라서 uin8로 설정하면 자원을 아낄 수 있다.   
블루프린트의 Byte 타입은 C++의 uint8과 매칭돼서 별도의 변환이 필요 없다.   
리플렉션 시스템이 데이터 크기를 정확히 알 수 있어서 직렬화(Serialization) 과정을 더 빠르고 안전하게 처리할 수 있다.   

<br/>

***

<br/>

### IsVaild()   

<br/>

```cpp
IsValid(GetOwner())
```
`GetOwner()`가 destroyed 되거나 그 직전 상황인 경우 크래시가 날 수 있기 때문에 무조건 검사를 하는 습관을 기르자.   

<br/>

***

<br/>

### FMath::RandRange()

```cpp
FVector RandomOffset(
	FMath::RandRange(-100.0f, 100.0f),
	FMath::RandRange(-100.0f, 100.0f),
	FMath::RandRange(-100.0f, 100.0f)
);
```
위 코드처럼 `FMath::RandRange()`에 범위를 넣어주면 된다. float를 넣으면 자동으로 float이 나온다.  

<br/>

***

<br/>

### FMath::Clamp()

<br/>

값을 설정한 범위 내에 가둔다.

```cpp
float Health = 120.0f;
Health = FMath::Clamp(Health, 0.0f, 100.0f); 
// 결과: 100.0f (체력은 100을 넘을 수 없음!)
```
   

<br/>

***

<br/>

### FMath::Lerp  

*FMath::Lerp(Start, End, Alpha)*   
Lerp는 Linear Interpolation(선형 보간)의 약자.   
-> 두 지점 사이의 중간값을 비율로 찾기   

부드러운 연출을 나타낼 때 매우 유용하다.     

```cpp
ElapsedTime += DeltaTime;

// 0.0 ~ 1.0 범위로 정하고 (경과된 시간 / 내가 정해준 시간)으로 로직을 설정했다.
// 내가 정한 시간만큼 흐르면 Alpha값이 최대값인 1.0이 된다.
float Alpha = FMath::Clamp(ElapsedTime / ActionMap[EAction::Disappear].Duration, 0.0f, 1.0f);

// 시간이 흐를수록 Alpha값이 1.0에 다가가게 하여 
// 현재 크기부터 0까지 부드럽게 줄어들게 만듦
FVector NewScale = FMath::Lerp(StartScale, FVector::ZeroVector, Alpha);
```

<br/>

***

<br/>


### Static Class

객체를 생성하지 않고 정적으로 U클래스 타입(리플렉션 시스템이 관리하는)으로 정보를 준다.

```cpp
// GameMode에서 설정해주는 예시 
DefaultPawnClass = ASpartaCharacter::StaticClass();
```

<br/>

***

<br/>