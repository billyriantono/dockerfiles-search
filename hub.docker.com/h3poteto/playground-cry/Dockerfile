FROM golang:1.10-alpine3.8

ENV APP ${GOPATH}/src/github.com/h3poteto/playground-cry

COPY . ${APP}

WORKDIR ${APP}

RUN set -ex && \
    go build

CMD ./playground-cry
