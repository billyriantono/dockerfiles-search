FROM gliderlabs/alpine:3.3

RUN apk add --update \
      bash \
      vim \
      tmux \
      git \
      python \
      nodejs \
      build-base

ADD .tmux.conf /root
ADD .vimrc /root

VOLUME /project
WORKDIR /project


