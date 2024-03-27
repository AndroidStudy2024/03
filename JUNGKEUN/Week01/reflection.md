## 첫 스터디 진행 절차는 야심차게(?) 다음과 같이 준비함

1. icebreaking: 편하게 간단한 자기소개  
    - “나는 왜 취업이 절실한가” 한번 고민해보고 와서 공유해주시면 좋습니다
      
2. diagnostic test: 자기 스스로 상태(?) 점검용 모의 면접  
    - 진짜 면접 대비하기 위함이 아니라, “내가 진짜 빡세게 준비해야겠구나” 느끼고 동기부여하기 위함입니다  
    - 안드로이드/코틀린 관련 예상 면접 질문 최소 5~10개 텍스트로 준비해주세요  
        - 내가 면접관이라고 생각하고, 핵심적인 주제/지엽적인 주제, 난이도 하/상 고려해서 선별해주시면 좋습니다  
        - 자바와의 비교나 CS 지식이 포함된 질문도 OK (저도 잘 모르지만 실제 면접에 충분히 나올 수 있음)  
        - 내가 완벽하게 답할 수는 없어도 대충이라도 답할 수 있게 아는 내용 위주로 해주세요 (이번에 찾아보고 공부해서 새롭게 알게 된 내용도 Good)  
        - 개수가 많다고 생각할 수 있지만 겹칠 가능성 고려해서 정했고, 이상 목표치니 너무 부담 갖지 마세요  
    - 진행 방식은, 한 명씩 교대로 질문 공유하고, 공유자 외 나머지 팀원들이 교대로 답변 시도(?)하고 아예 모르는 주제면 패스하면 됩니다~  
      
3. diagnostic test review: 모의 면접 복기 및 리뷰  
    - 질문별로 하나씩 리뷰하면서, 답변 내용 중에 틀린 부분 있으면 서로 고쳐주고 잘한 부분 있으면 칭찬해주면 됩니다  
    - 모의 면접을 쭉 진행한 다음, 리뷰를 할까 하는데 병렬 진행도 괜찮구요  
      
4. plan:  추후 안드로이드/코틀린 스터디 주제 토의 및 선정  
   
6. plan ii: 자바, CS, 코테 등 기타 주제 관련 토의 및 선정  

> 내가 시간 관리에 소홀한 바람에 모의 면접과 리뷰만 진행했고, 다음 스터디 주제를 의논할 시간이 없었음  
> 급한 대로 Compose + 코틀린 함수로 결정!  

## 모의 면접 질의 응답 사이클을 생각보다 몇 번 못 돔

- <img src="../res/jungkeun.png" alt="jungkeun" width="24"/> 정근: Scope Function이 무엇이 있는지 간단히 설명해주시고, 프로젝트에 어떻게 활용했는지 소개해주세요  

- <img src="../res/heepyo.png" alt="heepyo" width="24"/> 희표: Abstract Class와 Interface의 차이를 설명해주세요.  

- <img src="../res/seungmin.png" alt="seungmin" width="24"/> 승민: 안드로이드 4대 컴포넌트에 대해 설명해주세요.  

- <img src="../res/gunhee.png" alt="gunhee" width="24"/> 건희: 변수 생성시 val var 키워드 차이점  

- <img src="../res/hyewoon.png" alt="hyewoon" width="24"/> 혜운: 액티비티 생명주기는?  

- <img src="../res/jungyun.png" alt="jungyun" width="24"/> 정현: 큐와 스택의 차이  

- <img src="../res/hyewoon.png" alt="hyewoon" width="24"/> 혜운: 코틀린에서 ?, !! 의미는? 코루틴과 스레드의 차이?  

- <img src="../res/jungkeun.png" alt="jungkeun" width="24"/> 정근: 멀티스레드 환경의 동시성 문제를 설명해주시고, MutableStateFlow가 어떻게 이 문제에 대응해 Thread-safe한지 설명해주세요  

> 마지막에 수소폭탄급 고난도 질문을 투척해버림;;  
> 건희님이 선방  

## 복기

### Abstract Class VS Interface

> **추상의 역설**  
> : 추상을 이해하려면 구체를 기억하라

갑자기 차이를 설명하려니 헷갈림  
플젝의 활용 사례를 떠올리며 차근차근 정리해보자  

```
abstract class PreloadFragment : Fragment() {

    protected abstract val viewModel: LoginViewModel

    protected suspend fun preloadProfileImage(currentUser: FirebaseUser?) {
        ...
        Glide.with(requireContext())
            .load(storageRef)
            .preload()
    }
}
```

```
interface UserService {

    @GET("$REMOTE_DATABASE_USERS/{id}.json")
    suspend fun getRemoteUserById(@Path("id") id: String): UserDTO
}
```

근데 코드 스니펫만 봐서는 둘의 차이를 짐작할 수 없음!!  
대충 IDE Lint의 도움을 받아 테스트해본 결과,  

|          | 추상 클래스 | 인터페이스 |
| -------- | -------- | ------- |
|   생성자   |    O     |    X    |
|  멤버 변수  |    O    | property initializer는 안 되고, getter만 됨 |
|   메서드   |    O    |     O   |
|    상속    |   단일   |    다중   |

멤버 변수 얘기를 다르게 하면, 인터페이스는 **필드를 가질 수 없다**  
그 이유는 다음에..  
여기서 꼭 기억하고 넘어갈 부분은, **둘 다 추상, 구체 프로퍼티와 메서드가 허용된다는 것!**  
그리고 특이사항은, abstract 키워드가 inheritance modifier로서 open의 의미를 포괄하기 때문에  
클래스 자체의 상속은 허용되나, 개별 멤버들은 open 없이 상속 불가  

> 사실 이런 기술적인 차이들보다, 각각의 존재론적(?) 의의가 어떻게 다른지가 핵심  
> 추상 클래스는 여러 클래스들의 공통분모를 뽑아서 베이스가 되는 클래스를 추상화시켜놓은 개념이라면,  
> 인터페이스는 대략적인 목적과 동작 방식을 정해 놓은 클래스의 인스턴스를 다양한 방식으로 구현시킬 수 있도록 추상화시켜놓은 개념  
> *by 내피셜*  

### 안드로이드 4대 컴포넌트

무려 App Fundamentals 섹션에 실린 내용  
[공식문서피셜 4대 컴포넌트](https://developer.android.com/guide/components/fundamentals)  
Fundamental-less (근본없는) 나는 다음에 공부하기로..  
한 가지 기억할 건, 컴포넌트끼리 소통할 때, **Intent 활용한다는 것**  

### Activity Lifecycle

Lifecycle이라 하면, 대충 Lifecycle State와 Lifecycle Callback을 아우르는 뜻으로 받아들이자  
created -> started -> resumed -> RUNNING -> paused -> stopped -> destroyed  
RUNNING -> paused -> resumed -> RUNNING  
RUNNING -> paused -> stopped -> restarted -> started -> resumed -> RUNNINNG

> 여기서 핵심은, **앱이 Resumed 상태일 때, 비로소 뷰가 다 그려지고 유저와 상호작용이 가능해진다는 것**  
> 그리고 Resumed -> Paused 넘어가는 경우는, 앱이 **더 이상 focus를 받지 못하고 foreground에서 사라질 때**  
> (앱을 사용하다 갑자기 전화를 받는다거나, 멀티 윈도우 모드에서 다른 앱을 클릭한다거나, 등등)  
> 또한 액티비티가 종료되기 전에 유저 데이터를 저장하고 싶다면?
> **onPause 말고 onStop에서** 처리!  

### Stack VS Queue

컴퓨터에서 스택은, 함수의 콜스택이라는 굉장히 친숙한 사용처가 존재  
그렇다면 안드로이드 OS에서는?  
바로 젯팩 내비게이션의 **NavBackStackEntry**!  
그럼 큐는??  
~~모르겠다~~  
예약 시스템을 구현할 때, 큐를 사용하면 될 거 같은데, 여기서 기습 질문이 들어옴  

*큐의 중간에 있는 값을 삭제하고 싶다면?!*  

처음 든 생각은, 맨 앞부터 해당 인덱스까지 전부 삭제하고 그 전까지 다시 생성해서 나머지를 덧붙이면 안 되나..? (~~겁나 비효율적일 듯~~)  
모의 면접관(?)님의 답변은 큐로는 불충분하고 인덱스 정보까지 포함한 ???을 활용해야 함  
기억 안 나서 대충 찾아 보니, **LinkedList**가 그 주인공인 듯  
[참고](https://stackoverflow.com/questions/45798281/how-to-remove-a-specific-element-from-queue-in-javanot-priority-queue)  

-- To be continued..
