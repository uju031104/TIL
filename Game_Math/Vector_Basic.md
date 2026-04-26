# Vector

<br/>

2d 좌표   
수학은 우리가 알고있는 기본 x, y   
코딩에서 기본 2d 좌표는 y가 반전이다.(아래로 갈수록 y값이 커짐)   

점은 원점을 기준으로   
벡터는 (0, 0) ~ (2, 2)나 (-2, -2) ~ (0, 0)이나 똑같은 벡터이다. 기준이 없어서 그렇다. 크기랑 방향만 가지고 있음.   

점과 벡터 모두 (x, y)로 표현하는데 의미가 다르다.   

>B - A = v(벡터)   
점 A = (2, 4), 점 B = (5, 1)   
벡터 v = B - A = (5 - 2, 1 - 4) = (3, -3)   

<br/>

***

<br/>

### 벡터의 덧셈   

두 벡터를 더하면 두 이동을 연달아 하는 것   
벡터a + 벡터b = (ax + bx, ay + by)

<br/>

***

<br/>

### 벡터의 뺄셈과 스칼라곱  

뺄셈   
두 점의 차이로 방향 벡터를 구할 때 사용   
벡터a - 벡터b = (ax - bx, ay - by)   

스칼라곱   
방향은 유지, 크기만 변경   
음수 곱하면 방향 반대   

<br/>

***

<br/>

### 벡터의 크기   
벡터의 크기 = 화살표의 길이 = "얼마나 멀리?"   

피타고라스 정리와 같다.   
x방향, y방향으로 직각삼각형을 만들고 빗변의 길이를 구하는것.   
벡터v = (3, 4)  -> (3제곱 + 4제곱)에 루트 = 5   

<br/>

***

<br/>

### 벡터의 정규화(Normalize)   
방향은 유지하고 크기는 1로   
벡터 (3, 4) -(정규화)-> (0.6, 0.8) 크기 1로 만듦   

왜 정규화가 필요한가?    
적이 3칸 떨어져 있든 100칸 떨어져 있든 캐릭터 이동속도는 같아야한다.   
방향 벡터를 정규화하면 거리에 상관없이 순수한 방향 정보만 얻을 수 있고 여기에 속도를 곱하면 일정한 속도로 이동.   

position += direction.normalized() x speed x dt   

위의 식 해석   
거리 = 속력 x 시간   
여기에 방향을 주는것.   

**UE5에서 사용법**
```cpp
FVector MyLoc = GetActorLocation();
FVector TargetLoc = Target->GetActorLocation();

FVector Dir = (TargetLoc - MyLoc).GetSafeNormal(); // 정규화로 방향 정보만 빼오기

FVector NewLoc = MyLoc + Dir * Speed * DeltaTime;
SetActorLocation(NewLoc);
```