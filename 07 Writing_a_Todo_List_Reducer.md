
## Todo List Reducer

####为Todo List添加一个reducer

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
    default:
      return state;
  }
};

const testAddTodo = () => {
  const stateBefore = [];
  const action = {
      type: 'ADD_TODO',
      id: 0,
      text: 'Learn Redux'
  };
  const stateAfter = [{
      id: 0,
      text: 'Learn Redux',
      completed: false
  }];

  deepFreeze(stateBefore);
  deepFreeze(action);

  expect(
    todos(stateBefore, action)
  ).toEqual(stateAfter);
};

testAddTodo();
console.log('All tests passed')
```

以上添加了一个reducer处理type为'ADD_TODO'的action,起始state为[],经过添加action后，state包含一个元素。

#### 再添加一个action type "TOGGLE_TODO"

```JavaScript
const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      // ... ADD_TODO logic as above
    case 'TOGGLE_TODO':
      return state.map(todo => {
        if (todo.id !== action.id) {
          return todo;
        } else {
		// for the todo that matches the action id return all other information the same
		// but change the completed property to the opposite of what it was previously
          return {
            ...todo,
            completed: !todo.completed
          };
        }
      });
    default:
      return state;
  }
};

const testToggleTodo = () => {
  const stateBefore = [
    {
      id: 0,
      text: 'Learn Redux',
      completed: false
    },
    {
      id: 1,
      text: 'Go Shopping',
      completed: false
    }
  ];
  const action = {
      type: 'TOGGLE_TODO',
      id: 1
  };

  const stateAfter = [
    {
      id: 0,
      text: 'Learn Redux',
      completed: false
    },
    {
      id: 1,
      text: 'Go Shopping',
      completed: true
    }
  ];

  deepFreeze(stateBefore);
  deepFreeze(action);

  expect(
    todos(stateBefore, action)
  ).toEqual(stateAfter);
};

testAddTodo();
testToggleTodo();
console.log('All tests passed.');
```