FROM node:10.16-alpine

WORKDIR /usr/src/app

COPY . /usr/src/app

RUN apk add git && \
    npm install && \ 
    npm install -g bower && \
    bower install --allow-root

EXPOSE 8080

CMD ["node", "app.js"]