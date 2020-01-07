# Inspired by https://github.com/melo/docker-perl-carton-base/blob/master/Dockerfile
FROM perl:slim
LABEL maintainer "Mike Stemle, Jr. <themanchicken@gmail.com>"

RUN apt-get update -y \
  && apt-get install -y build-essential \
  && cpanm local::lib \
  && cpanm Carton \
  && rm -rf "$HOME/.cpanm" \
  && /usr/sbin/useradd -m -d /app -s /bin/nologin -U app \
  && apt-get clean autoclean \
  && apt-get autoremove -y

ONBUILD WORKDIR /app
ONBUILD USER app
ONBUILD ENV APP_WORKDIR /app