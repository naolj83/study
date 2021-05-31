# 객체지향프로그래밍1

## 1.2 객체지향언어의 장점

    1. 코드의 재사용성이 높다.
        - 새로운 코드를 작성할 때 기존의 코드를 이용하여 쉽게 작성할 수 있다.
    2. 코드의 관리가 용이하다.
        - 코드간의 관계를 이용해서 적은 노력으로 쉽게 코드를 변경할 수 있다.
    3. 신뢰성이 높은 프로그래밍을 가능하게 한다.
        - 제어자와 메서드를 이용해서 데이터를 보호하고 올바른 값을 유지하도록 하며, 코드의 중복을 제거하여 코드의 불일치로 인한 오작동을 방지할 수 있다.

=> 재사용성, 유지보수, 중복된 코드의 제거   
<br>

## 2.클래스와 객체

## 2.1 클래스와 객체의 정의와 용도

    클래스의 정의 - 클래스란 객체를 정의해 놓은 것이다.
    클래스의 용도 - 클래슨는 객체를 생성하는데 사용된다. 
<br>

    객체의 정의 - 실제로 존재하는 것, 사물 또는 개념
    객체의 용도 - 객체가 가지고 있는 기능과 속성에 따라 다름
<br>
=> 클래스는 설계도, 객체는 제품<br>
객체지향이론에서는 유형적인 것 뿐만 아니라 개념이나 논리와 같은 무형적인 것들도 객체로 간주한다. 프로그래밍에서의 객체는 클래스에 정의된 내용대로 메모리에 생성된 것을 뜻한다.

<br>

## 2.2 객체와 인스턴스

    클래스 --------------> 인스턴스(객체)
             인스턴스화

인스턴스는 객체와 같은 의미이지만, 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖고 있으며, 인스턴스는 어떤 클래스로부터 만들어진 것인지를 강조하는 보다 구체적인 의미를 갖고 있다.   
ex) '책상은 인스턴스다' -> '책상은 객체다'   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; '책상은 책상 클래스의 객체다' -> '책상은 책상 클래스의 인스턴스다'

<br>

## 2.3 객체의 구성요소 - 속성과 기능
객체는 속성과 기능, 두 종류의 구성요소로 이루어져 있다.   
즉, 객체는 속성과 기능의 집합이라고 할 수 있다.   
객체가 가지고 있는 속성과 기능을 그 객체의 멤버라 한다.

    속성(property) - 멤버변수(variable)
    기능(function) - 메서드(method)

<br>

## 2.4 인스턴스의 생성과 사용

    클래스명 변수명;            // 클래스의 객체를 참조하기 위한 참조변수를 선언   
    변수명 = new 클래스명();    // 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장

=> 인스턴스는 참조변수를 통해서만 다룰 수 있으며, 참조변수의 타입은 인스턴스의 타입과 일치해야한다.   
참조변수에는 하나의 값(주소)만이 저장될 수 있으므로   
둘 이상의 참조변수가 하나의 인스턴스를 가리키는(참조하는) 것은 가능하지만   
하나의 참조변수가 여러 개의 인스턴스를 가리키는 것을 불가능하다.

<br>

## 2.5 객체 배열
많은 수의 객체를 다뤄야 할 때, 배열로 다루면 편리할 것이다. 객체 배열 안에 객체가 저장되는 것은 아니고, 객체의 주소가 저장된다. 사실 객체 배열은 참조변수들을 하나로 묶은 참조변수 배열인 것이다.   

    Tv tv1, tv2, tv3;    ------>    Tv[] tvArr = new Tv[3];     // 길이가 3인 Tv타입의 참조변수 배열

&nbsp;&nbsp;tvArr&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tvArr[0]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tvArr[1]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tvArr[2]   
&nbsp;0x100&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;----->&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;null&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;null&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;null   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ox100   

=> 객체의 배열을ㄹ 생성하는 것은, 그저 객체를 다루기 위한 참조변수들이 만들어진 것일 뿐, 아직 객체가 저장되지 않았다. 객체를 생성해서 객체의 배열의 각 요소에 저장한는 것을 잊으면 안된다.   

    Tv[] tvArr = new Tv[3];     // 참조변수 배열(객체 배열)을 생성

    // 객체를 생성해서 배열의 각 요소에 저장
    tvArr[0] = new Tv();
    tvArr[1] = new Tv();
    tvArr[2] = new Tv();

    // 한 줄로 작성
    Tv[] tvArr = { new Tv(), new Tv(), new Tv() };

    // 객체의 수가 많을 때는 for문 사용
    Tv[] tvArr = new Tv[100];

    for (int i=0; i < tvArr.length; i++) {
        tvArr[i] = new Tv();
    }
=> 모든 배열이 그렇듯이 객체 배열도 같은 타입의 객체만 저장할 수 있지만 '다형성'을 배우면 하나의 배열로 여러 종류의 객체를 다룰 수 있게 된다.

<br>

## 2.6 클래스의 또 다른 정의
객체지향 관점 - 클래스는 '객체를 생성하기 위한 틀' 이며 '클래스는 속성과 기능으로 정의되어 있다'   

프로그래밍 관점 -
1. 클래스 - 데이터와 함수의 결합   
프로그래밍언어에서 데이터 처리를 위한 데이터 저장형태의 발전과정은 다음과 같다.   
변수&nbsp;&nbsp;&nbsp;&nbsp;------>&nbsp;&nbsp;&nbsp;&nbsp;배열&nbsp;&nbsp;&nbsp;&nbsp;------>&nbsp;&nbsp;&nbsp;&nbsp;구조체&nbsp;&nbsp;&nbsp;&nbsp;------>&nbsp;&nbsp;&nbsp;&nbsp;클래스   

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 1&nbsp;&nbsp;&nbsp;&nbsp;   
---------- | ---------- | ---------- | ----------   
&nbsp; | 2 | 10.0f | 10.of   
&nbsp; | 3 | 'a' | 'a'
&nbsp; | | | + 함수   
    1. 변수 - 하나의 데이터를 저장할 수 있는 공간
    2. 배열 - 같은 종류의 여러 데이터를 하나의 집합으로 저장할 수 있는 공간
    3. 구조체 - 서로 관련된 여러 데이터를 종류에 관계없이 하나의 집합으로 저장할 수 있는 공간
    4. 클래스 - 데이터와 함수의 결합(구조체 + 함수)
=> 자바와 같은 객체지향언어에서는 변수(데이터)와 함수를 하나의 클래스에 정의하여 서로 관계가 깊은 변수와 함수들을 함께 다룰 수 있게 했다.   
<br>

2. 클래스 - 사용자정의 타입(user-defined type)
프로그래머가 서로 관련된 변수들을 묶어서 하나의 타입으로 새로 추가하는 것을 사용자정의 타입이라고 한다.   
자바와 같은 객체지향언어에서는 클래스가 곧 사용자 정의 타입이다.

<br>

## 3. 변수와 메서드
## 3.1 선언위치에 따른 변수의 종류

``` java
class variables {
    int iv;             // 인스턴스변수
    static int cv;      // 클래스변수(static변수, 공유변수)

    void method() {
        int lv = 0;     // 지역변수
    }
}
```
변수의 종류 | 선언위치 | 생성시기 
:---:|:---:|:---:|
클래스변수(cv) | 클래스 영역 | 클래스가 메모리에 올라갈 때
인스턴스변수(iv) | 클래스 영역 | 인스턴스가 생성되었을 때
지역변수(lv) | 클래스 영역 이외의 영역<br>(메서드, 생성자, 초기화 블럭 내부) | 변수 선언문이 수행되었을 때

<br>
1. 인스턴스변수(instance variable)<br>
클래스 영역에 선언되며, 클래스의 인스턴스를 생성할 때 만들어진다. 인스턴스마다 고유한 상태 를 유지해야하는 속성의 경우, 인스턴스 변수로 선언한다.
<br><br>
2. 클래스변수(class variable)<br>
클래스 변수를 선언하는 방법은 인스턴스 변수 앞에 static을 붙이기만 하면 된다. 인스턴스변수와는 달리, 한 클래스의 모든 인스턴스들이 공통적인 값을 유지해야하는 속성의 경우, 클래스변수로 선언해야 한다. 클래스 변수는 인스턴스를 생성하지 않고도 언제든지 바로 사용 가능하며, '클래스이름.클래서변수'와 같은 형식으로 사용한다.<br>
ex) Variable.cv
<br><br>
3. 지역변수(local variable)<br>
메서드 내에 선언되어 메서드 내에서만 사용 가능하며, 메서드가 종료되면 소멸되어 사용할 수 없게 된다. 블럭 내에서 선언된 지역변수는 블럭{}을 벗어나면 소멸되어 사용할 수 없게 된다.<br>

    인스턴스변수는 인스턴스가 생성될 때 마다 생성되므로 인스턴스마다 각기 다른 값을 유지할 수 있지만, 클래스 변수는 모든 인스턴스가 하나의 저장공간을 공유하므로, 항상 공통된 값을 갖는다.

<br>

## 3.3 메서드
