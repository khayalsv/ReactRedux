# Using Create React App

npx create-react-app my-app --template redux

# An Existing React App​

npm install react-redux

# Connecting React to Redux

1. store faylını yaradıldığı fayldan export. ( export { store }; )
2. index.js faylında store-i import. ( import { store } from "./store" )
3. Provider-i react-redux kitabxanasından import. ( import { Provider } from "react-redux"; )
4. App componentini Providerin daxilinə atırıq və 'store' prop olaraq Provider-a göndəririk.

```js
import { createRoot } from "react-dom/client";
import { Provider } from "react-redux";
import App from "./App";
import { store } from "./store"

const rootElement = document.getElementById("root");
const root = createRoot(rootElement);

root.render(
    <Provider store={store}>
        <App />
    </Provider>
);
```

## store && slice

Redux Toolkit istifadə edərək, slice və store adı verilən obyekt yaradırıq.Yəni store, bütün proyektimizin stateni tutacaq bir obyektdir.Proyektlərdə əsasən 1 ədəd store olur. 1-dən çox store nadir hallarda və ara sıra çox-çox böyük proyektlərdə görülür.

Slice bizim üçün actionları və reducerləri yaradır.3 məqsədi var
- Slice başlanğıc vəziyyəti müəyyənləşdirir. (initialState)
- Mini-reducer proseslərini alıb, böyük bir reducer-də birləşdirir. (reducers) -> (reducer)
- Action funksiyalarını yaradır.

#### code

1. src-də store folderi yaradırıq
2. store folderində index.js faylı
3. import { configureStore, createSlice } from '@reduxjs/toolkit'
4. yeni bir dəyişən yaradırıq (slice)
5. store dəyişəni yaradıb, configureStore-u göndəririk, və sonda 'console.log(store);' yazıb, işlədiyini yoxlayırıq
6. index.js - də import "./store"
7. store-ni manuel yoxlamaq üçün
8. state-i dəyişdirmək üçün dispatch-dən istifadə edirik

```js
import { configureStore, createSlice } from '@reduxjs/toolkit'

const songsSlice = createSlice({
    name: 'song',
    initialState: [],
    reducers: {
        // 'song' + '/' + 'addSong' = 'song/addSong
        addSong(state, action) {
            state.push(action.payload);
        },
        removeSong(state, action) {

        }
    }
})

const store = configureStore({
    reducer: {
        songs: songsSlice.reducer
    }
});

export { store };
export const {addSong} =songsSlice.actions;

// // console.log(songsSlice.actions.addSong());  action creator

// // const startingState = store.getState();
// // console.log(JSON.stringify(startingState));

// // store.dispatch({
// //     type: 'song/addSong',
// //     payload: 'New Song!!'
// // })

// store.dispatch(songsSlice.actions.addSong("Some song!"));

// const finalState = store.getState();
// console.log(finalState);

```

### Changing State
Layihə başına dəfələrlə istifadə olunur

1. State-ni müəyyən bir şəkildə dəyişən slice-lardan birinə reducer əlavə edirik.
2. Slice-nin avtomatik yaratdığı 'action creator'-ı ixrac edirik.
3. Dispatch etmək istədiyimiz componenti tapırıq.
4. 'action creator'-ı və 'useDispatch' funksiyasını 'react-redux' kitabxanasından import edirik.
5. Dispatch funksiyasına daxilm olmaq üçün 'useDispatch' hookunu çağırırıq.
6. İstifadəçi bir şey etdikdə, action-ı əldə etmək üçün 'action creator'-ı çağırıb onu göndəririk.

#### code

```js
1.
const songsSlice = createSlice({
    name: 'song',
    initialState: [],
    reducers: {
        // 'song' + '/' + 'addSong' = 'song/addSong
        addSong(state, action) {
            state.push(action.payload);
        },
        removeSong(state, action) {

        }
    }
})

2.
export const {addSong} = songsSlice.actions;

3.
const handleSongAdd = (song) => {
    //
    console.log(song);
};

4.
import { useDispatch } from "react-redux";
import { addSong } from "../store"

5.
const dispatch = useDispatch();

6.
// const handleSongAdd = (song) => {
//     const action = addSong(song);
//     console.log(action);
   
//     dispatch(action);
// };

const handleSongAdd = (song) => {
    dispatch(addSong(song));
};
```
![Screenshot_1](https://user-images.githubusercontent.com/88320671/210997944-757b8630-ea9c-49c6-8cfb-1e4ecac8644e.png)

