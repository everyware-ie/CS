# Join(조인)

## 1. JOIN이란?

- 데이터베이스에서 ‘두 개 이상의 테이블’을 연결하여 ‘하나의 결과의 테이블’로 만드는 것을 의미하며 이를 통해 데이터를 효율적으로 검색하고 처리하는데 도움을 줌
- JOIN을 사용하는 이유는 데이터베이스에서 테이블을 분리하여 ‘데이터 중복을 최소화’하고 ‘데이터의 일관성’을 유지하기 위함

관계형 데이터베이스에서는 중복 데이터를 피하기 위해서 데이터를 쪼개 여러 테이블로 나눠서 저장함. 이렇게 분리되어 저장된 데이터에서 원하는 결과를 다시 도출하기 위해서는 여러 테이블을 조합할 필요가 있음. 그래서 조인은 관련 있는 컬럼을 기준으로 행을 합쳐주는 연산.

## 2. 내부 조인(INNER JOIN)

- 두 테이블에서 ‘공통된 값’을 가지고 있는 행들만을 반환

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Ffc8f7c83-be20-4ee2-9070-b5ddb2ea69c3%2FUntitled.png?table=block&id=0d0e9d8e-b0ce-4539-8bc4-64060a1d731b&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)

```sql
SELECT *
FROM 테이블1
INNER JOIN 테이블2
ON 테이블1.열 = 테이블2.열;
```

### SELF INNER JOIN

- 하나의 테이블 내에서 다른 열을 참조하기 위해 사용하는 ‘자기 자신과의 조인’ 방법. 이를 통해 데이터베이스에서 한 테이블 내의 레코드를 다른 레코드와 연결할 수 있음

### CROSS INNER JOIN

- 두 개 이상의 테이블에서 ‘모든 가능한 조합’을 만들어 결과를 반환하는 조인 방법. 이를 통해 두 개 이상의 테이블을 조합하여 새로운 테이블을 생성할 수 있음.
- Cross Join은 일반적으로 테이블간의 관계가 없을 때 사용됨. 각 행의 모든 가능한 조합을 만들기 때문에 결과가 매우 큰 테이블이 될 수 있으므로 사용에 주의가 필요.

```sql
SELECT 테이블1.열, 테이블2.열
FROM 테이블1
CROSS JOIN 테이블2;
```

## 3. 외부 조인(OUTER JOIN)

- Outer Join은 두 테이블에서 ‘공통된 값을 가지지 않는 행들’도 반환
- Left Join, Right Join, Full Join

### LEFT OUTER JOIN

- ‘왼쪽 테이블의 모든 행’과 ‘오른쪽 테이블에서 왼쪽 테이블과 공통된 값’을 가지고 있는 행들을 반환
- 만약 오른쪽 테이블에서 공통된 값을 가지고 있는 행이 없다면 NULL 값을 반환

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fb55dd582-8d8f-48fa-85a3-63d4808b2d46%2FUntitled.png?table=block&id=a1033b8a-094e-41c9-b566-672e9d7eb935&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)

```sql
SELECT *
FROM 테이블1
LEFT JOIN 테이블2
ON 테이블1.열 = 테이블2.열;
```

### RIGHT OUTER JOIN

- Left Join과 반대로 ‘오른쪽 테이블의 모든 행’과 ‘왼쪽 테이블에서 오른쪽 테이블과 공통된 값’을 가지고 있는 행들을 반환합니다. 만약 왼쪽 테이블에서 공통된 값을 가지고 있는 행이 없다면 NULL값을 반환.

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F3d172b1a-8729-4a45-bbd1-a6b4105f1936%2FUntitled.png?table=block&id=d3e37941-a28b-4911-9797-ca670ea86d0c&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)

```sql
SELECT *
FROM 테이블1
RIGHT JOIN 테이블2
ON 테이블1.열 = 테이블2.열;
```

### FULL OUTER JOIN

- 두 테이블에서 ‘모든 값’을 반환. 만약 공통된 값을 가지고 있지 않는 행이 있다면 NULL 값을 반환

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F964bbc94-219e-4609-8ca6-a4158381fafe%2FUntitled.png?table=block&id=e15ebf49-8022-42d9-8b98-57c6ea75b674&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)

```sql
SELECT *
FROM 테이블1
FULL OUTER JOIN 테이블2
ON 테이블1.열 = 테이블2.열;
```