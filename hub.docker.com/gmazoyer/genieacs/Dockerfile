FROM node:8-alpine as builder

ARG GIT_TAG=v1.1.3

RUN apk update \
    && apk add build-base python git \
    && mkdir /usr/lib/genieacs
WORKDIR /usr/lib/genieacs
RUN git clone https://github.com/zaidka/genieacs.git . \
    && git checkout tags/$GIT_TAG \
    && npm install \
    && npm run compile \
    && npm run configure

# Final image, no need to compile stuff

FROM node:8-alpine

COPY --from=builder /usr/lib/genieacs /usr/lib/genieacs/

RUN ln -s /usr/lib/genieacs/bin/genieacs-cwmp /usr/bin/genieacs-cwmp \
    && ln -s /usr/lib/genieacs/bin/genieacs-fs /usr/bin/genieacs-fs \
    && ln -s /usr/lib/genieacs/bin/genieacs-nbi /usr/bin/genieacs-nbi
