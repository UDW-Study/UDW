# Direct3D 11

## IUnknown

참조 카운팅 및 uuid기반 캐스팅을 지원하는 모든 Com 인터페이스의 루트   
Com = Component Object Model

멤버 함수:
| 함수 | 설명 |
|---|---|
| `HRESULT QueryInterface(REFIID riid, void **ppvObject)` | 객체가 지원하는 다른 인터페이스를 요청하는 함수 |
|`HRESULT QueryInterface(Q**)`| 템플릿 인자 Q로 `__uuidof` 를 자동 호출하는 버전 |
| `ULONG AddRef()` | 참조 카운트 증가. 반환값은 증가된 참조 카운트 값 |
| `ULONG Release()` | 참조 카운트 감소. 반환값은 감소된 참조 카운트 값. 참조 카운트가 0이 되면 자기 자신을 삭제함. |

QueryInterface 추가설명:
- riid : 요청하는 인터페이스의 IID
- ppvObject : 성공 시 해당 인터페이스 포인터 반환

Com에서는 클래스 타입을 직접 캐스팅하지 않음. 인터페이스를 질의하여 가져와야 함.
성공 시 AddRef 호출됨

## ComPtr

IUnknown에 들어있는 레퍼런스 카운팅을 RAII 형태로 자동화 해주는 스마트 포인터

IUnknown을 상속받은 Com 인터페이스만 템플릿으로 사용 가능함. 모든 객체를 지원해야 하는 shared_ptr과 다르게 ComPtr은 Com 인터페이스만을 대상으로 하므로 컨트롤 블록을 따로 가지지 않음.

D3D의 API는 실행의 성공 여부를 반환값으로 받고 (`HRESULT` 등), 실제 실행 결과는 OUT 파라미터로 받는 패턴을 주로 사용함. OUT 파라미터는 대부분 더블 포인터임. ComPtr의 `GetAddressOf()` 함수로 더블 포인터를 얻어 쉽게 전달 가능

기본 정보:
- Header: `wrl.h` or `wrl/client.h`
- Namespace: `Microsoft::WRL`

멤버 함수:
| 함수 | 설명 |
|---|---|
| `T* Get()` | 원본 포인터 리턴 |
| `T** GetAddressOf()` | 원본 포인터의 포인터를 리턴 |
| `unsigned long Reset()` | 원본을 null로 설정하고 참조 카운트 감소 (comptr = nullptr 을 사용해도 같은 효과) |

추가 내용:
- `template<class U> friend class ComPtr;`
- 서로 다른 템플릿 인스턴스가 상대의 private 멤버 접근가능

## ID3DBlob

DirectX에서 여러 용도로 사용하는 단순한 메모리 버퍼 인터페이스. 메모리에 대한 void형 포인터와 크기를 가지고 있음. 컴파일된 셰이더 바이트코드를 넣거나, 에러 메시지를 받을때도 사용함.   
BLOB = Binary Large Object

기본 정보:
- Header: `d3dcommon.h`
- `IUnknown` 에서 상속됨

멤버 함수:
| 함수 | 설명 |
|---|---|
| `LPVOID GetBufferPointer()` | 데이터에 대한 포인터를 가져옴 |
| `SIZE_T GetBufferSize()` | 데이터의 크기를 가져옴 |

## __uuidof

어떤 클래스에 연결된 UUID 값을 가져올 때 사용

```c++
// Visual C++에서 독자적으로 확장한 구문의 경우, __declspec 예약어를 사용
#define DECLSPEC_UUID(x) __declspec(uuid(x))
#define DECLSPEC_NOVTABLE __declspec(novtable)
#define MIDL_INTERFACE(x) struct DECLSPEC_UUID(x) DECLSPEC_NOVTABLE

MIDL_INTERFACE("08CD54FE-75C1-4BF4-99FC-C2ED9237A9A8")
Test
{
public:
    void Do() { }
};

int main() {
    GUID guid1 = __uuidof(Test);
}
```

즉 클래스마다 uuid를 기록해놓고, 나중에 이를 가져와서 인터페이스 변환 등에 사용함   
[UUID 스펙](http://www.webdav.org/specs/draft-leach-uuids-guids-01.txt)

