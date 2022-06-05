## 1주차
### 2. 자바스크립트 기초(2)
#### 2.1 let,const, scope
- **var** : 함수 단위
- **let** : block 단위 (변수: let으로 선언한 변수는 값이 변할 수 있다.)
- **const**: block 단위(상수: 한번 선언한 값은 바꿀 수 없다.)
- 스코프(Scope)란 어떤 변수를 선언했을 때, 그 변수를 사용할 수 있는 유효 범위를 스코프라고 한다.

```javascript
function scope(){
 const a = 0;
 let b = 0;
 var c = 0;

 // {} 증괄호 안에 든 내용을 블럭이라고 표현해요.
 
 if(a === 0){
  const a = 1;
  let b = 1;
  var c = 1;
  console.log(a, b, c);
 }
 // 앗! c는 값이 변했죠? 
 // 그렇습니다. var는 함수 단위라서 if문 밖에서 선언한 값이 변했어요.
 // let과 const로 선언한 겂은 어떤가요? if문 안쪽 내용이 바깥 내용에 영향을 끼치지 않죠?
 console.log(a, b, c);
}
```

#### 2.2 함수
- 함수는 **function do_something() { ... }** 처럼 생긴 것들을 말한다.
- 어떤 코드의 묶음이고, **do_something()** 처럼 ()를 붙여주면 미리 만들어둔 코드 묶음이 실행되는 것이다.
- **내장 함수**는 직접 만들지 않아도 자바스크립트가 쓰기 편하라고 미리 만들어둔 코드 묶음들이다.

#### 2.3 Class
- 객체 지향 프로그래밍에서 클래스는 **특정 객체를 생성하기 위해 변수와 함수를 정의하는 일종의 틀**을 말한다.
- 객체를 정의하기 위한 상태와 함수로 구성되어 있다.
- 객체 단위로 코드를 그룹화하고 쉽게 재사용하려고 사용한다.
- 클래스 안에는 객체를 정의하기 위한  **상태(property)** 와 함수가 있다.

```javascript
class Cat {
 // 생성자 함수
  constructor(name) {
  // 여기서 this는 이 클래스입니다.
  this.name = name; 
 }

 // 함수
 showName(){
  console.log(this.name);
 }
}

// 여기서 new는 키워드예요. 새로운 무언가를 만들기 위해서 생성자 함수와 함께 씁니다.
// 네, new와 생성자 함수는 세트예요 :) (소근 
let cat = new Cat('perl');
cat.showName();
console.log(cat);
```

  - **생성자 함수**: 클래스 인스턴스를 생성하고 생성한 인스턴스를 초기화(초기 값을 설정한다)하는 역할을 한다.
  - **함수**: 어떤 일을 하는 함수이다.
- 클래스를 상속한다는 건, **이미 만들어 둔 어떤 클래스를 가지고 자식 클래스를 만든다는 것이다.**

```javascript
class Cat {
 // 생성자 함수
  constructor(name) {
  // 여기서 this는 이 클래스입니다.
  this.name = name; 
 }

 // 함수
 showName(){
  console.log(this.name);
  return this.name;
 }
}

// extends는 Cat 클래스를 상속 받아 온단 뜻입니다.
class MyCat extends Cat {
 // 생성자 함수
  constructor(name, age) {
  // super를 메서드로 사용하기
  super(name); 
  this.age = age; 
 }
 
 // 부모 클래스가 가진 것과 같은 이름의 함수를 만들 수 있습니다.
 // 오버라이딩한다고 해요.
 showName(){
  console.log(this.name);
  // super를 키워드로 사용하기
  return '내 고양이 이름은 '+super.showName()+'입니다.';
 }
 
 showAge(){
  console.log('내 고양이는 '+this.age+'살 입니다!');
 }
}

let my_cat = new MyCat('perl', 4);
my_cat.showName();
my_cat.showAge();
```

- **super 키워드**
  - 메소드로 사용할 수 있다.(constructor 안에서)
    - 부모의 **constructor**를 호출하면서 인수를 전달한다.
    - **this**를 쓸 수 있게 해준다.
  - 키워드로 사용할 수 있다.
    - 부모 클래스에 대한 필드나 함수를 참조할 수 있다.

### 2.4 =와 ==와 ===
- **=** 는 할당을 뜻한다. 어떤 변수에 값을 할당할 때 쓴다.
- **==** 는 등차이다. 유형을 비교하지 않는 등차이다. 변수 값을 기반으로 비교한다. (ex. 0 == "0"은 true를 반환한다.)
- **===** 도 등차이다. 유형도 비교하는 등차이다. 엄격한 비교라고 생각하면 된다. (ex. 0 === "0"은 false를 반환한다. → 0은 숫자(number)고, "0"은 문자(string)이기 때문이다.)

### 2.5 Spread 연산자 (Spread 문법)
- 어떤 객체 안에 있는 요소들을 객체 바깥으로 꺼내주는 것이다.

```javascript
let array = [1,2,3,4,5];
// ... <- 이 점 3개를 스프레드 문법이라고 불러요.
// 배열 안에 있는 항목들(요소들)을 전부 꺼내준다는 뜻입니다.
// 즉 [...array]은 array에 있는 항목을 전부 꺼내 
// 새로운 배열([] => 이 껍데기가 새로운 배열을 뜻하죠!)에 넣어주겠단 말입니다!
let new_array = [...array];

console.log(new_array);
```

### 2.6 조건부 삼항 연산자
- 삼항 연산자는 if문의 단축 형태이다.
- **사용법: 조건 ? 참일 경우 : 거짓일 경우**
