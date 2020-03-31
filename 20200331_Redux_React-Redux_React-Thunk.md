# Redux
adalah state management pada javascript.


cara install Redux.

    NPM : 
        npm install redux
        npm install react-redux
    Yarn :
        yarn add redux
        yarn add react-redux

flow Redux :
Component -> Action -> Store -> Reducer -> Store -> Component



Cara Pemakaian :  
1. buat variabel konstan untuk tiap aksi sebagai key untuk redux nantinya dan disimpan pada folder actions, contoh :
``` Javascript
const FIND_ITEMS = 'FIND_ITEMS'
const FIND_ITEM_BY_ID = 'FIND_ITEM_BY_ID'
```

2. buat folder baru untuk reducer di dalam folder src

3. buat file aksi untuk reducer, contoh : items.js
4. buat function aksi pada reducer, contoh : 

```Javascript
export function findItemById(state = {}, action) {
    switch (action.type) {
        case FIND_ITEM_BY_ID:
            for (const e of data) {
                if (e.id == action.id) {
                    return e;
                }
            }
        default:
        return state;
    }
}

export function findItems(state = [], action) {
    switch(action.type) {
        case FIND_ITEMS :
            return data;
        default:
            return state;
    }
}
```

5. pada folder reducers buat file index.js yang berisi :

```Javascript
import { combineReducers } from 'redux';
import {findItemById, findItems} from './items';

export default combineReducers({
    findItems,
    findItemById
});
```

6. pada index.js utama import provider, createStore, dan reducers lalu bungkus component <App /> dengan component <Provider>. contoh : 

```Javascript
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import reducers from './reducers';

const store = createStore(reducers);

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```

7. Pada halaman yang ingin di integrasikan dengan redux, tambahkan function dam import connect :

```Javascript
import { connect } from 'react-redux';

const mapStateToProps = state => ({
  data: state.findItems
});

const mapDispatchToProps = {
  findAll
};

export default connect(
  mapStateToProps,
  mapDispatchToProps,
)(ItemsPage);

```

8. ubah componentDidMount() dan data pada table menjadi : 

```Javascript
// pada componentDidMount
  componentDidMount() {
    this.props.findAll();
  }
// pada Table
data={this.props.data}
```

# Redux-Thunk
Thunk adalah middleware pada redux berguna untuk menyisipkan function sebelum masuk ke store.
status pada async ada 3 yaitu, LOADING, RESPON dan ERROR.

cara install :

    NPM :
        npm install redux-thunk

    Yarn : 
        yarn add redux-thunk

cara pemakaian:


1. pada folder actions/items.js pindahkan data yang ada pada reducer dan ganti kode untuk aksi yang akan dijalankan.

```Javascript
import { 
  FIND_ITEM_REQUEST, FIND_ITEM_SUCCESS, FIND_ITEM_FAILURE,
  FIND_ITEMS_REQUEST , FIND_ITEMS_SUCCESS, FIND_ITEMS_FAILURE
 } from "./constants"; 
 const data = [
  {
    id: 1,
    name: 'Kecap Asin'
  },
  {
    id: 2,
    name: 'Garam Laut Mati'
  },
  {
    id: 3,
    name: 'Mi Goreng Tikus'
  }
];

function sleep(delay) {
  return new Promise(function (resolve) {
    setTimeout(resolve, delay);
  }); 
}

export const findById = (id) =>
  (dispatch) => {
    dispatch({
      type: FIND_ITEM_REQUEST
    });
      sleep(3000)
          .then(() => {
            let result = null;
              for (const e of data) {
                  if (e.id == id) {
                      result = e;
                  }
              }
              if (result) {
                dispatch({
                  type: FIND_ITEM_SUCCESS,
                  data: result
                });
              } else {
                throw new Error('Item Not Found')
              }
          })
          .catch(error => {
            dispatch({
              type: FIND_ITEM_FAILURE,
              error: error
            });
          });
}
export const findAll = () => 
  (dispatch) => {
    dispatch({
      type: FIND_ITEMS_REQUEST
    });
      sleep(3000)
          .then(() => {
              dispatch({
                type: FIND_ITEMS_SUCCESS,
                data: data
              });
          });
  }

```

2. Pada file constant.js ubah variabel konstan menjadi :

```Javascript
export const FIND_ITEM_REQUEST = 'FIND_ITEM_REQUEST';
export const FIND_ITEM_SUCCESS = 'FIND_ITEM_SUCCESS';
export const FIND_ITEM_FAILURE = 'FIND_ITEM_FAILURE';

export const FIND_ITEMS_REQUEST = 'FIND_ITEMS_REQUEST';
export const FIND_ITEMS_SUCCESS = 'FIND_ITEMS_SUCCESS';
export const FIND_ITEMS_FAILURE = 'FIND_ITEMS_FAILURE';

```

3. pada file reducers/items.js ubah menjadi

```Javascript
import { 
    FIND_ITEM_REQUEST, FIND_ITEM_SUCCESS, FIND_ITEM_FAILURE,
    FIND_ITEMS_REQUEST , FIND_ITEMS_SUCCESS, FIND_ITEMS_FAILURE
  
   } from "../actions/constants"; 
  
  
const defaultState = {data: null, loading: false, error: null};

export function findItemById(state = defaultState , action) {
    switch (action.type) {
        case FIND_ITEM_REQUEST:
            return {
                loading: true,
                error: null
            }
        case FIND_ITEM_SUCCESS:
            return {
                data: action.data,
                loading: false,
                error: null
            }
        case FIND_ITEM_FAILURE:
            return {
                ...state,
                loading: false,
                error: action.error
            }
        default:
        return state;
    }
}

export function findItems(state = defaultState, action) {
    switch(action.type) {
        case FIND_ITEMS_REQUEST:
            return {
                loading: true,
                error: null
            }
        case FIND_ITEMS_SUCCESS:
            return {
                data: action.data,
                loading: false,
                error: null
            }
        case FIND_ITEMS_FAILURE:
            return {
                ...state,
                loading: false,
                error: action.error
            }
        default:
            return state;
    }
}
```

3. Buat file store.js pada folder configs, 

```Javascript
import { createStore, applyMiddleware } from 'redux';
import reducers from '../reducers';

export default createStore(reducers,applyMiddleware(thunk));

```

4. lalu pada index.js utama hapus import createStore, dan reducers
5. ubah kode berikut pada variabel mapStateToProps pada file ItemsPage.js

```Javascript
const mapStateToProps = state => ({
  data: state.findItems.data || [],
  loading: state.findItems.loading,
  error: state.findItems.error
});

```

6. tambahkan kode berikut pada ItemsPage.js

```Javascript
// pada const dalam render
    const { data, loading} = this.props;
//pada table 
    data={data}
    isLoading={loading}
```