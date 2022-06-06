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