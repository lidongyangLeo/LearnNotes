RTK

RTK は ReduxToolKit



## API

### configureStore()

#### Parameters

- reducer  (必須)

root recucer for the store 

- middleware(非必須)

  An optional array of Redux middleware functions

- devTools
  
  - default： true

開発環境でtrue､puduction環境はfalse必要かな｡

```typescript
devTools: process.env.NODE_ENV !== 'production'
```

- preloadedState (初始化state)
  - An optional initial state value to be passed to the Redux CreateStore function.
- enhancers（还不太清楚这么使用）
  - An optional array of Redux store enhancers, or a callback function to customize the array of enhancers.



```typescript
import {configureStore} from "@reduxjs/toolkit"
import rootReducer from "./reducers"

const store = configureaStore({reuducer: rootReducer});
```

Full Example

```
import {configureStore} from "@reduxjs/toolkit"
import logger from "redux-logger"
import {reduxBatch } from "@manaflaire/redux-batch"

```



### combineReducers(reducers)

reducer合并成一个reducer函数

通过定义的key 来控制子reducer的state

```typescript
rootReducer = combineReducers({potato: potatoReducer, tomato: tomatoReducer})
// This would produce the following state object
{
  potato: {
    // ... potatoes, and other state managed by the potatoReducer ...
  },
  tomato: {
    // ... tomatoes, and other state managed by the tomatoReducer, maybe some nice sauce? ...
  }
}
```





### createReducer()



### createAction()





### createSlice()

公式ドキュメントからの抜粋(ばっすい)となります｡

```typescript
const counterSlice = createSlice({
		name: "counter",
		initialState: 0,
		reducers: {
			increment: state => state + 1,
			decrement: state => state - 1
		}
});

const store = configureStore({
   reducer: counterSlice.reducer
});

const { actions, reducer } = counterSlice;
const {increment, decrement} = actions;

```

こんな感じでAction, Reducerを定義できます｡

これよりほぼActionのコードがなくなる｡

Reducerのネストはいつも通り感じです｡

````typescript
const sliceA = creatSlice({
    name: "reducerA",
    .....
})

const sliceB = createSlice({
    name: "reducerB",
    .....
})

const mergeReducer = combineReducers({
   reducerA: sliceA.reducer,
   reducerB: sliceB.reducer,
})
````



### createAsyncThunk()



creatAsyncThunkを使用しない場合､非同期処理完了した後にdispatch(sliceに提起)



### createEntityAdapter



