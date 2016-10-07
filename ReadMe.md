
## Redux 学习笔记

![Redux](https://camo.githubusercontent.com/f28b5bc7822f1b7bb28a96d8d09e7d79169248fc/687474703a2f2f692e696d6775722e636f6d2f4a65567164514d2e706e67)

学习笔记翻译自[tayiorbeii/egghead.io_redux_course_notes](https://github.com/tayiorbeii/egghead.io_redux_course_notes)

笔记中以`Counter`与`TodoApp`例子为例,逐步介绍了redux的各个方面:

* 01 Intro

	介绍了redux的三大特性.

* 02 Reducer_Store

	介绍Reducer与Store对象.

* 03 Implementing_Store_from_Scratch

	手动构建一个store对象.

* 04 React_Counter_Example

	实现Counter例子

* 05 Avoiding_Array_Mutations

	介绍如何避免修改数组.使用`concat`方法而非`push`方法

* 06 Avoiding_Object_Mutations

	介绍如何避免修改对象.使用Object.assign()函数,如果支持ES7特性,可以使用`...spread`语法.

* 07 Writing_a_Todo_List_Reducer

	为Todo List添加一个reducer.

* 08 Reducer_Composition_with_Arrays

	针对state树中的数组,如何进行reducer分解.

* 09 Reducer_Composition_with_Objects

	针对state树中的对象属性,如何进行reducer分解.

* 10 Reducer_Composition_with_combineReducers

	使用帮助函数`combineReducers()`进行reducer composition.

* 11 Implementing_combineReducers_from_Scratch

	手动实现`combineReducers()`函数.

* 12 React_Todo_List_Example_Adding_a_Todo

	在Store定义后,定义React部分.

* 13 React_Todo_List_Example_Toggling_a_Todo

	实现`TOGGLE_TODO`action.

* 14 React_Todo_List_Example_Filtering_Todos

	实现实现FilterList功能

* 15 Extracting_Presentational_Components_Todo__TodoList

	将单个组件分解成多个简单的Presentational组件再重构.

* 16 Extracting_Presentational_Components_AddTodo__Footer__FilterLink

	继续使用Presentational Components进行重构.

* 17 Extracting_Container_Components_FilterLink

	实现Container组件FilterLink,以及它的缺陷.使用React提供的forceUpdate()方法强制更新.

* 18 Extracting_Container_Components_VisibileTodoList__AddTodo

	实现Container组件(VisibleTodoList,AddTodo)

* 19 Passing_the_Store_Down_Explicitly_via_Props

	将store以prop的形式传递给TodoApp组件,这种方法每个组件都显式定义一个名为store的prop.

* 20 Passing_the_Store_Down_Implicitly_via_Context

	通过React的context来进行store隐式传递.

* 21 Passing_the_Store_Down_with_Provider_from_React_Redux

	使用`react-redux`提供的Provider组件.

* 22 Generating_Containers_with_connect_from_React_Redux_VisibleTodoList

	引入connect()构建container组件

* 23 Generating_Containers_with_connect_from_React_Redux_AddTodo

	使用connect重构`VisibleTodoList`组件

* 24 Generating_Containers_with_connect_from_Readct_Redux_FooterLink 

	使用`connect()`构建FooterLink组件
