FROM alpine:latest

RUN apk add ruby-bundler ruby-dev ansible build-base
RUN adduser -S ci_user

USER ci_user
WORKDIR /home/ci_user

RUN bundle config path vendor/bundle

CMD sh