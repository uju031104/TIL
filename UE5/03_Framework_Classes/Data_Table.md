# DataTable

<br/>

### 데이터 테이블   

보통 기획자들이 많이 사용하는데 엑셀이나 JSON 파일로 데이터를 모아서 엔진에 임포트한 후 이 데이터들을 쉽게 사용함   
그 데이터들을 다룰 구조체를 구현해줘야함   

None으로 class하나 만들어주고 구조체를 구현해준다. (cpp파일은 안쓰니 #include 부분을 제외하고 다 지우기)   

```cpp
// 데이터 테이블을 위한 구조체 구현 예시
#pragma once

#include "CoreMinimal.h"
#include "ItemSpawnRow.generated.h"

USTRUCT(BlueprintType)
struct FItemSpawnRow : public FTableRowBase
{
	GENERATED_BODY()

public:
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	FName ItemName;
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	TSubclassOf<AActor> ItemClass;
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	float SpawnChance;

};
```