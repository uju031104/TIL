# Line Trace

<br/>

Trace 쓰는 방법은 2가지, 블루프린트(Kismet)와 C++ (GetWorld()->...)   
평소에 블루프린트로 쓰다가(디버깅이 매우 쉬워서) 출시 직전엔 GetWorld()방식   
C++ 방식이 미세하게 더 가볍다.   

   

### 싱글 트레이스

<br/>

```cpp
 //싱글 트레이스(UKismetSystemLibrary 사용)
 //싱글은 Block에만 막힘
void AMyActor::StartSingleTrace()
{
	TArray<AActor*> ActorsToIgnore;
	ActorsToIgnore.Add(this);
	FHitResult HitResult;

	// 첫 인자는 this 넣어도 작동함
	// .Add(this)를 해줬지만 한번 더 true로 해준다.
	// 이래야 버그가 안생김(가끔 다른 컴포넌트가 액터에 붙으면 검출되는 상황이 있음)
	UKismetSystemLibrary::LineTraceSingle(
    // this로 넣어줘도 됨
		GetWorld(), 
    // 시작지점
		GetActorLocation(),
    // 끝지점(액터의 방향벡터와 길이에 시작지점을 더해줘서 구함) 
		GetActorForwardVector() * 1000.f + GetActorLocation(), 
    // TraceType을 Visibility로 설정
		UEngineTypes::ConvertToTraceType(ECC_Visibility),
    // Complex 설정(false로 하면 simple이 됨)
		false,
    // 무시할 엑터를 모아둔 배열
		ActorsToIgnore,
    // 디버깅 얼마동안 할지(밑에 설정은 1프레임)
		EDrawDebugTrace::ForOneFrame,
    // 충돌 결과
		HitResult,
    // 나 자신을 무시할지 결정하는건데, 위에 이미 무시한다고 넣어놨지만 여기도 true로 해줘야 확실하게 무시하게 됨(버그 방지)
		true,
    // 트레이스 색깔
		FLinearColor::Red,
    // 트레이스 충돌 시 색깔
		FLinearColor::Green
	);
}
```
<br/>

***

<br/>

### 멀티 트레이스

<br/>

```cpp
// 멀티 트레이스(UKismetSystemLibrary 사용)
// Overlap은 다 뚫으면서 지나가고 Block에서 막히는데 Block만 있으면 싱글과 같은 기능을 함
// 싱글과 거의 같지만 충돌을 다중으로 하기 때문에 FHitResult만 TArray로 감싸주면 된다.
void AMyActor::StartSingleTrace()
{
	TArray<AActor*> ActorsToIgnore;
	ActorsToIgnore.Add(this);
	TArray<FHitResult> HitResult;

	UKismetSystemLibrary::LineTraceMulti(
		GetWorld(),
		GetActorLocation(),
		GetActorForwardVector() * 1000.f + GetActorLocation(),
		UEngineTypes::ConvertToTraceType(ECC_Visibility),
		false,
		ActorsToIgnore,
		EDrawDebugTrace::ForOneFrame,
		HitResult,
		true,
		FLinearColor::Red,
		FLinearColor::Green
	);
}
```

<br/>

***

<br/>

### 비동기 방식     

<br/>

위 2개는 블루프린트 방식으로 구현했으니 마지막 비동기는 C++ 방식으로 구현   

```cpp
// 비동기 방식
// 메인 스레드에서 다른 스레드한테 일을 짬때림. 그 스레드는 일을 끝내고 다시 결과물을 메인에 줌
void AMyActor::StartAsycnTrace()
{
	// AsyncLineTraceByChannel에 쓸 Delegate 함수 바인딩
	FTraceDelegate TraceDelegate;
	TraceDelegate.BindUObject(this, &AMyActor::OnAsyncTraceCompleted);

	// UWorld() 방식은 이렇게 쿼리를 직접 가져와서 세팅
	FCollisionQueryParams QueryParams;
	FCollisionResponseParams ResponseParams;

	QueryParams.AddIgnoredActor(this);
	QueryParams.bTraceComplex = false;

	// 이 액터랑 부딪히는 오브젝트의 타입이 WorldDynamic이면 콜리전 타입을 강제로 오버랩으로 바꿔버리는 기능
	// 근데 Ignore > Overlap > Block 순으로 약해져서
	// Ignore로 설정해뒀으면 밑에 코드에서 Block으로 바꿔도 안바꿔진다.
	// Block으로 해둔걸 Ignore나 Overlap으로 바꾸거나 Overlap을 Ignore로 바꾸는 용도
	ResponseParams.CollisionResponse.WorldDynamic = ECR_Block;

	// EAsyncTraceType::Test 는 bool 처럼 인식 했냐 안했냐만 체크를 하기때문에 매우 가볍다
	// 예를 들어 눈이 먼 몬스터처럼 인식만 가능한 경우 사용  
	GetWorld()->AsyncLineTraceByChannel(
		// TraceType을 Multi로
		EAsyncTraceType::Multi,
		// Trace 시작점
		GetActorLocation(),
		// Trace 끝점
		GetActorForwardVector() * 1000.f + GetActorLocation(),
		// TraceType
		ECC_Visibility,
		// 위에 설정해둔 QueryParams
		QueryParams,
		ResponseParams,
		// Delegate 함수
		&TraceDelegate
	);
}

// AsyncLineTraceByChannel을 위한 Delegate 함수
void AMyActor::OnAsyncTraceCompleted(const FTraceHandle& Handle, FTraceDatum& Data)
{
	for (const FHitResult& Hit : Data.OutHits)
	{
		AActor* HitActor = Hit.GetActor();

		if (!IsValid(HitActor)) return;

		GEngine->AddOnScreenDebugMessage(-1, 0.f, FColor::Green, FString::Printf(TEXT("Multi Hit Actor : %s"), *HitActor->GetName()));

		// 블루프린트 형식과 다르게 Debug를 알아서 해줘야한다.
		DrawDebugSphere(GetWorld(), Hit.ImpactPoint, 20.f, 12, FColor::Green, false, 2.f);

		// #include "Kismet/KismetSystemLibrary.h" 있어야함
		UGameplayStatics::ApplyPointDamage(
			// 데미지 받는 액터
			HitActor,
			// 기본 데미지 값
			50.f,
			// 데미지 방향
			GetActorForwardVector(),
			// 충돌 결과
			Hit,
			// 때린 놈의 컨트롤러
			GetInstigatorController(),
			// 때린 놈
			this,
			// UDamageType 클래스
			UMyFireDamageType::StaticClass()
		);
	}
}
```