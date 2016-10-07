
#### Couter Example Reducer

```js
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}
```

#### store方法:getState(),dispatch(),subscribe()

```
const store = createStore(counter);
```

store对象
* 保存有当前应用的state对象 getState()
* 可以disptch action动作 dispatch({ type:'INCREMENT' }),其中{ type:'INCREMENT' }为action对象
* 创建store时,需要指定针对action,state如何更改即reducer函数

store对象三个方法:
* getState()  获取当前state对象
* dispatch()  触发某个action
* subscribe() callback函数,当action被触发后调用
