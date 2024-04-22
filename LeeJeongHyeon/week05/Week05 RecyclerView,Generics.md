# Week05:
RecyclerView,Generics


### RecyclerView

**RecyclerView의 Adapter 데이터 업데이트 시 어떻게 효율적으로 변경 가능한가?**

ListAdapter 의 DiffUtil 과, Payloads 등의 방법을 통해 효율적으로 데이터 업데이트가 가능합니다

ListAdapter 의 DiffUtil은 두 데이터셋을 받아서 그 차이를 계산해주는 클래스로 변경된 부분만을 파악하여 반영할 수 있습니다. 

DiffUtil 의 메소드는 areItemsTheSame() 과 areContentsTheSame() 이 있으며, 각각 id 값을 비교하고 , 내부 값을 비교하는 작업을 수행합니다.

이 외에도 adapter 에서 제공하는 notifyItem 메소드를 사용해서 ViewHolder 내용을 갱신할 수 있습니다. 
<br>
<br>

**RecyclerView 의 컴포넌트**

RecyclerView 는 컴포넌트 기반 아키텍쳐로, 컴포넌트들이 서로 상호작용하여 하나의 목록형 레이아웃을 동작하게 합니다.

1. RecyclerView 
2. Layout Manager : ItemView를 올바를 위치에 배치해주는 컴포넌트
3. Item Animator : ItemView의 애니메이션을 담당하는 컴포넌트 
4. Adapter : RecyclerView 에 ItemView를 제공하고, Viewholder를 생성하는 컴포넌트

(ViewHolder 는 ItemView 재사용을 위해 추적 관측하는 용도로 사용하는 컴포넌트)
<br>
<br>

**ItemTouchHelper.Callback 의 주요 메소드**

- **getMovementFlags(RecyclerView, ViewHolder)**
    
    각각의 뷰에 수행할 수 있는 작업을 컨트롤 하기 위해서는, getMovementFlags(RecyclerView, ViewHolder) 메소드를 오버라이드하고 적절한 방향을 반환해야 합니다. makeMovementFlags(int, int)를 사용하여 쉽게 구성할 수도 있습니다. 또는 SimpleCallback을 사용할 수도 있습니다.
    
- **onMove(recyclerView, dragged, target)**
    
    만약 사용자가 아이템을 드래그한다면, ItemTouchHelper는 onMove를 호출합니다. 이 콜백 메소드를 받으면 어댑터에서 아이템을 이전 위치(dragged.getAdapterPosition())에서 새로운 위치(target.getAdapterPosition())로 이동해야 하고, RecyclerView의 Adapter에서 notifyItemMoved(int, int)를 호출해야 합니다.
    
- **onSwiped(ViewHolder, int)**
    
    View가 스와이프되면 ItemTouchHelper는 범위를 벗어날 때까지 View를 애니메이션화한 다음 이 메소드를 호출합니다. 여기서 어댑터를 업데이트 해야하고 관련된 Adapter의 notify 이벤트를 호출해야 합니다.
    
<br>
<br>

**Adapter 에 데이터를 보낼때 submit() 과 notifyItem 메소드의 차이** 

리스트 전체를 수정할 경우 notifyDataSetChanged() 를 사용해야하는데, 이는 모든 항목을 다시 그리기때문에 권장사항이 아니다. 
리스트 전체를 보낼경우 submit() 이 권장되며 item 하나의 수정이 이뤄져야하거나 하나의 아이템이 삽입/삭제 되는 경우 notifyItem 메소드가 권장됩니다.
<br>
<br>
<br>

### Generic

**제네릭이란 ? , 제네릭 사용시 장점**

**< T >** 와 같은 문법으로 작성되며, 클래스나 인터페이스 혹은 함수 등에서 동일한 코드로 여러 타입을 지원해주기 위해 사용됩니다. 

한가지 타입에 대한 템플릿이 아니라 여러가지 타입을 사용할 수 있는 클래스 같은 코드를 간단하게 작성할 수 있습니다. (재사용성)
<br>
<br>

**in , out 을 사용해야하는 이유** 

in , out 은 각각 반공변성과 공변성을 부여하기 위해 제네릭에서 사용되는 키워드입니다. 

일반적으로 List<> 에 담긴 type 이 하위 타입 객체라고 하더라도, List 이기에 상/하위 관계가 적용되지않는다.

그런데 out 키워드를 사용 시 공변성을 가지게 되고, 상위타입으로 반환하는 것이 가능합니다. 

즉 , Collection 의 상하위 관계를 지정하는 용도로 사용되며 이를 통해 타입 안정성 보장이 가능합니다. 

(공변성이란 상/하위 타입과의 관계가 유지되는 성질을 의미합니다.)

```jsx
open class Fruit
class Banana : Fruit()

fun toFruits(banana: Banana): List<out Fruit> {
    return listOf(banana)
}
```