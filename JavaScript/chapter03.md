#  3. 자바스크립트 데이터 타입과 연산자

[자바스크립트 데이터 타입]

- 기본 데이터 타입(숫자, 문자열, 불린값, null, undefined)
- 참조 데이터 타입(객체, 배열)
- 주의해야 할 연산자

## **3.1 자바스크립트 기본 타입**
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

## **3.1.1 숫자**
자바는 정수냐 실수냐에 따라 int, long, double, float 등과 같은 다양한 숫자 타입이 존재하지만, 자바스크립트는 하나의 숫자형만 존재한다. var 키워드로 선언된 자바스크립트 변수에는 정수나 실수 구분 없이 그 값을 바로 저장할 수 있으므로, intNum 과 floatNum 변수 모두 typeof 연산자의 결과값이 number 타입임을 확인 할 수 있다.    
자바스크립트에서는 정수형이 따로 없고, 모든 숫자를 실수로 처리하므로 나눗셈을 연산할 때 소수 부분까지 출력된다.
```javascript
var num = 5 / 2;

console.log(num);   // (출력값)  2.5
console.log(Math.floor(num));   // (출력값)  2
```
<br><br>

## **3.1.2 문자열**
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

## **3.1.3 불린값**
자바스크립트는 true 와 false 값을 나타내는 불린 타입을 가진다.   
<br><br>

## **3.1.4 null 과 undefined**
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
