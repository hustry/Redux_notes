

#### 避免对象被修改

为了避免对象被修改,使用Object.assign()方法与...spread.

```js
const toggleTodo = (todo) => {
  return Object.assign({}, todo, {
    completed: !todo.completed
  });
};
```

object.assign函数第一个参数是{},该对象会被修改，其他已存在对象不会被修改,后续参数对象的属性会被拷贝到第一个空对象,后续对象会覆盖前面对象的属性.
使用 ...spread语法, 该特性需要ES7支持.

```js
const toggleTodo = (todo) => {
  return {
    ...todo,
      completed: !todo.completed
  };
};
```
