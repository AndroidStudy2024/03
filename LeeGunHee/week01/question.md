# 첫번째 주

### **안드로이드 질문**

**1) DataBinding이 deprecated 되었는데 어떻게 할것인가 (중)**
- 현재 구글에서는 dataBinding의 대체자를 jetpack compose로 밀고있다. 예제를 보면 compose 예제가 늘고있다.
- compose로 작업하는것이 코드도 적게들고 kotlin만으로도 작업할 수 있어서 compose가 좋다고 생각한다.
- viewBinding으로 작업해서 activity나 fragment에 코드가 쌓이는것이 좋은 코드가 아니라고 생각한다.
- activity나 fragment의 경우 단순히 화면을 보여주기위한 이벤트나
  OS 상호작용 작업만 처리하는것이 좋기때문에 viewBinding을 선호하지 않는다.

**2) Paging 작업을 해본적이 있는가 왜 Paging을 사용하는가 (중)**
- 데이터를 효율적으로 관리할 수 있음
- Paging 데이터로 작업하는 동안 시스템 리소스를 효율적으로 사용 가능
- Paging jetpack 라이브러리의 경우 Coroutine과 Flow를 지원함

**3) Flow를 사용해본적이 있는가? 있다면 LiveData과 비교해서 장점 (중)**
- 두 라이브러리 다 State Holder로 적합함 (observable) 
- LiveData는 안드로이드 의존성이 있지만 Flow는 100% Kotlin으로 작성되어있기 때문에
  java/kotlin 모듈에서도 사용 가능함 (ex) domain layer)
- LiveData는 자동으로 안드로이드 생명주기에 따라 수집을 결정하지만 Flow는 직접 설정해줘야 함
  직접 생명주기에 달아줘야하는 단점이 있지만 마음대로 커스텀 가능
- 다양한 연산자로 많은 연산을 선언적으로 사용할 수 있음 
  
**4) StateFlow와 SharedFlow의 차이점 (중)**
- 둘다 Hot Stream으로서 다양한 소비자가 존재 가능함
- SharedFlow는 상태값 프로퍼티를 가지고 있음 즉 마지막에 수집된 값을 보관하고 있어서
  데이터의 상태를 확인해야하는 StateHolder로 사용하기 좋음 (RecyclerView Adapter의 List, 고유 상태값)
- SharedFlow는 상태값 프로퍼티가 없음
  그러므로 휘발성으로 날아가는 이벤트 호출에 좋음 네비게이션 이벤트나 toastMessage에 사용하기 좋음

### **Kotlin 질문***

**1) enum class와 sealed class의 차이점 (하)**
- sealed class는 추상 클래스로 상속받는 자식 클래스의 종류를 **제한**하는 특성을 가지고 있음
  자식 클래스의 종류를 제한하므로 when 구문의 else 브랜치를 만들지 않아도 되는 장점이 존재함
- enum class의 경우 iterate 가능함 그러므로 compose Bottom Bar의 item을 정의할때 사용할 수 있음
  
**2) 변수 생성시 val var 키워드 차이점 (중)**
- val은 변수가 **재 할당**이 불가능함 변수의 할당만 할 수 있을 뿐 중간에 변수를 재할당 할수는 없음
- var의 경우 변수 **재 할당**이 가능함
- val 변수의 타입의 프로퍼티가 var 타입이라면 해당 프로퍼티는 변경 가능

**3) lateinit과 by lazy의 차이점 (하)**
- lateinit은 var 키워드에서만 사용할 수 있으며 변수의 할당을 미룰 수 있음
  해당 변수가 초기화되지 않은채 사용한다면 UninitializedPropertyAccessException이 발생함
  NPE보다 직관적이며 에러를 찾기 쉬움
- by lazy는 해당 변수가 처음으로 사용될때 lazy 안의 람다가 실행됨
  메모리를 분산해서 사용한다는 장점이 존재함