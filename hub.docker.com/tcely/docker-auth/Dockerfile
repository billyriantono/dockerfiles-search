ARG DOCKER_AUTH_TAG=master

FROM golang:1-alpine AS builder

ARG DOCKER_AUTH_TAG

RUN apk --update upgrade && \
    apk add ca-certificates git make py2-pip && \
    rm -rf /var/cache/apk/*

RUN pip install GitPython

RUN git clone -b "$DOCKER_AUTH_TAG" 'https://github.com/cesanta/docker_auth.git' "$GOPATH/src/github.com/cesanta/docker_auth"

WORKDIR /go/src/github.com/cesanta/docker_auth/auth_server/
RUN make deps generate build

FROM alpine:edge

EXPOSE 5001
ENTRYPOINT ["/docker_auth/auth_server"]
CMD ["-logtostderr", "/config/auth_config.yml"]

RUN apk --update upgrade && \
    apk add ca-certificates && \
    rm -rf /var/cache/apk/*

COPY --from=builder /go/src/github.com/cesanta/docker_auth/auth_server/auth_server /docker_auth/auth_server

