FROM alpine:3.10

ARG VERSION=1.15.0

LABEL alpine-version=3.10
LABEL libmongoc-version=$VERSION
LABEL maintainer="Emmanuel Hadoux <emmanuel.hadoux@gmail.com>"

RUN apk add --no-cache build-base cmake openssl-dev
ADD https://github.com/mongodb/mongo-c-driver/releases/download/$VERSION/mongo-c-driver-$VERSION.tar.gz /tmp/mongoc.tar.gz
WORKDIR /tmp
RUN tar xzf mongoc.tar.gz
WORKDIR /tmp/mongo-c-driver-$VERSION/build
RUN cmake -DCMAKE_CXX_STANDARD=17 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/tmp/deps -DCMAKE_INSTALL_LIBDIR=lib \
  -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DENABLE_STATIC=OFF -DENABLE_TESTS=OFF -DENABLE_EXAMPLES=OFF .. \
  && make \
  && make install
