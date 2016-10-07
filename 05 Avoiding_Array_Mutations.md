
#### 避免数组被修改

考虑一个应用对应的state为一个counter列表数组.

```js

const addCounter = (list) => {
  list.push(0);
  return list;
};

const testAddCounter = () => {
  const listBefore = [];
  const listAfter = [0];

  //listBefore被冻结
  deepFreeze(listBefore);

  expect(
    addCounter(listBefore)
  ).toEqual(listAfter);
};

testAddCounter();
console.log('All tests passed')
```
listBefore被冻结后,添加元素失败.需要更改为concat方法.
concat方法不会更改原始对象

```js
const addCounter = (list) => {
	return list.concat([0]);
}
```
如果要删除元素,使用splice方法会更改原对象,使用slice方法.

```js
//splice方法
const removeCounter = (list, index) => {
  list.splice(index, 1);
  return list;
}

//slice方法
const removeCounter = (list, index) => {
  // Old way:
  //return list
  //  .slice(0, index)
  //  .concat(list.slice(index + 1));

  // ES6 way:
  return [
    ...list.slice(0, index),
    ...list.slice(index + 1)
  ];
};
```

现在实现counter操作函数,该函数输入array和要操作counter的索引.

```js
const incrementCounter = (list, index) => {
  list[index]++;
  return list;
};
```

上述方法不可行,修改了list数组.使用如下方法(slice与concat方法)

const incrementCounter = (list, index) => {
  // Old way:
  // return list
  //  .slice(0, index)
  //  .concat([list[index] + 1])
  //  .concat(list.slice(index + 1));

  // ES6 way:
  return [
    ...list.slice(0, index),
    list[index] + 1,
    ...list.slice(index + 1)
  ];
};



