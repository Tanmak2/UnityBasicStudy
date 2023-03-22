# 유니티 기본 공부(순서없음)

1. 열거형
```
열거형이란?

상수의 일종으로 const 키워드 대신 enum을 사용
열거형은 const와 다르게 값을 입력하지 않아도 자동으로 0,1,2,3... 대입
```
```
열거형의 장점

1. 코드가 단순해지며 가독성이 좋음
2. 상수이므로 if문, switch문에 사용할 수 있음
3. 키워드 enum을 사용하기 때문에 구현의 의도가 열거임을 분명하게 나타낼 수 있음
```
```cs
열거형 사용법

enum State { Idle, Walk, Attack, Dead};

State state = State.Idle;
```

|이전|이후|
|----|----|
|<pre><code>public int IDLE = 0;<br>public int WALK = 1;<br>public int ATTACK = 2;<br>public int DEAD = 3;<br><br>int state = IDLE;<br><br>void Start(){<br><br>}<br><br>void OnMouseDown(){<br><br>    state = DEAD;<br><br>    if (state == DEAD) { Debug.Log("죽음"); }<br>}</code></pre>|<pre><code>enum State { Idle, Walk, Attact, Dead};<br><br>State state = State.Idle;<br><br>void Start(){<br><br>}<br><br>void OnMouseDown(){<br><br>    state = State.Dead;<br><br>    if (state == State.Dead) { Debug.Log("죽음"); }<br><br>}<br><br><br></code></pre>|

2. 프로퍼티(Property)
```
프로퍼티란?

프로퍼티는 속성이라는 의미를 가짐
클래스에서 멤버 변수를 속성이라고도 함
정보은닉을 위해 private로 선언하여 해당 변수가 선언된 클래스 외부에서 접근 불가
getter, setter 메소드를 구현해야함
```
```cs
프로퍼티 사용법

class Car{
    private int displacement;
    public int GetDisplacement() { return displacement; }
    public void SetDisplacement(int num) { this.displacement = num; }
}
```
```cs
프로퍼티 기본 구조

class Car{
    private int displacement;

    public int Displacement{
        get{
            return displacement;
        }
        set{
            displacement = value;
        }
    }
}
```
```
프로퍼티 특징

1. 프로퍼티를 사용하면 클래스가 구현 또는 코드를 숨기는 동시에 값을 가져오고 설정하는 방법을 공개적으로 노출
2. get 속성 접근자는 속성 값을 반환하고, set 접근자는 새 값을 할당하는데 상용
3. set 접근자의 value 키워드는 set 접근자가 할당하는 값을 정의
4. set 접근자만을 구현하면 쓰기 전용, get 접근자만을 구현하면 읽기 전용
```
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CarController : MonoBehaviour
{
    private int displacement;

    public int Displacement{
        get{
            return displacement;
        }
        set{
            if(value < 1000){
                Debug.Log("배기량이 1000cc 이하는 등록이 불가합니다.");
            }
            else{
                displacement = value;
                DisplacementChange();
            }
        }
    }

    void Start(){
        Displacement = 950;
        Displacememt = 1599;
    }

    void DisplacementChange(){
        Debug.Log("배기량이 등록되었습니다.")
    }
}

```