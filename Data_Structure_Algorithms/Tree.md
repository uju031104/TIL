# 트리(Tree)

트리(Tree) 자료구조는 데이터를 계층적인 방식으로 조직하고 관리하는 비선형 자료구조다.   
이는 **배열**, **스택**, **큐**와 같은 선형 자료구조가 데이터를 순차적으로 저장하는 것과는 달리, 
트리는 각 데이터(노드) 간에 `부모-자식` 관계를 기반으로 한 계층 구조를 형성한다.

트리는 일반적으로 **루트(root)** 노드에서 시작하여, **간선(vertex)**를 통해
자식 노드로 확장되는 구조이며, 마치 나무를 거꾸로 뒤집은 형태와 유사하다.

<br/>

***

<br/>

### 이진 트리(Binary Tree)

자식 노드가 최대 두개인 트리

**배열로 구현**

```cpp
// - 인덱스 1부터 시작
// - 왼쪽 자식: index * 2
// - 오른쪽 자식: index * 2 + 1

#include <iostream>
using namespace std;

int main() {
    const int SIZE = 16;
    int tree[SIZE] = {0};

    // 트리 구성
    tree[1] = 1;  // 루트
    tree[2] = 2;
    tree[3] = 3;
    tree[4] = 4;
    tree[5] = 5;
    tree[6] = 6;
    tree[7] = 7;

    // 부모-자식 관계 출력
    for (int i = 1; i < SIZE; ++i) {
        if (tree[i] != 0) {
            int left = i * 2;
            int right = i * 2 + 1;

            cout << "부모 노드 (" << tree[i] << "): ";
            if (left < SIZE && tree[left] != 0)
                cout << "왼쪽 자식 -> " << tree[left] << " ";
            if (right < SIZE && tree[right] != 0)
                cout << "오른쪽 자식 -> " << tree[right];
            cout << endl;
        }
    }

    return 0;
}

/*
출력결과:
부모 노드 (1): 왼쪽 자식 -> 2 오른쪽 자식 -> 3
부모 노드 (2): 왼쪽 자식 -> 4 오른쪽 자식 -> 5
부모 노드 (3): 왼쪽 자식 -> 6 오른쪽 자식 -> 7
부모 노드 (4): 
부모 노드 (5): 
부모 노드 (6): 
부모 노드 (7): 
*/
```

<br/>

**인접리스트로 구현**
```cpp
// 동작: 각 노드는 자식 노드를 리스트로 저장하며, 출력 시 부모 -> 자식 관계를 보여줌

#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n = 9; // 노드 개수 (0부터 8까지 총 9개 노드)
    vector<vector<int>> tree(n);

    // 트리 간선 정보 추가 (0을 루트로 가정)
    tree[0].push_back(1);
    tree[0].push_back(2);
    tree[1].push_back(3);
    tree[1].push_back(4);
    tree[2].push_back(5);
    tree[2].push_back(6);
    tree[3].push_back(7);
    tree[4].push_back(8);

    // 트리 출력
    for (int i = 0; i < n; ++i) {
        cout << i << " -> ";
        for (int child : tree[i]) {
            cout << child << " ";
        }
        cout << endl;
    }

    return 0;
}

/*
출력결과
0 -> 1 2 
1 -> 3 4 
2 -> 5 6 
3 -> 7 
4 -> 8 
5 -> 
6 -> 
7 -> 
8 -> 
*/
```

<br/>

***

<br/>

### 순회

<br/>

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <iterator>

// 전위순회: 부모 노드 -> 왼쪽 자식 노드 -> 오른쪽 자식 노드
std::string preorder(const std::vector<int> &nodes, int idx)
{
    if (idx < nodes.size())
    {
        std::string ret = std::to_string(nodes[idx]) + " ";
        ret += preorder(nodes, idx * 2 + 1);
        ret += preorder(nodes, idx * 2 + 2);
        return ret;
    }
    return "";
}

// 중위순회: 왼쪽 자식 노드 -> 부모 노드 -> 오른쪽 자식 노드
std::string inorder(const std::vector<int> &nodes, int idx)
{
    if (idx < nodes.size())
    {
        std::string ret = inorder(nodes, idx * 2 + 1);
        ret += std::to_string(nodes[idx]) + " ";
        ret += inorder(nodes, idx * 2 + 2);
        return ret;
    }
    return "";
}

// 후위순회: 왼쪽 자식 노드 -> 오른쪽 자식 노드 -> 부모 노드
std::string postorder(const std::vector<int> &nodes, int idx)
{
    if (idx < nodes.size())
    {
        std::string ret = postorder(nodes, idx * 2 + 1);
        ret += postorder(nodes, idx * 2 + 2);
        ret += std::to_string(nodes[idx]) + " ";
        return ret;
    }
    return "";
}

std::vector<std::string> solution(const std::vector<int> &nodes)
{
    std::vector<std::string> result;
    std::string pre = preorder(nodes, 0);
    std::string in = inorder(nodes, 0);
    std::string post = postorder(nodes, 0);

    pre.pop_back();
    in.pop_back();
    post.pop_back();

    result.push_back(pre);
    result.push_back(in);
    result.push_back(post);

    return result;
}

void print(std::vector<std::string> vec)
{
    copy(vec.begin(), vec.end(), std::ostream_iterator<std::string>(std::cout, "\n"));
    std::cout << std::endl;
}

int main()
{
    print(solution({1, 2, 3, 4, 5, 6, 7}));
    return 0;
}
```

<br/>

***

<br/>

### 이진 탐색 트리(Binary Search Tree)

이진 탐색 트리(Binary Search Tree)는 원하는 값을 더 빠르게 찾기 위해 특정 규칙을 추가한 이진 트리다.   

각 노드에 대해 왼쪽 서브 트리에는 더 작은 값, 오른쪽 서브 트리에는 더 큰 값을 저장하는 구조다.

