## 2주차
### 1. Component(1)
#### 1.1 Component란?
- Component는 **클래스형과 함수형** 이 있다. 직전 강의에서 본 컴포넌트가 바로 클래스형 컴포넌트였다. 
- 이제 클래스형 컴포넌트는 잘 쓰지 않지만, 우리는 두 가지를 모두 살펴봐야한다. 왜냐하면, 이미 기개발된 프로젝트들(아마 회사에서도...!)은 클래스형 컴포넌트를 사용 중일수도 있다. **최소한 코드를 알아보고 고칠 수 있을 정도는 알아두는 편이 좋다.**

- 이전에 리액트는 레고라고 언급했었는데, 컴포넌트는 블록이다.
- 컴포넌트를 이해하고 잘 써먹으려면 웹 사이트를 잘 조각낼 줄 알아야 한다.
- 아래와 같은 웹 사이트를 만든다고 생각해보자.

```html
<header/>
<container/>
    <imagebanner/>
    <contents1/>
<footer/>
```

- 즉, 이 웹 사이트는, 크게 **header, container, footer** 세 개의 컴포넌트가 있고, **container 컴포넌트는 imagebanner, contents1 컴포넌트** 로 이루어져 있는 것이다.

- Component는 웹 사이트의 조각이고, 우리는 이 조각을 모아서 웹사이트에 뿌려준다.
- **즉, 웹 사이트를 잘 조각낼 줄 아는 사람 === 리액트를 잘 쓰는 사람이다.**

#### 1.2 State와 Props
- Component에서는 데이터 관리를 어떻게 할까?
- **state** 는 Component가 가지고 있는 데이터이다.
- header 컴포넌트를 예로 들어보면, 이 헤더에 들어갈 데이터는 뭐가 있을까? → 로고 이미지 경로, 메뉴 이름(온라인, 오프라인, 기업교육, 내 강의실)이 있을 것이다.
- 이 데이터는 **container나 footer 컴포넌트** 에서는 쓰지 않을 것이다.
- 즉, **header 컴포넌트** 에서만 쓰는 정보인 셈이다.
- **state는 한 컴포넌트에서만 사용하는 정보를 주로 넣어놓고 생성, 수정하는 데이터이다.**
- **생성도 수정도 오직 해당 컴포넌트 내에서만 이뤄진다.** 내꺼니까 생성도 수정도 자유로운 셈이다.


- props는 Component가 부모 Component로부터 받아온 데이터이다.

```html
<container>
 <imagebanner/>
 <contents1/>
</container>
```

- container 컴포넌트는 두 개의 자식 컴포넌트를 가지고 있다.
- container 컴포넌트만 imangebanner 컴포넌트한테 필요한 이미지 경로를 가지고 있다고 가정한다. (state로 가지고 있다고 가정한다.)
- 이 때 imagebanner 컴포넌트는 자신의 부모인 container  컴포넌트로부터 **이미지 경로**를 전달받아서 사용해야한다.
- container 가 가지고 있는 이미지 경로를 imagebanner 에게 전달해주면, 이 **이미지 경로**가 imagebanner 컴포넌트의 props가 된다.
- 다시 말해, **부모 컴포넌트로부터 전달 받은 데이터를 props라고 한다.**
- 그럼 부모 컴포넌트가 가지고 있는 데이터를 imagebanner 컴포넌트가 추가 하거나 수정할 수 있을까?
**Props로 받은 데이터는 남의 것이기 때문에 수정할 수 없다!**

### 2. Component(2)
#### 2.1 함수형 Component
- 아래 예제를 참조하면 된다.
- **폴더는 소문자로 시작하는 카멜케이스** 를 사용한다.
- **JS파일, 컴포넌트 이름은 대문자로 시작하는 카멜케이스** 를 사용한다.

```javascript
//BucketList.js 예제
// 리액트 패키지를 불러옵니다.
import React from 'react'; 

// 함수형 컴포넌트는 이렇게 쓸 수도 있고
// function Bucketlist(props){
//     return (
//         <div>버킷 리스트</div>
//     );
// }

// 이렇게 쓸 수도 있어요. =>가 들어간 함수를 화살표 함수라고 불러요.
// 저희는 앞으로 화살표 함수를 사용할거예요.
// 앗 () 안에 props! 부모 컴포넌트에게 받아온 데이터입니다.
// js 함수가 값을 받아오는 것과 똑같이 받아오네요.
const BucketList = (props) => {

    // 컴포넌트가 뿌려줄 ui 요소(리엑트 엘리먼트라고 불러요.)를 반환해줍니다.
    return (
        <div>
            버킷 리스트
        </div>
    );
}

// 우리가 만든 함수형 컴포넌트를 export 해줍니다.
// export 해주면 다른 컴포넌트에서 BucketList 컴포넌트를 불러다 쓸 수 있어요.
export default BucketList;
```


```javascript
//App.js 예제
import React from 'react';
import logo from './logo.svg';
import './App.css';
// BucketList 컴포넌트를 import 해옵니다.
// import [컴포넌트 명] from [컴포넌트가 있는 파일경로];
import BucketList from './BucketList';

function App() {

  return (
    <div className="App">
      <h1>내 버킷리스트</h1>
      {/* 컴포넌트를 넣어줍니다. */}
      <BucketList/>
    </div>
  );
}

export default App;
```

### 3. Component(3)
#### 3.1 클래스형 Component
- 아래는 App.js를 클래스형으로 바꾸고, BucketList 컴포넌트에 데이터를 넘겨준 예시이다.

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';
// BucketList 컴포넌트를 import 해옵니다.
// import [컴포넌트 명] from [컴포넌트가 있는 파일경로];
import BucketList from './BucketList';

// 클래스형 컴포넌트는 이렇게 생겼습니다!
class App extends React.Component {

  constructor(props){
    super(props);
    // App 컴포넌트의 state를 정의해줍니다.
    this.state = {
      list: ['영화관 가기', '매일 책읽기', '수영 배우기'],
    };
  }

  // 랜더 함수 안에 리액트 엘리먼트를 넣어줍니다!
  render() {
      return (
      <div className="App">
        <h1>내 버킷리스트</h1>
        {/* 컴포넌트를 넣어줍니다. */}
        <BucketList/>
      </div>
    );
  }
}

export default App;
```

- this 키워드는 깊이 들어가면 context 객체와 연관이 있다.
- **우리는 함수나 클래스 안에서 사용하면 this를 쓴 위치(위의 경우에는 App 클래스)에 있는 값을 가지고 온다고 생각하면 된다.**
> ex) App 클래스 안에서 쓰면, this.[변수명]은 App 클래스 안에 있는 값을 가지고 온다.

- App 컴포넌트에서 BucketList 컴포넌트로 state를 넘겨줄 땐, 다음과 같이 사용하면 된다.
```javascript
render() {
    // this 키워드를 통해 state에 접근할 수 있어요.
    console.log(this.state);

      return (
      <div className="App">
        <h1>내 버킷리스트</h1>
        {/* 컴포넌트를 넣어줍니다. */}
        {/* <컴포넌트 명 [props 명]={넘겨줄 것(리스트, 문자열, 숫자, ...)}/> */}
        <BucketList list={this.state.list}/>
      </div>
    );
  }
```

- BucketList.js 파일을 열고, 아래와 같이 입력하면 된다.
```javascript
const BucketList = (props) => {
    
    console.log(props);

    // 컴포넌트가 뿌려줄 ui 요소(리엑트 엘리먼트라고 불러요.)를 반환해줍니다.
    return (
        <div>
            버킷 리스트
        </div>
    );
}
```
