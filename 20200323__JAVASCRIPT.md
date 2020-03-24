### PROMISE
Promise adalah objek yang merepresentasikan function suatu callback

Implementasi promise `createAudioFileAsync()`:
```js
const promise = createAudioFileAsync(audioSettings); 
promise.then(successCallback, failureCallback);
```
atau bisa seperti ini:
```js
createAudioFileAsync(audioSettings).then(successCallback, failureCallback);
```
struktur code seperti itu biasanya di namakan pemanggilan function secara asyncrhonous


**Guarantees**

 yaitu pemanggilan callback dengan menambahkan syntax `.then()`

**Chaining**

yaitu implementasi pemanggilan callback baru secara berantai 

Contoh :
```js
const promise = doSomething();
const promise2 = promise.then(successCallback, failureCallback);
```
atau

```js
const promise2 = doSomething().then(successCallback, failureCallback);
```
promise2 tidak hanya mengeksekusi `doSomething` tapi juga akan mengeksekusi *callback* `successCallback` serta `failureCallback` yang merupakan function asyncronous lainnya yang mengembalikan promise begitupun jika kita menambahkan beberapa *callback* didalam promise2 dan akan dieksekusi selanjutnya 

Adapun contoh *Promise chain*

```js
doSomething()
.then(function(result) {
  return doSomethingElse(result);
})
.then(function(newResult) {
  return doThirdThing(newResult);
})
.then(function(finalResult) {
  console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);
```
atau

```js
doSomething()
.then(result => doSomethingElse(result))
.then(newResult => doThirdThing(newResult))
.then(finalResult => {
  console.log(`Got the final result: ${finalResult}`);
})
.catch(failureCallback);
```

**Chaining after a catch**

yaitu untuk memberi tau jika ada suatu *catch* / kegegalan didalam suatu *chain* / rantai

Contoh:
```js
new Promise((resolve, reject) => {
    console.log('Initial');

    resolve();
})
.then(() => {
    throw new Error('Something failed');
        
    console.log('Do this');
})
.catch(() => {
    console.error('Do that');
})
.then(() => {
    console.log('Do this, no matter what happened before');
});
```
dan akan menghasilkan output jika terjadi *catch* didalam proses *chain*

`Initial
Do that
Do this, no matter what happened before`

**async await**
yaitu proses menunggu untuk mengeksekusi *promise* selanjutnya

syntax async await dengan menambahkan `async` sebelum `function`
```js
async function name([param[, param[, ...param]]]) {
   statements
}
```

Implementasi async await 

```js
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
  // expected output: 'resolved'
}

asyncCall();
```

```
Catatan: suatu await akan berjalan pada async function
```
### Iterators
Dalam JavaScript, iterator adalah objek yang mendefinisikan urutan dan berpotensi mengembalikan nilai pada saat penghentiannya.

Secara khusus, iterator adalah objek apa pun yang mengimplementasikan protokol Iterator dengan metode next () mengembalikan objek dengan dua properti:

- `value` nilai
- `done` nilai pengembalian iterator berbentuk boolean *true / false*

```js
const it = makeRangeIterator(1, 10, 2);

let result = it.next();
while (!result.done) {
 console.log(result.value); // 1 3 5 7 9
 result = it.next();
}

console.log("Iterated over sequence of size: ", result.value); // [5 numbers returned, that took interval in between: 0 to 10]
```
Iterator dapat diulang kembali dengan cara eksplisit berulang kali dengan menggunakan `next()`

Iterator yang paling umum di Javascript adalah iterator Array, yang hanya mengembalikan setiap nilai dalam array terkait secara berurutan.

**Generator functions**

Biasanya dideklarasikan dengan menggunakan syntax `function *`  

```js
function* makeRangeIterator(start = 0, end = 100, step = 1) {
    let iterationCount = 0;
    for (let i = start; i < end; i += step) {
        iterationCount++;
        yield i;
    }
    return iterationCount;
}
```
`yield` merupakan return sementara

### Fetch API

`fetch()` syntax untuk mengambil/menggunakan suatu library dari luar

```js
fetch('http://example.com/movies.json')
  .then((response) => {
    return response.json();
  })
  .then((data) => {
    console.log(data);
  });
```

Berikut code untuk mengatur cors origin pada java
 
```java
@Bean
	public CorsFilter corsFilter() {
		final UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
		final CorsConfiguration config = new CorsConfiguration();
		config.setAllowCredentials(true);
		// Don't do this in production, use a proper list of allowed origins
		config.setAllowedOrigins(Collections.singletonList("*"));
		config.setAllowedHeaders(Arrays.asList("Origin", "Content-Type", "Accept"));
		config.setAllowedMethods(Arrays.asList("GET", "POST", "PUT", "OPTIONS", "DELETE", "PATCH"));
		source.registerCorsConfiguration("/**", config);
		return new CorsFilter(source);
	}
```

