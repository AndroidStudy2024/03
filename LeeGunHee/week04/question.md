# 셋째 주

### **Android Flows 질문**

**1) Hot Stream과 Cold Stream의 차이점 (하)**  
Hot Stream은 collect 혹은 subscribe를 호출할 때마다 flow block이 호출되지 않는다.
즉 collect() 시점 이후에 emit된 데이터를 받게됩니다.
TV와 같다 지나간 데이터는 다시 수집하지 않음

Cold Stream은 collect() 혹은 subscribe를 호출할 때마다 flow block이 재실행됨
1~10까지 emit하는 것이 있으면 collect 할 때마다 매번 1~10을 전달받음
원하는 시점에 데이터 수집이 가능합니다.

**2) StateFlow와 SharedFlow의 차이점 (중)**  
StateFlow는 상태값을 가지고있기때문에 상태값을 다시 조회해야하는경우 사용해야합니다.  
RecyclerView Adapter의 item, searchQuery, count등 기존의 LiveData를 대체 가능
SharedFlow의 경우 상태값을 가지고 있지 않아 휘발성이 있는 이벤트에 사용 가능함
NavAction이나 toastMessage같은것에 사용

**3) StateHolder로 LiveData를 사용하는 경우 StateFlow로 이전할 때 고려해야할 사항은? (중)**  
StateFlow는 안드로이드 생명주기에 종속적이지 않으므로 수집과 해제를 직접 Lifecycle에 등록해줘야함, 만약 중복값에도 로직을 처리해야할경우 해당 사항을 고려해야함  
생명주기 상태의 어느지점에서 값을 수집할지 지정 가능
   
### **Kotlin Coroutine 질문**

**1) GlobalScope란?(하)**  
coroutine Scope는 각각의 생명주기를 가지고있어 종료할 수 있는 반면 
GlobalScope는 싱글톤으로 이루어져있고 안드로이드 생명주기에 연결되어있고
시스템 전반에 영향을 미칠 수 있다
  
**2) coroutine의 경우 자식 코루틴이 취소될 경우 부모 코루틴이 취소되는데 이런 경우를 방지하기 위해서는 어떻게 해야하는가 (하)**  
SupervisiorJob을 사용해서 특정 코루틴이 취소될경우 해당 exception을 부모나 자식 코루틴에 전파하지 않는다.
  
**3) suspend 키워드가 달린 함수는 컴파일 되었을때 어떻게 되는가 (중)**  
해당 함수의 마지막 파라미터로 continuation 객체가 생기며
해당 continuation 객체는 Any타입을 가지며 suspend 함수들의 반환값을 캐스팅해 다음 함수를 진행한다. 이 과정에서 재귀함수로 진행되며 continuation 객체에 라벨값이 존재하며
특정 분기마다 라벨값을 변경한다 내부적으로 콜백함수를 작성한다.
마지막 suspend 함수가 끝났을경우 원래 함수의 반환 타입으로 캐스팅하여 리턴한다.