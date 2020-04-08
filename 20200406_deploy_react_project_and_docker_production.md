# Deploy React Project

## Intro

Deploy project adalah istilah untuk membuild project yang bertujuan untuk mempublish project kita ke web server dan dalam keadaan terkompres(teringkas).

## Pembahasan

Langkah-langkah :

1. buat atribut basename di file App.js pada tag Router tambahkan attribute basename dengan value absolute-path nama project, sebagai berikut :

   ```html
   <Router basename"/web-client"></Router>
   ```

2. tambahkan homepage di file package.json dengan nama project(disarankan)

```json
{
  "bla...": "bla...",
  "homepage": "web-client",
  "bla...": "bla..."
}
```

3. build project dengan command "npm run build" pada directori project

4. di dalam folder build buat file .htaccess dengan isi

```
   " Options -MultiViews
   RewriteEngine On
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^ index.html [QSA,L] "
   tampa kutip
```

5. copy folder build nya ke apache(web server)

   - /var/www/html (linux - apche2)

6. akses localhost atau port umumnya yak nih 172.0.0.1

Referensi atau pelajari lebih lanjut :

- https://create-react-app.dev/docs/deployment/

# React Docker Production

## Pembahasan

Langkah-langkah :

1. Tambahkan file dengan nama "Dockerfile" pada folder project, dengan isi :

```
# base image
FROM node:12.2.0-alpine

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /app/package.json
RUN npm install --silent
RUN npm install react-scripts@3.0.1 -g --silent

# start app
CMD ["npm", "start"]
```

2. Tambahkan file ".dockerignore" pada folder project, dengan isi file atau folder yang tidak akan di publish ke docker :

```
node_modules
```

3. kemudian build docker dengan perintah

   Note : ganti sample:dev dengan nama project(disarankan)

```
$ docker build -t sample:dev .
```

4. Run docker dengan command

```
$ docker run -v ${PWD}:/app -v /app/node_modules -p 3001:3000 --rm sample:dev
```

Referensi atau pelajari lebih lanjut:

- https://mherman.org/blog/dockerizing-a-react-app/ (langkah-langkah inisialisasi docker)
- https://hub.docker.com/_/node/ (versi docker node)
- https://nodejs.org/fr/docs/guides/nodejs-docker-webapp/ (inisialisasi docker node)
- https://medium.com/@shakyShane/lets-talk-about-docker-artifacts-27454560384f
