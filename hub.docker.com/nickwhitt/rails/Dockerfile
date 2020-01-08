FROM ruby:alpine

RUN apk add --virtual build-deps build-base && \
    gem install rails && \
    apk del build-deps

WORKDIR /usr/src/app

CMD ["--help"]
ENTRYPOINT ["rails"]
