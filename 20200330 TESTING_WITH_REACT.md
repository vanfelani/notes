# Testing With React
***

Ada beberapa cara untuk menguji React Component. Secara umum, mereka dibagi menjadi dua kategori:

- `Rendering component trees` di dalam *environment* tes yang sudah disederhanakan dan ditegaskan pada keluarannya.
- `Menjalankan aplikasi lengkap` di dalam *environment* peramban asli (juga dikenal sebagai tes `“end-to-end”`).

Bagian dokumentasi ini berfokus pada strategi tes untuk kasus pertama. Sementara tes end-to-end secara menyeluruh bisa sangat berguna untuk mencegah regresi terhadap alur kerja yang penting, tes semacam itu tidak diperhatikan terutama pada komponen React, dan berada di luar cakupan bagian ini.

## ~ Recommended Tools

- `Jest` adalah *test runner* pada JavaScript yang memungkinkan Anda mengakses DOM melalui `jsdom`. Sementara jsdom hanyalah perkiraan cara kerja browser, seringkali cukup baik mengetes komponen pada React. Jest memberikan kecepatan iterasi yang bagus dikombinasikan dengan fitur-fitur yang *powerful* seperti *mocking modules* dan *timers* sehingga Anda dapat memiliki kontrol lebih pada kode yang dijalankan.

- `React Testing Library` adalah seperangkat *helpers* yang memungkinkan Anda mengetes komponen pada React tanpa bergantung pada detail implementasinya. Pendekatan ini membuat *refactoring* menjadi mudah dan juga mendorong Anda untuk menerapkan *best practices* untuk aksesbilitas. Mungkin tidak memberikan cara untuk me-*render* secara “dangkal” pada sebuah komponen tanpa anak, *test runner* seperti Jest yang memungkinkan Anda melakukan `mocking`.

## ~ How To Configure *Jest*

- **Install With Npm**
```
npm install --save-dev jest babel-jest @babel/preset-env @babel/preset-react react-test-renderer
```
- **Install With Yarn**
```
yarn add --save-dev jest babel-jest @babel/preset-env @babel/preset-react react-test-renderer
```

## ~ How To Configure *React Testing Library*

### - Installation
- **Install With Npm**
```
npm install --save-dev enzyme enzyme-adapter-react-16
npm install --save-dev jest-environment-enzyme jest-enzyme
```

- **Install With Yarn**
```
yarn add --save-dev enzyme enzyme-adapter-react-16
yarn add --save-dev jest-environment-enzyme jest-enzyme
```
### - SetUp

Tambahkan Script dibawah ini di dalam file `setupTest.js`

```js
import { configure } from "enzyme";
import Adapter from "enzyme-adapter-react-16";
import 'jest-enzyme';

configure({
adapter: new Adapter(),
setupFilesAfterEnv: ["jest-enzyme"],
testEnvironment: "enzyme",
snapshotSerializers: ["enzyme-to-json/serializer"]
});
```



