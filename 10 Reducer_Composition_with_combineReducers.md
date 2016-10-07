
## combineReducers

上节所述reducer composition太常见了,reducer Redux提供了帮助函数`combineReducers()`

使用`combineReducers`前

```JavaScript
const todoApp = (state = {}, action) => {
  return {
     todos: todos( 
      state.todos,
      action
    ),
    visibilityFilter: visibilityFilter(
      state.visibilityFilter,
      action
    )
  };
};
```

使用`combineReducers`后

```JavaScript
const todoApp = combineReducers({
  todos: todos,
  visibilityFilter: visibilityFilter
});
```
`combineReducers()`唯一参数为一个对象，该对象将state树中的属性映射到对应的reducer函数.使用ES6语法可以更简洁.

```JavaScript
const todoApp = combineReducers({
  todos,
  visibilityFilter
});
```
