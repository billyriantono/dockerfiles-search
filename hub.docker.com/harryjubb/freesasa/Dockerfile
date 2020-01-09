FROM alpine:3.8

ADD https://github.com/mittinatten/freesasa/releases/download/2.0.3/freesasa-2.0.3.tar.gz .
RUN tar -xzf freesasa-2.0.3.tar.gz freesasa-2.0.3
WORKDIR freesasa-2.0.3

RUN apk add --no-cache \
  libxml2-dev \
  json-c-dev

RUN apk add --no-cache --virtual .build-dependencies \
  build-base \
  && ./configure && make && make install \
  && apk del .build-dependencies

WORKDIR ..
RUN rm ./freesasa-2.0.3.tar.gz && rm -rf ./freesasa-2.0.3
