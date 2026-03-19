# 정렬(Sort)

<br>

정렬이란, 사용자가 정의한 순서대로 데이터를 나열하는 것을 의미한다. 사용자가 정의한 순서는 오름차순, 내림차순, 임의로 정한 조건이다.   

정렬을 하는 이유는 원하는 값을 빨리 찾기 위해서, 정렬이 전제 조건인 알고리즘을 사용하기 위해서이다.   

### 삽입정렬(Insertion Sort)

정렬되지 않은 데이터를 이미 정렬된 부분 배열의 적절한 위치에 차례로 삽입하여 전체 데이터를 정렬하는 알고리즘   

시간복잡도는 O(N^2)이다.   
최선의 경우: 오름차순인 배열 -> O(N)   
최악의 경우: 내림차순인 배열 -> O(N^2)   

따라서 정렬이 거의 완성된 상태의 배열에서 효율이 극대화된다.   

```cpp
// 삽입 정렬을 이용하여 정수 배열을 오름차순으로 정렬하는 예제
#include <iostream>
using namespace std;

int main() {
    int arr[] = {5, 2, 4, 6, 1, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    // 배열의 사이즈를 알 수 있는 옛날방식이다.
    // C++ 11 이상은 std::size(arr)로 간편하게 알 수 있다.
    // 단, #include <iterator> 필요!

    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        // key보다 큰 요소를 한 칸씩 뒤로 이동
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    // 출력결과
    // 1 2 3 4 5 6
}

```

<br/>

***

<br/>

### 병합 정렬(Merge Sort)

정렬되지 않은 데이터를 계속 반으로 나눈 뒤, 작은 단위부터 정렬하며 병합해 나가는 방식의 정렬 알고리즘이다.   
분할 정복(Divide and Conquer)과 재귀 함수(Recursive Function)를 이용한다.   

병합 정렬의 시간 복잡도는 O(NlogN)이다.   

```cpp
#include <iostream>
using namespace std;

void merge(int arr[], int left, int mid, int right) {
    int size = right - left + 1; // 임시 배열의 크기
    int* temp = new int[size];   // C-style 동적 배열 할당

    int i = left;    // 첫 번째 부분 배열(arr[left...mid])의 시작 인덱스
    int j = mid + 1; // 두 번째 부분 배열(arr[mid+1...right])의 시작 인덱스
    int k = 0;       // 임시 배열(temp)의 시작 인덱스

    // 두 부분 배열을 비교하며 임시 배열에 정렬하여 저장
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
        }
    }

    // 첫 번째 부분 배열에 남은 요소가 있다면 임시 배열에 복사
    while (i <= mid) {
        temp[k++] = arr[i++];
    }

    // 두 번째 부분 배열에 남은 요소가 있다면 임시 배열에 복사
    while (j <= right) {
        temp[k++] = arr[j++];
    }

    // 임시 배열(temp)에 정렬된 요소들을 원래 배열(arr)의 해당 위치에 복사
    for (int idx = 0; idx < size; ++idx) {
        arr[left + idx] = temp[idx];
    }

    delete[] temp;
}

// mergeSort 함수는 변경할 필요 없음
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        // (left + right) / 2 는 큰 값에서 오버플로우를 일으킬 수 있음
        int mid = left + (right - left) / 2;

        // 왼쪽 부분 배열 정렬
        mergeSort(arr, left, mid);
        // 오른쪽 부분 배열 정렬
        mergeSort(arr, mid + 1, right);

        // 정렬된 두 부분 배열 병합
        merge(arr, left, mid, right);
    }
}

int main() {
    int arr[] = {9, 3, 1, 5, 13, 12};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "원본 배열: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    mergeSort(arr, 0, n - 1);

    cout << "정렬된 배열: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    // 출력 결과
    // 원본 배열: 9 3 1 5 13 12
    // 정렬된 배열: 1 3 5 9 12 13

    return 0;
}
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


