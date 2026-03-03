# 스택 메모리(Stack Memory)

컴퓨터의 메모리 레이아웃은 `스택 메모리`, `힙 메모리`, `데이터 섹션`, `코드 섹션`으로 나뉜다.   
스택 메모리는 함수 호출에 할당될 메모리 (지역변수들이 저장되는 공간)    
스택 메모리는 스택 포인터와 베이스 포인터, 스택 프레임들로 구성 되어있다.



### 스택 프레임(Stack Frame)

>함수가 호출되면 해당 함수가 사용할 메모리 크기만큼 공간이 확보된다.  
해당 함수를 위해 확보된 메모리 공간이 `스택프레임`이다.   
함수가 종료될 때 해당 스택프레임은 다시 반환된다.

### 스택 포인터(Extended Stack Pointer, ESP)

> 현재 스택 프레임의 Top를 가리킨다.   
> push 명령어나 pop 명령어의 피연산자.

### 베이스 포인터(Extende Base Pointer, EBP)

> 현재 스택 프레임의 시작 주소를 가리킨다.

### 소스코드와 어셈블리 코드

```c
// 소스코드

#include <stdio.h>

int add(int a, int b)
{
	return a + b;
}

int main(void)
{
	int res;

	res = add(2, 5);****

	return 0;
}
```

```c
// 어셈블리 코드(예시)
_main:                   # @main
    pushl %ebp           # esp -= 4하고 [esp] = ebp
    movl %esp, %ebp      # ebp = esp
    subl $16, %esp       # esp -= 16 (로컬 변수 공간 확보)
    ...
    call _add            # add() 함수 호출
    ...
    addl $16, %esp       # esp += 16 (스택 정리)
    popl %ebp            # ebp = [esp]하고 esp += 4
    ret

_add:                    # @add
    pushl %ebp           # esp -= 4, [esp] = ebp
    movl %esp, %ebp      # ebp = esp
    subl $36, %esp       # esp -= 36
    ...
    addl $36, %esp       # esp += 36
    popl %ebp            # ebp = [esp]하고 esp += 4
    ret
```

