FROM ruby:2.3.3-alpine

MAINTAINER Myros <myros.net@gmail.com>

ARG APP_LOCAL_PATH
ARG buildno

ENV PACKAGES \
	build-base \
	mysql-dev \
	libcurl \
	libxml2-dev \
	libxslt-dev \
	libffi-dev \
	libmcrypt-dev \
	openssl


RUN apk update && apk add $PACKAGES
RUN rm -rf /var/cache/apk/*

RUN apk add

RUN echo $APP_LOCAL_PATH

# vars
ENV CONTAINER_APP_FOLDER /app
ENV BUNDLE_PATH /bundle

# Run `bundle install` BEFORE adding the Rails application directory structure
# to /app on the container's filesystem.
RUN mkdir $CONTAINER_APP_FOLDER



# Add the Rails application directory structure to $CONTAINER_APP_FOLDER on the container's filesystem
ADD ./Gemfile $CONTAINER_APP_FOLDER/Gemfile
# ADD ./Gemfile.lock $CONTAINER_APP_FOLDER/Gemfile.lock

WORKDIR $CONTAINER_APP_FOLDER

RUN gem install bundler

RUN bundle install --jobs 20 --retry 5

# Make directories we need
RUN mkdir -p /tmp/videos
RUN mkdir -p /tmp/dnload
RUN mkdir -p /tmp/test

# Overridable startup commands
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

# The main command to run when the container starts. Also
# tell the Rails dev server to bind to all interfaces by
# default.
# CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
