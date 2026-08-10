# Motion Matching   

프로젝트에 모션 매칭을 적용시키기 위해서 샘플 프로젝트를 깔아서 ABP를 분석해보았다.   

기존 ABP가 `State Machine으로 애니메이션을 정한다`면, 이 샘플은 `데이터를 만들고 → 후보군을 거르고 → Motion Matching이 포즈를 고르고 → 후처리로 보정한다`는 구조이다.   

**기존 ABP**   
```
Character
   ↓
Speed / Direction
   ↓
State Machine
 ├ Idle
 ├ Walk
 ├ Run
 ├ Jump
 └ Fall
   ↓
BlendSpace
   ↓
Output Pose
```

<br/>

**Game Animation Sample**   
```
Character Movement
        ↓
[Essential Values 계산]
        ↓
[현재 State 판단]
        ↓
[Trajectory 생성]
        ↓
[Chooser]
"지금 어떤 Pose DB를 검색할까?"
        ↓
[Motion Matching]
"그 DB 안에서 어떤 프레임이 제일 적합하지?"
        ↓
[Blend Stack / Steering / Orientation Warping]
        ↓
[Lean / Aim Offset]
        ↓
[Montage Slot]
        ↓
[Offset Root Bone]
        ↓
[Leg IK]
        ↓
Output Pose
```

<br/>

## 1.UpdateEssentialValues   

여기서 캐릭터의 Transform, 이동 속도, 방향, Gameplay State 관련 값들을 캐싱한다.   

```
기존 ABP에서 계산하던 방식

Get Velocity
→ Vector Length XY
→ Speed

Get Acceleration

Get Actor Rotation
Get Velocity Direction
Is Falling
```

위의 내용을 `UpdateEssentialValues`에서 잘 정리해서 업데이트 해준다고 생각하면 된다.   

요약: **ABP에서 쓸 공통 변수 업데이트**

<br/>

## 2. GenerateTrajectory   

  
```
기존 ABP에서의 과정

현재 Speed = 300
현재 Direction = 30도

        ↓

BlendSpace에서

Speed 300
Direction 30
```


하지만 `Trajectory`는 예측이 들어간다.   

```
대략적인 예측 그래프

과거        현재             미래

 -0.3       0        +0.3       +0.6
  ●---------●----------●----------●
             \
              \
               → 예상 이동 방향
```

여기서 플레이어가 왼쪽 버튼을 누른다면?   

```
현재 캐릭터
   ↑

미래 Trajectory
   ↖
  ↖
 ↖
```

이런식으로 예측을 하게 된다.   

이 기능 덕분에 기존 애니메이션과 달리 반응성이 좋고 역동적으로 보이게 된다.   

<br/>

## 3.UpdateStates   

처음 봤을 때 가장 복잡해보였던 부분이다.   

```
MovementState
RotationMode
Stance
IsStarting
IsPivoting
IsMoving
ShouldTurnInPlace
JustLanded
...

엄청 많은 것들이 여기서 만들어진다.
```

여기서 만들어지는 States는 State Machine을 위한게 아니라 대부분 `Chooser`에게 정보를 주기 위한 상태 값이다.   
`UpdateStates`에서 현재 게임 플레이 상태를 `Enum` 등으로 정리하고, 이를 주로 `Motion Matching Chooser`에서 `DB를 필터링`하는데 사용한다.   

예를 들어   
```
MovementState = Moving
Gait = Walk
RotationMode = Strafe
IsPivoting = false
```
이런 값이 있으면 Chooser가
```
PSD_Walk_Strafe
```
이 데이터베이스를 허용한다.   

<br/>

## 4.Chooser   

`Update_MotionMatching`을 보면 `Evaluate Chooser`가 있다. Epic 샘플에서 얘가 `CHT_PoseSearchDatabases`를 평가해서 현재 사용할 `Pose Search Database`를 정한다.   

즉, 간단히 말하면 `Motion Matching`이 재생할 애니메이션을 어디서 찾을 지 알려주는것.   

예를 들어 애니메이션 DB가 아래와 같다고 하자.   
```
Walk
Run
Sprint
Idle
Start
Stop
Pivot
Jump
Fall
Land
TurnInPlace
...
```

만약 현재 상태가   
```
Walk
+
Moving
+
OrientToMovement
```

이면 `Chooser`가    

```
Walk 관련 DB
Moving 관련 DB
```
이 두가지만 `Motion Matching`에게 넘길 수 있다는 것이다.   
즉, `Chooser`가 `Pose Search DB`를 미리 필터링하여 결과를 통제하면서 검색량도 줄이는 구조이다.   

<br/>

## 5.Motion Matching Node   

```
Chooser
      ↓
Pose Search Databases
      ↓
Motion Matching
      ↑
Trajectory
      ↑
Pose History
```

<br/>

`Motion Matching`은 `State Machine`의 대체 방식으로 사용할 수 있는 `query` 기반 `pose selection` 시스템이다.   

쉽게 말해서 `Motion Matching`은 현재 캐릭터 상태와 가장 비슷한 애니메이션 프레임을 검색한다고 보면 된다.   

```
현재 포즈
+
과거 포즈
+
현재 Velocity
+
미래 Trajectory
```

위의 포즈들을 통해 가장 비슷한 프레임을 찾아낸다.   

<br/>

## 6.Pose History   

방금 전까지 캐릭터가 어떤 포즈였는지 저장하는 노드이다.   
`Pose History`가 이전 포즈 데이터를 캐싱하고 `Trajectory`를 가지고 있으며, 이 데이터가 `Motion Matching Query`에 사용된다.   

`Pose Search Schema`에서도 발 같은 특정 `Bone`의 `Position/Velocity`와 `Trajectory` 등에 가중치를 줄 수 있다.   

<br/>

## 7.Orientation Warping / Steering   

예를 들어 `Motion Matching`이 45도 방향의 애니메이션을 골랐는데 실제로는 53도 방향으로 가야한다면 어느정도 절차적으로 회전/보정을 해준다.   

`Motion Matching`과 `Animation Warping`을 함께 사용해 애니메이션 데이터 커버리지 부족을 보완할 수 있다.   

<br/>

## 8.Offset Root Bone   

기본적으로 `Capsule`과 `Character Mesh`가 같이 움직이는데 애니메이션의 `Root Movement`와 `Capsule Movement`가 완전히 일치하지 않을 수 있다.   

`Offset Root Bone`은 `Mesh Root`가 `Capsule`에서 잠깐 벗어나는 것을 허용해서 애니메이션 움직임을 더 자연스럽게 보이게 한다. 샘플에서는 시작/피벗 등에서 `translation offset`을 허용하고, `rotation도 capsule`과 독립적으로 움직일 수 있도록 사용한다.   

-> 샘플 프로젝트의 급정지, 180도 턴, Pivot, Start가 멋지게 나오데에 중요한 역할을 함.   

<br/>

## 9.Leg IK   

기존 ABP에서도 볼 수 있었던 것으로 발을 바닥에 잘 붙여주는 단계이다. `IK foot bone` 위치를 기준으로 발을 고정하는 용도로 사용한다.   

```
Motion Matching
      ↓
Warping
      ↓
Root 보정
      ↓
Leg IK
```