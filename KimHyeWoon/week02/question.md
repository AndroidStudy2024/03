# week02
## 질문 : 코루틴에서 recyclerview 만들려면? 
기존 xml에서 `recylcerview`에 해당하는 뷰을 Compose의 `LazyColumn`, `LazyRow` 이용해서 구현할 수 있다. 

![image](https://github.com/AndroidStudy2024/03/assets/113662682/b1d049cc-3a64-4ff7-824a-16848ff13162)

![image](https://github.com/AndroidStudy2024/03/assets/113662682/28ae9c88-7105-42ac-9cf8-afd34a1a9374)



## 질문 : 람다함수에서 it은 언제 사용하는가 ? 
파라미터가 하나만 있는 경우 객체를 `it`으로 받아서 사용할 수있다. </br>
예시)
val upperCase5 :(String)->String={it.uppercase()} //파라미터 하나인 경우 

`람다함수` 타입추론과 암묵적 it 변수 이용해서 간결하게 람다함수 작성 가능 

val upperCase1:(String)->String={str: String ->str.uppercase()}
val upperCase2:(String) ->String ={str -> str.uppercase()}// 타임추론
val upperCase3 = {str: String -> str.uppercase()}//타입추론
//val upperCase4 ={str ->str.uppercase()}//타임추론 불가능
val upperCase5 :(String)->String={it.uppercase()} //파라미터 하나인 경우 
val upperCase6:(String)-> String= String::uppercase//람다가 딱 한번의 함수호출로 구성될 경우




