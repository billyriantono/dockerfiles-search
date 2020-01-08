FROM ruby:2.6-alpine

LABEL maintainer="aleksey@kolyadin.ru"

RUN apk update                          && \
    apk upgrade                         && \
    apk add --no-cache rsync            && \
    rm -rf /tmp/* /var/cache/apk/*