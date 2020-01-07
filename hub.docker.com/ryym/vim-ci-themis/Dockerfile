# Ref: https://hub.docker.com/r/lambdalisue/vim-themis/dockerfile

ARG TAG="v8.1.2000"
FROM lambdalisue/vim-ci:${TAG}

RUN apk add --no-cache --virtual build-deps git \
 && git clone --depth 1 --single-branch https://github.com/thinca/vim-themis /opt/vim-themis \
 && apk del build-deps

ENV THEMIS_HOME=/opt/vim-themis \
    THEMIS_VIM=/usr/local/bin/vim \
    PATH=/opt/vim-themis/bin:$PATH

ENTRYPOINT ["themis"]
