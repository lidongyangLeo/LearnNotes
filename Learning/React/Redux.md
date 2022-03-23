## Redux とは

state(状態)を容易に管理をするためのフレームワークのこと｡



#### stateとは



Redux の主に要素(機能)

- Action
- Reducer
- Store

ActionをStoreへdispatch(送信)すると､storeのstateが変更される｡stateの変更は必ずActionを経由して行う｡

Reducer

Stroreから受け取ったActionとstateに応じて､変更されたstateを返す純粋関数(同じ引数を渡されたら必ず同じ結果を返す関数)｡

Store

アプリケーションの全てのstateを保持するオブジェクト｡

ActionをStoreにdispatchする手段(store.dispatch())を提供する｡また､storeとdispatchされたActionを､指定したReducerに渡してstateを変更する｡



RTK

Create a Redux Store 

combineReducers

useSelector

useDispatch

combineReducers 

Redux  

想要更新state中的数据，你需要发起一个Action

把action和state串起来，开发一些函数 就是reducer 

state是只读的， 唯一改变state的方法就是触发action，action是一个用于描述已发生事件的普通对象





React.ReactElement  使用React.createElement创建的，可以简单理解为react中的jsx的元素。

React.ReactNode.  ------ <div>xxx</div> xx的合法类型

React.CSSProperties ---- 组件内联的style对象的类型

React.RefObject` —— `React.createRef`创建的类型，只读不可改

React.MutableRefObject` —— `useRef`创建的类型，可以修改











## Redux 

redux 是一个状态管理的





