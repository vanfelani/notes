### **Axios**

Promise based HTTP client for the browser and node.js, that have a few features like:

- Make [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) from the browser
- Make [http](http://nodejs.org/api/http.html) requests from node.js
- Supports the [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- Intercept request and response
- Transform request and response data
- Cancel requests
- Automatic transforms for JSON data
- Client side support for protecting against [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)



then install in our project using : `$ npm install axios`

after install **Axios** then we can put localhost address in other file that also using Promised, we create **apiUtils**, then we make this code in apiUtils file:

```` javascript
`const axios = require('axios')`



`const comAxios = axios.create({`

  `baseURL: 'http://localhost:8080'`

`})`



`comAxios.interceptors.response.use(function (response) {`

  `const { data } = response;`

  `if (data.code !== 0) {`

​    `throw new Error(data.message || 'Uknown error.');`

  `}`

  `return data.data;`

`}, function (error) {`



  `return Promise.reject(error);`

`});`





`export { comAxios };`


````

after we add this file, we can put on our address just like this :

````javascript
onAdd = () => {
        this.props.history.push(`/items/add`);
    };
````





then we change our table with MUIDataTable, so we install MUIDataTable with this code in our promp/docker : `npm install mui-datatables --save`



after we install MUIDataTable we add this code in our tag <Page> :

````javascript
<MUIDataTable

​            title={"Item List"}

​            data={!loading ? data : []}

​            columns={columns}

​            options={options}

​          />






````

Then we add some function in our code to make our tables functional, first of all we add few function to make the table could sorting, searching, set the page and etc.

````javascript
onChangePage = (currentPage) => {
        const { table } = this.state;
        this.setState({ table: { ...table, page: currentPage } });
    }

    onRowClick = rowData => {
        this.props.history.push(`/items/${rowData[0]}`);
    };

    onRowsDeleted = (rowsDeleted) => {
        const { list } = this.props.data
        const e = list[rowsDeleted.data[0].index];
        this.props.deleteById(e.id);
        return false
    };

    onChangeRowsPerPage = (numberOfRows) => {
        const { table } = this.state;
        this.setState({ table: { ...table, size: numberOfRows } });
    }

    onSearchChange = (searchText) => {
        const { table } = this.state;
        this.setState({ table: { ...table, search: { name: searchText } } });
    }

    onColumnSortChange = (changedColumn, direction) => {
        const { table } = this.state;
        const sort = direction === 'descending' ? 'desc' : 'asc';
        this.setState({ table: { ...table, sort } });
    }
````

````javascript
 const options = {
            serverSide: true,
            page: table.page,
            count: total,
            rowsPerPage: table.size,
            rowsPerPageOptions: [2, 5, 10, 15],
            searchText: table.name,
            selectableRows: 'single',
            onRowsDeleted: this.onRowsDeleted,
            onRowClick: this.onRowClick,
            onChangePage: this.onChangePage,
            onChangeRowsPerPage: this.onChangeRowsPerPage,
            onSearchChange: this.onSearchChange,
            onColumnSortChange: this.onColumnSortChange,
            textLabels: {
                body: {
                    noMatch: loading ? <CircularProgress /> : "Sorry data not found."
                }
            }
        }
````



then we set this function above for enable function that we created before, after that we make delete method in our file to make our web could delete data, first of all we make constant request in constant file :

````javascript
export const DELETE_ITEM_REQUEST = 'FIND_ITEM_REQUEST';
export const DELETE_ITEM_SUCCESS = 'FIND_ITEM_SUCCESS';
export const DELETE_ITEM_FAILURE = 'FIND_ITEM_FAILURE';

````

then in file Items.js in folder actions we also add import code like code above, after that we import Axios in ApiUtil files to use constant variable that contain Promised, add code below :

````javascript
export const deleteById = (id) =>
    (dispatch) => {
        dispatch({
            type: DELETE_ITEM_REQUEST
        });

        comAxios.delete(`items/${id}`)
            .then(data => sleep(1000, data))
            .then(data => {
                dispatch(deleteItemSuccess(data));
            })
            .catch(error => {
                dispatch(deleteItemFailure(error));
            });
    }
````

then add function for set the type for dispatch in code below, add this code :

````javascript
function deleteItemSuccess(data) {
    return {
        type: DELETE_ITEM_SUCCESS,
        data: data
    };
}

function deleteItemFailure(error) {
    return {
        type: DELETE_ITEM_FAILURE,
        error: error
    };
}
````



after that add the function that we had in index in reducers file :

````javascript
import { deleteItemById, findItemById, findItems } from './items';

export default combineReducers({
    deleteItemById,
    findItemById,
    findItems
});
````

then add this function in items.js in reducers file`s:

````javascript
export function deleteItemById(state = defaultState, action) {
    switch (action.type) {
        case DELETE_ITEM_REQUEST:
            return {
                ...state,
                loading: true,
                error: null
            };
        case DELETE_ITEM_SUCCESS:
            return {
                data: action.data,
                loading: false,
                error: null
            };
        case DELETE_ITEM_FAILURE:
            return {
                ...state,
                loading: false,
                error: action.error
            };
        default:
            return state;
    }
}

````



 then we add this function to ItemsPage file :

````javascript
componentDidUpdate(prevProps, prevState) {
        const { deleteData, deleteError, data, error } = this.props;
        const { table } = this.state;

        if (prevProps.data !== data) {
            this.setState({ data: data.list, total: data.total });
        } else if (prevState.table !== table || prevProps.deleteData !== deleteData) {
            this.reload();
        } else if (deleteError && prevProps.deleteError != deleteError) {
            this.setState({ error: deleteError });
        } else if (error && prevProps.error != error) {
            this.setState({ error: error });
        }
    }
````

and also this code for set the dispatch file that we created before:

````javascript
const mapStateToProps = state => ({
    deleteData: state.deleteItemById.data,
    deleteError: state.deleteItemById.error,
    data: state.findItems.data,
    loading: state.findItems.loading || state.deleteItemById.loading,
    error: state.findItems.error
});

const mapDispatchToProps = {
    deleteById, findAll
};
````



after that we create the error, we want to error pop up in every file that contain page, because of that we put the error pop up in Page file, add this code inside page tag and main tag :

````javascript
<Snackbar open={this.state.showAlert} autoHideDuration={3000} onClose={this.hideAlert}>
                        <Alert onClose={this.hideAlert} elevation={6} variant="filled" severity="error">{error?.message}
                        </Alert>
                    </Snackbar>
````

and also add the code on constructor that should contain showAlert function like this code below : 

````javascript
constructor(props) {
        super(props);

        this.state = {
            drawerOpen: false,
            showAlert: false
        };
    }
````

and add this function inside the class :

````javascript
hideAlert = () => {
        this.setState({ showAlert: false })
    }
````

