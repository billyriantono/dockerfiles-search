# Ref: https://hub.docker.com/r/lambdalisue/neovim-themis/dockerfile

ARG TAG="v0.4.2"
FROM lambdalisue/neovim-ci:${TAG}

RUN apk add --no-cache --virtual build-deps git \
 && git clone --depth 1 --single-branch https://github.com/thinca/vim-themis /opt/vim-themis \
 && apk del build-deps

ENV THEMIS_HOME=/opt/vim-themis \
    THEMIS_VIM=/usr/local/bin/nvim \
    THEMIS_ARGS="-e -s --headless" \
    PATH=/opt/vim-themis/bin:$PATH

ENTRYPOINT ["themis"]
