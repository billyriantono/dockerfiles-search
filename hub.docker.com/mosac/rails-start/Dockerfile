FROM library/ruby:2.6.3-alpine3.9
LABEL maintainer="Mosac https://github.com/Mosac"

WORKDIR /app
ADD rails/Gemfile-2.6.3 /app/Gemfile

RUN apk update && \
    apk upgrade && \
    apk add --update --no-cache --virtual=.build-dependencies \
      build-base \
      curl-dev \
      linux-headers \
      libxml2-dev \
      libxslt-dev \
      postgresql-dev \
      mysql-dev \
      sqlite-dev \
      ruby-dev \
      yaml-dev \
      zlib-dev && \
    apk add --update --no-cache \
      bash \
      curl \
      pcre \
      nodejs \
      libstdc++ \
      libxml2-dev \
      libxslt-dev \
      mysql-client \
      sqlite-libs \
      ruby-json \
      tzdata \
      yaml && \
    apk add --update --no-cache \
      bash \
      git \
      openssh \
      postgresql \
      ruby-json \
      tzdata \
      yaml && \
    mkdir /vendor && \
    bundle install -j4 --path /vendor && \
    apk del .build-dependencies && \
    rm /app/Gemfile /app/Gemfile.lock

ENTRYPOINT [ "/bin/bash" ]
