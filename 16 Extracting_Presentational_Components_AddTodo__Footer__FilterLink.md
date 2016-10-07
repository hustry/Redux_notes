
## 继续Presentational Components

现有 `TodoApp` 代码
```JavaScript
class TodoApp extends Component {
  render () {
    const {
      todos,
      visibilityFilter
    } = this.props;

    const visibleTodos = getVisibleTodos(
      todos,
      visibilityFilter
    );

    return (
      <div>
        <input ref={node => {
          this.input = node;
        }} />
        <button onClick={() => {
          store.dispatch({
            type: 'ADD_TODO',
            text: this.input.value,
            id: nextTodoId++
          });
          this.input.value = '';
        }}>
          Add Todo
        </button>
        <TodoList 
          todos={visibleTodos}
          onTodoClick={id =>
            store.dispatch({
              type: 'TOGGLE_TODO',
              id
            })
          } />

        <p>
          Show:
          {' '}
          <FilterLink
            filter="SHOW_ALL"
            currentFilter={visibilityFilter}
          >
            All
          </FilterLink>
          {', '}
          <FilterLink
            filter='SHOW_ACTIVE'
            currentFilter={visibilityFilter}
          >
            Active
          </FilterLink>
          {', '}
          <FilterLink
            filter='SHOW_COMPLETED'
            currentFilter={visibilityFilter}
          >
            Completed
          </FilterLink>
        </p>
      </div>
    );
  }
}
```

定义AddTodo Presentational 组件

Functional components没有实例,没有this对象,我们需要在函数内部定义变量`input`

```JavaScript
const AddTodo = ({
  onAddClick
}) => {
  let input;

  return (
    <div>
      <input ref={node => {
        input = node;             //闭包,替换this,引用input变量 
      }} />
      <button onClick={() => {
        onAddClick(input.value);  //闭包,引用input变量 
        input.value = '';
      }}>
        Add Todo
      </button>
    </div>
  );
};
```

在container组件中使用presentational组件AddTodo.

```JavaScript
.
. // inside `TodoApp`'s `render` method
.
return (
  <div>
    <AddTodo
      onAddClick={text =>
        store.dispatch({
          type: 'ADD_TODO',
          id: nextTodoId++,
          text  
        })
      }
    />
.
.
.
```
