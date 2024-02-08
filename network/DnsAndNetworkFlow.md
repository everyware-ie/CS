# DNS와 웹 통신 흐름

## 웹 통신의 큰 흐름

![img.png](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F5f177aed-bb23-4647-8f40-c3634c45b01c%2Fimg.png?table=block&id=bc1cefb7-7cb9-4ef5-a920-83d437ca2e03&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)

1. 사용자가 웹 브라우저를 통해 URL을 입력한다.
2. 입력된 URL 중 도메인 네임을 DNS 서버에서 검색한다.
3. DNS 서버에서 해당 도메인 네임에 해당하는 IP 주소를 찾아 사용자가 입력한 URL 정보와 함께 전달한다.
4. 웹 페이지 URL 정보와 전달받은 IP 주소를 이용해 HTTP 요청(HTTP Request) 메시지를 생성한다.
5. 요청은 TCP를 통해 서버로 전송된다.
6. 서버는 클라이언트의 요청을 받고 응답(=HTTP Response)을 전송한다.

## DNS 서버란?

- 우리는 대부분의 사이트 접속을 도메인 이름을 가지고 함
- 브라우저의 검색창에 도메인 이름을 입력하여 해당 사이트로 이동하기 위해서는 해당 도메인 이름과 매칭된 IP 주소를 확인하는 작업이 반드시 필요
- 네트워크에는 이것을 위한 서버가 별도로 있음
- 이 서버가 바로 DNS 서버

<aside>
👉 DNS는 Domain Name System의 약자로, 호스트의 도메인 이름을 IP 주소로 변환하거나 반대의 경우를 수행할 수 있도록 개발된 데이터베이스 시스템

</aside>

## DNS 동작 과정

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F097828df-de46-4e2c-bacd-b74caa3bf5cc%2FUntitled.png?table=block&id=d67c4bdb-6154-477e-a161-43d8537704d1&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=2000&userId=&cache=v2)

- Local(hosts) → DNS cashe table → DNS server
- 위 과정에서 없으면 최상위(루트도메인) → Top Level Domain → Second Level Domain → Subdomain 순으로 IP를 찾음

1. 웹 브라우저에 도메인을 입력
2. 웹 브라우저는 이전에 방문한적 있는지 찾음
    - 브라우저 캐시 확인
    - OS 캐시 확인
    - 라우터 캐시 확인
    - ISP 캐시 확인 (Recursive DNS Server)
3. ISP에서 DNS Iterative하게 쿼리를 날림
4. ISP는 Autoritative DNS 서버에서 최종적으로 IP 주소를 응답받음
5. ISP는 해당 IP 주소를 캐시함
6. 웹 브라우저에게 응답

### DNS 쿼리(Query)

- 쿼리는 Recursive(재귀) or Iterative(반복)으로 구분
- DNS 클라이언트와 서버는 서로 쿼리를 교환

### Recursive Query(재귀적 질의)

1. Client server가 Local DNS Server에 쿼리를 보냄. mail1.nwtraders.com의 IP P주소를 알고 있냐(Local DNS에서 모른다고 가정)
2. Local DNS는  mail1.nwtraders.com에 대해 모르면 가장 먼저 Root DNS에 쿼리를 보냄
3. 거기에서도 모른다고 답이오면 다음 DNS com을 관리하는 DNS에 물어봄
4. 여기데서도 모른다고 답이오면 다음 nwtraders.com에 물어봄
5. nwtraders.com을 관리하는 DNS 서버에서 IP 주소를 알고있다면 Qutoritative Response를 보냄
6. 그것을 받은 Local DNS 서버는 mail.nwtraders.com의 IP주소를 캐싱하고 Client 서버에 mail.nwtraders.com의 IP 주소를 전달해줌

→ 이렇게 Local DNS서버가 여러 DNS 서버를 차례대로 물어봐서 그 답을 찾는 과정을 Recursive Query라고 부름

### Iterative Query(반복적 질의)

→ 반복적 질의는 Local DNS 서버가 다른 DNS 서버에게 쿼리를 보내 답을 요청하는 작업

## 도메인 vs URL

### 도메인이란?

도메인이라는 단어는 영역, 범위, 영토, 분야와 같은 의미를 가지는 뜻으로 오늘날에는 인터넷 주소라는 의미로 많이 쓰여지고 있음

도메인은 서브도메인, 이름, 확장자로 이루어져 있음.

서브 도메인은 차상위 도메인이라고도 불림 → SLD(Second Level Domain)

확장자는 최상위 도메인 → TLD(Top Level Domain)

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F01dc6c2c-bf19-4048-8549-4ab0b77560d1%2FUntitled.png?table=block&id=cb8111de-fd7d-4e44-ae4b-4a57dc5f0f6a&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=670&userId=&cache=v2)

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F72b14edf-2920-4d9d-bb31-3224b0d48fa6%2FUntitled.png?table=block&id=63b86e55-62e6-4892-9ccd-fc4e18d2a37d&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=670&userId=&cache=v2)

### URL

URL은 프로토콜, 서브 도메인, 이름, 확장자로 이루어져 있음

웹 페이지의 경로까지 포함하여 URL이라고 함.

## URL vs ULI

### URI = 식별자, URL = 식별자 + 위치

URI는 URL의 의미를 품고 있음.

URL(Uniform Resource Locator)은 자원이 실제로 존재하는 위치를 가리키며, URI(Uniform Resource Identifier)는 자원의 위치뿐만 아니라 자원에 대한 고유 식별자로서 URL의 의미를 포함함

- naver.com은 URI. 리소스의 이름만 나타내기 때문
- 반면 https://naver.com은 URL임. 이름과 더불어, 어떻게 도달할 수 있는지 위치까지 나타내기 때문

### 정리

1. URL은 일종의 URI이다.
2. URL은 프로토콜과 결함한 형태
3. URI는 그 자체로 이름이 될 수 있다.

## 공인 IP vs 사설 IP

### 1. 공인 IP (Public IP)

인터넷 사용자의 로컬 네트워크를 식별하기 위해 **ISP(인터넷 서비스 공급자)가 제공하는 IP 주소**이다. 공용 IP 주소라고도 불리며 외부에 공개되어 있는 IP 주소.

- 공인 IP는 전세계에서 유일한 IP 주소를 갖는다.
- 공인 IP 주소가 외부에 공개되어 있기에 인터넷에 연결된 다른 PC로부터의 접근이 가능하다. 따라서 공인 IP 주소를 사용하는 경우에는 방화벽 등의 보안 프로그램을 설치할 필요가 있다.

### 2. 사설 IP (Private IP)

**일반 가정이나 회사 내 등에 할당된 네트워크**의 IP 주소이며, 로컬 IP, 가상 IP라고도 한다. IPv4의 주소부족으로 인해 서브넷팅된 IP이기 때문에 라우터에 의해 로컬 네트워크상의 PC 나 장치에 할당된다.

|  | 공인 IP (Public IP) | 사설 IP (Private IP) |
| --- | --- | --- |
| 할당 주체 | ISP(인터넷 서비스 공급자) | 라우터(공유기) |
| 할당 대상 | 개인 또는 회사의 서버(라우터) | 개인 또는 회사의 기기 |
| 고유성 | 인터넷 상에서 유일한 주소 | 하나의 네트워크 안에서 유일 |
| 공개 여부 | 내/외부 접근 가능. | 외부 접근 불가능 |

❗ 사설 IP 주소만으로는 인터넷에 직접 연결할 수 없다. **라우터를 통해 1개의 공인(Public) IP**만 할당하고, **라우터에 연결된 개인 PC는 사설(Private) IP**를 각각 할당 받아 인터넷에 접속할 수 있게 된다.
![](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fc76fb535-8446-4e6e-9248-3d3516077b6b%2FUntitled.png?table=block&id=f7b0fb58-dda3-49bf-bc69-5a1a180b9e1b&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)