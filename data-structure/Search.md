# 탐색

## 이진탐색(Binary Search)

- 정렬된 리스트에서 검색 범위를 줄여 나가면서 검색 값을 찾는 알고리즘
- 이진 탐색은 정렬된 리스트에만 사용할 수 있다는 단점이 있지만, 검색이 반복될 때마다 검색 범위가 절반으로 줄기 때문에 속도가 빠름

### 알고리즘

→ 어떤 숫자를 검색

1. 배열의 중간 값을 가져옴
2. 중간 값과 검색 값을 비교
    1. 중간 값이 검색 값과 같다면 종료 (mid = key)
    2. 중간 값보다 검색 값이 크다면 중간값 기준 배열의 오른쪽 구간을 대상으로 탐색 (mid < key)
    3. 중간 값보다 검색 값이 작다면 중간값 기준 배열의 왼쪽 구간을 대상으로 탐색 (mid > key)
3. 값을 찾거나 간격이 비어있을 때까지 반복

끝

### 시간 복잡도

|  | Best | Average | Worst |
| --- | --- | --- | --- |
| Search | O(1) | Θ(log n) | O(log n) |

n = 데이터 수

## 완전 탐색(Exhaustive Search)

- 알고리즘에서 사용되는 기법 중 하나로 모든 가능한 경우의 수를 탐색하여 최적의 결과를 찾는 방법
- 모든 가능성을 고려하기 때문에 항상 최적의 해를 찾을 수 있지만 경우의 수가 매우 많은 경우 시간과 메모리의 부담이 커짐. 그렇기 때문에 문제의 특성에 따라 다른 탐색 기법을 사용하는 것이 좋음

### 완전 탐색의 종류

브루트 포스트, 비트마스크, 백트래킹, 순열 탐색, 재귀함수, 비선형 구조 탐색

| 알고리즘 종류 | 설명 | 장점 | 단점 |
| --- | --- | --- | --- |
| 브루트 포스 | 모든 경우의 수를 탐색하면서 원하는 결과를 얻는 알고리즘 | 가능한 모든 경우를 다 검사하기 때문에 가장 최적의 결과를 얻을 수 있음 | 경우의 수가 많을 경우 시간이 오래 걸림 |
| 비트마스크 | 모든 경우의 수를 이진수로 표현하고 비트 연산을 통ㅇ해 원하는 결과를 빠르게 얻는 알고리즘 | 이진수 연산을 이용하여 계산 속도가 빠름 | 경우의 수가 많아질수록 메모리 사용량이 증가 |
| 백트래킹 | 결과를 얻기 위해 진행하는 도중에 막히게되면 그 지점으로 다시 돌아가서 다른 경로를 탐색하는 방식. 결국 모든 가능한 경우의 수를 탐색하여 해결책을 찾음 | 경우의 수를 줄이면서도 모든 경우를 탐색할 수 있음 | 재귀 함수를 이용하기 때문에 스택 오버플로우가 발생할 가능성 있음 |
| 순열 | 순열을 이용하여 모든 경우의 수를 탐색하는 방법. 순열은 서로 다른 n개 중에서 r개를 선택하여 나열하는 방법을 의미 | 경우의 수가 적을 때 사용하면 유용 | 경우의 수가 많을 경우 시간이 오래 걸림 |
| 재귀함수 | 자기 자신을 호출하여 모든 가능한 경우의 수를 체크하면서 최적의 해답을 얻는 방식 | 코드가 간결하며, 이해하기 쉬움 | 스택 오버플로우가 발생할 가능성이 있음 |
| DFS/BFS | 깊이 우선 탐색 : 루트 노드에서 시작하여 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법                         너비 우선 탐색 : 루트 노드에서 시작하여 인접한 노드를 먼저 탐색하는 방법을 의미 | 깊이 우선 탐색 : 최선의 경우, 가장 빠른 알고리즘. 운 좋게 항상 해에 도달하는 올바를 경로를 선택한다면 최소 실행시간에 해를 찾음                             너비 우선 탐색 : 최적해를 찾음을 보장 | 깊이 우선 탐색 : 찾은 해가 최적이 아닐 가능성이 있다. 최악의 경우 가능한 모든 경로를 탐험하고 해를 찾으므로 가장 오랜 시간이 걸림                        너비 우선 탐색 : 최소 실행시간보다는 오래 걸린다는 것이 확실 |

### 브루트 포스

→ 진짜 그냥 다 검사하는거 ex) for문으로 배열 다 검사하는 것

### 비트 마스크

- 비트 마스크를 사용하면 하나의 변수에 여러 개의 상태 정보를 저장할 수 있으며 이를 통해 복잡한 조건문을 간단하게 처리가능. 이 방법은 비트 연산을 사용하기 때문에 빠르게 계산할 수 있어서, 경우의 수가 많은 경우에 유용.

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F16be3d38-3696-44b2-92eb-95c042c77251%2FUntitled.png?table=block&id=4bda50e8-4d27-48da-8d66-4aee1144cbf4&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1060&userId=&cache=v2)

### 순열

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fd5039206-e565-4eac-af6a-e5c8d1ec379a%2FUntitled.png?table=block&id=347cf50d-d6be-4dc3-87fb-13b6fbc76954&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1060&userId=&cache=v2)

- Swap 이용
- Visited 배열 이용

### 재귀함수

- 재귀함수는 모든 경우의 수를 다 탐색하지 않고도 원하는 결과를 얻을 수 있는 경우도 있음. 따라서 재귀함수는 미완적탐색의 일종이라고는 할 수 있지만, 항상 미완전탐색이라고는 할 수는 없음.

## DFS, BFS 보충
![1.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F2aba60dd-2eb4-4cab-8f7f-339137c021ea%2F1.png?table=block&id=29aada26-88f7-4fb9-a996-aa9f02084ff1&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=860&userId=&cache=v2)

![2.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F48cfadb2-62fd-492b-9306-0d0f319289f6%2F2.png?table=block&id=bb82118e-1436-4007-858a-a1c686ff5b7b&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1470&userId=&cache=v2)

![3.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fe9001148-ca8b-4b88-b5c8-6fd89796a590%2F3.png?table=block&id=7b9132ba-2eb0-45d0-9f66-cdef8769565e&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=670&userId=&cache=v2)

![4.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fb775c6b1-8d05-42f5-9713-1f810671729d%2F4.png?table=block&id=2c3cd990-0c94-4b6d-8dab-ad13378102f2&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=860&userId=&cache=v2)

![5.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F7c8f6553-4fa6-4baf-9f78-9aec45eb4744%2F5.png?table=block&id=5a6fee09-b554-40f0-8084-5064d90c60f9&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=670&userId=&cache=v2)

![6.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fae8e95d8-d3f0-4491-9c60-44c3350bf729%2F6.png?table=block&id=7fcfd331-0c28-465e-b154-88d72b93f46b&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=860&userId=&cache=v2)