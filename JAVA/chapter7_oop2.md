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