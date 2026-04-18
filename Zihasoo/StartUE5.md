# 시작해요 언리얼 2026

## PCG

에디터에서 선택 모드를 PCG 모드로 전환 (왼쪽 상단)

PCG Actor를 선택하고 PCG 모드를 키면 기존 엑터 수정  
그렇지 않으면 새로운 PCG 엑터 생성

### Spline

- Draw Spline
    - Spacing Tool
    - Spline Mesh Tool
    - Linear Grammar Tool

- Draw Spline Surface
    - Area Tool

Draw Mode를 Click Auto Tangent로 설정하면 점을 찍어서 범위 지정 가능

### Paint

- Place Tool
- Layered Place Tool

단축키: 
- `Left Click`: 오브젝트 배치
- `Shift + Left Click`: 오브젝트 삭제
- `Mouse Wheel`: 오브젝트 방향 지정


> PCG 플러그인 설치 필요

## PLA

유니티의 프리팹과 느낌이 비슷함

### 생성 방법
- *오브젝트 다중 선택 -> 우클릭 -> 레벨 -> 패킹된 레벨 엑터 생성*

- 레벨 파일과 블루프린트 파일이 함께 생성되기 때문에 두 번 저장하게 됨

### 편집 방법
- *디테일 -> 레벨 인스턴스 -> 편집*

### PCG를 PLA로 만드는 법
- *PCG 엑터의 디테일 창-> PCG Tool Component -> PCG 링크 지우기*

- 이렇게 하면 Stamp라는 이름이 붙은 엑터가 나오고, 원래 PCG 엑터는 지우면 됨
- PLA에는 스태틱 메시만 사용 가능하다고 함.

### 씬에 배치된 엑터를 다른 엑터로 교체하는 법
- *오브젝트 선택 -> 우클릭 -> 선택된 엑터를 다음으로 대체 -> 원하는 엑터 결정*
