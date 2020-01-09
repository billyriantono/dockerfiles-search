#
# Gradle Dockerfile
#
# https://github.com/lukin0110/docker-slanger
#

# Pull base image
# https://hub.docker.com/_/ruby/
FROM ruby:2.3.0-alpine
MAINTAINER Maarten Huijsmans <maarten.huijsmans@gmail.com>

# API: 4567
# WebSocket: 8080
EXPOSE 4567 8080

# Inspiration: http://blog.codeship.com/build-minimal-docker-container-ruby-apps/
ENV BUILD_PACKAGES build-base

# Update and install all of the required packages.
# At the end, remove the apk cache
RUN apk update && \
    apk upgrade && \
    apk add $BUILD_PACKAGES && \
    rm -rf /var/cache/apk/*

# Install slanger
RUN gem install slanger

# Start the slanger server
CMD ["sh", "-c", "slanger --app_key ${PUSHER_APP_KEY} --secret ${PUSHER_APP_SECRET} -r redis://${REDIS_HOST}:${REDIS_PORT}/0"]
