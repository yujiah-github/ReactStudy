## 2주차
### 1. State 관리 (1)
#### 단방향 데이터 흐름이란?
- 데이터는 위에서 아래로, 부모에서 자식으로 넘겨줘야 한다는 이야기이다.

#### 왜 단방향으로 써야할까?
- 라이프 사이클과 함께 생각해보기
- 부모 컴포넌트의 state가 업데이트 되면 자식 컴포넌트도 리렌더링이 일어난다.
- 만약 자식 컴포넌트의 state가 바뀐 걸 부모 컴포넌트가 props로 받는다고 생각해보면, 자식 컴포넌트가 업데이트 될 때 부모 컴포넌트도 업데이트 된다.

#### 클래스형 컴포넌트에서 state 관리 - setState()
- 라이프 사이클을 볼 때 잠깐 봤던 setState()!
- 클래스형 컴포넌트의 state를 업데이트할 때 사용하는 함수이다.

```javascript
import React from "react";

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      count: 3, // 숫자넣기!
    };
  }

  componentDidMount() {}

  addNemo = () => {
    // this.setState로 count를 하나 더해줍니다!
    this.setState({ count: this.state.count + 1 });
  };

  removeNemo = () => {
    // 네모 갯수가 0보다 작을 순 없겠죠! if문으로 조건을 걸어줍시다.
    if (this.state.count > 0) {
      // this.setState로 count를 하나 빼줍니다!
      this.setState({ count: this.state.count - 1 });
    }else{
      window.alert('네모가 없어요!');
    }
  };

  render() {
    // 배열을 만듭니다.
    // Array.from()은 배열을 만들고 초기화까지 해주는 내장 함수입니다.
    // Array.from()의 첫번째 파라미터로 {length: 원하는 길이} 객체를,
    // 두번째 파라미터로 원하는 값을 반환하는 콜백함수를 넘겨주면 끝!
    // array의 내장함수 대부분은 콜백 함수에서 (현재값, index넘버)를 인자로 씁니다.
    const nemo_count = Array.from({ length: this.state.count }, (v, i) => i);

    // 콘솔로 만들어진 배열을 확인해봅니다. 숫자가 0부터 순서대로 잘 들어갔나요?
    console.log(nemo_count);

    return (
      <div className="App">
        {nemo_count.map((num, idx) => {
          return (
            <div
              key={idx}
              style={{
                width: "150px",
                height: "150px",
                backgroundColor: "#ddd",
                margin: "10px",
              }}
            >
              nemo
            </div>
          );
        })}

        <div>
          {/* 함수를 호출합니다. 이 클래스 안의 addNemo 함수를 불러오기 때문에 this.addNemo로 표기해요. */}
          <button onClick={this.addNemo}>하나 추가</button>
          <button onClick={this.removeNemo}>하나 빼기</button>
        </div>
      </div>
    );
  }
}

export default App;
```
