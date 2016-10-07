

## 使用`connect()`

使用connect重构`VisibleTodoList`组件

之前
```JavaScript
const AddTodo = (props, { store }) => {
  .
  .
  .
    <button onClick={() => {
      store.dispatch({
      .
      .
      .

}
AddTodo.contextTypes = {
  store: React.PropTypes.object
}
```

重构之后

```JavaScript
let AddTodo = ({ dispatch }) => {
  .
  . // inside `return`
  .
    <button onClick={() => {
      dispatch({
      .
      .
      .
}
// No more `AddTodo.contextTypes`

AddTodo = connect(
  state => {
    return {};
  },
  dispatch => {
    return { dispatch };
  }
)(AddTodo);

```