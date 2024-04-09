# 코루틴
## launch vs async
 * 둘다 코루틴을 생성하는 코루틴 빌더
 * 코루틴 스코프내에서만 사용가능

  launch : fire & forget
  비동기작업을 요청하고 자기 할 일 하는 경우에 주로 사용
  생성된 작업을 의미하는 job을 리턴
  취소 : job을 이용하여 job.cancel() 

  async : fire & wait
  Deffed<T>를 리턴 -> await()로 코루틴을 중단시키면서 값을 기다릴 수 있음
