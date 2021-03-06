## 1주차
### 1. 자바스크립트 기초(1)
#### 1.1 document로 DOM에 접근하기
##### document.getElementsByClassName

```javascript
const wraps = document.getElementsByClassName("wrap");
console.log(wraps);
```

##### document.getElementById

- 이번에는 id로 DOM 요소에 접근할 수 있다. 자바스크립트를 사용해서 CSS 변경도 가능하다. 
```javascript
const title = document.getElementById("title");
// 자바스크립트에서는 어떤 객체의 속성에 접근할 때 .을 이용해 접근할 수 있어요.
// title이라는 요소의 style 속성에 접근하려면 아래와 같이 title.style로 접근할 수 있습니다!
// style 안에 있는 속성에 접근할 때도 마찬가지예요. style.backgroundColor로 배경색 속성에 접근할 수 있어요.
title.style.backgroundColor = "yellow";
```

##### document.getElementsByTagName
- 태그명으로도 조작이 가능하다. 버튼을 눌렀을 때 onClick 이벤트를 발생시키는 것도 가능하다.

```javascript
function sayHello (event) {
            console.log("hello");             
         }

         const buttons = document.getElementsByTagName("button");

        // 이 구문은 X! html collection은 유사 배열이기 때문에 array의 내장함수를 쓸 수 없어요!
        //buttons.map(b => {
            //console.log(b);
        //});        

        for (let i=0; i< buttons.length; i++){
            // .addEventListener()로 클릭 이벤트를 연결해줍니다. 
            buttons[i].addEventListener("click", sayHello);
        }
```

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

#### 2.4 =와 ==와 ===
- **=** 는 할당을 뜻한다. 어떤 변수에 값을 할당할 때 쓴다.
- **==** 는 등차이다. 유형을 비교하지 않는 등차이다. 변수 값을 기반으로 비교한다. (ex. 0 == "0"은 true를 반환한다.)
- **===** 도 등차이다. 유형도 비교하는 등차이다. 엄격한 비교라고 생각하면 된다. (ex. 0 === "0"은 false를 반환한다. → 0은 숫자(number)고, "0"은 문자(string)이기 때문이다.)

#### 2.5 Spread 연산자 (Spread 문법)
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

#### 2.6 조건부 삼항 연산자
- 삼항 연산자는 if문의 단축 형태이다.
- **사용법: 조건 ? 참일 경우 : 거짓일 경우**

### 3. 자바스크립트 기초(3)
- 자바스크립트에서 자주 사용하는 **내장 함수들**이다.

#### 3.1 map
- map은 **배열에 속한 항목을 변환할 때** 많이 사용한다.
- 어떤 배열에 속한 항목을 원하는 대로 변환하고, 변환한 값을 새로운 배열로 만들어준다.
- **즉, 원본 배열은 값이 변하지 않는다.**

```javascript
const array_num = [0, 1, 2, 3, 4, 5];

const new_array = array_num.map((array_item) =>{ 
 return array_item + 1;
});
// 새 배열의 값은 원본 배열 원소에 +1 한 값입니다.
console.log(new_array);
// 원본 배열은 그대로 있죠!
console.log(array_num);
```

#### 3.2 filter
- **filter** 는 어떤 조건을 만족하는 항목들만 골라서 새 배열로 만들어주는 함수이다.
- 원본 배열은 변하지 않고, **원하는 배열을 하나 더 만들 수 있다.**

```javascript
const array_num = [0, 1, 2, 3, 4, 5];

// forEach(콜백함수)
const new_array = array_num.filter((array_item) => {
 // 특정 조건을 만족할 때만 return 하면 됩니다!
 // return에는 true 혹은 false가 들어가야 해요.
 return array_item > 3;
});

console.log(new_array);
```

#### 3.3 concat
- **concat**은 배열과 배열을 합치거나 배열에 특정 값을 추가해주는 함수이다.
- 원본 배열은 변하지 않는다. concat은 중복 항목을 제거해주지 않는다. **다른 내장함수와 함께 사용해서 제거해야 한다.**

```javascript
const array_num01 = [0, 1, 2, 3];
const array_num02 = [3, 4, 5];

const merge = array_num01.concat(array_num02);

// 중복 항목(숫자 3)이 제거되었나요? 아니면 그대로 있나요? :)
console.log(merge);
```

- 아래 방법도 자주 사용하는 방법이다.

```javascript
const array_num01 = [0, 1, 2, 3];
const array_num02 = [3, 4, 5];
// Set은 자바스크립트의 자료형 중 하나로, 
// 중복되지 않는 값을 가지는 리스트입니다. :)!
// ... <- 이 점 3개는 스프레드 문법이라고 불러요.
// 배열 안에 있는 항목들(요소들)을 전부 꺼내준다는 뜻입니다.
// 즉 [...array_num01]은 array_num01에 있는 항목을 전부 꺼내 
// 새로운 배열([] 이 껍데기가 새로운 배열을 뜻하죠!)에 넣어주겠단 말입니다!
const merge = [...new Set([...array_num01, ...array_num02])];

// 중복 항목(숫자 3)이 제거되었나요? 아니면 그대로 있나요? :)
console.log(merge);
```

#### 3.4 from
- from은 쓰임새가 다양하다.
  - 배열로 만들고자 하는 것이나 유사배열을 복사해서 새로운 배열로 만들 때
  - 새로운 배열을 만들 때 (초기화할 때)

- 유사배열이란?
- **[ 어떤 값들... ]** 이 모양으로 생겼지만 배열의 내장 함수를 사용하지 못하는 것이다. **DOM nodelist** 같은 게 유사배열이다.

```javascript
// 배열화 하자!
const my_name = "mean0";
const my_name_array = Array.from(my_name);
console.log(my_name_array);

// 길이가 문자열과 같고, 0부터 4까지 숫자를 요소로 갖는 배열을 만들어볼거예요. 
const text_array = Array.from('hello', (item, idx) => {return idx});

console.log(text_array);


// 새 배열을 만들어 보자!(=> 빈 배열을 초기화한다고도 해요.)
// 길이가 4고, 0부터 3까지 숫자를 요소로 갖는 배열을 만들어볼거예요. 
const new_array = Array.from({length: 4}, (item, idx)=>{ return idx;});

console.log(new_array);
```
