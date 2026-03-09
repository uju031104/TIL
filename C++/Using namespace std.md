# using namespace std

<br/>

```c
// main.cpp
#include <iostream>
//using namespace std;

int main()
{
	std::cout << "Hello, World!" << std::endl;
	return 0;
}
```
<br/>

***

<br/>

### using namespace std

>코딩 테스트에서의 실수를 최소화 하기 위해서 안쓰는 버릇을 들여보자.  

<br/>

***

<br/>

### std::<... >
```c
#include <iostream>
std::cout
std::cin
std::endl

#include <string>
std::string
std::toupper
std::tolower

#include <vector>
std::vector

#include <memory>
std::unique_ptr
std::shared_ptr
std::weak_ptr
```