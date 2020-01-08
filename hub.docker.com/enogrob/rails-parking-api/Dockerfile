FROM ruby:2.5.0
MAINTAINER Roberto Nogueira <enogrob@gmail.com>

# Install platform requirements for rails
RUN apt-get update -yqq
RUN apt-get install -yqq --no-install-recommends nodejs

# Install gem files for Development flow
COPY Gemfile* /usr/src/app/
WORKDIR /usr/src/app

COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["./docker-entrypoint.sh"]

ENV BUNDLE_PATH=/bundle \
    BUNDLE_BIN=/bundle/bin \
    GEM_HOME=/bundle
ENV PATH="${BUNDLE_BIN}:${PATH}"

RUN bundle install
