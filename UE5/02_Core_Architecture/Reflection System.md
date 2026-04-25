# 리플렉션 시스템(Reflection System)

<br/>

리플렉션이란 프로그램이 실행 중에 자신의 구조와 상태를 검사하고 수정할 수 있는 능력을 말한다.   
C++의 경우 자체적인 리플렉션 기능이 없기 때문에 언리얼 엔진은 자체적인 리플렉션 시스템을 구축한다.   

<br/>

***

<br/>

### 리플렉션의 필요성

<br/>

리플렉션은 `UObject`를 위한 `운영체제`와 같다. 언리얼 엔진 내부에서 동작하는 여러 모듈(가비지 컬렉터, 스크립트 시스템) 등은 모두 `UObject` 기반이다.   
하지만 사용자가 정의한 타입들의 경우 엔진에서 알지 못하므로, 이를 처리할 수 있도록 타입 정보를 공유해야 한다. 이를 위한 작업이 리플렉션이다.

<br/>

***

<br/>

### UHT 코드 생성기

<br/>

리플렉션의 핵심은 UHT 코드 생성기다. UHT는 C++ 컴파일러가 수행되기 되기 전에 동작한다.   
C++ 코드 내에서 메타 데이터를 얻고,  내부적으로 소스 코드를 생성한다. 이 동작이 완료된 이후에 C++ 컴파일러가 수행된다.

<br/>

<table border = "2">
    <tr align = "center">
        <td>매크로</td>
        <td>리플렉션에서의 목적</td>
        <td>일반적인 위치</td>
    </tr>
    <tr align = "center">
        <td>UCLASS()</td>
        <td>C++ 클래스를 UObject 기반의 리플렉션 시스템에 등록</td>
        <td>클래스 정의 앞</td>
    </tr>
    <tr align = "center">
        <td>UPROPERTY()</td>
        <td>멤버 변수를 리플렉션 시스템에 노출</td>
        <td>멤버 변수 선언 앞</td>
    </tr>
    <tr align = "center">
        <td>UFUNCTION()</td>
        <td>멤버 함수를 리플렉션 시스템에 노출</td>
        <td>멤버 함수 선언 앞</td>
    </tr>
    <tr align = "center">
        <td>USTRUCT()</td>
        <td>C++ 구조체를 리플렉션 시스템에 등록</td>
        <td>구조체 정의 앞</td>
    </tr>
    <tr align = "center">
        <td>GENERATED_BODY()</td>
        <td>UHT가 생성하는 리플렉션 및 엔진 지원 코드를 위한 삽입 지점</td>
        <td>클래스/구조체 본문 첫 줄</td>
    </tr>
</table>

<br/>

***

<br/>

### Class 리플렉션   

```cpp
#include "Item.generated.h"
// 위에서 오류의 원인이었던 헤더파일인데 이 파일이 리플렉션 시스템을 지원하는 헤더파일이다.
UCLASS()
// 클래스를 리플렉션 시스템을 등록해주는 기능을 한다.
GENERATED_BODY()
// 리플렉션 데이터를 자동으로 생성하기 위해서 엔진이 사용하는 매크로
```

UCLASS()은 인자들이 있다.
UCLASS(Blueprintable, BlueprintType)는 인자에 아무것도 안 쓴 상태(UCLASS())랑 같다.

Blueprintable은 상속이 가능하다는 뜻인데 NotBlueprintable처럼 상속을 막을수도 있다.   

BlueprintType은 블루프린트에서 해당 클래스를 상속받거나 변수로 선언하거나 참조할 수 있게 한다.   

UCLASS(BlueprintType)   
이렇게만 하면 상속은 불가능해서 헷갈릴 수 있다. 명시적으로 써주는게 좋다.   

<br/>

***

<br/>

### 변수 리플렉션   

```cpp
UPROPERTY()
USceneComponent* SceneRoot;
// 이런식으로 변수 위에 적으면 해당 변수가 리플렉션 시스템에 등록됨 
```

클래스와 다르게 변수는 디폴트 인자값이 없어서 따로 설정해줘야 한다.

```cpp
UPROPERTY(값 수정 유무, 블루프린트 get/set 유무, 카테고리 설정)
```

값 수정   
`VisibleAnywhere`: 둘 다 수정 불가   
`EditAnywhere`: 클래스 디폴트, 인스턴스 수정 가능   
`EditInstanceOnly`: 인스턴스만 수정 가능   
`EditDefaultsOnly`: 클래스 디폴트만 수정가능   

블루프린트   
`BlueprintReadOnly`: Get()만 가능   
`BlueprintReadWrite`: Get(), Set() 가능   

카테고리   
`Category="Item|Properties"`  
-> Item 하위 Properties에 넣겠다.

<br/>

***

<br/>

### VisibleAnywhere 이해하기  

VisibleAnywhere를 써도 수정 가능한 상황이 많이 나와서 찾아봤다.   

컴포넌트, 서브객체인 경우 이런 상황이 나온다.   
컴포넌트의 경우 컴포넌트 자체는 고정하고 세부 값만 건드리라는 뜻이다.   
즉, EditAnywhere로 바꾸면 컴포넌트 자체를 바꾸거나 비워버릴 수 있다는 것   

변수(메모리 주소) 자체를 수정할 수 있으면 Edit, 없으면 Visible 이란 뜻이다.   

<br/>

***

<br/>

### 함수 리플렉션   

```cpp
UFUNCTION(블루프린트 get/set 유무, 카테고리 설정)
```
함수도 인자를 적어줘야 한다.

`BlueprintCallable`: 블루프린트에서 호출 가능   
`BlueprintPure`: 블루프린트에서 값만 반환받는 함수로 호출   
`BlueprintImplementableEvent`: 구현을 C++이 아닌 블루프린트에서 했는데 C++에서도 호출 가능하게 한다   

