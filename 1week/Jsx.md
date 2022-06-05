## 1주차
### 1. JSX
- 리액트에서는 **딱 하나의 html 파일** 만 존재한다.
(public 폴더 아래에 있는 index.html)
- 리액트에서 뷰를 그릴 땐, App.js 파일에서 보이듯, **JSX 문법을 사용해서 React 요소를 만들고 DOM에 렌더링 시켜서 그린다.**
- **HTML 태그는 .js 파일 안에서 쓸 수 없다.** 그래서 나온 게 JSX이다.
- 자바스크립트 안에서 html 태그같은 마크업을 넣어 뷰(UI) 작업을 편하게 할 수 있다.

```javascript
const start_half = <div>
    <h1>안녕하세요!</h1>
    <p>시작이 반이다!</p>
  </div>;
```

- 그럼 JSX에서 쓰는 건 **DOM 요소** 일까? 아니다. 정확히는 **React 요소** 이다.
- 이건 다음 주차에서 가상돔을 배우면서 조금 더 자세히 다루고, 1주차에서는 **리액트 돔을 구성하는 건 리액트 요소! 돔을 구성하는 건 돔 요소!** 라고만 알아두면 된다.

### 2. JSX 사용법
- **태그는 꼭 닫아주기**
- 무조건 **1개의** 엘리먼트를 반환하기
- 자바스크립트를 가져올 땐 **중괄호** 를 사용하기
- 값을 가져올 때 뿐만 아니라,**map, 삼항 연산자 등 자바스크립트를 JSX 안에 쓸 때도 {}** 를 이용할 수 있다.
```javascript
 const cat_name = 'perl';
// return 부분만 복사해서 붙여넣고 크롬 브라우저로 돌아가 새로고침 해봅시다.
    return (
      <div>
        hello {cat_name}!
      </div>
    );
```
- class 대신 **className** 을 사용한다.
- 인라인으로 Style을 줄 때, json 형식으로 넣어주면 된다.

```html
<p style="color: orange; font-size: 20px;">orange</p>
```

```javascript
// 중괄호를 두 번 쓰는 이유? 딕셔너리도 자바스크립트니까요!
// 이렇게 쓰거나,
<p style={{color: 'orange', fontSize: '20px'}}>orange</p>

//혹은 스타일 딕셔너리를 변수로 만들고 쓸 수 있어요!
function App() {
  const styles = {
    color: 'orange',
    fontSize: '20px'
  };

  return (
    <div className="App">
      <p style={styles}>orange</p>
    </div>
  );
}
```

