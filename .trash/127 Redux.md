#### Installing and Using
`npm install redux react-redux`

A basic example of using Redux.
```typescript
export interface CounterState {
  data: number;
}

const initialState: CounterState = {
  data: 42
}

export default function counterReducer(state = initialState, action: any){
  return state;
}


// configureStore.ts
import { createStore } from 'redux';

export function configureStore(){
  return createStore(counterReducer);
}
```
#### Redux Actions


#### Redux Toolkit
`npm install @reduxjs/toolkit`

Same basic example.
```typescript
export interface CounterState {
  data: number;
}


```