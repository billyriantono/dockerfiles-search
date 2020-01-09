FROM alpine:edge
LABEL maintainer="Takashi Makimoto <mackie@beehive-dev.com>"

WORKDIR /usr/src/nvim
COPY config /root/.config/nvim

ENV LANGUAGE="ja_JP:ja" \
    LANG="ja_JP:UTF-8" \
    LC_ALL="ja_JP:UTF-8"

RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk update && \
    apk upgrade && \
    apk add --no-cache \
      curl \
      gcc \
      git \
      linux-headers \
      musl-dev \
      neovim \
      nodejs \
      nodejs-npm \
      python3-dev \
      py3-ujson@testing \
      ripgrep@testing && \
    pip3 install --upgrade pip pynvim python-language-server[all] && \
    npm install -g \
      typescript \
      typescript-language-server \
      vscode-css-languageserver-bin \
      dockerfile-language-server-nodejs && \
    nvim +UpdateRemotePlugins +qa && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["nvim"]
