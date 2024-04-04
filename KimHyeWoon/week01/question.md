# week01
##  질문 : 코틀린에서 ?, !!의 의미는 ? 
### ✔️` ? ` 이용해서 명시적으로 Nullable 표시해준다. </br>
변수 선언시 타입에 ?를 붙여서 nullable 선언해준다. ex) val name : String? = null </br>
### ✔️ ` !!  ` nullable 변수값이 null값이 아니라는 것 나타낼 때 사용한다.
하지만 '!!' 사용을 지양하고 있으므로 실제 사용할 때는 `엘비스 연산자(?:)` 를 이용하는 것이 더 좋다. 

 
## 질문 : 안드로이드   Activity 생명주기 ?

### ✔️ 생명주기 콜백 메서드

![image](https://github.com/AndroidStudy2024/03/assets/113662682/f786fbee-9a35-40ec-a992-b0ff677f3499)

### ✔️ 생명주기 호출 
* 액티비티 호출
![image](https://github.com/AndroidStudy2024/03/assets/113662682/e750c350-17fe-4670-bd0b-a17b817722d2)
  </br>
    </br>
* 액티비티 화면 제거
![image](https://github.com/AndroidStudy2024/03/assets/113662682/dbefa2cf-0e84-49b5-abf6-e5e850741e33)
  </br>
    </br>
* 액티비티를 종료하지 않고 다른 액티비티 실행
 ![image](https://github.com/AndroidStudy2024/03/assets/113662682/53a05c6d-60d5-4cf7-95f5-7ab74d707276)
  </br>
    </br>
* 액티비티 종료하지 않거나 모두 가져지지 않을 때 액티비티 실행
![image](https://github.com/AndroidStudy2024/03/assets/113662682/b9f65813-8fc0-47dc-81ed-e774bc0be0b3)

    </br>

* 참고사이트</br>
  https://blog.naver.com/lth9036/221572320853
  </br>
  https://developer.android.com/guide/components/activities/activity-lifecycle#saras
  





