
## Reducer Composition with Arrays

在reducer中对state进行更新,state中包含数组元素时，需要遍历数组元素，可读性差

```JavaScript
const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        {
          id: action.id,
          text: action.text,
          completed: false
        }
      ];
    case 'TOGGLE_TODO':
      return state.map(todo => {
        if (todo.id !== action.id) {
          return todo;
        }

        return {
          ...todo,
          completed: !todo.completed
        };
      });
  }
}
```

为了使结构简洁,最好将该函数进行分割成处理数组中单个元素的函数.在新的函数中`state`表示单个`todo`，不再是`todo`数组

```JavaScript
const todo = (state, action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return {
        id: action.id,
        text: action.text,
        completed: false
      };
    case 'TOGGLE_TODO':
      if (state.id !== action.id) {
        return state;
      }

      return {
        ...state,
        completed: !state.completed
      };
    default:
      return state;
  }
}
```

新的`todos` reducer更新如下,遍历每个`todo`项，调用上述`todo`函数更新`state`.

```JavaScript
const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        todo(undefined, action)
      ];
    case 'TOGGLE_TODO':
      return state.map(t => todo(t, action));
    default:
      return state;
  }
};
```

在redux实践中,上述过程称为 **reducer composition**.不同的reducer处理state树的不同部分。

