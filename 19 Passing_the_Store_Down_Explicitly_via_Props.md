
## 将Store显式注入组件

将store以prop的形式传递给TodoApp组件.

```JavaScript
ReactDOM.render(
  <TodoApp store={createStore(todoApp)} />,
  document.getElementById('root')
);
```

然后TodoApp将store自上而下传递给下面的container组件.

```JavaScript
const TodoApp = ({ store }) => (
  <div>
    <AddTodo store={store} />
    <VisibleTodoList store={store} />
    <Footer store={store} />
  </div>
);
```

在每个组件内部需要由`props`获取store在`componentDidMount()`与`render()`中使用.

```JavaScript
class VisibleTodoList extends Component {
  componentDidMount() {
    const { store } = this.props;
    this.unsubscribe = store.subscribe(() =>
      this.forceUpdate()   //引用store,当store更新时强制该组件更新
    );
  }
  .
  . // Rest of component as before to `render()` method
  .

  render() {
    const props = this.props;
    const { store } = props;
    const state = store.getState();  //引用store,获取当前状态用于渲染
    .
    .
    .
  }
}
```

