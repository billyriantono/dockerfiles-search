FROM alpine:3.5

MAINTAINER Kobi Meirson <kobi@kidbox.com>

RUN apk add --update \
      ruby ruby-bigdecimal ruby-bundler \
      ca-certificates libressl \
      libressl-dev build-base ruby-dev libxml2-dev libxslt-dev; \
\
bundle config git.allow_insecure true; \
\
gem install bundler --no-rdoc --no-ri; \
gem install json -v '1.8.6' --no-rdoc --no-ri; \
gem install unf_ext -v '0.0.7.4' --no-rdoc --no-ri; \
gem install nokogiri -v '1.8.1' --no-rdoc --no-ri; \
gem cleanup; \
rm -rf /usr/lib/ruby/gems/*/cache/*; \
apk del libressl-dev build-base ruby-dev libxml2-dev libxslt-dev; \
rm -rf /var/cache/apk/* /tmp;

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ONBUILD ADD Gemfile* $APP_HOME/
ONBUILD RUN bundle install --system --without="development test"
ONBUILD ADD . $APP_HOME
