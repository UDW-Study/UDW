# Unreal Engine

## 단축키

* 에디터:
    - Ctrl + N: 새 레벨 생성
    - Ctrl + Alt + F11: 라이브 코딩 빌드
    - Alt + S: 시뮬레이트
    - Edit -> Project Settings -> GameInstance 검색: 프로젝트의 게임인스턴스 설정 가능
    - P: 네비게이션 범위 시각화됨

* 블루프린트:
    - Ctrl + Variable D&D: Get
    - Alt + Variable D&D: Set
    - B + Left Click: 브랜치 생성
    - S + Left Click: 시퀀스 생성
    - F9: 중단점 생성
    - 구역 선택 + C: 주석 만들기
    - Reroute: 링크 점프

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
    - 프리뷰를 보고싶으면 그래프에서 ctrl을 누른 상태로 마우스를 움직이면 됨
- 리타게팅
    - 비슷한 뼈 구조를 가졌지만 비율이 다른 캐릭터들의 애니메이션을 재사용하기 위한 시스템
    - 양쪽 캐릭터에서 같은 역할을 하는 뼈를 하나하나 매핑한 후에 애니메이션을 변환할 수 있음 (한 번만 매핑해놓으면 됨)
- 몽타주
    - 여러 애니메이션 시퀀스를 하나의 에셋으로 결합시키는 기능 (콤보 공격 구현에 유용함)
- Animation Notify
    - 애니메이션 시퀀스에 동기화된 이벤트를 생성할 수 있게 해주는 기능
    - AnimNotify를 상속받아서 Custom Notify Event를 생성할 수 있음. 필요한 정보를 실을 수 있어서 태그를 멤버로 전달하여 무슨 이벤트인지 알려주는 것이 정석임

## 충돌

#### Collision Responses:
- Block
    - OnHit 이벤트가 호출되며, 물리적으로 서로가 이동하는 경로를 막음
    - 두 물체 모두 Block으로 설정되어야 함
- Overlap
    - 두 물체는 서로를 막지도 않고 무시하지도 않으며 서로 겹침. OnBeginOverlap 이벤트와 OnEndOverlap 이벤트가 호출됨
    - 두 물체 중 하나라도 GenerateOverlapEvents 속성이 true로 설정돼 있지 않으면 이 이벤트들은 호출되지 않음
- Ignore
    - 두 물체에 대해 아무런 이벤트도 호출되지 않으며, 두 물체는 서로가 없는 것처럼 동작하며 서로 겹침.
    - 둘 중 하나라도 Ignore로 설정돼있으면 서로 무시함

#### Collision Enabled:
- No Collision
    - 충돌 사용 안함
    - 움직이는 오브젝트에 최고의 퍼포먼스
- Query Only
    - 공간 쿼리(레이캐스트, 스윕, 오버랩)에만 사용됨
    - 피지컬 시뮬레이션이 필요 없는 오브젝트와 캐릭터 무브먼트에 유용함
- Physics Only
    - 피직스 시뮬레이션(리지드 바디, 컨스트레인트) 전용
    - 본 단위 탐지가 필요 없는 캐릭터의 이차 시뮬레이션 동작에 유용함
- Collision Enabled
    - 공간 쿼리(레이캐스트, 스윕, 오버랩)와 시뮬레이션(리지드 바디, 컨스트레인트)에 모두 사용 가능

#### Channel & Preset
- Object Channel
    - 새로운 오브젝트 타입을 정의함
    - 생성시 모든 Preset들에서 Collision Response를 맞춰줘야함
    - Project/Config/DefaultEngine.ini 파일에 저장됨
    - C++에서 사용할때는 이름이 아니라 ini파일에 저장된 채널 번호로 접근해야 함
- Trace Channel
    - Object Channel과 비슷한데 개념적인 상황에 사용함
    - Sphere Trace By Channel에 사용됨 (유니티 BoxCast랑 비슷)
    - 위의 함수 사용시에 상대가 Overlap이면 탐지 안됨. Block이어야 함
- Preset
    - 다양한 Object와 Trace에 대해 Collision Responses를 미리 정의해놓은 것

## AI
- BlackBoard
    - Behavior Tree가 결정을 내리는데 사용하는 정보(상태)를 저장함
    - Key - Value 구조로 되어있음
    - BlackBoard의 정보를 관찰하고 있다가 변경되는 순간 실행되도록 관찰자 패턴으로 만드는 것이 가능

- BlackBoard Decorator 관련 프로퍼티
    | Notify Observer | |
    |---------------------------|----------------------------|
    | On Result Change | 조건이 변경될 때만 재평가 |
    | On Value Change | 관찰된 블랙보드 키가 변경될 때 재평가 |

    | Observer Aborts |    |
    |---|---|
    | None | 아무것도 중단하지 않음  |
    | Self | 자신 및 이 노드 아래에서 실행 중인 모든 서브트리를 중단  |
    | Lower Priority | 이 노드의 오른쪽에 있는 모든 노드를 중단  |
    | Both | 자신, 이 노드 아래에서 실행 중인 모든 서브트리, 이 노드의 오른쪽에 있는 모든 노드를 중단 |

- Behavior Tree
    | 노드 | 설명 |
    |---|---|
    | Task | 실행할 수 있는 액션을 나타내며, 출력 연결을 갖지 않음 |
    | Service | Composite 노드에 부착되며, 자신의 분기가 실행되는 동안에 한해 정의된 주기로 실행됨 |
    | Decorator | 다른 노드에 부착되어 트리의 분기나 단일 노드의 실행 여부를 결정함 |
    | Composite | 자손들의 실행 흐름을 결정함 |

- Composite 노드 종류
    | 노드 | 설명 |
    |---|---|
    | Selector | 자식들 중에 하나라도 성공하면 성공으로 처리되고 실행 중단 |
    | Sequence | 자식들 중에 하나라도 실패하면 실패로 처리되고 실행 중단 |
    | Simple Parallel | - Main Task와 Background Branch 2개의 분기만 연결 가능<br>- Main Task가 실행되는 동안 Background Branch가 병렬 실행됨<br>- Main Task에는 Task 노드만 할당 가능 |

## UI

#### UserWidget
- 모든 UI의 부모가 되는 클래스
- C++로 UI를 만들 때 해당 클래스를 상속받으면 됨

#### UWidgetComponent
- UI를 컴포넌트로 배치하고 싶을때 사용하는 클래스
- 해당 컴포넌트의 `WidgetClass`를 원하는 UI로 설정해주면 해당 UI가 배치됨
- `WidgetSpace`를 `World`또는 `Screen`으로 설정 가능
- `DrawAtDesiredSize`를 켜주면 디자인한 크기대로 랜더링됨

#### Widget Blueprint
- UI에서 사용하는 블루프린트
- 기본 부모는 `UUserWidget`
- Designer 탭에서 UI를 편집하고 Graph 탭에서는 일반적인 블루프린트 작성
- C++에서 `UPROPERTY(meta=(BindWidget))` 로 해놓으면, 해당 멤버 변수는 이름이 정확히 같은 UI요소와 연결됨 (없으면 오류남)

#### OnDragOver vs NativeOnDragOver
- 전자는 블루프린트용 래퍼 함수, Native는 C++용
- 래퍼 함수는 인자가 좀 더 단순하고 C++에서 오버라이드 할 수 없음 (가상함수가 아님)
- `NativeOnDragOver`내부에서 `OnDragOver`를 호출하는 형태로 되어있음
- `UUserWidget`의 API 대부분이 Native와 래퍼 함수의 세트로 구성됨

#### 드래그 관련 함수들

|      함수      |          설명         |
|--------------|---------------------|
| OnDragDetected | 드래그 시작           |
| OnDragEnter    | 위젯에 처음 들어올 때 |
| OnDragOver     | 위에 있는 동안 계속   |
| OnDragLeave    | 벗어날 때             |
| OnDrop         | 드롭 시               |

## GAS

#### AbilitySystemComponent (ASC)
- GAS 중앙 관리자
- 캐릭터에 하나씩 부착하여 사용

#### IAbilitySystemInterface
- 액터가 GAS를 사용하게 하려면 해당 인터페이스를 구현하고 `GetAbilitySystemComponent()` 함수를 오버라이드 해야 함.
- 해당 함수는 단순히 ASC를 리턴하는 역할
- 플레이어의 경우에는 `PlayerState`에 실제 ASC를 넣어놓고, 캐릭터에는 참조를 넣어놨다가 위의 함수에서 리턴하도록 설계함
- PlayerState는 서버에서 클라로 주기적으로 배포되는 액터이고, 캐릭터가 소멸되고 리스폰될때도 살아있어서 주로 사용한다고 함

### Gameplay Attributes
- 캐릭터의 스탯
- 모든 속성은 `FGameplayAttributeData` 클래스를 사용해야 함
- BaseValue와 CurrentValue가 있음
- BaseValue는 기본값, CurrentValue는 현재 활성화된 모든 이펙트를 적용한 값
- 몇몇 매크로를 사용하면 getter와 setter를 자동 생성할 수 있음
- 모든 값은 float 고정임
- Owner Actor의 생성자에서 AttributeSet을 생성하면 ASC에 자동으로 등록된다고 함

`PostGameplayEffectExecute` 함수로 GameplayEffect 실행후에 값 Clamp및 UI업데이트 가능

AttributeSet, Character, PlayerState, PlayerController 등 수많은 클래스들이 서로의 정보가 시시각각 필요한 경우가 많음. Unity였으면 싱글톤을 사용하거나 참조 포인터를 하나하나 연결해줬겠지만, GAS에선 ASC가 확실한 중심점 역할을 해줌. ASC에는 대부분의 참조가 모두 들어있기 때문에, 일단 ASC를 얻으면 Getter로 필요한 건 대부분 얻을 수 있음.

- `GetSet` 함수로 AttributeSet 획득
- `GetAvatarActor` 함수로 아바타 액터 획득 (Character)
- `GetOwnerActor` 함수로 오너 액터 획득 (Player의 경우 PlayerState)
- AttributeSet에서는 `GetOwningAbilitySystemComponent`로 ASC획득 가능
- Gameplay Ability에서는 인자로 들어오는 `ActorInfo->AbilitySystemComponent`로 ASC를 얻을 수 있음

### Gameplay Ability
- 실제 스킬이나 행동을 정의함
- 문 열기, 점프 등 단순한 행동부터 복잡한 스킬까지 표현가능
- [Gameplay Ability 개요](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/using-gameplay-abilities-in-unreal-engine)

Gameplay Ability 주요 함수들:

    CanActivateAbility()	- const function to see if ability is activatable. Callable by UI etc

    TryActivateAbility()	- Attempts to activate the ability. Calls CanActivateAbility(). Input events can call this directly.
                            - Also handles instancing-per-execution logic and replication/prediction calls.
                            - UGameplayAbility 멤버 함수가 아님. UAbilitySystemComponent 멤버임
    
    CallActivateAbility()	- Protected, non virtual function. Does some boilerplate 'pre activate' stuff, then calls ActivateAbility()

    ActivateAbility()		- What the abilities *does*. This is what child classes want to override.

    CommitAbility()			- Commits reources/cooldowns etc. ActivateAbility() must call this!
    
    CancelAbility()			- Interrupts the ability (from an outside source).

    EndAbility()			- The ability has ended. This is intended to be called by the ability to end itself.

함수 호출 구조

    TryActivateAbility (ASC)
      ↓
    CanActivateAbility 체크
        ↓
    CallActivateAbility
        ↓
    ActivateAbility (Ability 구현부)
        ↓
    CommitAbility (마나 사용, 쿨다운 처리)
        ↓
    EndAbility

> CommitAbility, EndAbility는 ActivateAbility내에서 명시적 호출 필요


Gameplay Ability의 cost 처리와 cooldown 처리
- GA의 Costs 부분과 Cooldowns 부분에 적절한 GE를 넣어주면 `CommitAbility` 실행시 알아서 처리됨
- AttributeSet.Mana / Op Add / Scalable Float -20로 설정한 GE를 넣어주면 어빌리티 시전시 마나 20을 소모함
- cooldown을 위한 GE는 Duration을 설정해주면 해당 Duration이 쿨타임이 됨.
- 이때 Components -> Grant Tags to Target Actor 부분에 태그를 하나 넣어줘야 함. (왜 필요한지는 아직 모름)

### Gameplay Effect
- 능력이 만들어내는 효과
- 로직은 거의 없고 Attributes처럼 데이터 위주임
- Duration Policy를 Instant/Infinite/Has Duration 중에 고를 수 있음
- Duration을 가지도록 설정하면 실행 기간, 주기 등을 설정하는 것이 가능 (도트뎀 디버프 구현 가능)
- Modifiers에 어떤 Attribute를 건드릴 것인지, 어떤 Operation을 할 것인지 설정하여 Effect구현
- 예를 들어 R1AttributeSet.Health를 Op Add로 -50을 넣어주면, 해당 Effect는 적용 대상의 HP 50을 감소시킴

#### 기타 팁

~키를 누르면 콘솔을 열 수 있고, 콘솔에 `showdebug abilitysystem` 명령어를 입력하면 어빌리티 시스템의 현황을 화면에서 확인할 수 있다


`InitAbilityActorInfo` 함수를 반드시 호출해야 함. 인자는 OwnerActor, AvatarActor
```c++
// PossessedBy 시점에 실행할 것 (네트워크와 관련 있다고 함)
void AR1Player::PossessedBy()
{
    Super::PossessedBy(NewController);

    if (AR1PlayerState* PS = GetPlayerState<AR1PlayerState>())
    {
        AbilitySystemComponent = Cast<UR1AbilitySystemComponent>(PS->GetAbilitySystemComponent());
        AbilitySystemComponent->InitAbilityActorInfo(PS, this);
    }
}
```

## 네트워크

NetMode
- 현재 실행 중인 인스턴스가 어떤 네트워크 모드에서 동작 중인지 구분하는 값
- `GetWorld()->GetNetMode()` 함수를 사용하면 `ENetMode` 열거형이 나옴

    - `NM_Standalone` : 네트워크 없이 혼자 실행
    - `NM_ListenServer` : 서버와 클라이언트 양쪽 역할을 모두 맡음
    - `NM_DedicatedServer` : 전용 서버
    - `NM_Client` : 서버에 접속한 클라이언트
    
- 플레이 세팅에서 플레이어 인원수 및 NetMode 설정 가능

Netrole
- 각 액터가 네트워크에서 어떤 권한을 가지는지 나타냄:

    - `ROLE_Authority` : 서버가 소유, 권한 있음
    - `ROLE_AutonomousProxy` : 클라이언트에서 자신이 조종하는 Pawn
    - `ROLE_SimulatedProxy` : 클라이언트에서 다른 유저가 조종하는 Pawn

- 간단하게 HasAuthority() 함수로 서버인지 체크하고 서버에서만 실행할 코드를 작성 가능

Replication 관련 액터 설정들
- Replicates
    - 액터를 레플리케이트할지 설정
- Net Load on Client
    - 켜져 있으면 클라이언트에도 해당 액터가 로드됨
    - Replicates가 꺼져 있어도 작동함
    - 반대로 Replicates가 켜져있으면 이 옵션이 꺼져있어도 클라이언트에 로드됨
- Replicate Movement
    - 액터의 위치를 동기화해줌

Variable Replication
- Replicated
    - 변수를 동기화해줌
    - 클라이언트의 변경 사항은 동기화 안됨. 서버에서 클라 방향으로만 동기화됨
- RepNotify
    - Replication을 해주고 Replication이 일어났을 때 지정된 함수를 실행해줌
    - 이 함수에서 변수가 변경되었을 때 해야하는 처리를 추가해줄 수 있음
    - 보통 함수 이름은 OnRep_XXX임
    - C++에서는 변수를 수정했을 때 클라이언트에서만 OnRep함수가 실행됨 (즉 실제로 동기화가 일어난 원격에서만 실행되는 것)
    - 블루프린트에서는 변수를 수정한 서버에서도 실행됨
- Replication은 변수가 변경되는 즉시 일어나는것이 아니라 스케쥴링되어 일어남
- RPC는 호출 즉시 통신하여 실행함

```c++
UPROPERTY(ReplicatedUsing = OnRep_PlayerHealth)
int32 PlayerHealth;

void AMyPlayerCharacter::OnRep_PlayerHealth()
{
    // PlayerHealth 변수가 업데이트 되면 실행
    UpdateHealthBar(PlayerHealth);
}

// 이 함수를 오버라이드 해줘야한다
void AMyPlayerCharacter::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const
{
    Super::GetLifetimeReplicatedProps(OutLifetimeProps);
    // DOREPLIFETIME 함수의 인자로 (해당 Class - 변수 이름)을 넣는다.
    DOREPLIFETIME(AMyPlayerCharacter, PlayerHealth);
}
```

RPC
