# 정렬(Sort)

<br>

정렬이란, 사용자가 정의한 순서대로 데이터를 나열하는 것을 의미한다. 사용자가 정의한 순서는 오름차순, 내림차순, 임의로 정한 조건이다.   

정렬을 하는 이유는 원하는 값을 빨리 찾기 위해서, 정렬이 전제 조건인 알고리즘을 사용하기 위해서이다.   

정렬 특징들 간단히 정리   

버블   
인접한 애 비교하고 스왑함   
최대값/최소값을 맨 뒤로가게 하는 원리   
비교, 스왑 횟수가 1씩 줄어듦(최대길이 - 1 씩)   
비교횟수 == 교환횟수 O(n^2)   
최선 : O(n^2)   

선택   
시작 시 맨 앞 값을 최대값/최소값으로 설정   
뒤로 쭉 비교해서 조건에 맞으면 스왑함   
비교횟수O(n^2) > 교환횟수O(n)   
최선 : O(n^2)   

삽입   
시작 시 맨 앞 값은 정렬된 값으로 취급   
정렬 안된 첫 값을 key로 두고 정렬된 곳과 비교해서 적절한 위치에 삽입   
비교횟수 == 교환횟수 O(n^2)   
최선 : O(n) -> C++ sort()에서 크기가 16 이하이면 삽입정렬을 실행함   

c++ sort()는 퀵 정렬 기반에 안전장치가 달린 Introsort 하이브리드 알고리즘이다   
-> 안전장치 : 16개 이하면 삽입 정렬, 최악의 경우가 감지되면 힙 정렬   

<br/>

버블, 선택, 삽입 정렬 안보고 직접 구현해봄   

```cpp
// 버블 정렬
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> bubble_array = {5, 4 ,1, 3, 2};

    for(int i = 0; i < bubble_array.size() - 1; ++i)
    {
        for(int j = 0; j < bubble_array.size() - 1 - i; ++j)
        {
            if(bubble_array[j] > bubble_array[j + 1])
            {
                swap(bubble_array[j], bubble_array[j + 1]);
            }
        }
    }

    for(const int& num : bubble_array)
    {
        cout << num << " ";
    }

    return 0;
}
```

<br/>

```cpp
// 선택 정렬
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> selection_array = {5, 4, 1, 3, 2};
    int min;

    for (int i = 0; i < selection_array.size() - 1; ++i)
    {
        min = i;
        for (int j = i; j < selection_array.size(); ++j)
        {
            if (selection_array[min] > selection_array[j])
            {
                min = j;
            }
        }
        if (min != i)
        {
            swap(selection_array[i], selection_array[min]);
        }
    }

    for (const int &num : selection_array)
    {
        cout << num << " ";
    }

    return 0;
}
```

<br/>

```cpp
// 삽입 정렬
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> insertion_array = {5, 4, 1, 3, 2};

    for (int i = 1; i < insertion_array.size(); ++i)
    {
        int key = insertion_array[i];
        int j = i - 1;
        while (j >= 0 && insertion_array[j] > key)
        {
            insertion_array[j + 1] = insertion_array[j];
            --j;
        }
        insertion_array[j + 1] = key;
    }

    for (const int &num : insertion_array)
    {
        cout << num << " ";
    }

    return 0;
}
```

<br/>

**병합정렬 문제 풀기1**

단순하기만 할 줄 알았는데 배열을 딱 2개만 써야해서 시간이 좀 걸렸다.   
큰 값을 뒤부터 채워넣으면 된다.   
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        // nums1 index: 0 ... m - 1
        // nums2 indes: m ... m + n - 1
        int nums1_index = m - 1;
        int nums2_index = n - 1;

        for(int i = m + n - 1; i >= 0; --i)
        {
            if(nums1_index == -1)
            {
                nums1[i] = nums2[nums2_index--];
                continue;
            }
            
            if(nums2_index == -1)
            {
                nums1[i] = nums1[nums1_index--];
                continue;
            }

            if(nums1[nums1_index] >= nums2[nums2_index])
            {
                nums1[i] = nums1[nums1_index--];
            }
            else
            {
                nums1[i] = nums2[nums2_index--];
            }      
        }
    }
};
```

<br/>

**병합정렬 문제 풀기2**   

굉장히 복잡하다. 직접 구현은 못하였고 코드를 보며 병합 정렬의 방식을 이해하였다.   
정렬된 두 배열을 합치면서 새 배열을 만들어내기 때문에 정렬에는 O(n)만 걸린다.(각각의 최솟값만 비교하면 됨)      
분할은 계속 반으로 쪼개기 때문에 O(logn)이다.   


```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }
    
    void mergeSort(vector<int>& nums, int left, int right) {
        if (left >= right) return;

        int mid = left + (right - left) / 2;

        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);

        merge(nums, left, mid, right);
    }

    void merge(vector<int>& nums, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        vector<int> L(n1), R(n2);

        for (int i = 0; i < n1; i++) 
        {
            L[i] = nums[left + i];
        }
        for (int j = 0; j < n2; j++) 
        {
            R[j] = nums[mid + 1 + j];
        }

        int i = 0, j = 0, k = left;

        while (i < n1 && j < n2) 
        {
            if (L[i] <= R[j]) 
            {
                nums[k++] = L[i++];
            } 
            else 
            {
                nums[k++] = R[j++];
            }
        }

        while (i < n1) 
        {
            nums[k++] = L[i++];
        }
        while (j < n2)
        {
            nums[k++] = R[j++];
        } 
    }
};
```

<br/>

***

<br/>

### 계수 정렬(Counting Sort)

계수 정렬은 데이터값 자체를 인덱스로 사용하는 데이터 의존적인 정렬 방식이다. 각 값의 빈도 수를 세어 그 정보를 기반으로 정렬을 수행한다.   

계수 정렬의 시간복잡도는 O(N+K)이다.   
K는 입력 배열의 최댓값인데 이 배열을 초기화 할때 O(K)이다.   

계수 정렬은 음수값이 있거나, 값의 차이가 너무 큰 경우(값이 500, 10억 이러면 그 사이에 낭비되는 공간이 너무 많음)에는 쓰면 안된다.   

```cpp
// 목적: 양의 정수만으로 이루어진 배열을 계수 정렬로 정렬한다.
// 동작: 배열에서 최댓값을 찾아 그 크기만큼 카운트 배열을 만들고, 카운트 정보를 기반으로 정렬된 결과 생성

#include <iostream>
using namespace std;

int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    // 1. 최댓값 찾기
    int max = arr[0];
    for (int i = 1; i < n; ++i)
        if (arr[i] > max) max = arr[i];

    // 2. 카운트 배열 생성 및 초기화
    int* count = new int[max + 1]{};

    // 3. 각 요소 개수 세기
    for (int i = 0; i < n; ++i)
        count[arr[i]]++;

    // 4. 정렬 결과 저장
    int idx = 0;
    for (int i = 0; i <= max; ++i) {
        while (count[i]--) {
            arr[idx++] = i;
        }
    }

    // 5. 출력
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    delete[] count;

    return 0;
}

//
// 출력결과:
// 1 2 2 3 3 4 8
//

```

<br/>

***

<br/>

### 힙 정렬(Heap Sort)

힙 정렬은 힙이라는 자료구조를 사용한 정렬 방법이다. 따라서 힙이라는 자료구조를 먼저 알아야한다.   

**힙이란?**
힙은 조건을 만족하는 이진 트리다.   
보통 최대 힙과 최소 힙으로 구분된다.   

최대 힙은 모든 부모 노드의 값이 자식 노드의 값 보다 크거나 같고, 최소 힙은 반대다.   
최대 힙과 최소 힙은 각각 전체가 정렬된 상태는 아니다.   

힙 정렬의 시간복잡도는 O(NlogN)이다.   
힙 자료구조의 장점은 삽입/삭제시 힙 성질을 유지할 수 있다는 점인데 그래서 삽입/삭제 시간복잡도는 O(logN)이다.   

```cpp
// 최대 힙(Max Heap)을 이용하여 정수 배열을 오름차순 정렬하는 힙 정렬 예제
#include <iostream>
using namespace std;

void heapify(int arr[], int n, int i) {
    int largest = i;         // 루트를 가장 큰 값으로 시작
    int left = 2 * i + 1;    // 왼쪽 자식
    int right = 2 * i + 2;   // 오른쪽 자식

    if (left < n && arr[left] > arr[largest])
        largest = left;

    if (right < n && arr[right] > arr[largest])
        largest = right;

    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);  // 재귀적으로 하위 트리 정리
    }
}

void heapSort(int arr[], int n) {
    // 배열을 힙 구조로 만들기 (Build Heap)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // 힙에서 하나씩 요소를 추출
    for (int i = n - 1; i >= 0; i--) {
        swap(arr[0], arr[i]);        // 루트와 마지막 요소 교환
        heapify(arr, i, 0);          // 줄어든 힙에 대해 다시 heapify
    }
}

int main() {
    int arr[] = {4, 10, 3, 5, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    heapSort(arr, n);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    // 출력결과
    // 1 3 4 5 10
}
```


