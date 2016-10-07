
## 通过context隐式将store传递给组件

通过react的context可以隐式将store传递给组件,首先创建一个`Provider`组件,在`render()`中返回其子组件.

```JavaScript
class Provider extends Component {
  render() {
    return this.props.children;
  }
}

ReactDOM.render(
  <Provider store={createStore(todoApp)}>
    <TodoApp />
  </Provider>,
  document.getElementById('root')
);
```

现在添加context,这样可以使store对每个子组件可见.我们需要在组件中提供`childContextTypes`,这与React的`PropTypes`定义类似.

```JavaScript
class Provider extends Component {
  getChildContext() {
    return {
      store: this.props.store //添加store到context中.
    };
  }
  render() {
    return this.props.children;
  }
}

//必须定义如下childContextTypes
Provider.childContextTypes = {
  store: React.PropTypes.object
}
```

**重构组件由context而不是props中获取store**

```JavaScript
class VisibleTodoList extends Component {
  componentDidMount() {
    const { store } = this.context;
    this.unsubscribe = store.subscribe(() =>
      this.forceUpdate()
    );
  }
  .
  . // Rest of component as before to `render()` method
  .

  render() {
    const props = this.props;
    const { store } = this.context;
    const state = store.getState();
    .
    .
    .
  }
}
```




