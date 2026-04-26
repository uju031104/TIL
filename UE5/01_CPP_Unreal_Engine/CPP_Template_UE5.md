# CPP_Template_UE5

<br/>  

### TSubclassOf   

포인터라기 보다 클래스를 참조하기 위한 템플릿 데이터 구조   

`TSubclassOf`: 하드 레퍼런스   
클래스가 항상 메모리에 로드 된 상태에서 바로 접근   
`TSoftClassPtr`: 소프트 레퍼런스   
클래스의 경로만 유지하고 필요한 상황에 메모리에 로드 

```cpp
// TSubclassOf는 어떤 클래스 타입을 등록할건지 설정해줄 수 있다. UClass는 불가능(모든 클래스 다보여줘서 디자이너가 실수 할 가능성이 높음)
	UPROPERTY(EditAnywhere, Category = "Class")
	UClass* MyClass;
	UPROPERTY(EditAnywhere, Category = "Class")
	TSubclassOf<UClass> MyClass2;
```

<br/>

***

<br/>

### TObjectPtr

<br/>

언리얼엔진에서는 클래스의 멤버 변수에는 `TObjectPtr`을 쓰고 함수의 매개변수, 지역변수에는 기존 포인터를 쓰는 게 가이드라인이라고 한다.   

```cpp
	// TObjectPtr 사용할때 참조 사용을 권장
	for (TObjectPtr<USceneComponent>& Component : Components)
	{

	}

	for (USceneComponent* Component : Components)
	{

	}
```

<br/>

***

<br/>

### TArray

<br/>

```cpp
	TArray<int32> IntArray;

	// 공간을 하나 만들어서 거기 두고 넣기. 명시적이라서 오류의 가능성이 없음.
	IntArray.Add(5);
	// 복사 없이 바로 넣음(성능이 조금 더 좋음) 눈에 보이지 않는 변환이 있을 수 있어서 아주 조금 불안정함
	IntArray.Emplace(6);
	// UE5는 성능 쥐어짜는 경우 제외하면 Add를 권장

	// 성능 안좋아서 무조건 TSet을 쓰면 된다.
	IntArray.AddUnique(6);

	IntArray.Insert(600, 2);

	//IntArray.Num(); 그냥 이렇게 쓰면 오류남. for문 if문 사용해야함
	for (int32 i = 0; i < IntArray.Num(); ++i)
	{

	}

	if (IntArray.Num())
	{

	}

	// 함수객체
	IntArray.Sort([](int32 A, int32 B) { return A > B; });

	TArray<int32> ReturnIntArray = IntArray.FilterByPredicate([](const int32 FindValue) { return FindValue < 9; });

	int32 index = IntArray.Find(5);
	bool b = IntArray.Contains(5);

	IntArray.Remove(10); // 모든 10값을 삭제
	IntArray.RemoveSingle(10);  // 10값 중 가장 첫 번째꺼

	if (IntArray.IsValidIndex(2)) // 먼저 2번째 인덱스에 값이 있는지 확인
	{
		IntArray.RemoveAt(2);  // 2번째 인덱스 값 삭제
		IntArray.RemoveAt(2, EAllowShrinking::No);  
		// 두번째 인자는 인덱스값 삭제 했을 때 제일 뒤에 빈 공간을 없앨것이냐 그대로 둘 것이냐를 정함. 기븐온 Yes고 삭제를 함
	}
	
	// []안에 지역변수 (=, &) 클래스 내부 멤버 변수 (this)
	IntArray.RemoveAll([](int32 Value) { return Value % 3 == 0; });

	IntArray.Empty(); // 다 지우기
```

<br/>

**TArray 사용해보기**

```cpp
// 수업때 코드 짠건데 Arr.Num()을 사용안했다.
// 그리고 변수 이름도 RandonValue 이런식으로 하는게 좋다.
	TArray<int32> Arr;
	int32 count = 0;
	while (count < 30)
	{
		int32 Num = FMath::RandRange(0, 1000);
		if (Num <= 100)
		{
			Arr.Add(Num);
			++count;
		}
	}
	Arr.RemoveAll([](int32 Value) { return Value < 50; });
	Arr.Sort([](int32 A, int32 B) { return A < B; });
```
<br/>

***

<br/>

### TSet

<br/>

```cpp
  TSet<int32> IntArraySet;

IntArraySet.Add(100);

if (IntArraySet.Contains(100))
{

}

// TSet의 Find는 포인터를 반환한다.
int32* FoundPtr = IntArraySet.Find(20);

// TSet 순회하는 방법
for (TSet<int32>::TIterator It = IntArraySet.CreateIterator(); It; ++It)
{
	if (*It < 60)
	{
		It.RemoveCurrent();
	}
}

// Const로 받고 싶을때
for (TSet<int32>::TConstIterator It = IntArraySet.CreateConstIterator(); It; ++It)
{

}
// 제일 편한건 auto로 받는거지만 확실한거 아니면 안쓰는게 좋긴하다.(권장하지 않음)


TSet<int32> SetA = { 1, 2, 3 };
TSet<int32> SetB = { 3, 4, 5 };

TSet<int32> SetC = SetA.Union(SetB); // 합집합
TSet<int32> SetC = SetA.Intersect(SetB); // 교집합

SetC.Compact(); // 삭제해서 비어버린 부분을 다 뒤로 옮김
SetC.Shrink();  // 비어버린 부분 싹 다 정리

TArray<int32> MyArray = SetC.Array(); // 배열로 자동으로 넘어간다.

// Set 사용하는 곳 : 무기를 휘두룰때 그 범위에 같은 몬스터가 여러번 들어오면 Set을 이용해서 중복된 값을 없애면 몬스터에게 딱 한번만 데미지가 들어가게 된다.
```

<br/>

***

<br/>

### TMap

<br/>

```cpp
// TMap

TMap<int32, FString> ItemMap;

ItemMap.Add(101, TEXT("Sword"));
ItemMap.Add(102, TEXT("Shield"));

ItemMap.Emplace(103, TEXT("Potion"));

ItemMap.Add(101, TEXT("Hello")); // 덮어씌워짐

if (ItemMap.Contains(101))
{
	FString* FoundItem = ItemMap.Find(101);
}

FString& ItemRef = ItemMap.FindOrAdd(104); // 찾지 못하면 만들어라
ItemRef = TEXT("Bow");

// 위험한 코드(바로 접근)
FString Name = ItemMap[105];
// 이렇게 해줘야함 - 기존 C++과 달리 없으면 만들지 않고 Crash 나기 때문
if (ItemMap.Contains(105))
{
	FString Name = ItemMap[105];
}

for (const TPair<int32, FString>& i : ItemMap)
{

}

// 지우면서 갈 땐 무조건 Iterator를 사용하자(정말 혹시 모를 오류 하나라도 제거) 그냥 순회하면 위험할 수도 있다.
for (TMap<int32, FString>::TIterator It = ItemMap.CreateIterator(); It; ++It)
{
	if (It.Key() == 103)
	{
		It.RemoveCurrent();
	}
}

// 삭제
ItemMap.Remove(102);
// 빈공간 뒤로 몰고 삭제하기!
ItemMap.Compact();
ItemMap.Shrink();
```