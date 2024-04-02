# week02
## 질문 : 코루틴에서 recyclerview 만들려면? 
기존 xml에서 `recylcerview`에 해당하는 뷰을 Compose의 `LazyColumn`, `LazyRow` 이용해서 구현할 수 있다. 

![image](https://github.com/AndroidStudy2024/03/assets/113662682/b1d049cc-3a64-4ff7-824a-16848ff13162)

![image](https://github.com/AndroidStudy2024/03/assets/113662682/28ae9c88-7105-42ac-9cf8-afd34a1a9374)



## 질문 : 람다함수에서 it은 언제 사용하는가 ? 
`파라미터 하나인 경우`
`람다함수` 타입추론과 암묵적 it 변수 이용해서 간결하게 람다함수 작성 가능 
예시)
val upperCase5 :(String)->String={it.uppercase()} //파라미터 하나인 경우 



