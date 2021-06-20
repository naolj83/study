# 객체지향프로그래밍2

##  1. 상속(inheritance)
## 1.1 상속의 정의와 장점
상속이란, 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다. 상속을 통해서 클래스를 작성하면 보다 적은 양의 코드로 새로운 클래스를 작성할 수 있고 코드를 공통적으로 관리할 수 있기 때문에 코드의 추가 및 변경이 용이하다.
```java
class Child extends Parent {

}
```
    조상 클래스 - 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스
    자식 클래스 - 자식(child)클래스, 하위(sub)클래스, 파생된(derived)클래스

자손 클래스는 조상 클래스의 모든 멤버를 상속받기 때문에, Child클래스는 Parent클래스의 멤버들을 포함한다고 할 수 있다.
조상 클래스가 변경되면 자손 클래스는 자동적으로 영향을 받지만, 자손 클래스가 변경되는 것은 조상 클래스에 아무런 영향을 주지 못한다.   

    - 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다.
    - 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.
참고) 접근 제어자가 private 또는 default인 멤버들은 상속되지 않는다기보다 상속은 받지만 자손 클래스로부터의 접근이 제한되는 것이다.   

    자손 클래스의 인스턴스를 생성하면 조상 클래스의 멤버와 자손 클래스의 멤버가 합쳐진 하나의 인스턴스로 생성된다.
<br><br>

## 1.2 클래스간의 관계 - 포함관계
상속외에도 클래스를 재사용하는 또 다른 방법이 있는데, 그것은 클래스 간에 '포함'관계를 맺어 주는 것이다. 클래스 간의 포함관계를 맺어 주는 것은 한 클래스의 멤버변수로 다른 클래스 타입의 참조변수를 선언하는 것을 뜻한다.
```java
class Circle {
    int x;          // 원점의 x 좌표
    int y;          // 원점의 y 좌표
    int r;          // 반지름
}
```
```java
class Point {
    int x;          // x 좌표
    int y;          // y 좌표
}
```
Point클래스를 재사용해서 Circle클래스를 작성한다면
```java
class Circle {
    Point c - new Point();      // 원점
    int r;
}
```
<br><br>

## 1.3 클래스간의 관계 설정하기
클래스를 작성하는데 있어서 상속관계를 맺어 줄 것인지 포함관계를 맺어 줄 것인지 결정하는 것은 때때로 혼돈스러울 수 있다.   
    
    상속관계    ' ~ 은 ~ 이다. (is -a)'
    포함관계    ' ~ 은 ~ 을 가지고 있다. (has -a)'
<br><br>

## 1.4 단일 상속(single inheritance)
자바에서는 단일 상속만을 허용한다. 그래서 하나 이상의 클래스로부터 상속을 받을 수 없다.   
<br><br>

## 1.5 Object 클래스 - 모든 클래스의 조상
Object클래스는 모든 클래스 상속계층도의 최상위에 있는 조상클래스이다. 다른 클래스로부터 상속 받지 않는 모든 클래스들은 자동적으로 Object 클래스로부터 상속받게 함으로써 이것을 가능하게 한다.   
<br><br><br>

## 2. 오버라이딩(overriding)
## 2.1 오버라이딩이란?
조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것을 오버라이딩이라고 한다. 상속받은 내용을 그대로 사용하기도 하지만, 자손 클래스 자신에 맞게 변경해야하는 경우가 많다. 이럴 때 조상의 메서드를 오버라이딩한다. (덮어쓰는 것)
```java
class Point {
    int x;
    int y;

    String getLocation(){
        return "x :" + x + "y :" + y;
    }

class Point3D extends Point {
    int z;

    String getLocation(){           // 오버라이딩
        return "x :" + x + "y :" + y + "z :" + z;
    }
}
```
<br><br>

## 2.2 오버라이딩의 조건
오버라이딩은 메서드의 내용만을 새로 작성하는 것이므로 메서드의 선언부는 조상의 것과 완전히 일치해야 한다.

    자손 클래스에서 오버라이딩하는 메서드는 조상 클래스의 메서드와
        - 이름이 같아야 한다.
        - 매개변수가 같아야 한다.
        - 반환타입이 같아야 한다.
=> 선언부가 서로 일치해야 한다. 다만 접근 제어자와 예외는 제한된 조건 하에서만 다르게 변경할 수 있다.   
<br>

    1. 접근 제어자는 조상 클래스의 메서드보다 좁은 버위로 변경 할 수 없다.
        - 대부분의 경우 같은 범위의 접근 제어자를 사용한다.
        - public > protected > (default) > private    
<br>

    2. 조상 클래스의 메서드보다 많은 수의 예외를 선언할 수 없다.(적거나 같아야한다.)
```java
class Parent {
    void parentMethod() throws IOException, SQLException {
        //..
    }
}

class Child extends Parent {
    void parentMethod() throws IOExcception {
        //..
    }
}

// 에러 - 조상클래스에 정의된 메서드보다 적은 개수의 예외를 선언한 것처럼
// 보이지만 Exception은 모든 예외의 최고 조상이므로 가장 많은 개수의 예외를 던질 수 있도록 선언한 것이다.
class Child extends Parent {
    void parentMethod() throws Excception {
        //..
    }
}
```
<br>

    3. 인스턴스 메서드를 static 메서드로 또는 그 반대로 변경할 수 없다.

Q. 조상 클래스에 정의된 static 메서드를 자손 클래스에서 똑같은 이름의 static 메서드로 정의할 수 있나요?
A. 가능합니다. 하지만 이것은 각 클래스에 별개의 static메서드를 정의한 것일 뿐 오버라이딩이 아닙니다. 각 메서드는 클래스이름으로 구별될 수 있으며, 호출할 때는 '참조변수.메서드이름()' 대신 '클래스이름.메서드이름()'으로 하는 것이 바람직합니다. static멤버들은 자신들이 정의된 클래스에 묶여있다고 생각하세요.   
<br><br>

## 2.3 오버로딩 vs 오버라이딩

    오버로딩(overloading) - 기존에 없는 새로운 메서드를 정의하는 것(new)
    오버라이딩(overriding) - 상속받은 메서드의 내용을 변경하는 것(change, modify)
```java
class Parent {
    void parentMethod() {}
}

class Child extends Parent {
    void parentMethod() {}          // 오버라이딩
    void parentMethod(int i) {}     // 오버로딩

    void childMethod() {}           
    void childMethod(int i) {}      // 오버로딩
    void childMethod() {}           // 에러. 중복정의 되었음
    }
}
```
<br><br>

## 2.4 super
super는 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조변수이다. 멤버변수와 지역변수의 이름이 같을 때 this를 사용해서 구별했듯이 상속받은 멤버와 자신의 클래스에 정의된 멤버의 이름이 같을 때는 super를 사용해서 구별할 수 있다.   
조상 클래스로부터 상속받은 멤버도 자손 클래스 자신의 멤버이므로 super대신 this를 사용할 수 있다. 그래도 조상 클래스의 멤버와 자손 클래스의 멤버가 중복 정의되어 서로 구별해야하는 경우에만 super를 사용하는 것이 좋다.   
모든 인스턴스메서드에는 자신이 속한 인스턴스의 주소가 지역변수로 저장되는데, 이것이 참조변수인 this와 super의 값이 된다.   
static메서드(클래스메서드)는 인스턴스와 관련이 없다. 그래서 this와 마찬가지로 super역시 static메서드에서는 사용할 수 없고 인스턴스메서드에서만 사용할 수 있다.   

```java
class SuperTest2 {
    public static void main(String args[]) {
        Child c = new Child();
        c.method();
    }
}

class Parent {
    int x = 10;
}

class Child extends Parent {
    int x = 20;

    void method() {
        System.out.println("x =:" + x);
        System.out.println("this.x =:" + this.x);
        System.out.println("super.x =:" + super.x);
    }
}

-> console
    x =20
    this.x = 20
    super.x = 10
```
```java
class Point {
    int x;
    int y;

    String getLocation() {
        return "x :" + x + ", y :" + y;
    }
}

class Point3D extends Point {
    int z;
    
    String getLocation() {     // 오버라이딩
     // return "x :" + x + "y :" + y + "z :" + z;
        return super.getLocation() + ", z :" + z;       //조상의 메서드 호출
    }
}
```
=> 조상클래스의 메서드의 내용에 추가적으로 작업을 덧붙이는 경우라면 이처럼 super를 사용해서 조상클래스의 메서드를 포함시키는 것이 좋다. 후에 조상클래스의 메서드가 변경되더라도 변경된 내용이 자손클래스의 메서드에 자동적으로 반영될 것이기 때문이다.   
<br><br>

## 2.5 super() - 조상 클래스의 생성자
this() 와 마찬가지로 super( ) 역시 생성자이다. this( ) 는 같은 클래스의 다른 생성자를 호출하는 데 사용되지만, super( ) 는 조상 클래스의 생성자를 호출하는데 사용된다. 자손 클래스의 인스턴스를 생성하면, 자손의 멤버와 조상의 멤버가 모두 합쳐진 하나의 인스턴스가 생성된다. 그래서 자손 클래스의 인스턴스가 조상 클래스의 멤버들을 사용할 수 있는 것이다. 이 때 조상 클래스 멤버의 초기화 작업이 수행되어야 하기 때문에 자손 클래스의 생성자에서 조상 클래스의 생성자가 호출되어야 한다.    
**생성자의 첫 줄에서 조상클래스의 생성자를 호출해야하는 이유는 자손 클래스의 멤버가 조상 클래스의 멤버를 사용할 수도 있으므로 조상의 멤버들이 먼저 초기화되어 있어야 하기 때문이다.**   

    Object 클래스를 제외한 모든 클래스의 생성자 첫 줄에는 생성자 this( ) 또는 super( ) 를 호출해야 한다.   
    그렇지 않으면 컴파일러가 자동적으로 'super( );' 를 생성자의 첫 줄에 삽입한다.

인스턴스를 생성할 때는 클래스를 선택하는 것만큼 생성자를 선택하는 것도 중요한 일이다.

    1. 클래스 - 어떤 클래스의 인스턴스를 생성할 것인가?
    2. 생성자 - 선택한 클래스의 어떤 생성자를 이용해서 인스턴스를 생성할 것인가?
```java
class Point {
    int x;
    int y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Point3D extends Point {
    int z;
    
    Point3D(int x, int y, int z) {
        this.x = x;
        this.y = y;
        this.z = z;
    }
}
=> [컴파일 에러]
```
-> 컴파일러는 자동적으로 'super( );' 를 Point3D 클래스의 생성자의 첫 줄에 넣어 준다.
```java
Point3D(int x, int y, int z) {
        super( );
        this.x = x;
        this.y = y;
        this.z = z;
}
```
그러나 Point 클래스에 생성자 Point() 가 정의되어 있지 않기 때문에 위와 같은 컴파일 에러가 발생한 것이다.   
-> Point 클래스에 생성자 Point( ) 를 추가해주던가, 생성자 Point3D(int x, int y, int z)의 첫 줄에서 Point(int x, int y)를 호출하도록 변경하면 된다.
```java
Point3D(int x, int y, int z) {
        super(x, y);        // 조상클래스의 생성자 Point(int x, int y)를 호출한다ㅣ.
        this.z = z;
}
```
<br>

**조상 클래스의 멤버변수는 이처럼 조상의 생성자에 의해 초기화되도록 해야 하는 것이다.**

<br>

'Point3D = new Point3D(); 와 같이 인스턴스를 생성하면, 아래와 같은 순서로 생성자가 호출된다.

```java
public class Object {
    ...
    public Object( ) { }    <-- 4. --
    ...
}



class Point extends Object {
    int x = 10;
    int y = 20;

    Point(int x, int y) {    <-- 3. --
        super( );    -- 4. -->
        this.x = x;
        this.y = y;
    }
    ...
}


 
class Point3D extends Point {
    int z = 30;
    
    Point3D(int x, int y, int z) {   <-- 2. --
        super(x, y);    -- 3. -->
        this.z = z;
    }

    Point3D( ) {    --- 1.
        this(100, 200, 300);    -- 2.-->
    }
}
```
<br><br><br>

## 3. package 와 import
## 3.1 패키지(package)
패키지란, 클래스의 묶음이다. 패키지에는 클래스 또는 인터페이스를 포함시킬 수 있으며, 서로 관련된 클래스들끼리 그룹 단위로 묶어 놓음으로써 클래스를 효율적으로 관리할 수 있다. 같은 이름의 클래스 일지라도 서로 다른 패키지에 존재하는 것이 가능하다. 클래스의 실제 이름 ( full name ) 은 패키지명을 포함한 것이다.   
클래스가 물리적으로 하나의 클래스파일 ( .class ) 인 것과 같이 패키지는 물리적으로 하나의 디렉토리이다.    
참고) 클래스 파일들을 압축한 것이 jar ( *jar ) 이며, jar 파일은 'jar.exe' 외에도 알집이나 winzip 으로 압축을 풀 수 있다.    
디렉토리가 하위 디렉토리를 가질 수 있는 것처럼, 패키지도 다른 패키지를 포함할 수 있으며 점 ' . ' 으로 구분한다.
    
    - 하나의 소스파일에는 첫 번째 문장으로 단 한 번의 패키지 선언만을 허용한다.
    - 모든 클래스는 반드시 하나의 패키지에 속해야 한다.
    - 패키지는 점 ( . ) 을 구분자로 하여 계층구조로 구성할 수 있다.
    - 패키지는 물리적으로 클래스 파일 ( .class ) 을 포함하는 하나의 디렉토리이다.

<br><br>

## 3.2 패키지의 선언
패키지명은 대소문자를 모두 허용하지만, 클래스명과 쉽게 구분하기 위해서 소문자로 하는 것을 원칙으로 하고 있다.   
참고) 클래스패스 (classpath) 는 컴파일러 (java.exe) 나 JVM 등이 클래스의 위치를 찾는데 사용되는 경로이다.   
<br><br>

## 3.3 import 문
소스코드를 작성할 때 다른 패키지의 클래스를 사용하려면 패키지명이 포함된 클래스 이름을 사용해야 한다. 하지만, 매번 패키지명을 붙여서 작성하기란 여간 불편한 일이 아닐 것이다. 클래스의 코드를 작성하기 전에 import 문으로 사용하고자 하는 클래스의 패키지를 미리 명시해주면 소스코드에 사용되는 클래스이름에서 패키지명은 생략할 수 있다.   
<br><br><br>

## 4. 제어자(modifier)
## 4.1 제어자란?
제어자 (modifier) 는 클래스, 변수 또는 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여한다. 제어자의 종류는 크게 접근 제어자와 그 외의 제어자로 나눌 수 있다.

    접근 제어자 - public, protected, default, private
    그 외 - static, final, abstract, native, transient, synchronized, volatile, strictfp

제어자는 클래서나 멤버변수와 메서드에 주로 사용되며, 하나의 대상에 대하여 여러 제어자를 조합하여 사용하는 것이 가능하다.
단, 접근 제어자는 한 번에 네 가지 중 하나만 선택해서 사용할 수 있다.
<br><br>

## 4.2 static - 클래스의, 공통적인
static 은 '클래스의' 또는 '공통적인' 의 의미를 가지고 있다. 인스턴스변수는 하나의 클래스로부터 생성되었더라도 각기 다른 값을 유지하지만, 클래스변수 (static 멤버변수) 는 인스턴스에 관계없이 같은 값을 갖는다. 그 이유는 하나의 변수를 모든 인스턴스가 공유하기 때문이다.    
static 이 붙은 멤버변수와 메서드, 그리고 초기화 블럭은 인스턴스가 아닌 클래스에 관계된 것이기 때문에 인스턴스를 생성하지 않고도 사용할 수 있다.    
인스턴스메서드와 static메서드의 근본적인 차이는 메서드 내에서 인스턴스 멤버를 사용하는가의 여부에 있다.

    static 이 사용될 수 있는 곳 - 멤버변수, 메서드, 초기화 블럭

제어자 - static   
<br>
멤버변수 
- 모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.
- 클래스변수는 인스턴스를 생성하지 않고도 사용 가능하다.
- 클래스가 메모리에 로드될 때 생성된다.

<br>

메서드   
- 인스턴스를 생성하지 않고도 호출이 가능한 static 메서드가 된다.
- static 메서드 내에서는 인스턴스멤버들을 직접 사용할 수 없다.

<br>
인스턴스 멤버를 사용하지 않는 메서드는 static을 붙여서 static 메서드로 선언하는 것을 고려해보도록 하자.   

```java
class StaticTest {
    static int width = 200;             // 클래스 변수 (static 변수)
    static int height = 120;            // 클래스 변수 (static 변수)

    static {                            // 클래스 초기화 블럭
        // static 변수의 복잡한 초기화 수행
    }

    static int max(int a, int b) {      // 클래스 메서드(static 메서드)
        return a > b ? a : b;
    }
}
```
<br><br>

## 4.3 final - 마지막의, 변경될 수 없는
final 은 '마지막의' 또는 '변경될 수 없는' 의 의미를 가지고 있으며 거의 모든 대상에 사용될 수 있다.

    final 이 사용될 수 있는 곳 - 클래스, 메서드, 멤버변수, 지역변수

제어자 - final   
<br>
클래스
- 변경될 수 없는 크래스, 확장될 수 없는 클래스가 된다.   
그래서 final로 지정된 클래스는 다른 클래스의 조상이 될 수 없다.

<br>

메서드   
- 변경될 수 없는 메서드, final 로 지정된 메서드는 오버라이딩을 통해 재정이 될 수 없다.   

<br>

멤버변수 / 지역변수
- 변수 앞에 final 이 붙으면, 값을 변경할 수 없는 상수가 된다.

<br>
참고) 대표적인 final 클래스로는 String 과 Math 가 있다.    
<br><br>

**생성자를 이용한 final 멤버 변수의 초기화**   
final이 붙은 변수는 상수이므로 일반적으로 선언과 초기화를 동시에 하지만, 인스턴스변수의 경우 생성자에서 초기화 되도록 할 수 있다.   
클래스 내에 매개변수를 갖는 생성자를 선언하여, 인스턴스를 생성할 때 final 이 붙은 멤버변수를 초기화하는데 필요한 값을 생성자의 매개변수로 제공받는 것이다. 이 기능을 활용하면 각 인스턴스마다 final 이 붙은 멤버변수가 다른 값을 갖도록 하는 것이 가능하다.   
```java
class Card {
    final int NUMBER;       // 상수지만 선언과 함께 초기화 하지 않고
    final String KIND;         // 생성자에서 단 한번만 초기화 할 수 있다.
    static int width = 100;
    static int height = 250;

    Card(String kind, int num) {
        KIND = kind; 
        NUMBER = num;       // 매개변수로 넘겨받은 값으로 KIND 와 NUMBER 를 초기화한다.
    }

    Card ( ) {
        this("HEART", 1);
    }

    public String toString( ) {
        return KIND + " " + NUMBER;
    }
}

class FinalCardTest {
    public static void main (String args[]) {
        Card c = new Card("HEART", 10);
        C.nUMBER = 5;       // 에러!! final 값 변경 불가
        System.out.println(c.KIND);
        System.out.println(c.NUMBER);
        System.out.println(c);  // System.out.println(c.toString());
    }
}
[실행결과]
HEART
10
HEART 10
```
<br><br>

## 4.4 abstract - 추상의, 미완성의
abstract 는 '미완성'의 의미를 가지고 있다. 메서드의 선언부만 작성하고 실제 수행내용은 구현하지 않은 추상 메서드를 선언하는데 사용된다.   
그리고 클래스에 사용되어 클래스 내에 추상메서드가 존재한다는 것을 쉽게 알 수 있게한다.   

    abstract 가 사용될 수 있는 곳 - 클래스, 메서드

제어자 - abstract   
<br>
클래스
- 클래스 내에 추상 메서드가 선언되어 있음을 의미한다.  

<br>

메서드   
- 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알린다.

<br><br>
추상 클래스는 아직 완성되지 않은 메서드가 존재하는 '미완성 설계도'이므로 인스턴스를 생성할 수 없다.   
```java
abstract class AbstractTest {           // 추상 클래스(추상 메서드를 포함한 클래스)       
    abstract void move( );              // 추상 메서드(구현부가 없는 메서드)
}
```
꽤 드물지만 추상 메서드가 없는 클래스, 즉 완성된 클래스도 abstract 를 붙여서 추상 클래스로 만드는 경우도 있다.    
<br><br>

## 4.5 접근 제어자(access modifier)
접근 제어자는 멤버 또는 클래스에 사용되어, 해당하는 멤버 또는 클래스를 외부에서 접근하지 못하도록 제한하는 역할을 한다.   
접근 제어자가 default임을 알리기 위해 실제로 default를 붙이지 않는다. 클래스나 멤버변수, 메서드, 생성자에 접근 제어자가 지정되어 있지 않다면, 접근 제어자가 default임을 뜻한다.

    접근 제어자가 사용될 수 있는 곳 - 클래스, 멤버변수, 메서드, 생성자

    private     - 같은 클래스 내에서만 접근이 가능하다.
    default     - 같은 패키지 내에서만 접근이 가능하다.
    protected   - 같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근이 가능하다.
    public      - 접근 제한이 전혀 없다.

제어자 | 같은 클래스 | 같은 패키지 | 자손클래스 | 전&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;체
 :---: | :---: | :---: | :---: | :---: |
 public | ⭕ | ⭕ | ⭕ | ⭕ |
 protected | ⭕ | ⭕ | ⭕ |  |
 (default) | ⭕ | ⭕ |  |  |
 private | ⭕ |  |  |  |

    public > protected > (default) > private

대&nbsp;&nbsp;&nbsp;&nbsp;상 | 사용가능한 접근 제어자
:---: | :---:
클래스 | public, ( default )
메서드 / 멤버변수 | public, protected, ( default ), private
지역변수 | 없음

<br><br>
**접근 제어자를 이용한 캡슐화**   
클래스나 멤버, 주로 멤버에 접근 제어자를 사용하는 이유는 클래스의 내부에 선언된 데이터를 보호하기 위해서이다.   
데이터가 유효한 값을 유지하도록, 또는 비밀번호와 같은 데이터를 외부에서 함부로 변경하지 못하도록 하기 위해서는 외부로부터의 접근을 제한하는 것이 필요하다.   
이것을 감추기( data hiding )라고 하며, 객체지향개념의 캡슐화( encapsulation )에 해당하는 내용이다.   
또 다른 이유는 클래스 내에서만 사용되는, 내부 작업을 위해 임시로 사용되는 멤버변수나 부분작업을 처리하기 위한 메서드 등의 멤버들을 클래스 내부에 감추기 위해서이다. 외부에서 접근할 필요가 없는 멤버들을 private 으로 지정하여 외부에 노출시키지 않음으로써 복잡성을 줄일 수 있다. 이것 역시 캡슐화에 해당한다.   

    접근 제어자를 사용하는 이유
    - 외부로부터 데이터를 보호하기 위해서
    - 외부에는 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서

접근 제어자를 적절히 선택해서 접근 범위를 최소화하도록 노력하자.   
<br>

```java
public class TimeTest {
    public static void main (String args[]) {
        Time t = new Time(12, 35, 30;
         System.out.println(t);
         t.hour = 13;               // 에러!! hour의 접근제어자가 private이므로 접근할 수 없다.
         t.setHour(t.getHour()+1);
        System.out.println(t);      //  System.out.println(t.toString());
}

public class Time {
    private int hour;       
    private int minute;         // 접근제어자를 private으로 하여     
    private int second;         // 외부에서 직접 접근하지 못하도록 한다.

    Time(int hour, int minute, int second) {
        setHour(hour);
        setMinute(minute);
        setSecond(second);
    }

    public int getHour( ) { return hour; }
    public void setHour(int hour) {
        if (hour < 0 || hour > 23) 
            return;
        this.hour = hour;
    }

    public int getMinute( ) { return minute; }
    public void setMinute(int minute) {
        if (minute < 0 || minute > 59) 
            return;
        this.minute = minute;
    }

    public int getSecond( ) { return second; }
    public void setSecond(int second) {
        if (second < 0 || second > 59) 
            return;
        this.second = second;
    }

    public String toString( ) {
        return hour + ":" + minute + ":" + second;
    }
    
}
[실행결과]
12:35:30
13:35:30
```
get으로 시작하는 메서드는 단순히 멤버변수의 값을 반환하는 일을 하고, set으로 시작하는 메서드는 매개변수에 지정된 값을 검사하여 조건에 맞는 값일 때만 멤버변수의 값을 변경하도록 작성되어 있다.   
만일 상속을 통해 확장될 것이 예상되는 클래스라면 멤버에 접근 제한을 주되, 자손클래스에서 접근하는 것이 가능하도록 하기 위해 private 대신 protected 를 사용한다.    
보통 멤버변수의 값을 읽는 메서드의 이름을 'get멤버변수이름'으로 하고, 멤버변수의 값을 변경하는 메서드의 이름을 'set멤버변수이름'으로 한다. get으로 시작하는 메서드를 getter, set으로 시작하는 메서드를 setter라고 부른다.   
<br>

**생성자의 접근 제어자**   
생성자에 접근 제어자를 사용함으로써 인스턴스의 생성을 제한할 수 있다. 보통 생성자의 접근제어자는 클래스의 접근 제어자와 같지만, 다르게 지정할 수도 있다.    
생성자의 접근 제어자를 private으로 지정하면, 외부에서 생성자에 접근할 수 없으므로 인스턴스를 생성할 수 없게 된다. 그래도 클래스 내부에서는 인스턴스의 생성이 가능하다.   
```java
class Singleton {
    // ...

    // getInstance( ) 에서 사용될 수 있도록 인스턴스가 미리 생성되어야 하므로 static이어야 한다. 
    private static Singleton s = new Singleton( ); 

    private Singleton( ) {
        // ...
    }

    // 인스턴스를 생성하지 않고도 호출할 수 있어야 하므로 static이어야 한다.
    public static Singleton getInstance( ) {
        return s;
    }

    // ...
}
```
이처럼 생성자를 통해 직접 인스턴스를 생성하지 못하게 하고 public 메서드를 통해 인스턴스에 접근하게 함으로써 사용할 수 있는 인스턴스의 개수를 제한할 수 있다.   
또 한 가지, 생성자가 private 인 클래스는 다른 클래스의 조상이 될 수 없다. 왜냐하면, 자손클래스의 인스턴스를 생성할 때 조상클래스의 생성자를 호출해야만 하는데, 생성자의 접근 제어자가 private이므로 자손클래스에서 호출하는 것이 불가능하기 때문이다. 그래서 클래스 앞에 final 을 더 추가하여 상속할 수 없는 클래스라는 것을 알리는 것이 좋다.
```java
final class Singleton {
    private static Singleton s = new Singleton( );

    private Singleton( ) {
        // ...
    } 

    public static Singleton getInstance( ) {
        if (s = null) [
            s = new Singleton( );
        ]
        return s;
    }
    // ...
}

class SingletonTest {
    public static void main (String args[]) {
        Singleton s = new Singleton( );     // 에러!! private이라서 접근 불가
        Singleton s = Singleton.getInstance( );
}
```
<br><br>

## 4.6 제어자(modifier)의 조합
대&nbsp;&nbsp;&nbsp;&nbsp;상 | 사용가능한 제어자
:---: | :---:
클래스 | public, (default), final, abstract
메서드 | 모든 접근 제어자, final, abstract, static
멤버변수 | 모든 접근 제어자, final, static
지역변수 | final
<br>

1. 메서드에 static과 abstract를 함께 사용할 수 없다.
- static메서드에는 몸통이 있는 메서드에만 사용할 수 있기 때문이다.

<br>

2. 클래스에 abstract와 final을 동시에 사용할 수 없다.
- 클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고 abstract는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순되기 때문이다.

<br>

3. abstract메서드의 접근 제어자가 private일 수 없다.
- abstract메서드는 자손클래스에서 구현해주어야 하는데 접근 제어자가 private이면, 자손클래스에서 접근할 수 없기 때문이다.

<br>

4. 메서드에 private과 final을 같이 사용할 필요는 없다.
- 접근 제어자가 private인 메서드는 오버라이딩될 수 없기 때문이다. 이 둘 중 하나만 사용해도 의미가 충분하다.    

<br><br><br>

## 5. 다형성(polymorphism)
## 5.1 다형성이란?
객체지향개념에서 다형성이란 '여러 가지 형태를 가질 수 있는 능력'을 의미하며, 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 프로그램적으로 구현하였다. 이를 좀 더 구체적으로 말하자면, **조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였다**는 것이다.   
```java
class Tv {
    boolean power;      // 전원상태(on/off)
    int channel;        // 채널

    void power( )       {   power = !power;     }
    void channeluP( )   {   ++channel;          }
    void channelDown( ) {   --channel;          }
    
}

class CaptionTv extends Tv {
    String text;        // 캡션을 보여 주기 위한 문자열
    void caption( )     {   /* 내용 생략*/    }

}
```
클래스 Tv와 CaptionTv는 서로 상속관계에 있으며, 이 두 클래스의 인스턴스를 생성하고 사용하기 위해서는 다음과 같이 할수 있다.
```java
Tv t = new Tv( );
CaptionTv c = new CaptionTv( );
```
지금까지 우리는 생성된 인스턴스를 다루기 위해서, 인스턴스의 타입과 일치하는 타입의 참조변수만을 사용했다. 이처럼 인스턴스의 타입과 참조변수의 타입이 일치하는 것이 보통이지만, Tv와 CaptionTv클래스가 서로 상속관계에 있을 경우, 다음과 같이 조상 클래스 타입의 참조변수로 자손 클래스의 인스턴스를 참조하도록 하는 것도 가능하다.
```java
Tv t = new CaptionTv( );    // 조상 타입의 참조변수로 자손 인스턴스를 참조
```
Tv타입의 참조변수로는 CaptionTv인스턴스 중에서 Tv클래스의 멤버들(상속받은 멤버포함)만 사용할 수 있다. 따라서, 생성된 CaptionTv인스턴스의 멤버 중에서 Tv클래스에 정의 되지 않은 멤버, text와 caption( )은 참조변수 t로 사용이 불가능하다. 즉, t.text, t.caption( )와 같이 사용할 수 없다는 것이다. **참조 변수의 타입에 따라 사용할 수 있는 멤버의 개수가 달라진다.**   
<br>
반대로 아래와 같이 자손타입의 참조변수로 조상타입의 인스턴스를 참조하는 것은 가능할까?   
```java
CaptionTv c = new Tv( );        // Error!!
```
그렇지 않다. 이유는 실제 인스턴스인 Tv의 멤버 개수보다 참조변수 C가 사용할 수 있는 멤버의 개수가 더 많기 때문이다. 그래서 이를 허용하지 않는다.   
그래서, 자손타입의 참조변수로 조상타입의 인스턴스를 참조하는 것은 존재하지 않는 멤버를 사용하고자 할 가능성이 있으므로 허용하지 않는 것이다. **참조변수가 사용할 수 있는 멤버의 개수는 인스턴스의 멤버 개수보다 같거나 적어야 한다.**   
참고) 조상 인스턴스의 멤버 개수는 자손 인스턴스의 멤버 개수보다 항상 적거나 같다.   
참조변수의 타입이 참조변수가 참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 개수를 결정한다는 사실을 이해하는 것은 매우 중요하다.   

    조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있다.
    반대로 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수는 없다.
<br><br>

## 5.2 참조변수의 형변환
기본형 변수와 같이 참조변수도 형변환이 가능하다. 단, 서로 상속관계에 있는 클래스사이에서만 가능하기 때문에 자손타입의 참조변수를 조상타입의 참조변수로, 조상타입의 참조변수를 자손타입의 참조변수로의 형변환만 가능하다.   
기본형 변수의 형변환에서 작은 자료형에서 큰 자료형의 형변환은 생략이 가능하듯이, 참조형 변수의 형변환에서는 자손타입의 참조변수를 조상타입으로 형변환하는 경우에는 형변환을 생략할 수 있다.   

    자손타입 ---> 조상타입 (Up-casting)     : 형변환 생략가능
    조상타입 ---> 자손타입 (Down-casting)   : 형변환 생략불가

자손 타입의 참조변수를 조상타입의 참조변수로 형변환 하는 것은 참조변수가 다룰 수 있는 멤버의 개수가 실제 인스턴스가 갖고 있는 멤버의 개수보다 적을 것이 분명하므로 문제가 되지 않는다. 그래서 형변환을 생략할 수 있도록 한 것이다.   
하지만, 조상타입의 참조변수를 자손타입의 참조변수로 변환하는 것은 참조변수가 다룰 수 있는 멤버의 개수를 늘리는 것이므로, 실제 인스턴스의 멤버 개수보다 참조변수가 사용할 수 있는 멤버의 개수가 더 많아지므로 문제가 발생할 가능성이 있다. 그래서 자손타입으로의 형변환은 생략할 수 없으며, 형변환을 수행하기 전에 instanceof 연산자를 사용해서 참조변수가 참조하고 있는 실제 인스턴스의 타입을 확인하는 것이 안전하다.   
<br>
**형변환은 참조변수의 타입을 변환하는 것이지 인스턴스를 변환하는 것은 아니기 때문에 참조변수의 형변환은 인스턴스에 아무런 영향을 미치지 않는다.**   
**단지 참조변수의 형변환을 통해서, 참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위(개수)를 조절하는 것뿐이다.**   

```java
class CastingTest1 {
    public static void main(String args[]) {
        Car car = null;
        FireEngine fe = new FireEngine();
        FireEngine fe2 = null;

        fe.water();
        car = fe;               // car = (Car)fe; 에서 형변환이 생략된 형태다.
    //  car.water();            Eroor!! Car 타입의 참조변수로는 water() 호출 불가능
        fe2 = (FireEngine)car;  // 조상타입 ---> 자손타입
        fe2.water();
    }
}

class Car {
    String color;
    int door;
    void drive( ) {
        System.out.println("drive, Brrrr~");
    }
    void stop( ) {
        System.out.println("stop!!!");
    }
}

class FireEngine extends Car {
    void water( ) {
        System.out.println("water!!!");
    }
}
[실행 결과]
water!!!
water!!!
```
- car = fe;   
  자손타입 ---> 조상타입
  참조변수 car를 통해서도 FireEngine 인스턴스를 사용할 수 있지만, fe와는 달리 car는 Car타입이므로 Car클래스의 멤버가 아닌 water()는 사용할 수 없다.
- fe2 = (FireEngine)car;
  조상타입 ---> 자손타입
  참조변수 fe2를 통해서도 FireEngine인스턴스를 사용할 수 있지만, car와는 달리, fe2는 FireEngine타입으므로 FireEngine인스턴스의 모든 멤버들을 사용할 수 있다.    

```java
class CastingTest2 {
    public static void main(String args[]) {
        Car car = new Car();
        Car car2 = null;
        FireEngine fe = null;

        car.drive();
        fe = (FireEngine)car;       // 컴파일은 OK, 실행 시 에러가 발생
        fe.drive();
        car2 = fe;
        car2.drive();
    }
}
[실행 결과]
drive, Brrr~~~
java.lang.ClassCastException: Car at ~
 ```
 캐스트 연산자를 이용해서 조상타입의 참조변수를 자손타입의 참조변수로 형변환한 것이기 때문에 문제가 없어 보이지만, 문제는 참조변수 car가 참조하고 있는 인스턴스가 Car타입의 인스턴스라는데 있다. 조상타입의 인스턴스를 자손타입의 참조변수로 참조하는 것은 허용되지 않는다.   
 위의 예제에서 'Car car = new Car();' ---> 'Car car = new FireEngine();'와 같이 변경하면, 컴파일할 때 뿐 만 아니라 실행할 때도 에러가 발생하지 않을 것이다.   

    서로 상속관계에 있는 클래스 타입의 참조변수간의 형변환은 양방향으로 자유롭게 수행될 수 있으나, 참조변수가 참조하고 있는 인스턴스의 자손타입으로 형변환 하는 것은 허용되지 않는다. 참조변수가 가리키는 인스턴스의 타입이 무엇인지 확인하는 것이 중요하다.

<br><br>

## 5.3 instanceof 연산자
참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 instanceof 연산자를 사용한다. 주로 조건문에 사용되며, instanceof의 왼쪽에는 참조변수를 오른쪽에는 타입(클래스명)이 피연산자로 위치한다. 그리고 연산의 결과로 boolean값인 true와 false 중의 하나를 반환한다.   
instanceof를 이용한 연산결과로 true를 얻었다는 것은 참조변수가 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.   
참고) 값이 null인 참조변수에 대해 instanceof연산을 수행하면 false를 결과로 얻는다.   
```java
void doWork(Car c) {
    if (c instanceof FireEngine) {
        FireEngine fe = (FireEngine)c;
        fe.water();
    } else if (c instanceof Ambulance) {
        Ambulance a = (Ambulance)c;
        a.siren();
    }
}
```
위의 코드는 Car 타입의 참조변수 c를 매개변수로 하는 메서드이다. 이 메서드가 호출될 때, 매개변수로 Car클래스 또는 그 자손 클래서의 인스턴스를 넘겨받겠지만 메서드 내에서는 정확히 어떤 인스턴스인지 알 길이 없다. 그래서 instanceof연산자를 이용해서 참조변수 c가 가리키고 있는 인스턴스의 타입을 체크하고, 적절히 형변환한 다음에 작업을 해야한다.   
조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있기 때문에, 참조변수릥 타입과 인스턴스의 타입이 항상 일치하지는 않는다는 것을 배웠다. 조상 타입의 참조변수로는 실제 인스턴스의 멤버들을 모두 사용할 수 없기 때문에, 실제 인스턴스와 같은 타입의 참조변수로 형변환을 해야만 인스턴스의 모든 멤버들을 사용할 수 있다.
```java
class InstanceofTest {
    public static void main(String args[]) {
        FireEngine fe = new FireEngine();

        if (fe instanceof FireEngine) {
            System.out.println("This is a FireEngine instance.");
        }

        if (fe instanceof Car) {
            System.out.println("This is a Car instance.");
        }

        if (fe instanceof Object) {
            System.out.println("This is an Object instance.");
        }

        System.out.println(fe.getClass().getName());
    }
}

class Car { }
class FireEngine extends Car { }

[실행 결과]
This is a FireEngine instance.
This is a Car instance.
This is an Object instance.
FireEngine
```
생성된 인스턴스는 FireEngine타입인데도, Object타입과 Car타입의 instanceof연산에서도 true를 결과로 얻었다. 그 이유는 FireEngine클래스는 Object클래스와 Car클래스의 자손 클래스이므로 조상의 멤버들을 상속받았기 때문에, FireEngine 인스턴스는 Object인스턴스와 Car인스턴스를 포함하고 있는 셈이기 때문이다.   
요약하면, 실제 인스턴스와 같은 타입의 instanceof연산 이외에 조상타입의 instanceof 연산에도 true를 결과로 얻으며, instanceof연산의 결과가 true라는 것은 검사한 타입으로의 형변환을 해도 아무런 문제가 없다는 뜻이다.   

    어떤 타입에 대한 instanceof 연산의 결과가 true라는 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.

<br><br>

## 5.4 참조변수와 인스턴스의 연결
조상타입의 참조변수와 자손타입의 참조변수의 차이점이 사용할 수 있는 멤버의 개수에 있다고 배웠다. 여기서 한 가지 더 알아두어야 할 내용이 있다.   
조상 클래스에 선언된 멤버변수와 같은 이름의 인스턴스변수를 자손 클래스에 중복으로 정의했을 때, 조상타입의 참조변수로 자손 인스턴스를 참조하는 경우와 자손타입의 참조변수로 자손 인스턴스를 참조하는 경우는 서로 다른 결과를 얻는다.   
**메서드의 경우 조상 클래스의 메서드를 자손의 클래스에서 오버라이딩한 경우에도 참조변수의 타입에 관계없이 항상 실제 인스턴스의 메서드(오버라이딩된 메서드)가 호출되지만,** **멤버변수의 경우 참조변수의 타입에 따라 달라진다.**   
참고) static메서드는 static변수처럼 참조변수의 타입에 영향을 받는다. 참조변수의 타입에 영향을 받지 않는 것은 인스턴스메서드 뿐이다. 그래서 static메서드는 반드시 참조변수가 아닌 '클래스이름.메서드()'로 호출해야 한다.   
<br>
=> 멤버변수가 조상 클래스와 자손 클래스에 중복으로 정의된 경우, 조상 타입의 참조변수를 사용했을 때는 조상 클래스에 선언된 멤버변수가 선언되고, 자손타입의 멤버변수를 사용했을 때는 자손 클래스에 선언된 멤버변수가 사용된다.   

```java
class BindingTest {
    public static void main(String args[]) {
        Parent p = new Child();
        Child c = new Child();

        System.out.println("p.x = " + p.x);
        p.method();

        System.out.println("c.x = " + c.x);
        c.method();
    }
}

class Parent {
    int x = 100;

    void method() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent {
    int x = 200;

    void method() {
        System.out.println("Child Method");
    }
}

[실행 결과]
p.x = 100
Child Method
c.x = 200
Child Method
```

```java
class BindingTest2 {
    public static void main(String args[]) {
        Parent p = new Child();
        Child c = new Child();

        System.out.println("p.x = " + p.x);
        p.method();

        System.out.println("c.x = " + c.x);
        c.method();
    }
}

class Parent {
    int x = 100;

    void method() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent { }

[실행 결과]
p.x = 100
Parent Method
c.x = 100
Parent Method
```
이전의 예제와는 달리 Child 클래스에는 아무런 멤버도 정의되어 있지 않고 단순히 조상으로부터 멤버들을 상속받는다. 그렇기 때문에 참조변수의 타입에 관계없이 조상의 멤버들을 사용하게 된다.   
참조변수의 타입에 따라 결과가 달라지는 경우는 조상 클래스의 멤버변수와 같은 이름의 멤버변수를 자손 클래스에 중복해서 정의한 경우뿐이다.   

```java
class BindingTest3 {
    public static void main(String args[]) {
        Parent p = new Child();
        Child c = new Child();

        System.out.println("p.x = " + p.x);
        p.method();
        System.out.println();
        System.out.println("c.x = " + c.x);
        c.method();
    }
}

class Parent {
    int x = 100;

    void method() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent {
    int x = 200;

    void method() {
        System.out.println("x=" + x);       // this.x 와 같다.
        System.out.println("super.x=" + super.x);
        System.out.println("this.x=" + this.x);
    }
}

[실행 결과]
p.x = 100
x=200
super.x=100
this.x=200

c.x = 200
x=200
super.x=100
this.x=200
```
자손 클래스 Child에 선언된 인스턴스변수 x와 조상 클래스 Parent로부터 상속받은 인스턴스변수 x를 구분하는데 참조변수 super와 this가 사용된다. 자손인 Child클래스에서의 super.x는 조상 클래스인 Parent에 선언된 인스턴스변수 x를 뜻하며, this.x 또는 x는 Child클래스의 인스턴스변수 x를 뜻한다. 그래스 위 겨로가에서 x와 this.x의 값이 같다.   
<br><br>

## 5.5 매개변수의 다형성
참조변수의 다형적인 특징은메서드의 매개변수에도 적용된다.
```java
class Product {
    int price;
    int bonusPoint;
}

class Tv extends Product { }
class Computer extends Product { }
class Audio extends Product { }

class Buyer {
    int money = 1000;
    int bonusPoint = 0;

    void buy(Tv t) {
        money = money - t.price;
        bonusPoint = bonusPoint + t.bonusPoint;
    }

    void buy(Computer c) {
        money = money - c.price;
        bonusPoint = bonusPoint + c.bonusPoint;
    }

    void buy(Audio a) {
        money = money - a.price;
        bonusPoint = bonusPoint + a.bonusPoint;
    }
}
```
이렇게 되면, 제품의 종류가 늘어날 때마다 Buyter 클래스에는 새로운 buy 메서드를 추가해 주어야 할 것이다. 그러나 메서드의 매개변수에 다형성을 적용하면 아래와 같이 하나의 메서드로 간단히 처리할 수 있다.

```java
void buy(Product p) {
    money = money - p.price;
    bonusPoint = bonusPoint + p.bonusPoint;
}
```
매개변수가 Product타입의 참조변수라는 것은, 메서드의 매개변수로 Product클래스의 자손타입의 참조변수면 어느 것이나 매개변수로 받아들일 수 있다는 뜻입니다.   

```java
Buyer b = new Buyer();
Tv t = new Tv();
Computer c = new Computer();
b.buy(t)l
b.buy(c);
```
참고) Tv t = new Tv(); b.buy(t); 를 한 문장으로 줄이면 b.buy(new Tv()); 가 된다.   
Tv클래스와 Computer클래스는 Product클래스의 자손이므로 위의 코드와 같이 buy(Product p)메서드에 매개변수로 Tv인스턴스와 Computer인스턴스를 제공하는 것이 가능하다.   
```java
class Product {
    int price;
    int bonusPoint;

    Product(int price) {
        this.price = price;
        bonusPoint = (int)(price/10.0);
    }
}

class Tv extends Product { 
    Tv() {
        // 조상클래스의 생성자 Product(int price)를 호출한다.
        super(100);         // Tv의 가격을 100만원으로 한다.
    }
    public String toString() {  // Object크래스의 toString()을 오버라이딩한다.
        return "Tv";
    }
}
class Computer extends Product {
    Computer() {
        super(200);
    }
     public String toString() {  
        return "Computer";
    }
 }

class Buyer {
    int money = 1000;
    int bonusPoint = 0;

    void buy(Product p) {
        if(money < p.price>) {
            System.out.println("잔액이 부족하여 물건을 살 수 없습니다.");
            return;
        }
        money -= p.price;
        bonusPoint += p.bonusPoint;
        System.out.println(p + "을/를 구입하셨습니다.");
    }
}

class PolyArgumentTest {
    public static void main(String args[]) {
        Buyer b = new Buyer();
        
        b.buy(new Tv());
        b.buy(new Computer());

        System.out.println("현재 남은 돈은" + b.money + "만원입니다.");
        System.out.println("현재 보너스 점수는" + b.bonusPoint + "점 입니다.");
    }
}

[실행 결과]
Tv을/를 구입하셨습니다.
Computer을/를 구입하셧습니다.
현재 남은 돈은 700만원 입니다.
현재 보너스점수는 30점 입니다.
```
<br><br>

## 5.6 여러 종류의 객체를 배열로 다루기
조상타입의 참조변수로 자손타입의 객체를 참조하는 것이 가능하므로, Product클래스가 Tv, Computer, Audio클래스의 조상일 때, 다음과 같이 할 수 있다.   

    Product p1 = new Tv();
    Product p2 = new Computer();
    Product p3 = new Audio();
위의 코드를 Product타입의 참조변수 배열로 처리하면 아래와 같다.

    Product p[] = new Product[3];
    p[0] = new Tv();
    p[1] = new Computer();
    p[2] = new Audio();
이처럼 조상타입의 참조변수 배열을 사용하면, 공통의 조상을 가진 서로 다른 종류의 객체를 배열로 묶어서 다룰 수 있다. 또는 묶어서 다루고자하는 객채들의 상속관계를 따져서 가장 가까운 공통조상 클래스 타입의 참조변수 배열을 생성해서 객체들을 저장하면 된다.   
```java
class Product {
    int price;
    int bonusPoint;

    Product(int price) {
        this.price = price;
        bonusPoint = (int)(price/10.0);
    }
    
    Product() { }
}

class Tv extends Product { 
    Tv() {
        super(100);      
    }
    public String toString() { 
        return "Tv";
    }
}
class Computer extends Product {
    Computer() {
        super(200);
    }
     public String toString() {  
        return "Computer";
    }
 }
 class Audio extends Product {
     Audio() {
         super(50);
     }
     public String tOString() {
         return "Audio";;
     }
 }

class Buyer {
    int money = 1000;
    int bonusPoint = 0;
    Product[] item = new Product[10];
    int i = 0;

    void buy(Product p) {
        if (money < p.price) {
            System.out.println("잔액이 부족하여 물건을 살수 없습니다.");
            return;
        }
        money -= p.price;
        bonusPoint += p.bonusPoint;
        item[i++] = p;
        System.out.println(p + "을/를 구입하셨습니다.");
    }

    void sumary() {
        int sum = 0;
        String itemList = "";

        for (int i=0; i < item.lengh; i++) {
            if (item[i] == null) break;
            sum += item[i].price;
            itemList += item[i] + ",";
        }
        System.out.println("구입하신 물품의 총금액은" + sum + "만원입니다.");
        System.out.println("구입하신 제품은" + itemList + "입니다.");
    }
}

class PolyArgumentTest2 {
    public static void main(String args[]) {
        Buyer b = new Buyer();
        
        b.buy(new Tv());
        b.buy(new Computer());
        b.buy(new Audio());
        b.summary();
    }
}

[실행 결과]
Tv을/를 구입하셨습니다.
Computer을/를 구입하셨습니다.
Audio을/를 구입하셨습니다.
구입하신 물품의 총금액은 350만원입니다.
구입하신 제품은 Tv, Computer, Audio, 입니다.
```
참고) 구입한 제품목록의 마지막에 출력되는 콤마(,)가 눈에 거슬린다면, itemList += item[i] + ", ";를 itemList += (i==0) ? "" + item[i] : ", " + item[i]; 과 같이 변경하자.   
<br>

<Vector 클래스의 주요 메서드>
메서드 / 생성자 | 설&nbsp;&nbsp;&nbsp;&nbsp;명
:---: | :---
Vector () | 10개의 객체를 저장할 수 있는 Vector인스턴스를 생성한다. 10개 이상의 인스턴스가 저장되면, 자동적으로 크기가 증가된다.
boolean add (Object o) | Vector에 객체를 추가한다. 추가에 성공하면 결과값으로 true, 실패하면 false를 반환한다.
boolean remove (Object o) | Vector에 저장되어 있는 객체를 제거한다. 제거에 성공하면 true, 실패하면 false를 반환한다.
boolean isEmpty () | Vector가 비어있는지 검사한다. 비어있으면 true, 비어있지 않으면 false를 반환한다.
Object get (int index) | 지정된 위치(index)의 객체를 반환한다. 반환타입이 Object타입이므로 적절한 타입으로의 형변환이 필요하다.
int size () | Vector에 저장된 객체의 개수를 반환한다.

```java
import java.util.*;         //Vector 클래스를 사용하기 위해서 추가해주었다.

class Product {
    int price;
    int bonusPoint;

    Product(int price) {
        this.price = price;
        bonusPoint = (int)(price/10.0);
    }
    
    Product() {
        price = 0;
        bonusPoint = 0;
     }
}

class Tv extends Product { 
    Tv() {
        super(100);      
    }
    public String toString() { 
        return "Tv";
    }
}
class Computer extends Product {
    Computer() {
        super(200);
    }
     public String toString() {  
        return "Computer";
    }
 }
 class Audio extends Product {
     Audio() {
         super(50);
     }
     public String tOString() {
         return "Audio";;
     }
 }

class Buyer {
    int money = 1000;
    int bonusPoint = 0;
    Vector item = new Vector();         // 구입할 제품을 저장하는데 사용될 Vector객체

    void buy(Product p) {
        if (money < p.price) {
            System.out.println("잔액이 부족하여 물건을 살수 없습니다.");
            return;
        }
        money -= p.price;
        bonusPoint += p.bonusPoint;
        item.add(p);                    // 구입한 제품을 Vector에 저장한다.
        System.out.println(p + "을/를 구입하셨습니다.");
    }

    void refund(Product p) {
        if (item.remove(p)) {           // 제품을 Vector에서 제거한다.
            money += p.price;
            bonusPoint = -= p.bonusPoint;
            System.out.println(p + "을/를 반품하셨습니다.");
        } else {
            System.out.println("구입하신 제품 중 해당 제품이 없습니다.");
        }
    }

    void sumary() {
        int sum = 0;
        String itemList = "";

        if (item.isEmpty()) {            // Vector가 비어있는지 확인한다.
            System.out.println("구입하신 제품이 없습니다.");
            return;
        }

        for (int i=0; i < item.size(); i++) {
            Product p = (Product)item.get(i);       // Vector의 i번째에 있는 객체를 얻어온다.
            sum += p.price;
            itemList += (i==0) ? "" + p : "," + p;
        }
        System.out.println("구입하신 물품의 총금액은" + sum + "만원입니다.");
        System.out.println("구입하신 제품은" + itemList + "입니다.");
    }
}

class PolyArgumentTest3 {
    public static void main(String args[]) {
        Buyer b = new Buyer();
        Tv tv = new Tv();
        Computer com = new Computer();
        Audio audio = new Audio();
        
        b.buy(tv);
        b.buy(com);
        b.buy(audio);
        b.summary();
        System.out.println();
        b.refund(com);
        b.summary();
    }
}

[실행 결과]
Tv을/를 구입하셨습니다.
Computer을/를 구입하셨습니다.
Audio을/를 구입하셨습니다.
구입하신 물품의 총금액은 350만원입니다.
구입하신 제품은 Tv, COmputer, Audio입니다.

Computer을/를 반품하셨습니다.
구입하신 물품의 총금액은 150만원입니다.
구입하신 제품은 Tv, Audio입니다.
```
<br><br>

## 6. 추상클래스(abstract class)
## 6.1 추상클래스란?
