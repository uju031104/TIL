# DamageType

<br/>

### DamageType

<br/>

DamageType이라는 클래스가 있는데 내용을 보면 진짜 별거 없는 베이스 클래스이다.   

```cpp
// 실제 UDamageType 내부 모습
// 데미지 관련 변수들만 가득하다.
UCLASS(MinimalAPI, const, Blueprintable, BlueprintType)
class UDamageType : public UObject
{
	GENERATED_UCLASS_BODY()

	/** True if this damagetype is caused by the world (falling off level, into lava, etc). */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=DamageType)
	uint32 bCausedByWorld:1;

	/** True to scale imparted momentum by the receiving pawn's mass for pawns using character movement */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=DamageType)
	uint32 bScaleMomentumByMass:1;

	/** When applying radial impulses, whether to treat as impulse or velocity change. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = RigidBody)
	uint32 bRadialDamageVelChange : 1;

	/** The magnitude of impulse to apply to the Actors damaged by this type. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=RigidBody)
	float DamageImpulse;

	/** How large the impulse should be applied to destructible meshes */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Destruction)
	float DestructibleImpulse;

	/** How much the damage spreads on a destructible mesh */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Destruction)
	float DestructibleDamageSpreadScale;

	/** Damage fall-off for radius damage (exponent).  Default 1.0=linear, 2.0=square of distance, etc. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=DamageType)
	float DamageFalloff;
};
```

<br/>

***

<br/>

### Default DamageType   

<br/>

```cpp
// 아무런 로직이 없기 때문에 순수하게 데미지만 전달된다.
UGameplayStatics::ApplyPointDamage(
			HitActor,
			50.f,
			GetActorForwardVector(),
			Hit,
			GetInstigatorController(),
			this,
			// 기본 UDamageType 쓰기
			UDamageType::StaticClass()
		);
```

<br/>

***

<br/>

### Custom DamageType 

<br/>

```cpp
// UDamageType을 상속받은 커스텀 데미지 타입을 만든다. 
// MyFireDamageType.h
UCLASS()
class MYPROJECT_API UMyFireDamageType : public UDamageType
{
	GENERATED_BODY()
	
public:

	UMyFireDamageType();
	
	// 화상 지속시간
	UPROPERTY(EditAnywhere, BlueprintReadOnly)
	float BurnDuration;
	// 방어구 관통
	UPROPERTY(EditAnywhere, BlueprintReadOnly)
	float ArmorPenetration;
};

// MyFireDamageType.cpp
UMyFireDamageType::UMyFireDamageType()
{
	// 화상 지속시간
	BurnDuration = 5.f;
	// 방어력 관통
	ArmorPenetration = 0.2f;
}
```

<br/>

***

<br/>

### Actor에서 Custom DamageType 사용   

```cpp
// 실제 데미지를 입는 Actor에 TakeDamage 함수를 오버라이드해서 사용해보았다.  
// ACharacter 사용

float AMyProjectCharacter::TakeDamage(float DamageAmount, FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser)
{
	float ActualDamage = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	
  // 이부분은 기본 데이터타입 사용
	// #include "Engine/DamageEvents.h" 필요
	// 헤더에 있는 UDamageType으로 사용
	//const UDamageType* DT = DamageEvent.DamageTypeClass->GetDefaultObject<UDamageType>();
	
	//if (DT && DT->bCausedByWorld)
	//{
	//	// 낙사, 트랩...

	//	UE_LOG(LogTemp, Warning, TEXT("ByWorld Damage Received"));
	//}

	//if (EventInstigator)
	//{
	//	UE_LOG(LogTemp, Warning, TEXT("Im Enemy"));
	//}


	// 내가 만든 데미지 타입으로 커스텀
	const UMyFireDamageType* FireDamage = DamageEvent.DamageTypeClass->GetDefaultObject<UMyFireDamageType>();

	if (FireDamage)
	{
    // 커스텀 해준 값들 실제로 사용
		ActualDamage *= (1.f + FireDamage->ArmorPenetration);

		// 화상효과, 이펙트, 사운드 설정 추가 가능

		UE_LOG(LogTemp, Warning, TEXT("Fire Damage Received"));
	}

	// HP -= ActualDamage; 

	return ActualDamage;
}
```