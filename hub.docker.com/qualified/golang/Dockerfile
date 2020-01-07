FROM golang:1.12.7-buster

RUN set -ex; \
    useradd --create-home codewarrior; \
    mkdir /workspace; \
    chown codewarrior:codewarrior /workspace;

WORKDIR /workspace

USER codewarrior
COPY --chown=codewarrior:codewarrior rootfs/workspace /workspace
RUN set -ex; \
    go mod vendor; \
    go test -mod=vendor; \
    rm *.go;
