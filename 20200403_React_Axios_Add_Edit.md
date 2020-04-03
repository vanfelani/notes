# AXIOS IN REACT (ADD & EDIT)


Nah, yang pertama. buat dulu sebuah request ke server dengan
> PUT : untuk Edit
> 
> POST : untuk Tambah
```javascript
export const saveItems = ({ id, name }) => dispatch => {
  dispatch({ type: SAVE_ITEM_REQUEST });

  const request = id
    ? instanceAxios.put(`items/${id}`, { id, name })
    : instanceAxios.post(`items`, { name });
  request
    .then(data => sleep(500, data))
    .then(data => data)
    .then(data => {
      dispatch(saveSuccess(data));
    })
    .catch(error => {
      dispatch(saveFailure(error));
    });
};


// Class constantnya
// export const SAVE_ITEM_REQUEST = "SAVE_ITEM_REQUEST";
// export const SAVE_ITEM_SUCCESS = "SAVE_ITEM_SUCCESS";
// export const SAVE_ITEM_FAILURE = "SAVE_ITEM_FAILURE";
```
Nah, kebetulan untuk setiap **State** yang ada diProject React saya menggunakan **State Management REDUX** jadi untuk membuat sebuah *Request* import juga state didalam Reduxnya.


```javascript
import {
  FIND_ITEM_REQUEST,
  FIND_ITEM_SUCCESS,
  FIND_ITEM_FAILURE,
  FIND_ITEMS_REQUEST,
  FIND_ITEMS_SUCCESS,
  FIND_ITEMS_FAILURE,
  DELETE_ITEM_REQUEST,
  DELETE_ITEM_SUCCESS,
  DELETE_ITEM_FAILURE,
  SAVE_ITEM_FAILURE,
  SAVE_ITEM_REQUEST,
  SAVE_ITEM_SUCCESS
} from "../action/constants";

export function saveItems(state = defaultState, action) {
  switch (action.type) {
    case SAVE_ITEM_REQUEST:
      return {
        ...state,
        loading: true,
        data: null
      };
    case SAVE_ITEM_SUCCESS:
      return {
        data: action.data,
        loading: false,
        error: null
      };
    case SAVE_ITEM_FAILURE:
      return {
        ...state,
        loading: false,
        error: action.error
      };
    default:
      return state;
  }
}
```


Untuk tombol editnya saya tidak menggunakan **Button** tetapi hanya dengan meng**Click** rows nya maka akan *Link* ke Page Edit.

```Javascript
const router = [{
    path: "/items/add",
    component: ItemPage
  },
  {
    path: "/items/:id",
    component: ItemPage
  },
  {
    path: "/items",
    component: ItemListPage
  }]
```

```Javascript
const mapStateToProps = state => (
  {
    loading: state.saveItems.loading,
    saveData: state.saveItems.data,
    saveError: state.saveItems.error
  }
);
```

```Javascript
// buat onSubmit untuk mengirim data yang akan di edit atau juga di tambah

  onSubmit = event => {
    event.preventDefault();
    this.props.saveItems(this.state.form);
    console.log(this.state);

// componentDidUpdate: adalah state yang ada direducer yang akan di gunakan dihalaman ini
  componentDidUpdate(prevProps, prevState) {
    const { saveData, data, error, saveError, history } = this.props;

    if (prevProps.data != data) {
      this.setState({ form: data });
    } else if (prevProps.saveError !== saveError) {
      this.setState({ error: saveError });
    } else if (prevProps.error !== error) {
      this.setState({ error: error });
    } else if (saveData && prevProps.saveData !== saveData) {
      history.goBack();
    }
  }
  };
```
Sebelum belajar **Axios** ada baiknya kita memahami apa itu router.

Routing sendiri adalah proses pemetaan antara sebuah URL ke dalam sebuah halaman yang terdapat konten / UI (User Interface) sesuai dengan URL yang dituju.

Jika ingin membuat routing membutuhkan library tambahan karena tidak secara langsung tersedia. Ternyata ada beberapa library yang bisa digunakan, diantara library yang sangat familiar adalah react-router dan reach/router. Sebenernya yang dipakai untuk routing di React biasanya react-router-dom anak dari react-router, yang mana selain react-router-dom juga terdapat react-router-native yang bisa digunakan untuk development aplikasi Android dan iOS.


BrowserRouter digunakan sebagai router yang menggunakan API history dari HTML5, sehingga dapat menggunakan location untuk mensingkronasi UI dengan url. Di dalam object location sendiri merepresentasikan dimana lokasi aplikasi sekarang.


dan juga sebaiknya memahami apa itu **Redux**

Redux itu ibarat database di frontend
Redux itu ibarat database di sisi frontend. Sepertinya layaknya database kita bisa melakukan operasi database seperti query,filter,insert,delete. Jika anda dari background MVC ( Model View Controller ) redux mirip seperti Model dan Controller. Redux tidak menyebutnya database tapi store dan hanya ada satu store dalam satu aplikasi yang disebut Single Source of Truth
UI=f(data)
Redux terhubung dengan tampilan atau UI aplikasi, perubahan data di redux akan merubah UI secara otomatis. Jadi prinsipnya adalah :
“data berubah = UI berubah”
Redux sebagai tempat businness logic
Businnes logic seperti validasi, verifikasi, authorisasi, proses asynchronous dan lain-lain, pada implementasi banyak di tempatkan di dalam redux. Memang tidak wajib tergantung dari jenis aplikasinya.


Satu bahasan tambahan tentang Asynchronous Request.
Asynchronous JavaScript and XMLHTTP atau biasa disebut AJAX merupakan salah satu konsep yang menerapkan metode asynchronous dalam menjalankan pekerjaannya. Biasa nya AJAX digunakan untuk melakukan permintaan data (request) dan menangani sebuah tanggapan (handling response), baik response dalam bentuk XML, Javascript ataupun JSON dari sebuah Rest API.

![GitHub Logo](https://www.dicoding.com/blog/wp-content/uploads/2019/06/ajax.png)