#Call by Reference (참조에 의한 호출)

<br/>

```c
// 참조에 의한 전달: x는 원본의 "별명"
void addOneByRef(int& x) {
    x = x + 1;
    cout << "  [함수 내부] x = " << x << endl;
}

int main() {
    // 참조에 의한 전달 -- 원본이 바뀜
    int b = 10;
    cout << "[참조 전달] 호출 전: b = " << b << endl;
    addOneByRef(b);
    cout << "[참조 전달] 호출 후: b = " << b << "  ← 변화 있음!" << endl;

    return 0;
}
```