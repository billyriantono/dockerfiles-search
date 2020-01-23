##
# A simple docker image to allow bootstrapping of Rails applications.
# Usage: 
#     docker run --rm -v <path-to-output-directory>:/app freeatnet/alpine-rails-bootstrap:latest rails new <app-name> --database=postgresql
# 
# Unlicensed 2018, Arseniy Ivanov <arseniy@freeatnet.com>
# 
# Other credits:
# Package list reused from @pacuna, cf. https://github.com/pacuna/rails5-docker-alpine.

FROM ruby:2.7.0-alpine
LABEL maintainer="hello+alpine-rails@freeatnet.com"

ENV RAILS_VERSION '~> 6.0.0'
ENV WORKDIR /app

# Minimal requirements to run a Rails app
RUN apk add --no-cache --update build-base \
                                linux-headers \
                                git \
                                postgresql-dev \
                                nodejs \
                                tzdata \
                                yarn

# All this to just to keep bundler from complaining about root user installs.
RUN addgroup -S app && adduser -S -G app app
RUN mkdir -p $WORKDIR && chown -R app:app $WORKDIR
USER app
WORKDIR $WORKDIR

RUN gem install --version "$RAILS_VERSION" rails

CMD rails new
