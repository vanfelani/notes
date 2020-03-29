# **MATERIAL UI TABLE & FORM**

## TABLE

Disini akan dijelaskan cara menambahkan tampilan table pada web yang kita buat

### Langkah Pertama

1, Install material-table :
- Menggunakan npm
```
npm install material-table --save
```
- Menggunakan yarn
```
yarn add material-table
```
2, Menambahkan material-icons pada index.html : 
```
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
```

### Langkah Kedua

1, Menambahkan import untuk material table :
```
import MaterialTable from 'material-table';
```

2, Menambahkan kodingan table :
```
<div style={{ maxWidth: '100%' }}>
      <MaterialTable
          columns={[
            { title: 'ID', field: 'id' },
            { title: 'NAMA', field: 'name' }
          ]}
          //data akan ditampilkan pada table
          data={[{ id: '1', name: 'Alex' }]}
          title="Demo Title"
      />
</div>
```
adapun cara kita untuk menampilkan data dengan menggunakan array :
```
const data = [
    {id: '1', name: 'Alex'},
    {id: '2', name: 'Varhoud'},
    {id: '3', name: 'Other'}
]
```
### Langkah Ketiga
1, Menambahkan import untuk Button AddIcon :
```
import AddIcon from "@material-ui/icons/Add";
import { Button } from "@material-ui/core";
```

2, Menampilkan Button AddIcon : 
```
<div className={classes.formButton}>
       <Button
            startIcon={<AddIcon />}
            onClick={this.onAdd}
            variant="contained"
            color="primary"
       >
            Add Item
       </Button>
</div>
```

3, Tambahkan function AddIcon :
```
onAdd = (event, data) => {
    this.props.history.push(`/items/add`);
  };
```
note: nantinya akan beralih ke form

#### All Props
adapun kegunaan yg bisa kita pakai dan bisa dilihat di https://material-table.com/#/docs/all-props

Contoh kodingan untuk onRowClick:
```
onRowClick = (event, data) => {
    this.props.history.push(`/items/${data.id}`);
};
```
lalu tambahkan pada MaterialTable:
```
onRowClick={this.onRowClick}
```
note: nantinya akan beralih ke itemPage(Detail dari Item)

## FORM

Disini akan dijelaskan cara menambahkan tampilan form pada web yang kita buat

### Langkah Pertama
1, Buatlah file js baru atau file js yangg sudah ada

2, Tambahkan import untuk Button(Save), TextField dan SaveIcon :
```
import { Button, TextField } from "@material-ui/core";
import SaveIcon from "@material-ui/icons/Save";
```

3, Tambahkan kodingan untuk tampilan form :
```
<form noValidate autoComplete="off" onSubmit={this.onSubmit}>
          {id && (
            <div className={classes.formField}>
              <TextField
                id="id"
                name="id"
                label="ID"
                value={id}
                fullWidth
                InputProps={{ readOnly: true }}
              />
            </div>
          )}
          <div className={classes.formField}>
            <TextField
              id="name"
              name="name"
              label="Name"
              value={name}
              fullWidth
              onChange={this.onChange}
            />
          </div>
          <div className={classes.formButton}>
            <Button
              startIcon={<SaveIcon />}
              variant="contained"
              color="primary"
              type="submit"
            >
              Save
            </Button>
          </div>
        </form>
```