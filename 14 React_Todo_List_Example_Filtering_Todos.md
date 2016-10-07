
## React Todo List Example (Filtering Todos)

实现Filter功能,首先创建一个`FilterLink`组件,点击后可以切换当前显示的todo List,触发`SET_VISIBILITY_FILTER`action.

```JavaScript
.
. // Reducer code, etc.
.
const FilterLink = ({
  filter,
  children
}) => {
  return (
    <a href='#'
       onClick={e => {
         e.preventDefault();
         store.dispatch({
           type: 'SET_VISIBILITY_FILTER',
           filter
         });
       }}
    >
      {children}  //将文本子元素显示在<a>中
    </a>
  )
}
.
.
.
```

在`TodoApp`组件中使用`FilterLink`.

```JavaScript
.
.
.
<p>
  Show:
  {' '}
  <FilterLink
    filter='SHOW_ALL'
  >
    All
  </FilterLink>
  {' '}
  <FilterLink
    filter='SHOW_ACTIVE'
  >
    Active
  </FilterLink>
  {' '}
  <FilterLink
    filter='SHOW_COMPLETED'
  >
    Completed
  </FilterLink>
</p>
.
. // close the containing `<div>` and the TodoComponent
.
```


