
## 使用`connect()` (FooterLink组件)


**mapStateToProps定义**

基于组件自身传递的props与store中state确定传递的`active`prop. `mapStateToProps`函数第2个参数为ownProps表征组件自身传递的props，而非由state转换后的props

```JavaScript
const mapStateToLinkProps = (
  state,                            //第一个参数为state
  ownProps                          //组件自身props
) => {
  return {
    active:
      ownProps.filter ===
      state.visibilityFilter
  }
};
```

**mapDispatchToProps定义**

```JavaScript
const mapDispatchToLinkProps = (
  dispatch,
  ownProps
) => {
  return {
    onClick: () => {
      dispatch({
        type: 'SET_VISIBILITY_FILTER',
        filter: ownProps.filter
      });
    }
  };
}
```

**使用connect()结合两个函数构建Container组件FilterLink**

```JavaScript
const FilterLink = connect(
  mapStateToLinkProps,
  mapDispatchToLinkProps
)(Link);
```