FROM ruby:2.3.1-alpine

VOLUME ["/data"]
WORKDIR /data

RUN apk add --no-cache \
  build-base \
  && rm -rf /var/cache/apk/* \
  && gem install jekyll

EXPOSE 4000

ENTRYPOINT jekyll
CMD help
