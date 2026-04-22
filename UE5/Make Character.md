# Make Character  

<br/>

과제 8번이 챕터 2~ 4에 했던거에 더 보충하는 느낌인데 이미 해놓은거에 덮어씌우는거보단 최대한 보지않고 직접 다시 구현해보는게 좋을 것 같다고 판단했다.   

1.클래스간 구조 파악 다시 한번 더 해보고 정리   
2.추가로 스마트포인터를 사용하면서 코딩  
3.UPROPERTY, UFUNCTION 같은 언리얼 리플렉션 매크로의 설정을 최대한 보수적으로(VisibleAnywhere 등등) 잡아서 감각 늘리기 

<br/>

### Character   

Character   
Camera, SpringArm   

```cpp
// 카메라와 스프링암

#include "Camera/CameraComponent.h" // 카메라 헤더
#include "GameFramework/SpringArmComponent.h" // 스프링암 헤더

PrimaryActorTick.bCanEverTick = false;

SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArm"));
// RootComponent(Character는 자동으로 캡슐이 루트)
SpringArm->SetupAttachment(RootComponent);
// 스프링암 길이 설정
SpringArm->TargetArmLength = 500.f;
// Pawn(Character)의 회전과 스프링암 회전을 같게 할 것인지
SpringArm->bUsePawnControlRotation = true;

Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("Camera"));
// 카메라가 붙는 SpringArm 맨 끝이 SocketName이다 
// 그냥 Camera->SetupAttachment(SpringArm)이라고 해도 되지만 SocketName을 명시해주면 더 명확해진다.
Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);
// 카메라는 어차피 스프링암에 붙어있기 때문에 false
Camera->bUsePawnControlRotation = false;
```

<br/>

### PlayerController

PlayerController   
IA, IMC   
BeginPlay() -> IMC 연결   

```cpp
// IMC 등록하기

// Subsystem을 불러오기 위해 필요한 헤더
#include "EnhancedInputSubsystems.h"

void AMyPlayerController::BeginPlay()
{
	Super::BeginPlay();

	// 1.LocalPlayer를 가져온다.
	if (TObjectPtr<ULocalPlayer> LocalPlayer = GetLocalPlayer())
	{
		// 2.LocalPlayer의 Subsystem을 가져온다.
		if (TObjectPtr<UEnhancedInputLocalPlayerSubsystem> Subsystem = LocalPlayer->GetSubsystem<UEnhancedInputLocalPlayerSubsystem>())
		{
			if (InputMappingContext) // IMC가 있다면
			{
				// 3.LocalPlayer의 Subsystem에 IMC를 등록해준다. 0은 제일 높은 우선순위.
				Subsystem->AddMappingContext(InputMappingContext, 0);
			}
		}
	}
}
```
<br/>

### GameMode   
기본 설정을 한다.   
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


### 실제 캐릭터 움직임 바인딩하기 

컨트롤러가 IA, IMC를 가지고 있고 캐릭터는 실제 움직임을 가지고 있는데 이 두가지를 연결해야한다.   

<br/>

```cpp
// 예시는 Move() 함수

// Character.h
// 전방선언
struct FInputActionValue;

// 리플렉션 시스템에 등록한다.
// BindAction을 할 때 리플렉션 시스템에 등록됐는지 확인을 하기 때문이다.
// 또한 함수 이름으로 호출도 가능해진다.
// 델리게이트 시스템에도 연동이 된다.   
UFUNCTION()
// 인자는 IA의 값을 넣어준다.   
void Move(const FInputActionValue& Value);



// Character.cpp
// 밑에 코드를 위해서는 #include "InputActionValue.h"를 써도 되는데 결국 바인딩도 하기 때문에 더 넓은 범위의 헤더파일을 가져옴
#include "EnhancedInputComponent.h"

void AMyCharacter::Move(const FInputActionValue& Value)
{
	// 캐릭터가 Possess 되어야 로직을 처리할 수 있어서 체크
	if (!GetController()) return;

	// 에디터에서 IA의 Value Type을 FVector2D 값으로 설정해뒀기 때문
	FVector2D const MoveInput = Value.Get<FVector2D>();
	
	// Input Value의 X값이 0이 아닐때(X축으로 움직일때만)
	if (!FMath::IsNearlyZero(MoveInput.X))
	{
		// GetActorForwardVector()는 액터의 정면 "방향"을 가져온다.
		AddMovementInput(GetActorForwardVector(), MoveInput.X);
	}
	// Input Value의 Y값이 0이 아닐때(Y축으로 움직일때만)
	if (!FMath::IsNearlyZero(MoveInput.Y))
	{
		// GetActorForwardVector()는 액터의 오른쪽 "방향"을 가져온다.
		AddMovementInput(GetActorRightVector(), MoveInput.Y);
	}
}
```


<br/>

### Enhanced Input 관련 헤더들  

<br/>

```cpp
//컴포넌트 및 바인딩 관련
#include "EnhancedInputComponent.h"
//IMC 추가/제거 관련
#include "EnhancedInputSubsystems.h" 
//입력 값 추출 관련
#include "InputActionValue.h" 
```
