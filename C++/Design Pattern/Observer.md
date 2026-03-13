# 옵저버 패턴(Observer Pattern)

<br/>

행동 패턴(Behavioral Patterns)중 하나

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Observer 인터페이스
// - Observer 패턴에서 상태 변화를 알림받는 객체들의 공통 인터페이스
// - Observer들은 이 인터페이스를 구현하여 `update` 메서드를 통해 데이터를 전달받음
class Observer {
public:
    virtual ~Observer() = default;               // 가상 소멸자
    virtual void update(int data) = 0;           // 데이터 업데이트 메서드 (순수 가상 함수)
};

// Subject 클래스 (엑셀 시트 역할)
// - 데이터의 상태 변화를 관리하며, 모든 등록된 Observer들에게 변경 사항을 알림
class ExcelSheet {
private:
    vector<Observer*> observers;                 // Observer들을 저장하는 리스트
    int data;                                    // 현재 데이터 상태

public:
    ExcelSheet() : data(0) {}                    // 생성자: 초기 데이터 값은 0

    // Observer 등록 메서드
    // - 새로운 Observer를 등록하여 변경 사항 알림을 받을 수 있도록 추가
    void attach(Observer* observer) {
        observers.push_back(observer);
    }

    // 데이터 변경 알림 메서드
    // - 등록된 모든 Observer들의 `update` 메서드를 호출하여 데이터 변경 사항을 알림
    void notify() {
        for (Observer* observer : observers) {
            observer->update(data);              // 각 Observer에게 데이터를 전달
        }
    }

    // 데이터 설정 메서드
    // - 데이터를 변경하고 변경 사항을 모든 Observer에게 알림
    void setData(int newData) {
        data = newData;                          // 새로운 데이터로 갱신
        cout << "ExcelSheet: Data updated to " << data << endl;
        notify();                                // Observer들에게 알림
    }
};

// 구체적인 Observer 클래스: BarChart (막대 차트)
// - 데이터를 막대 그래프로 표현
class BarChart : public Observer {
public:
    void update(int data) {                      // 데이터 업데이트 시 호출됨
        cout << "BarChart: Displaying data as vertical bars: ";
        for (int i = 0; i < data; ++i) {
            cout << "|";                         // 데이터 값만큼 막대 출력
        }
        cout << " (" << data << ")" << endl;
    }
};

// 구체적인 Observer 클래스: LineChart (라인 차트)
// - 데이터를 선형 그래프로 표현
class LineChart : public Observer {
public:
    void update(int data) {                      // 데이터 업데이트 시 호출됨
        cout << "LineChart: Plotting data as a line: ";
        for (int i = 0; i < data; ++i) {
            cout << "-";                         // 데이터 값만큼 선 출력
        }
        cout << " (" << data << ")" << endl;
    }
};

// 구체적인 Observer 클래스: PieChart (파이 차트)
// - 데이터를 파이 그래프로 표현
class PieChart : public Observer {
public:
    void update(int data) {                      // 데이터 업데이트 시 호출됨
        cout << "PieChart: Displaying data as a pie chart slice: ";
        cout << "Pie [" << data << "%]" << endl; // 데이터 값 출력 (가정: % 비율로 표현)
    }
};

// 메인 함수
int main() {
    // Subject 생성
    ExcelSheet excelSheet;                       // 데이터를 관리하는 엑셀 시트 객체 생성

    // Observer 객체 생성 (각 차트 객체)
    BarChart* barChart = new BarChart();         // 막대 차트 생성
    LineChart* lineChart = new LineChart();      // 라인 차트 생성
    PieChart* pieChart = new PieChart();         // 파이 차트 생성

    // Observer 등록
    // - 각 차트(Observer)를 엑셀 시트(Subject)에 등록
    excelSheet.attach(barChart);
    excelSheet.attach(lineChart);
    excelSheet.attach(pieChart);

    // 데이터 변경 테스트
    // - 데이터를 변경하면 등록된 모든 Observer들이 알림을 받고 화면에 갱신
    excelSheet.setData(5);                       // 데이터 변경: 5
    excelSheet.setData(10);                      // 데이터 변경: 10

    // 메모리 해제
    // - 동적 할당된 Observer(차트) 객체 삭제
    delete barChart;
    delete lineChart;
    delete pieChart;

    return 0;
}

```