FROM composer/composer:1.1-alpine
MAINTAINER Antonio Canas <antonio.canas.poblete@gmail.com>

ENV \
  PACKAGES=' \
    # For git hosted Composer packages
    openssh-client \
  '

RUN \
  apk add --update --no-cache $PACKAGES && \
  composer global require franzl/studio && \
  composer clear-cache
