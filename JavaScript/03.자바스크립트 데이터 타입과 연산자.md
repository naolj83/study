#  3. 자바스크립트 데이터 타입과 연산자

[자바스크립트 데이터 타입]

- 기본 데이터 타입(숫자, 문자열, 불린값, null, undefined)
- 참조 데이터 타입(객체, 배열)
- 주의해야 할 연산자

## 3.1 자바스크립트 기본 타입
자바스크립트에서 기본 타입은 **숫자, 문자열, 불린값, null, undefined** 라는 타입이 있다.   
이들 타입의 특징은 그 자체가 하나의 값을 나타낸다는 것이다.    
자바스크립트는 **느슨한 타입 체크 언어**다. 변수를 선언할 때 타입을 미리 정하지 않고, var라는 한 가지 키워드로만 변수를 선언한다. 이렇게 선언된 변수에는 어떤 타입의 데이터라도 저장하는 것이 가능하다. 따라서 자바스크립트는 변수에 어떤 형태의 데이터를 저장하느냐에 따라 해당 변수의 타입이 결정된다.
```javascript
// 숫자 타입
var intNum = 10;
var floatNum = 0.1;

// 문자열 타입
var singleQuoteStr = 'Single quote string';
var doubleQuoteStr = "double quote string";
var singleChar = 'a';

// 불린 타입
var boolVar = true;

// undefined 타입
var emptyVar;

// null 타입
var nullVar = null;     -------------- 5

console.log(
    typeof intNum,
    typeof floatNum,
    typeof singleQuoteStr,
    typeof doubleQuoteStr,
    typeof boolVar,
    typeof emptyVar,
    typeof nullVar,
);
```
[출력결과]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- typeof 연산자는 피연산자의 타입을 리턴한다.

    number  number  string  string  boolean  undefined  object

<br><br>

## 3.1.1 숫자
자바는 정수냐 실수냐에 따라 int, long, double, float 등과 같은 다양한 숫자 타입이 존재하지만, 자바스크립트는 하나의 숫자형만 존재한다. var 키워드로 선언된 자바스크립트 변수에는 정수나 실수 구분 없이 그 값을 바로 저장할 수 있으므로, intNum 과 floatNum 변수 모두 typeof 연산자의 결과값이 number 타입임을 확인 할 수 있다.    
자바스크립트에서는 정수형이 따로 없고, 모든 숫자를 실수로 처리하므로 나눗셈을 연산할 때 소수 부분까지 출력된다.
```javascript
var num = 5 / 2;

console.log(num);   // (출력값)  2.5
console.log(Math.floor(num));   // (출력값)  2
```
<br><br>

## 3.1.2 문자열
문자열은 작은 따옴표 (') 나 큰 따옴표 (") 로 생성한다. 자바스크립트에서는 char 타입과 같이 문자 하나만을 별도로 나타내는 데이터 타입은 존재하지 않는다. 주의해야 할 점은 한 번 정의된 문자열은 변하지 않는다는 것이다.
```javascript
// str 문자열 생성
var str = 'test';
console.log(str[0], str[1], str[2], str[3]);    // (출력값) test

// 문자열의 첫 글자를 대문자로 변경?
str[0] = 'T';
console.log(str);   // (출력값) test
```
문자열은 문자 배열처럼 인덱스를 이용해서 접근할 수 있다. 위의 코드 출력하면 에러는 발생하지 않았지만 자바스크립트에서는 한 번 생성된 문자열을 읽기만 가능하지 수정은 불가능하다.   
<br><br>

## 3.1.3 불린값
자바스크립트는 true 와 false 값을 나타내는 불린 타입을 가진다.   
<br><br>

## 3.1.4 null 과 undefined
이 두 타입은 모두 자바스크립트에서 '값이 비어있음'을 나타낸다.   
자바스크립트 환경 내에서 기본적으로 값이 할당되지 않은 변수는 undefined 타입이며, undefined 타입의 변수는 변수 자체의 값 또한 undefined 이다. 이처럼 자바스크립트에서 **undefined 는 타입이자, 값을 나타낸다**는 것에 주의하자.     
5의 nullVar 변수와 같이 null 타입 변수의 경우는 개발자가 명시적으로 값이 비어있음을 나타내는 데 사용한다.    
여기서 주의할 점은 null 타입 변수인 nullVar 의 typeof 결과가 null 이 아니라 object 라는 것이다. 때문에 자바스크립트에서는 null 타입 변수인지를 확인할 때 typeof 연산자를 사용하면 안 되고, 일치 연산자 (===) 를 사용해서 변수의 값을 직접 확인해야 한다.
```javascript
// null 타입 변수 생성
var nullVar = null;

console.log(typeof nullVar === null);       // (출력값)  false
console.log(nullVar === null);              // (출력값)  true
```
<br><br>

## 3.2 자바스크립트 참조 타입(객체 타입)
자바스크립트에서 숫자, 문자열, 불린값, null, undefined 같은 기본 타입을 제외한 모든 값은 객체다. 따라서 배열, 함수, 정규표현식 등도 모두 결국 자바스크립트 객체로 표현된다.   
자바스크립트에서 객체는 단순히 '이름(key):값(value)' 형태의 프로퍼티들을 저장하는 컨테이너이다. 자바스크립트에서 기본 타입은 하나의 값만을 가지는 데 비해, 참조 타입인 객체는 여러 개의 프로퍼티들을 포함할 수 있으며, 이러한 객체의 프로퍼티는 기본 타입의 값을 포함하거나, 다른 객체를 가리킬 수도 있다. 이러한 프로퍼티의 성질에 따라 객체의 프로퍼티는 함수로 포함할 수 있으며, 자바스크립트에서는 이러한 프로퍼티를 메서드라고 부른다.   
<br><br>

## 3.2.1 객체 생성
자바스크립트에서는 클래스라는 개념이 없고, 객체 리터럴이나 생성자 함수 등 별도의 생성 방식이 존재한다.   
자바스크립트에서 객체를 생성하는 방법은 크게 세 가지가 있다.
- 기본 제공 Object( ) 객체 생성자 함수 이용
- 객체 리터럴을 이용
- 생성자 함수를 이용

<br><br>

## 3.2.1.1 Object( ) 생성자 함수 이용
자바스크립트에서는 객체를 생성할 때, 내장 Object( ) 생성자 함수를 제공한다. 

```javascript
// Object( )를 이용해서 foo 빈 객체 생성
var foo = new Object( );

// foo 객체 프로퍼티 생성
foo.name = 'foo';
foo.age = 30;
foo.gender = 'male';

console.log(typeof foo);        // (출력값) object
console.log(foo);        // (출력값) { name: 'foo', age: 30, gender: 'male' }
```
Object( ) 생성자 함수를 이용해서 foo라는 빈 객체를 생성한 후, 몇 가지 프로퍼티(name, age, gender)들을 추가한 것이다.   
<br><br>

## 3.2.1.2 객체 리터럴 방식 이용
리터럴이란 용어의 의미는 표기법이라고 생각하면 된다. 따라서 객체 리터럴이란 객체를 생성하는 표기법을 의미한다. 객체 리터럴 방식은 간단한 표기법만으로도 객체를 생성할 수 있는 자바스크립트의 강력한 문법이다.   
객체 리터럴은 중괄호({})를 이용해서 객체를 생성한다. { } 안에 아무것도 적지 않은 경우는 빈 객체가 생성되며, 중괄호 안에 "프로퍼티 이름":"프로퍼티 값" 형태로 표기하면, 해당 프로퍼티가 추가된 객체를 생성할 수 있다. 여기서 프로퍼티 이름은 문자열이나 숫자가 올 수 있다. 그리고 프로퍼티값으로는 자바스크립트의 값을 나타내는 어떤 표현식도 올 수 있으며, 이 값이 함수일 경우 이러한 프로퍼티를 메서드라고 부른다.   
```javascript
// 객체 리터럴 방식으로 foo 객체 생성
var foo = {
    name = 'foo',
    age = 30,
    gender = 'male'
};

console.log(typeof foo);        // (출력값) object
console.log(foo);        // (출력값) { name: 'foo', age: 30, gender: 'male' }
```
<br><br>

## 3.2.2 객체 프로퍼티 읽기/쓰기/갱신
객체는 새로운 값을 가진 프로퍼티를 생성하고, 생성된 프로퍼티에 접근해서 해당 값을 읽거나 또는 원하는 값으로 프로퍼티의 값을 갱신할 수 있다.   
<br>
객체의 프로퍼티에 접근하려면 두 가지 방법을 사용한다.
- 대괄호([ ]) 표기법
- 마침표( . ) 표기법

```javascript
// 객체 리터럴 방식을 통한 foo 객체 생성
var foo = {
    name = 'foo';
    major = 'computer science'
};

// 객체 프로퍼티 읽기                               ---------- 1
console.log(foo.name);                      // (출력값) foo
console.log(foo['name']);                   // (출력값) foo         
console.log(foo.nickname);                  // (출력값) undefined

// 객체 프로퍼티 갱신                               ---------- 2           
foo.major = 'electronics engineering';            
console.log(foo.major);                     // (출력값) electronics engineering
console.log(foo['major']);                  // (출력값) electronics engineering

// 객체 프로퍼티 동적 생성                         ----------  2
foo.age = 30;
consle.log(foo.age);                        // (출력값) 30

// 대괄호 표기법만을 사용해야 할 경우               ----------  3 
foo['full-name'] = 'foo bar';
console.log(foo['full-name']);              // (출력값) foo bar
console.log(foo.full-name);                 // (출력값) NaN
console.log(foo.full);                      // (출력값) undefined
console.log(name);                          // (출력값) undefined

```
1. 객체의 프로퍼티 접근은 대괄호 표기법이나 마침표 표기법으로 가능하다.   
마침표 표기법은 객체 다음에 마침표를 찍고 원하는 속성값을 적으면 된다.   
**대괄호 표기법**은 접근하려는 객체의 프로퍼티를 **문자열 형태**로 만든 다음 대괄호를 둘러싸면 된다. 여기서 주의할 점은 대괄호 표기법에서는 접근하려는 프로퍼티 이름을 문자열 형태로 만들어야 한다는 것이다.   
만약 console.log(foo['name']); --> console.log(foo[name]); 이라면   
'foo' 가 아닌 undefined 값이 출력된다.   
why? -> 자바스크립트에서는 대괄호 표기법에서 접근하려는 프로퍼티의 이름을 문자열 형태로 만들지 않으면 모든 자바스크립트 객체에서 호출 가능한 toString( )이라는 메서드를 자동으로 호출해서 이를 문자열로 바꾸려는 시도를 한다.    
만약, 객체에 없는 프로퍼티에 접근하는 경우는 undefined 값이 출력된다.   
<br>

2. **자바스크립트 객체의 프로퍼티에 값을 할당할 때, 프로퍼티가 이미 있을 경우는 해당 프로퍼티의 값이 갱신되지만,  객체의 해당 프로퍼티가 없을 경우에는 새로운 프로퍼티가 동적으로 생성된 후 값이 할당된다.**
<br>

3. 일반적으로 자바스크립트는 마침표 표기법을 이용해서 객체의 프로퍼티에 접근한느 방법을 주로 사용한다. 하지만 객체 프로퍼티에 접근할 때 대괄호 표기법만을 사용해야 하는 경우가 있다. 접근하려는 프로퍼티가 표현식이나 예약어일 경우다. 이 때는 대괄호 표기법만을 이용해서 접근해야 한다.   
3에서 'full-name'프로퍼티의 경우는 '-'연산자가 있는 표현식이다. 그래서 대괄호 표기법만을 이용해서 ['full-name']형태로 프로퍼티에 접근해야 한다.   

<br>
    
    NaN (Not a Number) 값
    자바스크립트에서 NaN은 수치 연산을 해서 정상적인 값을 얻지 못할 때 출력되는 값이다.

3. console.log(foo.full-name); 여기서 NaN이 출력된 이유는 foo.full(foo 객체의 full 프로퍼티의 저장된 값)과 name이라는 변수의 값을 - 연산자로 계산하는 표현식을 취급했기 때문이다. foo.full은 존재하지 않는 프로퍼티이므로 undefined 값을 가지면 name 또한 선언되지 않은 변수이므로 undefined 값을 가진다. 자바스크립트에서 undefined-undefined의 연산 결과가 NaN으로 정의되므로 foo.full-name의 결과로 NaN이 출력된 것이다.  
   
<br><br>

## 3.2.3 for in 문과 객체 프로퍼티 출력
for in 문을 사용하면, 객체에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다.
```javascript
// 객체 리터럴을 통한 foo 객체 생성
var foo = {
    name: 'foo',
    age: 30,
    major: 'computer science'
};

// for in 문을 이용한 객체 프로퍼티 출력
var prop;
for (prop in foo) {
    console.log(prop, foo[prop]);
}

[출력결과]
name foo
age 30
major 'computer science'
```
for in 문이 수행되면서 prop 변수에 foo 객체의 프로퍼티가 하나씩 할당된다. 따라서 prop에 할당된 프로퍼티 이름을 이용해서 foo[prop]와 같이 대괄호 표기법을 이용해서 프로퍼티값을 출력한 것이다.
<br><br><br>


## 3.2.4 객체 프롷퍼티 삭제
자바스크립트에서는 객체의 프로퍼티를 delete 연산자를 이용해 즉시 삭제할 수 있다. 여기서 주의할 점은 delete 연산자는 객체의 프로퍼티를 삭제할 뿐, 객체 자체를 삭제하지는 못한다는 것이다.
```javascript
// 객체 리터럴을 통한 foo 객체 생성
var foo = {
    name = 'foo',
    nickname = 'babo'
};

console.log(foo.nickname);                  // (출력값) babo
delete foo.nickname;                        // (출력값) nickname 프로퍼티 삭제
console.log(foo.nickname);                  // (출력값) undefined   --- 1

delete foo;                                 // (출력값) foo 객체 삭제 시도
console.log(foo.name;                       // (출력값) foo         --- 2
```
1. 자바스크립트에서는 존재하지 않는 프로퍼티에 접근할 경우 undefined 값이 출력된다.
2. delete 연산자는 프로퍼티만을 삭제하기 때문에 foo객체가 삭제되지 않았다.
   

<br><br><br>


## 3.3 참조 타입의 특성
자바스크립트에서는 기본 타입인 숫자, 문자열, 불린값, null, undefined 5가지를 제외한 모든 값은 객체다. 배열이나 함수 또한 객체로 취급된다. 그리고 이러한 객체는 자바스크립트에서 참조 타입이라고 부른다. 이것은 객체의 모든 연산이 실제 값이 아닌 참조값으로 처리되기 때문이다. 
```javascript
var objA = {
    val : 40                                    --- 1
};
var objB = objA;                                --- 2

console.log(objA.val);          // (출력값) 40  
console.log(objB.val);          // (출력값) 40

objB.val = 50;                                  --- 3
console.log(objA.val);          // (출력값) 50
console.log(objB.val);          // (출력값) 50
```
1. objA 객체를 리터럴 방식으로 생성했다. 여기서 objA 변수는 객체 자체를 저장하고 있는 것이 아니라 생성된 객체를 가리키는 참조값을 저장하고 있다는 것을 기억하자.
2. objA는 1에서 생성된 객체를 가리키는 참조값을 가지고 있으므로 변수 objB에도 이같은 객체의 참조값이 저장된다. 즉, objA 와 objB 변수가 동일한 객체를 가리키는 참조값을 가지게 되는 것이다. 
3. objA도 변수 objB와 동일한 객체를 참조하고 있으므로 objB가 가리키는 객체의 val값이 바뀌면 같이 변경된다.    

<br><br>


## 3.3.1 객체 비교
동등 연산자(==)를 사용하여 두 객체를 비교할 때도 객체의 프로퍼티값이 아닌 참조값을 비교한다는 것에 주의해야 한다.
```javascript
var a = 100;
var b = 100;

var objA = { value: 100 };
var objB = { value: 100 };
var objC = objB;

console.log(a == b);                       // (출력값)   true       --- 1
console.log(objA == objB);                 // (출력값)   false      --- 2
console.log(objB == objC);                 // (출력값)   true       --- 2
``` 
1. 값을 비교한다. 100이라는 동일한 값을 가지고 있다.
2. 참조값을 비교한다. 

<br><br>


## 3.3.2 참조에 의한 함수 호출 방식
기본 타입과 참조 타입의 경우는 함수 호출 방식도 다르다. 기본 타입의 경우는 **값에 의한 호출(Call By Value) 방식**으로 동작한다. 즉, 함수를 호출할 때 인자로 기본 타입의 값을 넘길 경우, 호출된 함수의 매개변수로 **복사된 값**이 전달된다. 때문에 함수 내부에서 매개변수를 이용해 값을 변경해도, 실제로 호출된 변수의 값이 변경되지는 않는다.   
이에 반해 객체와 같은 참조 타입의 경우 함수를 호출할 때 **참조에 의한 호출(Call By Reference) 방식**으로 동작한다. 즉, 함수를 호출할 때 인자로 참조 타입인 객체를 전달할 경우, 객체의 프로퍼티값이 함수의 매개변수로 복사되지 않고, 인자로 넘긴 객체의 참조값이 그대로 함수 내부로 전달된다. 때문에 함수 내부에서 참조값을 이용해서 인자로 넘긴 실제 객체의 값을 변경할 수 있는 것이다.
```javascript
var a = 100;
var objA = { value: 100 };

function changeArg(num, obj){
    num = 200;                      
    obj.value = 200;                

    console.log(num);
    console.log(obj);
}

changeArg(a, objA);                

console.log(a);
console.log(objA);


[출력결과]
200
{ value: 200 }
100
{ value: 200 }
```

<br><br>

## 3.4 프로토타입
자바스크립트의 **모든 객체는 자신의 부모 역할을 하는 객체와 연결되어 있다.** 그리고 이것은 마치 객체지향의 상속 개념과 같이 부모 객체의 프로퍼티를 마치 자신의 것처럼 쓸 수 있는 것 같은 특징이 있다. 자바스크립트에서는 이러한 부모 객체를 **프로토타입 객체**(짧게는 **프로토타입**)라고 부른다.
```javascript
var foo = {
    name: 'foo',
    age: 30
};

console.log(foo.toString());

console.dir(foo);
```
위에서 생성한 foo 객체는 toString( ) 메서드가 없으므로 에러가 발생해야 하지만, 정상적으로 결과가 출력되었다. 이유는 바로 **foo 객체의 프로토타입**에 toString( ) 메서드가 이미 정의되어 있고, foo 객체가 상속처럼 toString( ) 메서드를 호출했기 때문이다.   
자바스크립트의 **모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]]라는 숨겨진 프로퍼티**를 가진다고 설명하고 있다.   
위와 같이 객체 리터럴 방식으로 생성된 객체의 경우 Object.prototype 객체가 프로토타입 객체가 된다는 것만 기억하고 넘어가자. 또한, 객체를 생성할 때 결정된 프로토타입 객체는 임의의 다른 객체로 변경하는 것도 가능한다. 즉, 부모의 객체르 동적으로 바꿀 수도 있는 것이다. 자바스크립트에서는 이러한 특징을 활용해서 객체 상속 등의 기능을 구현한다.    
<br><br>

## 3.5 배열
배열은 자바스크립트 객체의 특별한 형태다. 굳이 크기를 지정하지 않아도 되며, 어떤 위치에 어느 타입의 데이터를 저장하더라도 에러가 발생하지 않는다.   
<br><br>

## 3.5.1 배열 리터럴
배열 리터럴은 자바스크립트에서 새로운 배열을 만드는 데 사용하는 표기법이다. 객체 리터럴이 중괄호({ })를 이용한 표기법이었다면, 배열 리터럴은 대괄호([ ])를 사용한다. 
```javascript
// 배열 리터럴을 통한 5개 원소를 가진 배열 생성
var colorArr = ['orange', 'yellow', 'blue', 'green', 'red'];
console.log(colorArr[0]);           // (출력값) orange
console.log(colorArr[1]);           // (출력값) yellow
console.log(colorArr[4]);           // (출력값) red
```
객체 리터럴에서는 프로퍼티 이름과 프로퍼티값을 모두 표기해야 하지만, 배열 리터럴에서는 **각 요소의 값**만을 포함한다. 그리고 해당 프로퍼티에 접근하려면 대괄호 내에 접근하고자 하는 원소에 **배열 내 위치 인덱스값**을 넣어서 접근한다.

<br><br>

## 3.5.2 배열의 요소 생성
객체가 동적으로 프로퍼티를 추가할 수 있듯이, 배열도 동적으로 배열 원소를 추가할 수 있다. 특히, 자바스크립트 배열의 경우는 값을 순차적으로 넣을 필요 없이 아무 인덱스 위치에나 값을 동적으로 값을 추가할 수 있다.
```javascript
// 빈 배열
var emptyArr = [ ];                                 --- 1
console.log(emptyArr[0]);           // (출력값) undefined

// 배열 요소 동적 생성
emptyArr[0] = 100;                                  --- 2
emptyArr[3] = 'eight';
emptyArr[7] = true;
console.log(emptyArr);
    // (출력값) [100, undefined x 2, "eight", undefined x 3, true]
console.log(emptyArr.length);       // (출력값) 8
```
1. 배열 또한 자바스크립트 객체이기 때문에 객체에서도 포함하지 않은 객체의 프로퍼티에 접근한 경우 undefined가 출력된 것과 같이 배열의 경우도 같이 없는 원소에 접근할 경우 undefined가 출력되는 것이다.
2. 배열 의 요소는 숫자나 문자열 같은 기본 타입의 값들을 포함해서, 객체나 함수, 배열 등과같이 자바스크립트의 모든 데이터 타입의 값을 포함할 수 있다. **자바스크립트는 배열의 크기를 현재 배열의 인덱스 중 가장 큰 값을 기준으로 정한다.**그리고 **모든 배열은 이러한 length 프로퍼티가 있다.**

<br><br>

## 3.5.3 배열의 length 프로퍼티
자바스크립트의 모든 배열은 **length 프로퍼티**가 있다. lengh 프로퍼티는 배열의 원소 개수를 나타내지만, 실제로 배열에 존재한는 원소 개수와 일치하는 것은 아니다. 즉, length 프로퍼티는 **배열 내에 가장 큰 인덱스에 1을 더한 값이다.** 때문에 배열의 가장 큰 인덱스 값이 변하면, length 값 또한 자동으로 그에 맞춰 변경된다.
```javascript
var arr = [ ];
console.log(arr.length);            // (출력값) 0

arr[0] = 0;     // arr.length = 1
arr[1] = 1;     // arr.length = 2
arr[2] = 2;     // arr.length = 3
arr[100] = 100;
console.log(arr.length);            // (출력값) 101
```
실제 메모리는 length 크기처럼 할당되지는 않는다.
배열의 length 프로퍼티는 코드를 통해 명시적으로 값을 변경할 수도 있다.
```javascript
var arr = [0, 1, 2];
console.log(arr.length);            // (출력값) 3

arr.length = 5;
console.log(arr);                   // (출력값) [0, 1, 2, undefined x 2]

arr.length = 2;
console.log(arr);                   // (출력값) [0, 1]
console.log(arr[2]);                // (출력값) undefined           --- 3
```
3. length 프로퍼티를 벗어나는 실제 값은 삭제된다. 때문에 console.log(arr[2]) 값이 undefined로 출력되는 것이다.    

<br><br>

## 3.5.3.1 배열 표준 메서드와 length 프로퍼티
자바스크립트는 배열에서 사용 가능한 다양한 표준 메서드를 제공하낟. 이러한 배열 메서드는 **length 프로퍼티**를 기반으로 동작하고 있다.
```javascript
// arr 배열 생성
var arr = ['zero', 'one', 'two'];

// push( ) 메서드 호출
arr.push('three');
Console.log(arr);       // (출력값) ['zero', 'one', 'two', 'three']

// length 값 변경 후, push( ) 메서드 호출
arr.length = 5;
arr.push('four');
console.log(arr);       // (출력값) ['zero', 'one', 'two', 'three', undefined, 'four']
``` 
push( ) 메서드는 인수로 넘어온 항목을 배열의 끝에 추가하는 자바스크립트 표준 배열 메서드다. 이 메서드는 배열의 현재 length 값의 위치에 새로운 원소값을 추가한다.   
arr.length 프로퍼티값을 임의로 5러 비꾼 후 push( ) 메서드를 호출하게 되면 push( ) 메서드는 현재 변경된 arr.length가 가리키는 배열의 5번째 인덱스, arr[5]에 'four'문자열을 추가하게 된다. 배열의 length 프로퍼티는 배열 메서드의 동작에 영향을 줄 수 있을만큼 중요한 프로퍼티이므로 반드시 기억하도록 하자.   
<br><br>

## 3.5.4 배열과 객체
```javascript
// colorsArray 배열                                             --- 1
var colorArry = ['orange', 'yellow', 'green'];
console.log(colorsArray[0]);            // (출력값) orange
console.log(colorsArray[1]);            // (출력값) yellow
console.log(colorsArray[2]);            // (출력값) green

// colorsObj 객체
var colorsObj = {
    '0': 'orange',
    '1': 'yellow',
    '2': 'green'
};
console.log(colorsObj[0]);              // (출력값) orange
console.log(colorsObj[1]);              // (출력값) yellow
console.log(colorsObj[2]);              // (출력값) green

// typeof 연산자 비교                                           --- 2
console.log(typeof colorsArray;         // (출력값) object (not array)
console.log(typeof colorsObj);          // (출력값) object

// length 프로퍼티                                              --- 3
console.log(colorsArray.length);        // (출력값) 3
console.log(colorsObj.length);          // (출력값) undefined

// 배열 표준 메서드                                             --- 4
colorsArray.push('red');                // ['orange', 'yellow', 'green', 'red']
colorsObj.push('red');
        // Uncaught TypeError: Object #<Object> has no method 'push'
```
1. 객체의 프로퍼티 접근을 할 때, 대괄호 안에는 접근하려는 프로퍼티의 속성을 **문자열 형태**로 적어야 한다. 때문에 colorsObj[0]이 아니라 colorsObj['0']의 형태로 기입하는 것이 맞다. 자바스크립트 엔진이 [ ] 연산자 내에 숫자가 사용될 경우, 해당 숫자를 자동으로 문자열 형태로 바꿔주기 때문에 정상적인 결과가 출력되었다.
2. typeof 연산 결과는 배열과 객체가 모두 **object**라는 것을 기억하자. 자바스크립트도 배열을 객체라고 생각한다는 것이다.
3. 배열 colorsArray와 객체 colorsObj는 근본적으로 차이가 있다. 우선 colorsObj는 객체이므로 length 프로퍼티가 존재하지 않는다. 
4. colorsObj는 배열이 아니므로 push( )와 같은 표준 배열 메서드를 사용할 수 없다. 이것은 배열과 객체가 자신의 부모인 프로토타입 객체가 서로 다르기 때문이다.   
   <br>
객체 --------------> Object.prototype    
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[[Prototype]]   
배열 --------------> Array.prototype --------------> Object.prototype   
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[[Prototype]]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[[Prototype]]   
<br>

```javascript
var emptyArray = [ ];       // 배열 리터럴을 통한 빈 배열 생성
var emptyObj = { };         // 객체 리터럴을 통한 빈 객체 생성

console.log(emptyArray.__proto__);      // 배열의 프로토타입(Array.protorype) 출력
console.log(emptyObj.__proto__);      // 배열의 프로토타입(Object.protorype) 출력
```
<br><br>

## 3.5.5 배열의 프로퍼티 동적 생성
배열도 자바스크립트 객체이므로, 인덱스가 숫자인 배열 원소 이외에도 객체처럼 동적으로 프로퍼티를 추가할 수 있다.   
```javascript
[예제 3-20]

// 배열 생성
var arr = ['zero', 'one', 'two'];
console.log(arr.length);            // (출력값) 3

// 프로퍼티 동적 추가
arr.color = 'blue';
arr.name = 'number_array';
console.log(arr.length);            // (출력값) 3

// 배열 원소 추가
arr[3] = 'red';
console.log(arr.length);            // (출력값) 4

// 배열 객체 출력
console.dir(arr);
```
배열에 동적 프로퍼티가 추가될 경우에는 배열의 length 값이 3으로 바뀌지 않는다는 것이다. 그런 다음 다시 arr[3]에 배열 원소를 추가했을 때 length 값이 4로 바꼈음을 확인할 수 있다. 즉, **배열의 length 프로퍼티는 배열 원소의 가잗 큰 인텍스가 변했을 경우만 변경된다.**   
<br>

    [console.dir(arr)로 arr배열의 모든 프로퍼티 출력 결과]
    Array[4]
        0: "zero"
        1: "one"
        2: "two"
        3: "red"
        color: "blue"
        length: 4
        name: "number_array"
    __proto__: Array[0]
-> 배열도 객체처럼 'key: value' 형태로 배열 원소 및 프로퍼티 등이 있음을 알 수 있다.   
<br><br>

## 3.5.6 배열의 프로퍼티 열거
객체는 for in 문으로 프로퍼티를 열거한다고 설명했다. 배열도 객체이므로 for in 문을 사용해서 배열 내의 모든 프로퍼티를 열거할 수 있지만, 이렇게 되면 불필요한 프로퍼티가 출력될 수 있으모르 되도록 for 문을 사용하는 것이 좋다.   
앞의 예제 3-20에서 arr 배열을 for in 문과 for 문을 이용해서 출력해보자.
```javascript
for (var prop in arr) {
    console.log(prop, arr[prop]);
}

for (var i = 0, i < arr.length, i++) {
    console.log(i, arr[i]);
}

[출력결과]
0 zero
1 one
2 two
3 red
color blue
name number_array


0 "zero"
1 "one"
2 "two"
3 "red"
```
<br><br>

## 3.5.7 배열 요소 삭제
배열도 객체이므로, 배열요소나 프로퍼티를 삭제하는 데 delete 연산자를 사용할 수 있다.
```javascript
var arr = ['zero', 'one', 'two', 'three'];
delete arr[2];
console.log(arr);           // (출력값) ["zero", "one", undefined x 1, "three]
console.log(arr.length);    // (출력값) 4
```
delete 연산자는 해당 요소의 값을 undefined로 설정할 뿐 원소 자체를 삭제하지는 않는다. 때문에 보통 배열에서 요소들을 완전히 삭제할 경우 자바스크립트에서는 **splice( ) 배열 메서드**를 사용한다.

    splice( ) 배열 메서드
    splice(start, deleteCount, item...)
     - start - 배열에서 시작 위치
     - deleteCount : start에서 지정한 시작 위치부터 삭제할 요소의 수
     - item : 삭제할 위치에 추가할 요소

```javascript
var arr = ['zero', 'one', 'two', 'three'];

arr.splice(2, 1);               // 2번째 요소를 시작점으로 1개의 원소를 삭제한다.
console.log(arr);               // (출력값) ['zero', 'one', 'three']
console.log(arr.length);        // (출력값) 3
```
delete 연산자와는 다르게 배열 요소를 완전히 없애게 된다. 따라서 배열의 요소 개수도 3개가 됐다.   
<br><br>

## 3.5.8 Array( ) 생성자 함수
배열은 일반적으로 배열 리터럴로 생성하지만, 배열 리터럴도 결국 자바스크립트 기본 제공 **Array( ) 생성자 함수**로 배열을 생성하는 과정을 단순화시킨 것이다. 생성자 함수로 배열과 같은 객체를 생성할 때는 반드시 new 연산자를 같이 써야한다는 것을 기억하자.   
Array( ) 생성자 함수는 호출할 때 인자 개수에 따라 동작이 다르므로 주의해야 한다.   
- 호출할 때 인자가 1개이고, 숫자일 경우 : 호출된 인자를 length로 갖는 빈 배열 생성
- 그 외의 경우 : 호출된 인자를 요소로 갖는 배열 생성

```javascript
var foo = new Array(3);
console.log(foo);               // (출력값) [undefined, undefined, undefined]
console.log(foo.length);        // (출력값) 3

var bar = new Array(1, 2, 3);
console.log(bar);               // (출력값) [1, 2, 3]
console.log(bar.length);        // (출력값) 3
```
<br><br>

## 3.5.9 유사 배열 객체
일반 객체에 length라는 프로퍼티가 있으면 어떻게 될까? 자바스크립트에서는 이렇게 length 프로퍼티를 가진 객체를 **유사 배열 객체(array-like objects)**라고 부른다. 유사 배열 객체의 가장 큰 특징은 객체임에도 불구하고, 자바스크립트의 표준 배열 메서드를 사용하는 게 가능하다는 것이다.
```javascript
var arr = ['bar'];
var obj = {                     // obj는 유사 배열 객체
    name : 'foo',
    length : 1
};

arr.push('baz');
console.log(arr);               // (출력값) ['bar', 'baz']

obj.push('baz');                // (출력값) error
```
유사 배열 객체 obj는 당연히 배열이 아니므로 push( ) 메서드를 호출 할 경우 에러가 발생한다. 유사 배열 객체의 경우 **apply( ) 메서드**를 사용하면 객체지만 표준 배열 메서드를 활용하는 것이 가능하다.   
```javascript
var arr = ['bar'];
var obj = { name : 'foo', length : 1 };

arr.push('baz');
console.log(arr);               // (출력값) ['bar', 'baz']

Array.prototype.push.apply(obj, ['baz']);
console.log(obj);               // (출력값) { '1': 'baz, name: 'foo', length: 2 }
```
<br><br>

## 3.6 기본 타입과 표준 메서드
자바스크립트는 숫자, 문자열, 불린값에 대해 각 타입별로 호출 가능한 표준 메서드를 정의하고 있다. 하지만 기본 타입의 경우는 객체가 아닌데 어떻게 메서드를 호출할 수 있을까?   
기본 타입의 값들에 대해서 객체 형태로 메서드를 호출할 경우, 이들 기본값은 메서드 처리 순간에 객체로 변환된 다음 각 타입별 표준 메서드(예제의 경우 toExponential()이나 charAt())를 호출하게 되는 것이다. 그리고 메서드 호출이 끝나면 다시 기본값으로 복귀하게 된다.
```javascript
// 숫자 메서드 호출
var num = 0.5;
console.log(num.toExponential(1));              // (출력값) '5.0e-1'

// 문자 메서드 호출
console.log("test".charAt(2));                  // (출력값) 's'
```
**toExponential( )**는 표준 숫자형 메서드로서, 숫자를 지수 형태의 문자열로 반환한다. 인자로 받는 값은 소수점 아래 몇 번째 자리까지 표시할 것인지 지정한는 것이다.   
표준 문자열 메서드 **charAt( )**은 문자열에서 인자로 받은 위치에 있는 문자르 반환한다.   
이렇듯 숫자와 문자열 등은 기본 타입이지만, 이들을 위해 정의된 표준 메서드들을 **객체처럼 호출할 수 있다**는 것을 기억하자.   
<br><br>

## 3.7 연산자
## 3.7.1 +연산자
'+'연산자는 **더하기 연산**과 **문자열 연결 연산**을 수행한다.
```javascript
var add1 = 1 + 2;
var add2 = 'my ' + 'string';
var add3 = 1 + 'string';
var add4 = 'string' + 2;

console.log(add1);                  // (출력값) 3
console.log(add2);                  // (출력값) my string
console.log(add3);                  // (출력값) 1string
console.log(add4);                  // (출력값) string2
```
<br><br>

## 3.7.2 typeof 연산자
typeof 연산자는 피연산자의 타입을 문자열 형태로 리턴한다. 여기서 null과 배열이 'object'라는 점, 함수는 'functon'이라는 점에 유의해야 한다.   

[각 타입별 typeof 연산자 결과]   
&nbsp; |&nbsp; |&nbsp;
:---: | :---: | :---:
기본타입 | 숫자 | 'number'
기본타입 | 문자열 | 'string'
기본타입 | 불린값 | 'boolean'
기본타입 | **null** | **'object'**
기본타입 | undefined | 'undefined'
참조타입 | 객체 | 'object'
참조타입 | **배열** | **'object'**
참조타입 | **함수** | **'function'**

<br><br>

## 3.7.3 == (동등) 연산자와 === (일치) 연산자
자바스크립트에서는 두 값이 동일한지를 확인하는 데, 두 연산자를 모두 사용할 수 있다.  두 연산자의 차이는 == 연산자는 비교하려는 피연산자의 타입이 다를 경우에 타입 변환을 거친 다음 비교한다. 반면에 === 연산자는 피연산자 타입이 다를 경우에 타입을 변경하지 않고 비교한다.
```javascript
console.log(1 == '1');              // (출력값) true
console.log(1 === '1');             // (출력값) false
```
== 연산자의 비교는 타입 변환에 따른 잘못된 결과를 얻을 수 있으므로 대부분 자바스크립트 코딩 가이드에서는 == 연산자로 비교하는 것을 추천하지 않는다. === 연산자로 비교하기를 권하고 있다.   
<br><br>

## 3.7.4 !! 연산자
!! 의 역할은 피연산자를 불린값으로 변환하는 것이다.   
```javascript
console.log(!!0);                           // (출력값) false
console.log(!!1);                           // (출력값) true
console.log(!!'string');                    // (출력값) true
console.log(!!'');                          // (출력값) false
console.log(!!true);                        // (출력값) true
console.log(!!false);                       // (출력값) false
console.log(!!null);                        // (출력값) false
console.log(!!undefined);                   // (출력값) false
console.log(!!{});                          // (출력값) true
console.log(!![1, 2, 3]);                   // (출력값) true
```
객체는 값이 비어있는 빈 객체라도 true로 변환되는 것을 주의해야 한다.