
## 手动实现combineReducers函数

combineReducers()只有一个输入参数reducers,用于映射reducer函数,返回一个reducer函数,其包含两个参数state与action.

在返回的reducer函数内部,使用Object.keys()获取`reducers`对象的所有键值.使用reduce()函数返回一个表征下个状态的单个state对象.

```JavaScript
const combineReducers = reducers => {
  return (state = {}, action) => {

    // Reduce all the keys for reducers from `todos` and `visibilityFilter`
    return Object.keys(reducers).reduce(
      (nextState, key) => {
        // Call the corresponding reducer function for a given key
        nextState[key] = reducers[key] (
          state[key],
          action
        );
        return nextState;
      },
      {} // The `reduce` on our keys gradually fills this empty object until it is returned.
    );
  };
};
```