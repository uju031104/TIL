# 데코레이터 패턴(Decorator Pattern)

<br/>

```cpp
#include <iostream>
#include <string>

// 1. Component: 기본 인터페이스
class Beverage {
public:
    virtual std::string getDescription() = 0;
    virtual double cost() = 0;
    virtual ~Beverage() = default;
};

// 2. ConcreteComponent: 실제 알맹이 (기본 음료)
class Espresso : public Beverage {
public:
    std::string getDescription() override { return "Espresso"; }
    double cost() override { return 2.0; }
};

// 3. Decorator: 첨가물들을 위한 추상 클래스
class CondimentDecorator : public Beverage {
protected:
    Beverage* beverage; // 장식할 대상(음료)을 가리키는 포인터
public:
    CondimentDecorator(Beverage* b) : beverage(b) {}
};

// 4. ConcreteDecorator: 실제 첨가물 (기능 확장)
class Mocha : public CondimentDecorator {
public:
    Mocha(Beverage* b) : CondimentDecorator(b) {}
    
    std::string getDescription() override {
        return beverage->getDescription() + ", Mocha";
    }
    double cost() override {
        return beverage->cost() + 0.5; // 기존 가격 + 모카 가격
    }
};

class Whip : public CondimentDecorator {
public:
    Whip(Beverage* b) : CondimentDecorator(b) {}
    
    std::string getDescription() override {
        return beverage->getDescription() + ", Whip";
    }
    double cost() override {
        return beverage->cost() + 0.3;
    }
};

int main() {
    // 1. 순수 에스프레소 주문
    Beverage* b1 = new Espresso();
    std::cout << b1->getDescription() << " $" << b1->cost() << std::endl;

    // 2. 에스프레소 + 모카 + 휘핑크림 (동적 조립)
    Beverage* b2 = new Espresso();
    b2 = new Mocha(b2);
    b2 = new Whip(b2);
    
    std::cout << b2->getDescription() << " $" << b2->cost() << std::endl;

    delete b2; // 실제 구현 시에는 스마트 포인터를 권장합니다.
    return 0;
}
```