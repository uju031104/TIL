# UE_LOG

<br/>

### 로그 메세지  

```cpp
UE_LOG(LogTemp, Warning, TEXT("My Log!"));
// LogTemp는 카테고리
// Display는 흰색, Warning은 노란색, Error는 빨간색으로 나온다.
// TEXT는 출력 메세지
```

<br/>

***

<br/>

### 로그 카테고리 만들기    
```cpp
// LogSparta는 만든 카테고리 이름
// Warning이상의 메세지 출력
// All은 나중에 필요하면 모든 Log를 쓸 수 있게 열어두는 것
// 이 부분은 헤더에 정의
DECLARE_LOG_CATEGORY_EXTERN(LogSparta, Warning, All);

// cpp에 구현
DEFINE_LOG_CATEGORY(LogSparta);

보통은 로그만 모아둔 헤더를 따로 만들어서 관리
```