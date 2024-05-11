## Install and Using Redux
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



## Using Redux Toolkit
1. Store Configuration.
2. Slices.
```bash
npm i @reduxjs/toolkit react-redux
```

A refer: https://blog.logrocket.com/using-typescript-redux-toolkit/

#### Store Configuration
Create a store with all reducers from slices.
Define a dispatch for using in a component (see Use it section). 
```ts
// src/app/store/configureStore.ts
import { configureStore } from "@reduxjs/toolkit";
import { basketSlice } from "../../features/basket/basketSlice";
  
export const store = configureStore({
    reducer: {
        basket: basketSlice.reducer,
    },
});
  
export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;

// store/hooks.ts
import { useDispatch, useSelector } from 'react-redux'
import type { TypedUseSelectorHook } from 'react-redux'
import type { RootState, AppDispatch } from './store'

// Use throughout your app instead of plain `useDispatch` and `useSelector`
export const useAppDispatch: () => AppDispatch = useDispatch
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector
```

#### Provider
Add the Provider to the root component.
```tsx
import { Provider } from 'react-redux';
import { store } from './app/store/configureStore';
import { router } from './app/router/Routes';

// index.tsx
<Provider store={store}>
 <RouterProvider router={router} />
</Provider>
```

#### Slice
A slice example:
```ts
// basketSlice.ts
import { createSlice } from "@reduxjs/toolkit";
import { Basket } from "../../app/models/Basket";
  
interface BasketState {
    basket: Basket | null;
}
  
const initialState: BasketState = {
    basket: null,
};
  
export const basketSlice = createSlice({
    name: "basket",
    initialState,
    reducers: {
	    addDepartment: (state, action: PayloadAction<Department>) => {
            state.departments.push(action.payload);
        },
        setBasket: (state, action) => {
            state.basket = action.payload;
        },
        removeItem: (state, action) => {
            const { dishId, quantity } = action.payload;
            const itemIdex = state.basket?.items.findIndex((i) => i.dishId === dishId);
            if (itemIdex === -1 || itemIdex === undefined) return;
            state.basket!.items[itemIdex].quantity -= quantity;
            if (state.basket?.items[itemIdex].quantity === 0) state.basket?.items.splice(itemIdex, 1);
        },
    },
});
  
export const { setBasket, removeItem } = basketSlice.actions;

export default basketSlice.reducer;
```

#### Use it
```tsx
import { useAppDispatch } from "../../app/store/configureStore";
import { setBasket } from "../basket/basketSlice";

export default function DishCard({ dish }: Props) {
    const [loading, setLoading] = useState(false);
    const dispatch = useAppDispatch();
    
  
    function handleAddItem(dishId: number) {
        setLoading(true);
        agent.Basket.addItem(dishId)
            .then((basket) => dispatch(setBasket(basket)))
            .catch((error) => console.log(error))
            .finally(() => setLoading(false));
    }
}

//
const { basket } = useAppSelector(state => state.basket);
```

At this stage, the app communicates with API by agent, and manages the status by redux toolkit.

Async Function in Redux


#### CRUD Logic
