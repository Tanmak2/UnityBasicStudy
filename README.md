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

3. 정적(Static) 클래스(Class), 메소드(Method), 필드(Field)
```
정적 클래스란?

정적 클래스는 인스턴스화 할수없음
정적 클래스는 class 키워드 앞에 static 키워드를 선언해서 만듬
정적 클래스의 모든 멤버는 static으로 선언해야함
정적 클래스는 생성자를 포함할 수 없음
정적 클래스는 객체들이 처음 호출될 때 생성되고 프로그램이 종료될 때 해제되기 때문에 정적 클래스는 어디서든 접근 가능
전역적으로 접근해야 하는 유틸리티 클래스를 만들 때 정적 클래스로 만들면 유용
```
```cs
정적 클래스 예제

public static class Utils
{
    public static int Sum(int num1, int num2)
    {
        return num1 + num2;
    }

    public static string Log(string text)
    {
        return "로그기록 : " + text;
    }
}


using UnityEngine;

public class GameManager : MonoBehaviour
{
    void Start()
    {
        int add = Utils.Sum(5, 8);
        Debug.Log(Utils.Log("실행됨"));
    }
}
```

```
정적 메소드란?

정적 메소드는 인스턴스화 하지않아도 호출가능
정적 메소드는 static 키워드를 선언해서 만듬
정적 메소드는 메소드 내부에서 객체의 멤버를 참조할 수 없음
정적 메소드는 인스턴스에서는 호출할 수 없음
```
```cs
정적 메소드 예제

public class Converter
{
    public const float num = 2.54f;

    public static float InchToCentimeter(float inch)
    {
        return inch * num;
    }

    public static float CentimeterToInch(float centimeter)
    {
        return centimeter / num;
    }
}


using UnityEngine;

public class GameManager : MonoBehaviour
{
    void Start()
    {
        float inch = 24f;
        float centimeter = 100f;

        Debug.Log(Converter.InchToCentimeter(inch));
        Debug.Log(Converter.CentimeterToInch(centimeter));
    }
}
```

```
정적 필드란?

정적 필드는 인스턴스를 직접 생성하지 않고 접근할 수 있음
정적 필드는 자료형 앞에 static 키워드를 선언해서 만듬
정적 필드는 어디서든 접근 가능
```

```cs
public class Car
{
    public static int count = 0;

    private string name;

    public Car (string name)
    {
        this.name = name;
        count++;
    }
}

using UnityEngine;

public class GameManager : MonoBehaviour
{
    void Start()
    {
        Car car1 = new Car("K5");
        Car car2 = new Car("G90");

        Debug.Log("Car Count : " + Car.count);
    }
}
```