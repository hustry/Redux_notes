
#### 手动构建一个store对象

一般使用createStroe()构建,这里手动构建.

```js
const createStore = (reducer) =>{
	let state;
	let listeners = [];

	const getState = () => state;  //闭包,获取内部state

	const dispatch = (action) =>{
		//触发action后,调用reducer更新state
		state = reducer(state,action);
		//调用注册的listener回调函数
		listeners.forEach(listener => listener());
	};

	//用于注册回调函数,返回移除listener函数
	const subscribe = (listener) =>{
		//添加回调函数
		listeners.push(listener);
		//返回函数移除刚刚添加的listener
		return ()=>{
			listeners = listeners.filter(l => l!== listener);
		}
	};

	dispatch({});

	// 返回store对象包含 getState,dispatch,subscribe三个方法
	return { getState, dispatch, subscribe };

}
```