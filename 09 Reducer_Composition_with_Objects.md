
## Reducer Composition with Objects

上节针对state树中数组进行了分解。现在对对象进行分解。

state中对象包含大量属性,不同reducer只修改state树中对应项，结果更清晰.

下面为 Todo 应用添加一个reducer用于处理`SET_VISIBILITY_FILTER`action. 首先定义一个只更新state中visibilityFilter属性的reducer.


```JavaScript
const visibilityFilter = (
    state = 'SHOW_ALL',
    action
) => {
    switch (action.type) {
      case 'SET_VISIBILITY_FILTER':
        return action.filter;
      default:
        return state;
    }
};
```

reducer更新如下

```JavaScript
const todoApp = (state = {}, action) => {
  return {
     // 只更新state.todos
     todos: todos( 
      state.todos,
      action
    ),
    //  只更新state.visibilityFilter
    visibilityFilter: visibilityFilter(
      state.visibilityFilter,
      action
    )
  };
};
```

这种模式可以使得不同的reducer可以处理相同的action更新state树种不同项,不同reducer互不干扰.