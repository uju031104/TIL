# 함수 포인터(Pointer to Function)

함수도 메모리 어딘가에 존재하므로 메모리 주소를 가진다.   
함수 포인터는 해당 메모리 주소를 저장하는 변수이다.

<br/>

***

<br/>

### 함수 포인터 1

<br/>

```c
// Main.c

#include <stdio.h>

void PrintHello(void);

int main(void)
{
	void (*PtrToFunction)(void);

	PrintHello();

	PtrToFunction = PrintHello;

	PtrToFunction();

	return 0;
}

void PrintHello(void)
{
	printf("Hello, world!\n");

	return;
}
```


<br/>

***

<br/>

### 함수 포인터 2

<br/>

```c
// Main.c

#include <stdio.h>

int Add(int X, int Y);

int main(void)
{
	int (*PtrToFunction)(int, int);

	PtrToFunction = Add;

	printf("1 + 2 = %d\n", Add(1, 2));
	printf("1 + 2 = %d\n", PtrToFunction(1, 2));

	return 0;
}

int Add(int X, int Y)
{
	return X + Y;
}
```

<br/>

***

<br/>

### 콜백 함수(Call-Back Function)

>자신이 사용할 함수가 명시적으로 호출되지않고 함수 포인터에 의해서 호출되는 방식을 '콜백'이라고 부른다.   
그리고 호출되는 함수를 `콜백 함수`라고 부른다.

<br/>

```c
// 계산기 콜백함수 예시

#define _CRT_SECURE_NO_WARNINGS

#include <stdio.h>
#include <limits.h>

int Add(int A, int B);

int Sub(int A, int B);

int Mul(int A, int B);

int Div(int A, int B);

void PrintResult(int A, int B, int (*PtrToFunc)(int, int));

int main(void)
{
	char Operator;
	int A, B;
	int Loop = 1;

	while (Loop)
	{
		scanf("%d%c%d", &A, &Operator, &B);
		switch (Operator)
		{
		case '+':
			PrintResult(A, B, Add);
			break;

		case '-':
			PrintResult(A, B, Sub);
			break;

		case '*':
			PrintResult(A, B, Mul);
			break;

		case '/':
			PrintResult(A, B, Div);
			break;

		default:
			printf("wrong operator.\n");
			Loop = 0;
			break;
		}
	}

	return 0;
}

int Add(int A, int B)
{
	return A + B;
}

int Sub(int A, int B)
{
	return A - B;
}

int Mul(int A, int B)
{
	return A * B;
}

int Div(int A, int B)
{
	if (0 == B) { return INT_MAX; }
	return A / B;
}

void PrintResult(int A, int B, int (*PtrToFunc)(int, int))
{
	printf("Result: %d\n", PtrToFunc(A, B));

	return;
}

```