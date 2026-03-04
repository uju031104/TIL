# 구조체(Structure)

<br/>

### 구조체에서 멤버 함수처럼 쓰는 방법

```c
// Main.c
#define _CRT_SECURE_NO_WARNINGS  // strcpy error
#define STR_MAX 100

#include <stdio.h>
#include <stdlib.h>    // malloc
#include <string.h>    // strcpy
#include <stdbool.h>   // bool

typedef struct s_Pizza
{
	char *brand;
	char *size;
	int price;

	void (*pf)(bool);  // 함수 포인터 선언
}Pizza;

// 실제로 동작 할 함수 생성
void static preference(bool n)
{
	if (n)
	{
		printf("Like");
	}
	else
	{
		printf("Dislike");
	}
}

int main(void)
{
	int num = 0;

	Pizza* p = (Pizza*)malloc(sizeof(Pizza));
	if (p == NULL)
	{
		return 0;
	}
	p->brand = (char*)malloc(sizeof(char) * STR_MAX);
	if (p->brand == NULL)
	{
		return 0;
	}
	p->size = (char*)malloc(sizeof(char) * STR_MAX);
	if (p->size == NULL)
	{
		return 0;
	}

    // 구조체의 함수포인터에 실제 함수 참조
	p->pf = &preference;

	strcpy(p->brand, "domino's pizza");
	strcpy(p->size, "Large");
	p->price = 39800;
	
	printf("brand: %s\nsize: %s\nprice: %d\n", p->brand, p->size, p->price);
	
	while (1)
	{
		printf("If you like it, enter 1. dislike enter 0: ");
		scanf("%d", &num);

		if(num == 1 || num == 0)
		{
			p->pf(num); // 멤버함수처럼 사용
			break;
		}
		else
		{
			printf("enter 1 or 0\n");
		}
	}

	free(p->brand);
	free(p->size);
	p->pf = NULL;
	free(p);

	return 0;
}

```