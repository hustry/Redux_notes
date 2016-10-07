
## 实现Container组件FilterLink

当前Footer组件接受`visibilityFilter`与`onFilterClick`作为props,但它本身并不使用它们，仅仅将它们传递给`FilterLink`,重构如下:

```JavaScript
class FilterLink extends Component {
  render () {
    const props = this.props;
    // this just reads the store, is not listening
    // for change messages from the store updating
    const state = store.getState();

    return (
      <Link
        active={
          props.filter ===
          state.visibilityFilter
        }
        onClick={() =>
          store.dispatch({
            type: 'SET_VISIBILITY_FILTER',
            filter: props.filter
          })
        }
      >
        {props.children}
      </Link>
    );
  }
}
```

该组件在render()方法中使用store.getState()获取当前状态.但这种方法的问题在于该方法没有注册store,当state变化时,该组件不会被更新.

React提供了方法forceUpdate()来强制组件更新,结合store.subscribe()来实现组件更新.


```JavaScript
class FilterLink extends Component {
  componentDidMount() {
    this.unsubscribe = store.subscribe(() =>
      this.forceUpdate()    //当state更新后,该函数被调用,强制该组件更新.
    );
  }

  // Since the subscription happens in `componentDidMount`,
  // it's important to unsubscribe in `componentWillUnmount`.
  componentWillUnmount() {
    this.unsubscribe(); // return value of `store.subscribe()`
  }
.
. // `render()` method as above...
.
```