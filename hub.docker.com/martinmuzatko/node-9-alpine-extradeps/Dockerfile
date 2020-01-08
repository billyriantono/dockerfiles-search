FROM node:9-alpine

RUN apk update && \
    apk upgrade && \
    apk add libstdc++ linux-headers make python && \
    apk update && \
    npm install npm@latest -g

RUN apk add --no-cache \
        binutils-gold \
        curl \
        g++ \
        gcc \
        gnupg \
        libgcc \
        sqlite \
        openssl

RUN npm i node-sass -g
