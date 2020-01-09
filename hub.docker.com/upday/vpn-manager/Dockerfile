FROM ruby:alpine
MAINTAINER developer@upday.com

ENV BUILD_HOME /vpn-manager/
VOLUME $BUILD_HOME
WORKDIR $BUILD_HOME

RUN apk add --no-cache openssl

COPY . $BUILD_HOME

RUN gem build vpn-manager.gemspec && \
    gem install vpn-manager

ENTRYPOINT ["vpn-manager"]
