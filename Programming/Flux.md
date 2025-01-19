# Flux

Facebook이 만든 단방향 데이터 흐름 아키텍처 패턴으로, 애플리케이션에서 상태 관리 및 데이터 흐름을 명확하게 관리하기 위해 설계되었음

주로 React와 함께 사용됨

## 구성 요소

### Action

- 애플리케이션 내에서 발생하는 이벤트나 사용자 입력을 나타냄
- payload(데이터)를 포함하며, 이 데이터는 Dispatcher를 통해 전달됨
- 보통 액션 타입과 관련된 데이터를 가지고 있으며, 이를 통해 상태 변경을 트리거 함

```
const action = {
  type: 'ADD_ITEM',
  payload: {
    itemId: 1,
    itemName: 'New Item',
  },
};
```

### Dispatcher

- 모든 Action을 받아서 Store에 전달하는 역할을 함
- 모든 Action은 Dispatcher를 통해서만 Store로 전달되므로, 상태 변경이 일관되게 이루어짐
- 애플리케이션 내에서 단일 인스턴스로 존재하며, 모든 Action을 관리함

```
class Dispatcher {
  constructor() {
    this.callbacks = [];
  }

  register(callback) {
    this.callbacks.push(callback);
  }

  dispatch(action) {
    this.callbacks.forEach(callback => callback(action));
  }
}

const dispatcher = new Dispatcher();
```

### Store

- 애플리케이션의 상태를 관리하는 단일 상태 저장소
- 여러 개의 Store가 있을 수 있지만, 각 Store는 상태를 관리하고, 해당 상태가 변경되면 View에 알림
- 상태 변경을 처리하는 reducer와 유사한 로직을 가지고 있으며, Action을 처리하여 상태를 업데이트

```
class ItemStore {
  constructor() {
    this.items = [];
    dispatcher.register(this.handleActions.bind(this));
  }

  handleActions(action) {
    switch (action.type) {
      case 'ADD_ITEM':
        this.items.push(action.payload);
        break;
      default:
        break;
    }
  }

  getItems() {
    return this.items;
  }
}

const itemStore = new ItemStore();
```

### View(React 컴포넌트)

- 사용자가 보는 UI
- Store에서 데이터를 구독하고, 상태가 변경되면 UI를 업데이트
- 보통 React 컴포넌트가 이 역할을 함
- Store에서 제공하는 데이터를 표시하며, 사용자의 인터랙션을 통해 Action을 트리거

```
class ItemList extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      items: itemStore.getItems(),
    };
  }

  componentDidMount() {
    itemStore.addListener(this.updateItems.bind(this));
  }

  updateItems() {
    this.setState({
      items: itemStore.getItems(),
    });
  }

  render() {
    return (
      <div>
        <ul>
          {this.state.items.map(item => (
            <li key={item.itemId}>{item.itemName}</li>
          ))}
        </ul>
      </div>
    );
  }
}
```

## 데이터 흐름

Flux의 단방향 데이터 흐름은 아래와 같은 방식으로 작동

1. Action이 발생하면(예: 버튼 클릭, 서버 응답 등), Dispatcher를 통해 Action이 전달됨
2. Dispatcher는 모든 Store에 Action을 전달
3. Store는 Action을 처리하여 상태를 업데이트
4. Store는 상태가 변경되었음을 View에 알림 -> View는 상태 변경을 반영하여 UI를 업데이트

## 장점

### 단방향 데이터 흐름

- 데이터 흐름을 명확히 하여 상태 관리가 직관적이고 예측 가능함
- 상태 변화가 한 방향으로 흐르기 때문에 디버깅이 쉬워짐

### 애플리케이션 상태의 중앙 집중화

- 모든 상태는 Store에 관리되므로, 상태를 중앙에서 추적하고 관리할 수 있음

### 확장성

- 애플리케이션이 커지더라도 Flux의 구조는 변경 없이 상태 관리를 유지할 수 있음
- 새로운 Store를 추가하거나 Action을 추가하는 방식으로 애플리케이션을 확장할 수 있음

### 디버깅 용이

- Action과 Dispatcher의 흐름을 명확히 정의하기 때문에 상태 변화가 어디에서 발생했는지 추적하기 쉬움
