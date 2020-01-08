FROM node AS node

RUN mkdir abc
WORKDIR /abc

COPY package.json package.json
RUN npm install

COPY index.js index.js
COPY test.js test.js
RUN npm run build
RUN npm test


FROM nginx:alpine

LABEL maintainer="Miguel A. Pari Rojas"

WORKDIR /usr/share/nginx/html

COPY src/app.js src/app.js
COPY style/app.css style/app.css
COPY favicon.ico favicon.ico
COPY index.html index.html

COPY --from=node /abc/dist/* dist/
