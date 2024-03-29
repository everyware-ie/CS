# 파일 시스템

## 파일 (File)

- 사용자나 응용 프로그램 관점
    - 정보를 저장하고 관리하는 논리적인 단위
- 컴퓨터 시스템의 관점
    - 정보를 저장하는 컨테이너
    - 0과 1의 데이터 덩어리
    - 영구 저장 장치나 일시 저장 장치에 저장
- 운영체제의 주요한 역할 중 하나 → 파일 시스템 관리
    - 파일 생성, 기록, 읽기 모든 과정 통제
    - 응용프로그램은 운영체제 모르게 파일 다루기 불가능
    - 저장 매체, 빈 공간 등 관리는 모두 운영체제가

## 파일 보관 장치

- 자기장 기반(Magnetic)
    - Hard Disk Drive(HDD)
    - flopy disk(FD)
    - 자기 테이프
- 반도체 기반
    - Solid State Drive(SSD)
    - USB, memory stick
- 광학
    - Compact Disk(CD)
    - Digital Video Disk(DVD)

### 자기장 기반 방식

→ 저장 매체 위에 자기장에 반응하는 물질을 발라두고 헤드를 이용해 특정 위치의 값을 읽어오는 장치

### 반도체 기반 방식

→ 수많은 트랜지스터에서 전자를 뺏거나 넣거나를 반복하여 데이터를 읽고, 쓰고, 지우는 과정을 통해 작동

전기가 계속 refresh가 안되면 수명이 한정적

### 광학 기반 방식

→ 표면에 미세한 홈을 파서 헤드에서 발사된 레이저가 홈에 들어가 반사가 되지 않으면 0, 반사되어 돌아오면 1로 인식, 플라스틱을 녹여서 층을 만듦(CD를 굽는다고 표현하는 이유)

## 가장 빠른 방식

**→ 반도체 기반 방식**

- 기계적인 장치가 필요없이 오로지 전자적으로 작동
- 하드디스크나 CD등은 구동부(모터)가 필요함, 모터가 아무리 빨라도 빛보다 빠를 순 없음
- 반도체 기반 방식이 더 튼튼함
- 대신 반도체는 주기적으로 정기 충전이 필요함 → 아니면 데이터 증발 가능
- USB나 SSD도 안쓰고 놔두면 보존이 안됨. 그리고 온도 변화에도 취약함 저항이 바뀌기 때문
- 그래서 반도체 기반은 무전원 장기간 보관에는 부적합

## 파티션(Partition)

- 운영체제는 저장 장치를 하나의 연속된 데이터 블록으로 봄
    - 하드디스크가 2개라면 블록은 2개
    - 그렇다면 하나를 두 개, 또는 n개로 쪼개는건 어떨까?

### 파티션

- 디스크를 논리적으로 분할하는 작업 → 데이터 블록 하나를 n개로 나눈다고 보면 됨.
- 대용량 하드디스크의 경우 하나로 사용하기보다 여러 개로 나누어 사용하면 관리하기가 편함
- 반대로 여러 개의 디스크를 하나로 만들 수도 있음
    - 얘도 넓은 의미로는 파티션이라고도 부를 수 있지만
    - 레이드(Raid) 또는 LVM(Logical Volume Manager)

## 마운트

→ 파티션을 디렉터리에 연결하는 행위

### 마운트 포인트

→ 다른 파티션(파일 시스템)을 연결하기 위해 사용되는 디렉터리

### 마운트를 이용한 파티션 연결

- 여러 파티션에 설치된 파일 시스템을 연결하여 전체를 하나의 파일 시스템으로 사용
- 각 파티션에 파일 시스템 설치

## Raid(Redundant Array of Independent Disks)

- 여러 개의 디스크를 병렬로 연결하여 사용하는 방법
    - 저장장치를 여러 개를 묶어, 고용량, 고성능 디스크 하나와 같은 효과를 얻기 위함
    - 하나의 원본 디스크와 같은 크기의 백업 디스크에 같은 내용을 동시에 저장하고, 하나의 디스크가 고장났을 때 다른 디스크를 사용하여 데이터를 복구
    - 저장장치의 고장은 데이터의 손실 → 레이드는 데이터 신뢰성을 높일 수 있는 좋은 방법