FROM alpine:3.10
MAINTAINER Stuart McCulloch Anderson @stuartma

ENV REFRESHED_AT 2018-07-14

RUN apk upgrade --update \
 && apk add build-base git libatomic libffi-dev libxml2 libxml2-dev \
    libxslt libxslt-dev ncurses-terminfo ncurses-terminfo-base \
    nodejs openssh-client readline readline-dev rsync ruby \
    ruby-bigdecimal ruby-dev ruby-io-console ruby-irb ruby-json \
    ruby-rake ruby-rdoc yaml yaml-dev zlib zlib-dev

RUN gem --version
RUN gem install bundler
RUN bundle --version

CMD ["/bin/sh"]
