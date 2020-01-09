FROM ruby:2.4.4-alpine
MAINTAINER cdambrosio@gmail.com

RUN apk add --update build-base cmake git curl-dev openssl-dev

ENV PRONTO_ROOT /data
WORKDIR $PRONTO_ROOT

RUN gem install pronto:${PRONTO_VERSION:-0.9.5}
RUN gem install pronto-rubocop:${PRONTO_RUBOCOP_VERSION:-0.9.1}

RUN gem install rubocop:${RUBOCOP_VERSION:-0.63.0}

CMD [ "pronto", "run" ]
