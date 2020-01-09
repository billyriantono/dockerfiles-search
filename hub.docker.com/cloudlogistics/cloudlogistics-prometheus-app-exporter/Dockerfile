FROM ruby:2.5.1-alpine

ENV RELEASE_PATH /opt/cloudlogistics/current
ENV BUNDLE_GEMFILE /opt/cloudlogistics/current/Gemfile

RUN mkdir -p $RELEASE_PATH

EXPOSE 9394

ADD ./ $RELEASE_PATH

RUN apk --no-cache add \
    bash \
    vim \
    && cd ${RELEASE_PATH} \
    && gem install bundler --no-rdoc --no-ri \
    && bundle install --quiet \
    && rm -rf tmp/cache \
    && apk --no-cache del build-base

CMD bundle exec prometheus_exporter
