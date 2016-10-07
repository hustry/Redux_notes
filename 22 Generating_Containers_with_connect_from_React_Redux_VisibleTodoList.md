
## 使用connect()构建container组件

首先定义函数`mapStateToProps`,将state中数据映射到组件的props.

```JavaScript
const mapStateToProps = (state) => {
  return {
    todos: getVisibleTodos (
      state.todos,
      state.visibilityFilter
    )
  };
}
```

再定义函数`mapDispatchToProps`,将store的dispatch()方法作为其参数.

```JavaScript
const mapDispatchToProps = (dispatch) => {
  return {
    onTodoClick: (id) => {
      dispatch({
        type: 'TOGGLE_TODO',
        id
      })
    }
  };
};
```

使用connect()函数

基于上述两个函数,构建组件.

```JavaScript
const VisibleTodoList = connect(
  mapStateToProps,
  mapDispatchToProps
)(TodoList)
```




