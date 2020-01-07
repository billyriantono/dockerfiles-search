FROM ruby:alpine as builder

RUN apk add --no-cache --virtual \
      build-dependencies \
      build-base \
    && true

ARG TRAVIS_VERSION=1.8.11.travis.1001.9
RUN gem install travis -v $TRAVIS_VERSION

RUN rm -rf /usr/local/bundle/cache/*.gem \
 && find /usr/local/bundle/gems/ -name "*.c" -delete \
 && find /usr/local/bundle/gems/ -name "*.o" -delete

FROM ruby:alpine

LABEL io.whalebrew.name 'travis'
LABEL io.whalebrew.config.working_dir '/travis'

RUN apk --no-cache add git \
    && true

COPY --from=builder /usr/local/ /usr/local/

RUN adduser -S travis-cli
USER travis-cli
ENV HOME /home/travis-cli

WORKDIR /travis
ENTRYPOINT ["travis"]
CMD ["help"]
