# 포인터 연산자(Pointer Operator)

<br/>

포인터도 배열처럼 연산이 가능하다

>Array[1] == Pointer[1] == *(Array + 1) == *(Pointer + 1);

<br/>

***

<br/>

### 배열의 인덱스와 포인터 연산1

<br/>

```c
// Main.c
#include <stdio.h>

int main(void) 
{
	int Nums[5] = { 0, 1, 2, 3, 4 };
	int* Ptr = Nums;

	printf("%d %d %d\n", Nums[1], Ptr[1], *(Ptr + 1));

	return 0;
}
```

<br/>

***

<br/>

### 배열의 인덱스와 포인터 연산2

<br/>

```c
// Main.c

#include <stdio.h>

int main(void)
{
	int i;
	char Chars[5] = { '0', '1', '2', '3', '4' };
	int Nums[5] = { 0, 1, 2, 3, 4 };
	char* PtrToArrayOfChar = Chars;
	int* PtrToArrayOfInt = Nums;

	for (i = 0; i < 5; ++i)
	{
		printf("Chars[%d]: %p\t%c\n", i, (void*)PtrToArrayOfChar, *PtrToArrayOfChar);
		++PtrToArrayOfChar;
	}

	for (i = 0; i < 5; ++i)
	{
		printf("Nums[%d]: %p\t%d\n", i, (void*)PtrToArrayOfInt, *PtrToArrayOfInt);
		++PtrToArrayOfInt;
	}

	return 0;
}
/*
pointer to char에 1을 더하면 주소도 1 더해진다.
pointer to int에 1을 더하면 주소는 4가 더해진다.
즉, 자료형의 크기만큼 주소도 증가한다.
포인터에 ++연산을 가하면 다음 메모리 주소를 가르키게끔 설계되어 있다.
이는 덧셈 뺄셈 증감 모두 적용.
*/
```
<br/>

***

<br/>


### 포인터 + 정수의 의미

<br/>

>포인터에 정수 n을 더하거나 빼면 (sizeof(자료형) * n) 만큼 주소 이동된다.

<br/>

***

<br/>

### 배열 인덱스의 진짜 의미

>“시작 메모리 주소로부터의 떨어진 거리”   
떨어진 거리 정도를 다른 말로 오프셋(Offset)이라고도 한다.

ex) Array[0]는 “배열의 시작 메모리 주소로부터 0만큼 떨어져 있다.”