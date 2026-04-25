# Call by Value(값에 의한 호출)

<br/>

```c
// 값에 의한 전달: x는 원본의 "복사본"
void addOneByValue(int x) {
    x = x + 1;
    cout << "  [함수 내부] x = " << x << endl;
}

int main() {
    // 값에 의한 전달 -- 원본은 그대로
    int a = 10;
    cout << "[값 전달] 호출 전: a = " << a << endl;
    addOneByValue(a);
    cout << "[값 전달] 호출 후: a = " << a << "  ← 변화 없음!" << endl;

    return 0;
}
```