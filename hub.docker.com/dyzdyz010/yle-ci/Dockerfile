FROM python:3.7.1-stretch

LABEL maintainer="dyzdyz010@gmail.com"

RUN apt-get update && apt-get install -y emacs; wget -qO- https://get.haskellstack.org/ | sh

WORKDIR /root
