

### Counter Example Component

store中state数据更新后,render自动调用.

```js
const Counter = ({ value }) => (
  <h1>{value}</h1>
);

const render = () => {
  ReactDOM.render(
    <Counter value={store.getState()}/>,
    document.getElementById('root')
  );
};
//这里手动注册了render函数
store.subscribe(render);
render();
```


#### Counter 无状态组件

counter组件定义的props包括 value值, onIncrement与onDecrement回调函数.

当counter组件渲染时,我们由store对象的当前state指定value,当点击按钮后,onIncrement与onDecrement回调函数会触发对应的action给store, store.dispatch(action)

当store dispatch action后,reducer由当前状态和触发的action返回新的state

最终action触发后, store注册的render()函数会被调用,UI利用最新状态进行重绘.

```js
const Counter = ({
  value,
  onIncrement,
  onDecrement
}) => (
  <div>
    <h1>{value}</h1>
    <button onClick={onIncrement}>+</button>
    <button onClick={onDecrement}>-</button>
  </div>
);

const render = () => {
  ReactDOM.render(
    <Counter
      value={store.getState()}
      onIncrement={() =>
        store.dispatch({
          type: 'INCREMENT'
        })
      }
      onDecrement={() =>
        store.dispatch({
          type: 'DECREMENT'
        })
      }
    />,
    document.getElementById('root')
  );
}
```
