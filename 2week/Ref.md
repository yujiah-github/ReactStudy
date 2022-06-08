## 2주차
### 1. Ref
- **어떤 인풋박스에서 텍스트를 가져오고 싶으면 어떻게 접근해야할까?**
- DOM에서 다루는 방법은 1주차에 배웠는데, **리액트** 에선 어떻게 하면 좋을까?
- 아니, 그 전에 가상돔에서 가져오나? 아니면 DOM에서? → **답은, 리액트 요소에서 가져온다!**

- React 요소를 가지고 오는 방법1 : **React.createRef()**
```javascript
import React from "react";
import logo from "./logo.svg";
// BucketList 컴포넌트를 import 해옵니다.
// import [컴포넌트 명] from [컴포넌트가 있는 파일경로];
import BucketList from "./BucketList";
import styled from "styled-components";

// 클래스형 컴포넌트는 이렇게 생겼습니다!
class App extends React.Component {
  constructor(props) {
    super(props);
    // App 컴포넌트의 state를 정의해줍니다.
    this.state = {
      list: ["영화관 가기", "매일 책읽기", "수영 배우기"],
    };
    // ref는 이렇게 선언합니다! 
    this.text = React.createRef();
  }

  componentDidMount(){
  // 콘솔에서 확인해보자!
    console.log(this.text);
  console.log(this.text.current);
  }

  // 랜더 함수 안에 리액트 엘리먼트를 넣어줍니다!
  render() {
    
    return (
      <div className="App">
        <Container>
          <Title>내 버킷리스트</Title>
          <Line />
          {/* 컴포넌트를 넣어줍니다. */}
          {/* <컴포넌트 명 [props 명]={넘겨줄 것(리스트, 문자열, 숫자, ...)}/> */}
          <BucketList list={this.state.list} />
        </Container>

        <div>
          <input type="text" ref={this.text}/>
        </div>
      </div>
    );
  }
}

const Container = styled.div`
  max-width: 350px;
  min-height: 80vh;
  background-color: #fff;
  padding: 16px;
  margin: 20px auto;
  border-radius: 5px;
  border: 1px solid #ddd;
`;

const Title = styled.h1`
  color: slateblue;
  text-align: center;
`;

const Line = styled.hr`
  margin: 16px 0px;
  border: 1px dotted #ddd;
`;

export default App;
```

- React 요소를 가지고 오는 방법2 : **React.useRef()**
```javascript
import React from "react";
import styled from "styled-components";

const BucketList = ({ list }) => {
  const my_lists = list;
  const my_wrap = React.useRef(null);

  console.log(my_wrap); // 콘솔로 확인해봐요!

  window.setTimeout(() => { // 1초 뒤에는?!
    console.log(my_wrap);
  }, 1000);
  return (
    <div ref={my_wrap}>
      {my_lists.map((list, index) => {
        return <ItemStyle key={index}>{list}</ItemStyle>;
      })}
    </div>
  );
};

const ItemStyle = styled.div`
  padding: 16px;
  margin: 8px;
  background-color: aliceblue;
`;

export default BucketList;
```
