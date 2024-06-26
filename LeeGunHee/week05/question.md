# 다섯째 주

### **Android 4대 컴포넌트 + Intent**

**1) 암시적 인텐트와 명시적 인텐트의 차이**  
명시적인텐트는 특정 컴포넌트를 호출할때 이름을 명시 해놓은것, 리플렉션을 이용해 사용합니다.  
암시적인텐트는 설정한 **인텐트 필터**에 부합하는것을 모두 호출해줍니다.  
검색결과 여러개가 나올 수 있고 한개도 나오지 않을 수 있습니다.  
명시적 인텐트를 사용해서 특정 컴포넌트를 호출할 수 있는 상황에 암시적 인텐트로 호출하는것은 비효율적입니다.  

**2) 4대 컴포넌트를 호출하려면 어떻게 해야하는가**  
4대 컴포넌트의 객체는 직접 생성한믄것이 아닌 시스템에서 생성하므로 Intent를 통해 호출해야 합니다.  

**3) 안드로이드는 필요에 따라 앱의 프로세스를 중단시킬 수 있습니다. 컴포넌트마다 우선순위를 설명해주세요**  
1. 포그라운드 프로세스  
   onResume이 호출된 Activity(현재 표시되고있는 Activity), 현재 작업중인 BroadCastReceiver, 콜백을 타고있는 Service  
2. 가시적 프로세스  
   onPause가 호출된 Activity, 포그라운드 서비스가 진행중인 Service  
3. 서비스 프로세스  
   startService로 시작된 서비스  
4. 캐시된 프로세스