FROM docker:19-git

RUN apk update && \
    apk add bash curl go make musl-dev npm protobuf && \
    apk upgrade

ENV USE_PROVIDED_PROTOC=true

