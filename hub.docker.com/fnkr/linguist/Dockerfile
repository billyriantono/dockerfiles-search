FROM ruby:alpine

RUN apk --update add --virtual build_deps build-base libc-dev cmake linux-headers \
    && apk add icu-dev \
    && gem install github-linguist \
    && apk del build_deps && rm -rf /var/cache/apk/*

CMD ["linguist"]
