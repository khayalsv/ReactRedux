# Using Create React App

npx create-react-app my-app --template redux

# An Existing React App​

npm install react-redux


## store

Redux Toolkit istifadə edərək, slice və store adı verilən obyekt yaradırıq.Yəni store, bütün proyektimizin stateni tutacaq bir obyektdir.Proyektlərdə əsasən 1 ədəd store olur. 1-dən çox store nadir hallarda və ara sıra çox-çox böyük proyektlərdə görülür.

- 1. src-də store folderi yaradırıq
- 2. store folderində index.js faylı
- 3. import { configureStore, createSlice } from '@reduxjs/toolkit'
- 4. yeni bir dəyişən yaradırıq (slice). Daxilindəki propertylər name (string), initialState:[], reducers (object)
- 5. store dəyişəni yaradıb, configureStore-u göndəririk, və sonda 'console.log(store);' yazıb, işlədiyini yoxluyuruq
- 6. index.js - də import "./store"
- 7. store-ni manuel yoxlamaq üçün:
```js
    const startingState = store.getState();
    console.log(startingState);
```
- 8. state-i dəyişdirmək üçün dispatch-dən istifadə edək:
```js
    store.dispatch({
        type: 'song/addSong',
        payload: 'New Song!!'
    })

    const finalState = store.getState();
    console.log(finalState);
```