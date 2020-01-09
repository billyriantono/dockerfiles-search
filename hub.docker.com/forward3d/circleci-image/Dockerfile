FROM ruby:2.6.3-alpine3.10

RUN apk add --update --no-cache git openssh-client tar gzip ca-certificates \
    build-base bash curl aspell musl-dev

RUN gem install bundler -v 2.0.2

RUN addgroup --gid 3434 circleci && \
    adduser -u 3434 -G circleci -s /bin/bash -D circleci

USER circleci

CMD ["/bin/sh"]
