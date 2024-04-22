# 넷째 주

### **Android RecyclerView, Paging**

**1) RecyclerView의 Adapter의 데이터가 변경될 때 어떻게 효율적으로 변경하는가**  
ListAdapter의 경우 DiffUtil을 구현하면 Adapter에 데이터가 변경되었을 경우  
변경된 데이터를 조회 후 변경된것만 View를 다시 그려주는 방식  
RecyclerView.Adapter의 경우 notifyXXX 메서드를 이용해 효율적으로 변경 가능  

**2) Paging2에서 Paging3로 이전을 할 때 어떤 사항들을 고려해야 하는가**  
Paging2는 현재 deprecated 되었습니다.  
Paging3는 LiveData와 Flow, Rx를 최고수준으로 지원합니다.  
Paging3는 선택적으로 RemoteMediator를 사용해 서버에서 불러오는 데이터를 미리 캐싱해놓을 수 있습니다.  
Paging3는 Adapter에서 현재 로딩 상태를 조회 가능하기 때문에 로딩 상태에 따른 대응을 쉽게 할 수 있습니다.  

**3) Paging3에서 PagingData를 Flow로 사용할 때 주의해야할 사항은?**  
Paging3 코드랩에도 있던 주의사항.  
Flow를 사용할 때 stateIn 함수를 이용해 stateFlow를 사용하는것보다  
Paging3 라이브러리의 확장함수인 cachedIn 함수를 사용하는것이 보다 안전함  

Flow를 View 단에서 collect할때 collect 대신 collectLatest를 사용해야 합니다.  
Paging의 경우 데이터를 flow에 저장할때 다음번의 페이징 데이터 요청이 발생했을 때  
flow의 수집을 중단하고 새로운 데이터를 요청하는것이기 때문에 collectLatest함수를 사용해야 합니다.  
   
### **Kotlin Generics**

**1) Generic이란?**  
generic은 클래스나 메서드, 프로퍼티를 정의할 때 데이터 타입을 변수로 지정하고, 사용할 때 그 타입을 정해줄 수 있는 것  
특정 타입을 정할 때 Any 타입으로 모든것을 열어줄 수 없기때문에 코드의 일관성을 높이기위해 사용합니다.
  
**2) 공변성과 반공변성이란?**  
공변성은 특정 자료형을 할당할 때 해당 자료형의 상위타입 까지 받을 수 있는것  
반공변성이란 특정 자료형을 할당할 때 해당 자료형의 하위타입까지 받을 수 있는것
제네릭의 제약을 조금 풀어주는 형태로 사용할 수 있다.
  
**3) generic 예시**  
StateFlow나 RecyclerView의 Adapter와 ViewHolder