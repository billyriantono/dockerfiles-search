FROM ubuntu:14.04
MAINTAINER "Phillip Shipley" <phillip_shipley@sil.org>

ENV REFRESHED_AT 2015-06-08

# Install OS packages as well as commonly used NPM packages globally
RUN apt-get update -y \
    && apt-get install -y \
        curl \
        git \
        npm \
        ruby-dev \
    && gem install compass \
    && ln -s /usr/bin/nodejs /usr/bin/node \
    && npm install -g \
        bower \
        grunt-cli

CMD ["true"]