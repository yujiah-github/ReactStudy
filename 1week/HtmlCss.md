## 1주차
### 1. 프론트엔드 기초 지식
#### 1.1 서버와 클라이언트
##### 웹의 동작 개념
- 우리가 보는 웹페이지는 모두 서버에서 미리 준비해두었던 것을 받아서 그려주는 것이다.
- 즉, 브라우저가 하는 일은 **1) 요청을 보내고, 2) 받은 HTML 파일을 그려주는 일** 뿐이다.
- 서버가 만들어 놓은 "API"라는 창구에 미리 정해진 약속대로 요청을 보내는 것이다.
- 예) <https://naver.com/> → 이것은 "naver.com"이라는 이름의 서버에 있는, "/" 창구에 요청을 보내는 것이다.
![](https://velog.velcdn.com/images/cil05265/post/d8241c9f-c88c-497f-8598-b6f8179b0a0c/image.png)


##### 웹의 동작 개념(데이터만 받는 경우)
- 항상 HTML만 내려주는 경우보다 데이터만 내려 줄 때가 더 많다.
- 예) 공연 티켓을 예매하고 있는 상황에서, 좌석이 차고 꺼질때마다 보던 페이지가 리프레시 되면 난감할 것이다. 이럴 때, 데이터만 받아서 받아 끼우게 된다.
![](https://velog.velcdn.com/images/cil05265/post/91ccf4aa-eeb9-4518-a3c1-b539ff857690/image.png)

- 데이터만 내려올 경우는, 이런 형태이다. 이런 생김새를 JSON 형식이라고 한다.
![](https://velog.velcdn.com/images/cil05265/post/a8882ff3-4f5b-495e-8950-03c4755c5012/image.png)

##### 서버와 클라이언트란?
- 클라이언트는 웹사이트를 보는 도구 **(휴대폰, PC, 아x패드 ...)**가 모두 클라이언트이다. 서버는 우리가 보는 웹사이트에 뿌려줄 것(html이나 데이터)을 만들어서 클라이언트에 전달해주는 것이다.

#### 2. 프론트엔드 개발자가 할 일은?
- 우선, **화면을 그린다.** 눈에 보이는 부분을 만든다. 어디에는 글이 들어가고, 어디에는 아이콘을 넣어주고 ..., 더 나아가서는 마우스를 올릴 때만 글자색을 바꿔주는 등의 작업(인터렉션을 준다고 해요!)도 해준다.
- 서버에서 데이터를 가지고 와서 만든 화면에 넣어준다.

#### 3. 서버리스란?
- 서버리스라고 하면 아예 백엔드 개발을 안해도 되는 것이라고 오해를 하지만 그런 의미가 아니다. **서버리스라는 것은 내가 서버를 만들 필요가 없다**는 것이다.

##### 서버리스가 뭘까?
- **서버의 사양, 네트워크 설정 같은 게 미리 되어 있는 서버를 빌려 쓰니, 인프라 작업을 내가 안해도 된다**는 것이다.
- 즉, 서버리스가 백엔드리스라는 의미는 아니다.

### 2. 알면 쉬운데 모르면 괴로운 HTML
- **HTML(Hypertext Markup Language)은 마크업 언어** 이다.
- 마크업은 이름 그대로 표시하는 것이다.
- 우리가 보는 웹페이지는 그림도 있고, 글도 있고 표도 있고, 여러가지 요소가 잔뜩 들어있다. **"여기는 글자 영역이고 여기는 이미지 영역이야!"라고 표시해서 브라우저가 웹페이지를 잘 그릴 수 있도록** 하는 게 HTML이다.

##### 퀴즈 풀이 화면
![](https://velog.velcdn.com/images/cil05265/post/c7dba4d9-dcb8-4238-a65a-771f237b63fc/image.png)


#### 2.1 Dom
```html
<div>안녕</div>, <p>하세요</p>, <button>확인</button>
```
- 위의 예시들을 **태그(tag)**라고 생각할 수 있다. 그러나, 이것들은 **요소(elements)**라고 부른다.
- 태그는 요소를 사용할 때 만드는 **<>** 를 태그라고 한다.

- **DOM(문서객체모델)**은 html 단위 하나하나를 객체로 생각하는 모델이다.
- 예를 들면, 'div'라는 객체는 텍스트 노드, 자식 노드 등등, 하위의 어떤 값을 가지고 있다.
- 이런 구조를 **트리 구조**라고 하고, **DOM은 트리구조**이다.

#### 2.2 Dom 트리 확인하기
```javascript
// 현재 dom 트리를 볼 수 있어요. 
document

// dom 트리 중, body의 내용을 확인합니다.
document.body

// dom 트리 중, head의 내용을 확인합니다.
document.head
```

- document와 body, head는 **부모자식 관계**이다. body랑 head는 **형제 관계**이다. (sibling이라고도 한다.)

#### 2.3 자식 요소에 접근하기
```javascript
//childNodes에 접근하기
document.body.childNodes

//children에 접근하기
document.body.children

//getElementsByTagName("태그 이름")에 접근하기
document.getElementsByTagName("div")
```

### 3. 알면 쉬운데 모르면 괴로운 CSS
#### 3.1 Selector
- **selector는 꾸밀 요소를 선택하는 선택자**이다. 뭘 꾸밀 지 선택하고 속성을 넣어 예쁘게 꾸며주는 것이다.

```javascript
/*id selector*/
**#**id { ... }

/*class selector*/
**.**class { ... }

/*tag selector*/
**tagName** { ... }

/*여러 요소 선택하기*/
# id, .class { ... }

/*수도 클래스 선택자*/
/*어떤 요소가 특정 상태(마우스 올림, 포커스 됨 등등)일 때만 선택하게 해주는 선택자예요.*/
**button**:hover { ... }
```
- #id, .class를 선택자라고 부르는데, { ... }은 **선언부**라고 부른다. 속성 : 값;으로 이루어져 있다.

##### CSS를 적용한 예시
![](https://velog.velcdn.com/images/cil05265/post/efdb3944-48ac-4df8-ac0d-485b7fa245d3/image.png)

#### 3.2 그리드 시스템
- **margin box:** 가장 바깥 영역이다. margin 속성을 주면 이 영역이 바뀐다. 주로 다른 요소들과 간격을 줄 때 사용한다.
- **border box:** 테두리 영역이다. border 속성으로 테두리를 주면 이 영역이 바뀐다.
- **padding box:** 테두리와 콘텐츠 사이 영역이다. padding 속성을 주면 이 영역이 바뀐다. 박스 내부의 간격을 줄 때 사용한다.
- **contents box:** 실제 콘텐츠 영역이다. width, height 등으로 사이즈를 줄 수 있고, 따로 지정하지 않을 경우는 콘텐츠 내용(글이나 이미지 등)에 따라 임의로 사이즈가 잡힌다.

![](https://velog.velcdn.com/images/cil05265/post/30b8be0d-b19d-48de-a658-67c05a5a1571/image.png)

- 그리드 시스템은 **레이아웃**을 잡는데 사용하는 것이다.
- 예를 들자면, todo-card를 두 줄로 보여주고 싶을 때처럼, 가로, 세로를 나누어 화면 배치를 만져주는 것이다.
- flex 하나만 알아보았지만, 레이아웃을 잡을 때는 사실 **table, block, grid** 등 아주 다양한 방법을 사용한다.

##### 그리드 적용 예시
![](https://velog.velcdn.com/images/cil05265/post/beeccba6-0426-49cd-94ee-5c682d3ff07a/image.png)

#### 3.3. css 사칙 연산

- css도 **calc()를 사용하여** 연산이 가능하다.
- calc()는 **왼쪽에서 오른쪽으로, 곱셈, 나눗셈을 먼저, 덧셈, 뺄셈은 그 다음에,괄호가 있으면 괄호 안쪽을 먼저** 계산한다.

##### calc() 사용 예시
![](https://velog.velcdn.com/images/cil05265/post/dfb2fed8-a325-4ffc-bac3-c457d30035a9/image.png)
