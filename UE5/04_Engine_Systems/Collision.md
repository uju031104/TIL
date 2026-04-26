# Collision

<br/>

### 콜리젼 프리셋 종류  

`NoCollision`: 충돌 끄기(하늘 등 상호작용 안할것들)   
`BlockAll`: 모두 막음(보통 벽, 바닥 등)   
`OverlapAll`: 모두 감지함(센서, 트리거 등)   
`BlockAllDynamic`: 움직이는 객체만 막음(플레이어랑 상호작용 하는 문 등)   
`OverlapAllDynamic`: 움직이는 객체만 감지(센서, 트리거 등)   
`Pawn`: Pawn타입 대상으로 충돌 감지 

<br/>

***

<br/>

### 콜리전 커스텀 세팅   

`Collision Enabled(Query and Physics)`: 충돌, 물리적 반응 모두 활성화   
`Query Only`: 충돌(Overlap과 Hit)만 감지   
`Physics Only`: 물리적 반응만 감지   

<br/>

***

<br/>

### 콜리전 프리셋

나만의 콜리전 프리셋을 만들 수 있음      
project setting -> engine -> collision
Object Channels에 하나 만들어주고      
여기서 Preset-New Profile에 추가하고 설정해주면 된다.

<br/>

***

<br/>

### 큐브의 Default Collision   

큐브를 하나 꺼내보면 Block처리 되는데 큐브의 StaticMeshComponent에 있는 Collision이 Default로 되어있음   
이 뜻이 이 메시 자체에 있는 Collision 프리셋을 그대로 따르겠다는 뜻   
메시에 들어가서 콜리전을 직접 수정할 수 있는데 단순/복합이 있음    
심플은 가볍지만 정밀하지 않고 복합은 거의 폴리곤 단위로 콜리전이 있지만 부하가 심함    
여기서 Collision Complexity 들어가면 여러가지가 있는데 그중 Simple And Complex 는 평소엔 심플하게 하다가 충돌이 있을때 컴플렉스로 바꿈