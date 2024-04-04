# Week03 : Coroutine , Flow



### Coroutine

**동시성 문제를 일으키지 않고 공유 자원에 접근하는 방법은 무엇이 있나요**

- Mutex( ) : 공유된 자원에 대한 진입을 조절하여 동시 액세스를 제어
- Actor { } 빌더 : 상태를 캡슐화하고 메세지를 통해 상호 작용하는 독립적인 코루틴
- 세마포어 / 싱글 스레드  사용 등이 추가로 언급됨





**CoroutineScope 와 CoroutineConext 에 대해 설명해주세요**

CouroutineScope 는 코루틴의 범위와 생명주기를 관리합니다.

보통 특정한 스코프 내에서 코루틴을 실행하기 위해 사용할 때 사용하며 viewModelScope,  lifecycleScope 등 이 사용되며 , 코루틴 스코프는 범위 내에서 사용될 CoroutineContext를 가지고 있습니다. 코루틴 빌더 등의 함수는 모두 CoroutineScope의 확장 함수입니다.

CoroutineContext는 코루틴의 실제 실행 환경을 정의하는 개념입니다. 

코루틴 컨텍스트의 구성요소들의 예시 

- CoroutineDispatcher : 코루틴이 실행될 스레드나 스레드 풀을 지정
- CoroutineExceptionHanlder : 코루틴 내에서 발생한 예외를 처리하기 위한 핸들러
- CoroutineName : 코루틴에 이름을 부여하여 디버깅/로깅에 사용
- Job : 코루틴의 생명주기를 관리하고 취소할 수 있는 핸들



**viewModelScope 와 lifecycleScope**

viewModelScope는 ViewModel에서 사용되며, ViewModel의 수명 주기에 맞게 코루틴을 관리합니다. 일반적으로 ViewModel에 의해 보유된 데이터나 비즈니스 로직을 처리할 때 사용됩니다. 
viewModel 이 소멸될 때 (onCleared() 호출) viewModelScope 에 있는 모든 코루틴이 취소됩니다. 

lifecycleScope는 안드로이드 Jetpack 라이브러리에서 제공되며, LifecycleOwner(예: Activity, Fragment)의 수명 주기에 맞게 코루틴을 관리합니다. 이 범위는 액티비티나 프래그먼트의 수명 주기와 함께 코루틴을 실행하거나 중단시킬 때 사용됩니다. 
LifecycleOwner 가 소멸될 때 (onDestroy() 호출) lifecycleScope에 있는 모든 코루틴이 취소됩니다.



**화면이 회전될 때 viewModelScope 의 코루틴이 종료되지 않는 이유**

→ 화면 회전 시 fragment는 ondestroy → oncreate 과정을 거치는데 viewModel 에서는 화면 회전 이벤트를 조건문을 걸어 onCleared() 메소드를 호출하지 않는다.



**fragment backstack 시 viewModelScope 가 함께 cleared 되는 이유**

→ 기본적으로 viewModel 은 fragment 나 activity 보다 오래 지속됩니다. 

같은 화면의 여러 fragment 나 activity 간에 재사용되거나 유지될 수 있습니다.

하지만 일반적으로 Fragment 가 파괴될 때 Fragment와 연결된 ViewModel도 파괴되어 ViewModel에 의해 보유된 리소스가 정리됩니다. (메모리 누수 방지)



**ViewModel 의 onCleared() 호출 시점** 

- Activity 종료
- Fragment 분리
- 백스택에서 삭제



**Continuation**

Continuation은 코루틴이 일시 중단된 후에 다시 재개될 때 사용되는 개념입니다. 코루틴은 실행 중에 일시 중단될 수 있으며, 이때 코루틴이 다시 시작될 때 필요한 정보와 실행을 계속할 위치를 보유한 객체입니다.

코루틴이 일시 중단되면 해당 코루틴은 일시 중단된 지점 이후의 코드를 실행하지 않고, 코루틴을 실행한 스레드 또는 다른 스레드로 제어를 반환합니다. 이후 코루틴이 다시 시작되어 실행될 때는 해당 코루틴의 continuation을 통해 일시 중단된 지점 이후의 코드를 실행합니다.

코드 상에서 suspend fun 은 컴파일 할 때 continuation 객체를 파라미터로 가지고 있게 되며, suspend fun 은 이 객체에 중단 시점의 상태 정보를 저장합니다. 



**코루틴의 스케줄링 방식**

선점형 스케줄링 → 운영체제가 코루틴을 관리하고 실행하는 것을 의미한다 . 코루틴 실행중에 중단하고 다른 코루틴 실행될 수 있다

협동형 스케줄링 → 코루틴이 자체적으로 실행을 양보하고 제어권을 다른 코루틴에게 넘긴다. 코틀린이 채택한 코루틴 스케줄링 방식이다.





### Flow

1. **Flow의 개념과 사용 목적에 대해 설명해주세요.**
    
    Flow는 비동기적인 데이터 스트림을 처리하기 위한 Kotlin의 라이브러리입니다. 비동기적으로 데이터를 생성하고 소비할 수 있습니다.
    
    코루틴에서 Flow은 단일 값만 반환하는 *정지 함수*와 달리 여러 값을 순차적으로 내보낼 수 있는 유형입니다. 흐름(스트림)을 사용하여 데이터베이스에서 실시간 업데이트를 수신할 수 있습니다.


    
2. **Flow와 Sequence의 차이점은 무엇인가요.**
    
    둘 다 연속된 데이터의 처리할 수 있지만, flow 는 비동기적으로 데이터 스트림을 처리하는데 사용되며 비동기 작업을 지원합니다. sequence는 동기적으로 연속적인 데이터를 처리하는 데 사용되며 비동기 작업을 지원하지 않습니다.
    

    
3. **Flow의 Cold vs. Hot 특성에 대해 설명해주세요.**
    
    Cold Flow는 Flow가 수집되기 전까지 데이터를 생성하지 않는 것을 의미합니다. 즉, Flow를 수집하는 코루틴이 없는 경우 데이터가 생성되지 않습니다. 반면에 Hot Flow는 데이터가 생성되기 시작하면 Flow를 수집하는 코루틴과 관계없이 데이터가 생성됩니다.
