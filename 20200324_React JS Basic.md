# React Js Basic

Install react dengan menggunakan npx:
1. Ketik npx create-react-app web-client di cmd/terminal.
2. Running dengan ketik npm start

Npx sendiri adalah fasilitas untuk membantu menginstall react yang bersifat excuteable.

## React Js
create-react-app sudah termasuk dengan webpack (Asset (Html, Javascript, CSS) Bundling), babel (Transpile : Kode ke Kode.), dev server.

## Transpile:
java script react diconvert dengan babel ke js yang lebih bisa dimengerti oleh browser.

## Struktur Direktori
- src: source code
- public: folder tempat static file
- node_modules: folder tempat dependencies
- package.json: informasi terkait dependency dan konfigurasi
- package-lock.json: semua versi dependency yang dipakai
- readme.md: deskripsi project.

## JSX( special js dialect)
JSX seperti Html syntax (tapi bukan html) yang digunakan pada react yang extends ECMAScriptdiconvert. Nanti nya JSX diconvert menjadi js yang dimengerti oleh browser menggunakan babel.

## Class Component vs Functional Component

### Class Component:
Aturan class component:
1. harus javascript class
2. harus extend react.component dan membuat fungsi render dengan nilai return react element

### Functional Component
Functional component:
hanya perlu membuat komponen dengan cara membuat fungsi dengan javascript	
