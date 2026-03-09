# 리플렉션 시스템(Reflection System)

<br/>

리플렉션이란 프로그램이 실행 중에 자신의 구조와 상태를 검사하고 수정할 수 있는 능력을 말한다.   
C++의 경우 자체적인 리플렉션 기능이 없기 때문에 언리얼 엔진은 자체적인 리플렉션 시스템을 구축한다.   

<br/>

***

<br/>

### 리플렉션의 필요성

<br/>

>리플렉션은 `UObject`를 위한 `운영체제`와 같다.   
언리얼 엔진 내부에서 동작하는 여러 모듈(가비지 컬렉터, 스크립트 시스템) 등은 모두 `UObject` 기반이다.   
하지만 사용자가 정의한 타입들의 경우 엔진에서 알지 못하므로, 이를 처리할 수 있도록 타입 정보를 공유해야 한다.   
이를 위한 작업이 리플렉션이다.

<br/>

***

<br/>

### UHT 코드 생성기

<br/>

>리플렉션의 핵심은 UHT 코드 생성기다.   
UHT는 C++ 컴파일러가 수행되기 되기 전에 동작한다.   
C++ 코드 내에서 메타 데이터를 얻고,  내부적으로 소스 코드를 생성한다.   
이 동작이 완료된 이후에 C++ 컴파일러가 수행된다.

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