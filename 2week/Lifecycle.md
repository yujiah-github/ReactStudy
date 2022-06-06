## 2주차
### 1. 가상돔
- DOM은 **html 단위 하나하나를 객체로 생각** 하는 모델이다.
- 예를 들면, 'div'라는 객체는 텍스트 노드, 자식 노드 등등, 하위의 어떤 값을 가지고 있을 것이다. 이런 구조를 트리 구조라고 한다. **즉,DOM이 트리구조란 이야기이다.**
- DOM 트리 중 하나가 수정될 때마다 모든 DOM을 뒤지고, 수정할 걸 찾고, 싹 수정을 한다면 필요없는 연산이 너무 많이 일어난다. 그래서 등장한 게 **가상돔** 이다.
- **가상돔은 메모리 상에서 돌아가는 가짜 DOM이다.**
- 가상돔의 동작 방식: **기존 DOM과 어떤 행동 후 새로 그린 DOM(가상 돔에 올라갔다고 표현한다)을 비교해서 정말 바뀐 부분만 갈아끼워준다! → 돔 업데이트 처리가 간결해진다.**
- 처음 페이지 진입했을 때와 데이터가 변했을 때 DOM을 새로 그려주면 된다.

### 2. 라이프 사이클
- **컴포넌트의 라이프 사이클(= 컴포넌트 생명주기)** 은 정말 중요한 개념이다.
- 컴포넌트가 렌더링을 준비하는 순간부터, 페이지에서 사라질 때까지가 라이프 사이클이다.

![](https://velog.velcdn.com/images/cil05265/post/33678012-14d7-4007-ac01-e46403c9586f/image.png)

- **컴포넌트는 생성되고 → 수정(업데이트)되고 → 사라진다.**
- 생성은 처음으로 컴포넌트를 불러오는 단계이다.
- 수정(업데이트)는 사용자의 행동(클릭, 데이터 입력 등)으로 데이터가 바뀌거나, 부모 컴포넌트가 렌더링할 때 업데이트 된다.
    - **props가 바뀔 때**
    - **state가 바뀔 때**
    - **부모 컴포넌트가 업데이트 되었을 때(=리렌더링했을 때)**
    - **또는, 강제로 업데이트 했을 경우(forceUpdate()를 통해 강제로 컴포넌트를 업데이트할 수 있다.)**
- 제거는 페이지를 이동하거나, 사용자의 행동(삭제 버튼 클릭 등)으로 인해 컴포넌트가 화면에서 사라지는 단계이다.

### 3. 라이프 사이클 함수
- 라이프 사이클 함수는 **클래스형 컴포넌트**에서만 사용할 수 있다.
- 라이프 사이클을 아는 건 중요하지만, 클래스형 컴포넌트보다 **함수형 컴포넌트** 를 사용하는 것이 더 바람직하다.
- 그 이유는, 리액트 공식 매뉴얼에서 **함수형 컴포넌트** 를 더 권장하기 때문이다.(리액트 16.8버전부터 등장한 React Hooks으로 라이프 사이클 함수를 대체할 수 있기 때문이다.)

```javascript
import React from "react";

// 클래스형 컴포넌트는 이렇게 생겼습니다!
class LifecycleEx extends React.Component {

// 생성자 함수
  constructor(props) {
    super(props);

    this.state = {
      cat_name: '나비',
    };

    console.log('in constructor!');
  }

  changeCatName = () => {
    // 다음 강의에서 배울, state 업데이트 하는 방법입니다!
    // 지금은 componentDidUpdate()를 보기 위해 쓰는 거니까, 처음보는 거라고 당황하지 말기!
      this.setState({cat_name: '바둑이'});

      console.log('고양이 이름을 바꾼다!');
  }

  componentDidMount(){
    console.log('in componentDidMount!');
  }

  componentDidUpdate(prevProps, prevState){
      console.log(prevProps, prevState);
      console.log('in componentDidUpdate!');
  }

  componentWillUnmount(){
      console.log('in componentWillUnmount!');
  }

  // 랜더 함수 안에 리액트 엘리먼트를 넣어줍니다!
  render() {

    console.log('in render!');

    return (
      <div>
          {/* render 안에서 컴포넌트의 데이터 state를 참조할 수 있습니다. */}
        <h1>제 고양이 이름은 {this.state.cat_name}입니다.</h1>
        <button onClick={this.changeCatName}>고양이 이름 바꾸기</button>
      </div>
    );
  }
}

export default LifecycleEx;
```

#### 3.1 constructor()
- **생성자 함수**라고도 부른다. 컴포넌트가 생성되면 가장 처음 호출된다.

#### 3.2 render()
- 컴포넌트의 모양을 정의한다. 여기에서도 **state, props에 접근해서 데이터를 보여줄 수 있다.**
- 리액트 요소를 return에 넣어 반환해준다. **render()** 안에 들어갈 내용은 컴포넌트의 모양에만 관여하는 것이 가장 좋다.
- 즉, **state나, props** 를 건드려 데이터를 수정하려고 하면 안됩니다!

#### 3.3 componentDidMount()
- 컴포넌트가 화면에 나타나는 것을 **마운트(Mount)** 한다고 표현한다. didMount()는 마운트가 완료 되었다는 이야기다.
- 이 함수는 첫번째 렌더링을 마친 후에만 딱 한 번 실행된다. 컴포넌트가 리렌더링할 때는 실행되지 않는다.
보통은 이 안에서 **ajax 요청, 이벤트 등록, 함수 호출 등** 작업을 처리한다.
- 또, 이미 가상돔이 실제돔으로 올라간 후니까 DOM 관련 처리를 해도 된다.

#### 3.4 componentDidUpdate(prevProps, prevState, snapshot)
- DidMount()가 첫 렌더링 후에 호출 되는 함수라면, **DidUpdate()** 는 리렌더링을 완료한 후 실행되는 함수이다.
- 이 함수에 중요한 파라미터가 2개 있는데, **prevProps와 prevState** 이다. 각각 업데이트 되기 전 **props, state** 이다. 이전 데이터와 비교할 일이 있다면 가져다 쓸 수 있다.
- DidUpdate()가 실행될 때도 가상돔이 실제돔으로 올라간 후니까 DOM 관련 처리를 해도 된다.

#### 3.5 componentWillUnmount()
- 컴포넌트가 **DOM** 에서 제거 될 때 실행하는 함수이다.
만약 우리가 스크롤 위치를 추적 중이거나, 어떤 이벤트 리스너를 등록했다면 여기에서 꼭꼭 해제를 해줘야 한다.
컴포넌트 없이 이벤트만 남겨둘 순 없기 때문이다.
