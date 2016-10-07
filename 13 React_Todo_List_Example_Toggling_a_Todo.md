
## 实现 `TOGGLE_TODO`

在现有工作基础上,实现`TOGGLE_TODO`action,具体当点击todo项时触发,对应项的状态发生切换.在UI中使用`textDecoration`样式来表征不同状态.

React部分修改如下.

```Javascript
.
. // TodoApp component stuff
.
<ul>
  {this.props.todos.map(todo =>
    <li key={todo.id}
        onClick={() => {
          //dispatch toggle_todo action
          store.dispatch({
            type: 'TOGGLE_TODO',
            id: todo.id
          });
        }}
        style={{
          textDecoration:
            todo.completed ?
              'line-through' :
              'none'
        }}>
      {todo.text}
    </li>
  )}
</ul>
.
. // More TodoApp component stuff
.
```

定义对应的reducer函数,其调用了todo函数,用于更新每单个todo item.

```JavaScript
const todos = (state = [], action) => {
  switch (action.type) {
    // case 'ADD_TODO' stuff
    case 'TOGGLE_TODO':
      return state.map(t =>
        todo(t, action)
      );
    // default case stuff
  }
}
```

todo函数定义如下,使用了...spread语法.

```JavaScript
const todo = (state, action) => {
  // case 'ADD_TODO' stuff
  case 'TOGGLE_TODO':
    if (state.id !== action.id) {
      return state;
    }

    return {
      ...state,
      completed: !state.completed
    };
  // default case stuff
};
```
