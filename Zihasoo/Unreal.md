# 언리얼

## 단축키

* 에디터:
    - Ctrl + N: 새 레벨 생성
    - Ctrl + Alt + F11: 라이브 코딩 빌드
    - Alt + S: 시뮬레이트
    - Edit -> Project Settings -> GameInstance 검색: 프로젝트의 게임인스턴스 설정 가능

* 블루프린트:
    - Ctrl + Variable D&D: Get
    - Alt + Variable D&D: Set
    - B + Left Click: 브랜치 생성
    - S + Left Click: 시퀀스 생성
    - F9: 중단점 생성
    - 구역 선택 + C: 주석 만들기

* 머티리얼 그래프:
    - 숫자 1 ~ 4 + Left Click: float 값 생성
    - View에서 Shape및 View Mode등 설정 가능

## 블루프린트

레벨 블루프린트:
- 레벨 이벤트 흐름 제어용. 재사용 및 상속 불가능

블루프린트 클래스:
- 오브젝트 로직용. 여러 레벨에서 재사용 및 상속 가능. 여러개 생성 가능

문자열 타입:
- Name: 해쉬값으로 빠른 비교 가능 (자주 바뀌는 값에는 사용 X)
- String: 기본적인 문자열
- Text: 다국어 지원 가능한 문자열


## 빌드

비주얼 스튜디오에서 실행:
- 엔진(에디터)과 사용자 코드가 통째로 빌드돼서 실행됨 (엔진은 빌드돼있고 링킹만 하는듯)
- 코드가 수정돼도 완전히 빌드되는 것이라 오류 발생 확률이 적음
- 매번 실행할때마다 에디터가 새로 켜지고, 실행을 멈추면 에디터가 꺼져버리는 단점이 있음
- 특히 파일을 새로 생성하면 VS를 리로드해야하고, 이때 에디터를 멈춰야해서 파일을 추가 할때마다 다시 켜야함

에디터에서 실행 (라이브 코딩):
- 패치 시스템을 이용해 변경된 코드만 적용시킴 (에디터 실행 중에 변경 코드 적용 가능)
- 에디터를 새로 키고 끄지 않아도 돼서 편리하지만 문제가 생길 가능성이 있음 (블루프린트랑 섞어서 작업할 때)
- 유니티와 다르게 코드를 수정해도 자동으로 적용 안되고, 에디터의 실행 버튼은 빌드와는 별개임. 코드 수정하고 실행 버튼 눌러도 변경사항 적용 안됨
- 핫 리로드 vs 라이브 코딩   
핫 리로드는 구식 기술이고 프로젝트를 손상시킬 수 있음. 핫 리로드를 하고 라이브 코딩을 쓰면 정상 작동을 안함. 이때는 에디터를 닫고 아예 리빌드를 해야 함. 라이브 코딩은 언리얼 4.22에 추가된 기능   
- 전체 빌드와 라이브 코딩을 적절히 잘 섞어 써야할듯. 핫 리로드는 사용 X
- [핫 리로드와 라이브 코딩에 관한 글](https://unrealcommunity.wiki/live-compiling-in-unreal-projects-tp14jcgs)
- [빌드 설정 관련](https://bloodstrawberry.tistory.com/1157)

## 실행

- 시뮬레이트를 사용하면 게임을 실행은 하되 플레이어를 조작하지 않고 원래 에디터처럼 조작이 가능
- 언리얼 엔진은 유니티와 다르게 씬과 게임 뷰를 동시에 띄울 수 없음
- Eject 버튼을 누르면 시뮬레이트 상태로 전환 가능 (플레이어 빙의 해제 느낌)
- [플레이 및 시뮬레이션](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/playing-and-simulating-in-unreal-engine)


## 모듈
- 현대 언어의 모듈 시스템을 언리얼의 방식으로 구현한듯함.
- C#을 빌드 툴로 사용하는 것 같고, 정확히 내부 원리가 어떻게 돼있는지는 알려주지 않았음. (나중에 공부해보기)
- `[모듈이름].Target.cs`파일, `[모듈이름]`폴더, 그 폴더에 `[모듈이름].Build.cs`, `[모듈이름]Module.cpp` 을 생성해 프로젝트에 새로운 모듈 추가가능. `uproject`파일도 수정해함
- `[모듈이름].Build.cs`파일의 `PublicDependencyModuleNames.AddRange({...})` 부분을 수정하여 종속성을 추가할 수 있음

## 로그
- UE_LOG로 로깅 가능
- `UE_LOG(LogTemp, Warning, TEXT("Hello World"));`
- 로그 카테고리 / 로그 레벨 설정 가능
- 자체 로그 카테고리 정의 가능
- `UE_LOGFMT` 라는 최신 함수를 사용해 현대식 포메팅으로 로깅가능

## UObject
- 모든 언리얼 객체의 베이스 클래스
- `UCLASS()` 메크로를 붙여서 UObject 처리 시스템이 인식하도록 해야함.
- 메크로를 붙여주면 해당 오브젝트의 메타데이터 역할을 하는 `UCLASS` 객체가 생성되고, CDO를 하나 가지게 됨
- 이 `UCLASS` 객체를 통해 언리얼 에디터에서 클래스 정보를 조회할 수 있고, 런타임 cast를 빠르게 할 수 있음
- Intermediate 폴더에 `XX.gen.cpp`, `XX.generated.h` 파일로 생성됨
- `UR1Object* Obj1 = NewObject<UR1Object>();` 방식으로 생성 (`new`로 할당하면 안됨)
- `UPROPERTY()` 라는 메크로를 멤버 변수에 붙여서 리플렉션, 직렬화, GC등 제공되는 기능에 포함 가능
- `UPROPERTY()` 메크로의 지정자를 수정해 유니티처럼 에디터에서 변수 값을 편하게 지정 가능 (최소/최대값 설정 등)
- 언리얼 GC의 콜렉션 기준은 `UPROPERTY()` 메크로가 붙은 멤버 변수에 의한 참조임. 해당 메크로가 붙지 않은 일반 포인터로 참조하게 되면 GC 싸이클에 콜렉션됨
- 가비지 콜렉션 된다고 해서 해당 멤버 변수가 nullptr를 가리키지는 않음. 그냥 쓰레기 값을 가리키게 됨 (유니티도 똑같은데 유니티는 `==`을 오버로딩해서 해결함)
- `TWeakObjectPtr`로 이 문제를 어느 정도 해결 가능함

## 게임 프레임워크
- GameInstance: 게임 전체에서 1개의 객체를 유지할 수 있는 싱글톤 클래스. 프로젝트 설정에서 어떤 클래스를 게임 인스턴스로 정할지 설정 가능
- GameMode: 게임 전체의 메니저 같은 클래스. 게임의 룰이나 플레이어 컨트롤 방식, UI 등 플레이와 관련된 모든 것들을 관리함.
- 언리얼은 게임을 돌리기 위한 시스템이 이미 구조화되어 있고 이를 잘 따르기만 하면 매우 빠르게 개발이 가능함

## Actor
- `ConstructorHelpers`의 몇몇 클래스를 이용하면 에셋 경로로부터 에셋을 로드하는것이 가능함

```c++
// 예시
ConstructorHelpers::FClassFinder<T> FindClass(TEXT("경로"));
if (FindClass.Succeeded())
{
	DoSomething(FindObj.Class);
}
ConstructorHelpers::FObjectFinder<T> FindObj(TEXT("경로"));
if (FindObj.Succeeded())
{
	DoSomething(FindObj.Object);
}
```
- 블루프린트를 로드할때는 경로 맨 뒤에 `_C`를 붙여야함
- GetActor 함수 시리즈가 있음. 클래스, 태그 등 다양한 기준으로 월드에 있는 오브젝트를 가져올 수 있음
- `UGameplayStatics::GetActorOfClass(GetWorld(), AR1Actor::StaticClass());`
- `UGameplayStatics::GetAllActorsWithTag(GetWorld(), FName("R1ActorTag"), TArray<AActor*>());`
- `TArray`의 `Empty()`함수는 비어있는지 확인하는 함수가 아니라 clear처럼 내용물을 비우는 함수임. 비어있는지 확인하고 싶다면 `Num()`함수를 사용해 요소의 개수를 체크할 것

## Pawn & Character
- Pawn은 Actor를 상속받은 클래스임. 빙의하여 조종하는 것이 가능함
- Character는 Pawn을 상속받았고 Mesh, Capsule, Character Movement를 기본으로 가지고 있음.
- 움직임은 Pawn에 바로 넣어주고, 회전은 Player Controller에 넣는것이 일반적임. 이때 저장된 회전을 여러 설정을 통해 Pawn에 다르게 적용할 수 있음. (캐릭터에만 적용 / 카메라에만 적용 등등)
- GameplayTags라는 기능으로 에셋 관리를 편리하게 할 수 있음

## 컴포넌트
- 액터 컴포넌트는 움직임, 인벤토리, 어트리뷰트 관리 및 기타 비물리적 개념과 같은 추상적인 동작에 사용. 트랜스폼 없음
- 씬 컴포넌트 (액터 컴포넌트의 자손)는 지오메트리 표현이 필요하지 않은 위치 기반 동작을 지원함. (예: 스프링 암, 카메라, 물리적 힘, 컨스트레인트(물리적 오브젝트는 해당 없음), 오디오 등)
- 프리미티브 컴포넌트 (씬 컴포넌트의 자손)는 지오메트리 표현이 있는 씬 컴포넌트로, 주로 비주얼 요소 렌더링이나 물리적 오브젝트와의 충돌 또는 오버랩에 사용됨. (예: 박스, 캡슐, 구체 콜리전 볼륨, 스태틱/스켈레탈 메시, 스프라이트 또는 빌보드, 파티클 시스템)

## Asset Manager
- Data Asset:
    - 특정 시스템과 관련된 데이터를 해당 클래스의 인스턴스에 저장하는 자산
    - 원하는 형식의 데이터 저장용 클래스를 구현하면, 해당 클래스를 베이스로 Data Asset을 생성하고, 내용 설정 및 저장 가능 (Dto느낌)
    - UDataAsset을 상속받으면 됨. UMyDataAsset -> BP_MyDataAsset -> Data Asset 가능
- Primary Data Asset
    - `GetPrimaryAssetId`함수를 구현하는 Data Asset
    - 자산 번들 지원을 제공하여, 에셋 메니저에서 수동으로 Load/Unload 가능
- Asset Manager
    - Primary Asset의 탐색 및 로드를 관리하는 싱글톤 클래스
- Streamable Manager
    - Primary Data Asset에 포함되어있는 구조체
    - Async Load/Unload 하는 기능을 수행함
- [Data Asset과 Asset Manager](https://redchiken.tistory.com/358)
- [Unreal Docs: Data Assets](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/data-assets-in-unreal-engine)

## 애니메이션
- 애니메이션 블루프린트
    - 애니메이션의 주인이 되는 폰의 정보들을 감시하고 있다가, 특정 조건이 맞춰지면 애니메이션을 실행하는 형태임
    - AnimInstance를 상속받아서 C++에서 코드로 어느 정도 짜놓고, 다시 블루프린트로 상속받아서 사용해도 됨
    - State Machine으로 그래프를 캡슐화해서 사용가능. Cached Pose 기능으로 특정 SM에서 나온 결과물을 다른데서 사용 가능 (로지심의 터널 느낌)
    - State Alias로 여러 State로부터 트렌지션되는 상황을 한 번에 처리가능 (유니티 Any State 상위호환)
- Additive Animation
    - 원래의 애니메이션에 더해주는 애니메이션 (단독 실행 안됨)
    - 상, 하체를 분리하기 위해서 사용하는 Layered Animation보다 좀 더 자연스러운 연출 가능
- Blend Space
    - 여러 포인트에서 그래프를 따라 애니메이션을 지정하는 에셋 (이 포인트를 sample 이라고 함)
    - 전체 애니메이션은 각 축의 입력 값을 바탕으로 그래프에 있는 포인트 사이의 블렌딩을 통해 계산됨
    - `IDLE - 걷기 - 달리기` 같은 변수에 따른 애니메이션 전환을 이 에셋 하나로 매우 간단하게 표현 가능함
- 리타게팅
    - 비슷한 뼈 구조를 가졌지만 비율이 다른 캐릭터들의 애니메이션을 재사용하기 위한 시스템
    - 양쪽 캐릭터에서 같은 역할을 하는 뼈를 하나하나 매핑한 후에 애니메이션을 변환할 수 있음 (한 번만 매핑해놓으면 됨)
- 몽타주
    - 여러 애니메이션 시퀀스를 하나의 에셋으로 결합시키는 기능 (콤보 공격 구현에 유용함)