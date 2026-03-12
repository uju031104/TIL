# 싱글톤 패턴(Singleton Pattern)

<br/>

### Meyers' Singleton(C++ 11 이상)   

정적 지역 변수 방식이다.   
C++11 이후, Thread_safe를 보장하기 때문에 추천

```cpp
#include <iostream>
#include <string>

class DatabaseManager {
public:
    // 1. 인스턴스에 접근하는 유일한 메서드
    static DatabaseManager& getInstance() {
        // C++11부터 static 지역 변수 초기화는 thread-safe함이 보장됩니다.
        static DatabaseManager instance; 
        return instance;
    }

    // 2. 복사 생성자와 대입 연산자 제거 (복사 방지)
    DatabaseManager(const DatabaseManager&) = delete;
    DatabaseManager& operator=(const DatabaseManager&) = delete;

    // 예시용 멤버 함수
    void query(const std::string& sql) {
        std::cout << "Executing: " << sql << " on connection: " << connectionID << std::endl;
    }

private:
    // 3. 생성자와 소멸자를 private으로 설정 (외부 생성 방지)
    DatabaseManager() : connectionID("DB_001") {
        std::cout << "Database connection established." << std::endl;
    }
    ~DatabaseManager() {
        std::cout << "Database connection closed." << std::endl;
    }

    std::string connectionID;
};

int main() {
    // DatabaseManager db; // 오류: 생성자가 private임
    
    // getInstance()를 통해서만 접근 가능
    DatabaseManager& db1 = DatabaseManager::getInstance();
    db1.query("SELECT * FROM users");

    DatabaseManager& db2 = DatabaseManager::getInstance();
    db2.query("UPDATE settings SET value=1");

    // db1과 db2는 동일한 주소를 가리킵니다.
    std::cout << "Address 1: " << &db1 << std::endl;
    std::cout << "Address 2: " << &db2 << std::endl;

    return 0;
}
```

<br/>

위 예제에서 &를 붙이는 이유는 3가지다.   

첫번째, 복사(Copy) 방지(핵심적인 이유)
&가 없으면 직접 복사를 하기때문에 유일한 객체가 아니게된다.   

두번째, 메모리 및 성능 호율   
단순히 주소값만 전달하므로 성능 저하가 없다.   

세번째, 상태유지   
어디서 호출하든 동일한 메모리 공간의 데이터를 건드릴 수 있다.   

<br/>

***

<br/>

### 포인터 방식의 싱글톤
포인터 방식의 싱글톤은 객체를 Heap 영역에 저장하고 싶을 때 사용한다.   
```cpp
//위 코드에서 &를 *로 바꿨을때 예시
static DatabaseManager* getInstance() {
    static DatabaseManager instance;
    return &instance; // 주소 반환
}

// 사용 시
DatabaseManager* db = DatabaseManager::getInstance();
db->query("...");
```

<br/>

***

<br/>

### 참조자 사용을 권하는 이유


Null 체크 불필요   
포인터는 nullptr일 가능성이 항상 열려 있다. 사용하는 쪽에서 if (db != nullptr) 같은 체크를 해야 할 수도 있다. 반면, 참조자는 반드시 유효한 객체를 가리켜야 하므로 사용자 입장에서 훨씬 안전하고 편리하다.

소유권 오해 방지   
포인터를 반환하면, API를 잘 모르는 개발자가 "내가 delete를 호출해서 메모리를 해제해야 하나?"라고 오해할 여지가 있다. 참조자는 문법적으로 delete가 불가능하므로 이런 오해를 원천 차단한다.

구문상의 깔끔함   
참조자를 쓰면 일반 객체처럼 . 연산자를 사용할 수 있어 코드가 더 직관적이다.

<br/>

***

<br/>

### 지연 초기화와 조기 초기화(Lazy Initialization and Eager Initialization)

**지연 초기화**   
위의 정적 지연 변수방식이 지연 초기화이다.   

장점: 객체가 실제로 사용되지 않으면 메모리를 차지하지 않는다. 프로그램 시작 속도가 빨라진다.   

단점: 처음 getInstance()를 호출하는 시점에 객체 생성 비용(생성자 로직 등)이 발생하므로, 아주 미세한 지연이 생길 수 있다.   

<br/>

**조기 초기화**  

장점: 실제 로직 중에 객체 생성 비용이 들지 않아 실행 시점의 성능이 예측 가능하다.

단점: 객체가 쓰이지 않더라도 무조건 메모리를 점유한다. 또한, **정적 객체 초기화 순서 문제(Static Initialization Order Fiasco)** 라는 아주 골치 아픈 버그가 생길 수 있다.

<br/>

***

<br/>

### 정적 객체 초기화 순서 문제(Static Initialization Order Fiasco)

Logger 싱글톤과 Database 싱글톤이 각각 다른 파일에 있다.   

Database의 생성자에서 Logger::getInstance()를 호출해 로그를 남기려고 한다.   

그런데 운이 없어서 Database가 Logger보다 먼저 초기화된다면? 아직 생성되지도 않은 Logger 객체에 접근하려다 프로그램이 Crash(충돌)난다.   