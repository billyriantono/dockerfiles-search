FROM alpine:3.3
MAINTAINER John Downey <jdowney@gmail.com>

ENV RAILS_VERSION 4.2.5.1

RUN apk --update --upgrade add \
     build-base \
     libxml2-dev \
     libxslt-dev \
     nodejs \
     openssl-dev \
     ruby \
     ruby-bigdecimal \
     ruby-dev \
     ruby-io-console \
     ruby-irb \
     sqlite-dev \
     tzdata \
     yaml-dev \
  && gem install --no-document bundler \
  && gem install --no-document nokogiri -- --use-system-libraries \
  && gem install --no-document --version $RAILS_VERSION rails \
  && echo "gem: --no-document" >> /etc/gemrc \
  && chmod uog+r /etc/gemrc \
  && bundle config --global build.nokogiri  "--use-system-libraries" \
  && rm -rf /var/cache/apk/* \
  && rm -rf /usr/lib/lib/ruby/gems/*/cache/*

EXPOSE 3000
