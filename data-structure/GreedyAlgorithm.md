# 그리디 알고리즘

- 최적의 값을 구해야 하는 상황에서 사용되는 근시안적인 방법론으로 ‘각 단계에서 최적이라고 생각되는 것을 선택’해 나가는 방식으로 진행하여 최종적인 해답에 도달하는 알고리즘입니다.
- 항상 최적의 값을 보장하는 것이 아니라 최적의 값에 ‘근사한 값’을 목표로 하고 있습니다

### 근시안적 방법론

- 단기적인 목표를 중심으로 한 전략적인 접근 방법을 의미한다. 주로 현재의 문제를 해결하는 데 초점을 맞추며, 장기적인 전망보다는 단기적인 성과를 중요시한다.

### 근사 알고리즘

- 최적의 해를 구할 수 없는 문제에서 근사한 해를 구하는 알고리즘. 근사 알고리즘은 항상 최적해를 보장하지 않지만, 많은 경우에는 최적해에 근접한 값을 구할 수 있음

### 문제를 해결하는 방법

1. 선택 절차(selection procedure) : 현재 상태에서의 최적의 해답을 선택함
2. 적절성 검삭(feasibility check) : 선택된 해가 문제의 조건을 만족하는지 검사
3. 해답 검사(solution check) : 원래의 문제가 해결되었는지 검사하고, 해결되지 않았다면 선택 절차로 돌아가 위의 과정을 반복한다

### 그리디 알고리즘을 적용하기 위해서 문제가 다음 2가지 조건을 성립하여야 함

- 대부분 탐욕스런 선택 조건과 최적 부분 구조 조건이라는 2가지 도전이 만족된다
- 탐욕스런 선택 조건은 앞의 선택이 이후의 선택에 영향을 주지 않는다는 것이며, 최적 부분 구조 조건은 문제에 대한 최적해가 부분문제에 대해서도 역시 최적해라는 것이다.
1. 탐욕적 선택 속성 : 앞의 선택이 이후의 선택에 영향을 주지 않는다
2. 최적 부분 구조 : 문제에 대한 최종 해결 방법은 부분 문제에 대한 최적 문제 해결 방법으로 구성된다