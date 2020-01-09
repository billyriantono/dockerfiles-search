FROM ruby:2.4.3-stretch

RUN curl -sL https://deb.nodesource.com/setup_9.x | bash - ; \
    apt-get install -y nodejs

ENV PROJECT_ROOT /usr/src/app
ENV BUNDLE_PATH $PROJECT_ROOT/vendor/bundle
ENV GEM_HOME $PROJECT_ROOT/vendor/bundle
ENV BUNDLE_JOBS 2
ENV RAILS_LOG_TO_STDOUT 1

WORKDIR $PROJECT_ROOT

COPY ./Gemfile $PROJECT_ROOT
COPY ./Gemfile.lock $PROJECT_ROOT

RUN gem install bundler ; \
    bundle install

COPY ./ $PROJECT_ROOT
