FROM node:8-alpine

RUN apk add git jq
RUN apk add --no-cache --virtual .build-deps-git-crypt openssl-dev openssl nghttp2-libs libssh2 libcurl expat pcre2 ca-certificates

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-git-crypt/master/sgerrand.rsa.pub &&\
    wget https://github.com/sgerrand/alpine-pkg-git-crypt/releases/download/0.6.0-r0/git-crypt-0.6.0-r0.apk &&\
    echo "cd6945f08b2b263da24883c59e006ead1a4dd8c4ed2f2bf8edc0e3f1108a02d6  git-crypt-0.6.0-r0.apk" | sha256sum -c - &&\
    apk add git-crypt-0.6.0-r0.apk &&\
    apk del .build-deps-git-crypt

RUN npm i -g npm lerna typescript
