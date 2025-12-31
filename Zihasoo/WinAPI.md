# Window API

## Windows OS API 연표
|연도 | 기술 | 성격 | 핵심 역할|
|----|-----|------|--------|
|1985 | Win16 API | OS API | 초기 Windows 시스템 API|
|1993 | Win32 API | OS API | 현대 Windows의 핵심 OS API|
|1995 | MFC | 프레임워크 | Win32 C++ 래퍼|
|1996 | COM | 컴포넌트 모델 | 바이너리 인터페이스 표준|
|2000 | ATL | 프레임워크 | COM 경량 C++ 래퍼|
|2002 | .NET CLR | 런타임 | 관리 코드 실행 환경|
|2012 | WinRT | OS 런타임 | 차세대 Windows API 모델|
|2021 | Windows App SDK | 앱 플랫폼 | WinRT + Win32 통합|

## Windows 그래픽 기술 연표

| 기술             | 첫 등장  | 분류         | 주 용도        | 사용 언어  | GPU 가속 | 비고                                               |
|-----------------|---------|-------------|---------------|-----------|-----|---------------------------------------------------------|
| GDI             | 1985    | 그래픽 API   | 기본 2D UI     | C / C++   | ❌ | 레거시 (지원은 됨)                                        |
| Win32 Controls  | 1993    | UI 컨트롤    | 표준 GUI       | C / C++   | ❌ | 윈도우가 제공하는 UI 컴포넌트 (내부적으로 GDI 사용)           |
| DirectDraw      | 1996    | 그래픽 API   | 2D 게임        | C++       | ⚠️ | 지원 안함                                                |
| Direct3D        | 1998    | 그래픽 API   | 3D / UI 렌더링 | C++       | ✅  |                                                        |
| GDI+            | 2001    | 그래픽 API   | 향상된 2D      | C++ / C#  | ❌  | 레거시 (지원은 됨)                                       |
| WPF             | 2006    | UI 프레임워크 | 데스크톱 GUI   | C# / XAML | ✅  |                                                        |
| Direct2D        | 2009    | 그래픽 API   | 고성능 2D UI   | C++       | ✅  | GDI대체제로 권장                                         |
| DirectWrite     | 2009    | 텍스트 API   | 텍스트 렌더링   | C++       | ✅  | GDI대체제로 권장 (텍스트 랜더링용)                         |
| WinRT XAML      | 2012    | UI 프레임워크 | 터치 UI        | C# / C++  | ✅ | 망함                                                    |
| UWP             | 2015    | 앱 모델      | 스토어 앱       | C# / C++  | ✅ | WinRT기반으로 구축된 앱 모델. 망함                          |
| WinUI 2         | 2018    | UI 프레임워크 | UWP UI        | C# / C++  | ✅  | WinUI 3로 대체                                          |
| WinUI 3         | 2021    | UI 프레임워크 | 최신 Win32 UI  | C# / C++  | ✅ | 가장 최신의 윈도우 UI 프레임워크                           |

#### 1세대: 고전 Win32 시대 (1985~2000)
- GDI
- Win32 Controls

CPU 기반, 메시지 루프 중심, 현재도 Windows의 뼈대

#### 2세대: DirectX 등장 (1996~2005)
- DirectDraw
- Direct3D
- GDI+

게임과 UI 렌더링이 분리되기 시작, DirectDraw는 실패

#### 3세대: GPU 기반 UI 도입 (2006~2010)
- WPF
- DWM
- Direct2D
- DirectWrite

Vista 시절 대격변, GPU가 UI를 직접 그리기 시작

#### 4세대: 모바일 따라가기 실패 (2012~2018)
- WinRT
- WinRT XAML
- UWP
- WinUI 2

Win32와 단절, 샌드박스, 스토어 강제, Windows Phone 몰락과 함께 붕괴

#### 5세대: Win32로 회귀 (2018~현재)
- WinUI 3
- Windows App SDK

Win32 유지, UI만 현대화, 현재 Microsoft의 공식 방향

## 비주얼 스튜디오

비주얼 스튜디오의 공유 프로젝트:
- 공통으로 사용할 수 있는 코드를 모아두는 프로젝트 유형
- 고유 프로젝트 자체는 직접적으로 실행되거나 빌드되지 않음. 참조하는 프로젝트의 일부로 빌드됨