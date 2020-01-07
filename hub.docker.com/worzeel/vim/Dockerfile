FROM worzeel/tmux:base

RUN apk update \
    && apk upgrade \
    && apk add vim \
    && rm -rf /var/cache/apk/*

COPY base/.vim /root/.vim
COPY base/.vimrc /root/.vimrc
