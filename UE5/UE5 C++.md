# UE5 C++

<br/>

UE5에서 조금 다른 C++ 문법, 특징들 정리



### HLOD(Hierarchical Level of Detail)폴더    
성능을 위해 엔진이 자동으로 만든 데이터 보관소   
알아서 최적화 해주는데 용량도 좀 차지해서 상황에 따라 켜거나 끄는거 추천   

<br/>

***

<br/>

### 객체를 따로 안만드는 이유  
우리가 직접 new를 호출하지 않아도 언리얼 엔진의 '액터 생명주기(Actor Lifecycle)' 시스템이 우리 대신 객체를 만들고 관리해주기 때문이다.

**에디터에서 배치할 때**: 레벨(맵)에 액터를 드래그해서 놓으면, 레벨 파일 안에 해당 클래스의 정보가 저장된다.

**게임이 시작될 때**: 엔진이 레벨을 불러오면서 저장된 리스트를 보고 SpawnActor<AMyActor>()라는 내부 함수를 호출해 객체를 생성한다

<br/>

언리얼 엔진은 객체를 만든 후, 특정 시점이 되면 약속된 함수들을 순서대로 호출한다. 이를 콜백(Callback) 함수라고 한다

**Constructor(생성자)**   
클래스가 메모리에 만들어질 때 (컴포넌트 조립 등)

**PostInitializeComponents**   
모든 컴포넌트가 세팅 완료되었을 때

**BeginPlay**   
"이제 진짜 게임이 시작되었으니 로직을 실행해도 좋다" 라고 엔진이 신호를 보낼 때

**Super::BeginPlay()의 역할**   
부모 클래스가 기본적으로 준비해야할 것들을 다 한뒤 자식 클래스의 로직 실행

<br/>

***

<br/>

UE5에선 필수적으로 int말고 int32을 쓴다. 32비트라고 확실하게 말해주는 역할.

<br/>

***

<br/>

```cpp
//헤더파일
#include "Engine/Engine.h"
// GEngine이 존재하는지 확인 후 실행
if (GEngine)
{
    GEngine->AddOnScreenDebugMessage(-1, 3.0f, FColor::Red, FString::Printf(TEXT("Actor : %s"), *ActorLocation.ToString()));
}
```

위 코드에서 FString::Printf 안에서 %s는 TCHAR* 타입을 원한다. ActorLocation.ToString()은 FString 객체를 반환하므로, 그 앞에 **역참조 연산자(*)**를 붙여야 올바른 문자열 데이터로 변환된다.    

**더 자세한 설명**  
FString::Printf 함수에서 **%s**는 "여기에 문자열을 넣어줘"라는 약속이다. 그런데 표준 C++와 언리얼에서 %s는 FString 객체 그 자체를 이해하지 못한다.   

%s는 `"글자들이 적힌 종이의 시작점(주소)"`을 달라고 하는데, 우리는 `"종이가 들어있는 가방(FString 객체)"`을 통째로 던져주고 있는 상황이다.   
보통 C++에서 * 는 포인터가 가리키는 실제 값을 가져오는 '역참조' 연산자이다. 하지만 언리얼의 FString 클래스는 이 * 연산자를 특별하게 재정의(Overloading) 해두었다.   
FString 앞에 * 를 붙이면?  
"가방(객체) 안에 들어있는 실제 문자열 데이터(TCHAR*)의 시작 주소를 반환해라!"라는 뜻이 된다.   

<br/>

***

<br/>

루프안에서 sleep(), delay()등을 쓰면 루프문 안에 있는동안 화면이 멈춘다. 그래서 비동기적인 방식인 타이머를 사용