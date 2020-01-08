FROM ruby:2.5.3-alpine

# node installations command expect to run as root
USER root

RUN apk add --no-cache bash \
 		git \
 		openssh \
 		ruby \
 		ruby-nokogiri \
 		curl \
 		tzdata \
 		xz-libs \
 		libc6-compat \
 		openssl

# aws-cli
RUN apk -v --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        && \
    pip install --upgrade pip awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*
# end aws-cli

RUN mkdir -p /usr/src/rails
WORKDIR /usr/src/rails

COPY Gemfile /usr/src/rails/
COPY Gemfile.lock /usr/src/rails/

# nokogiri
RUN apk add --update \
  build-base \
  libxml2-dev \
  libxslt-dev \
  postgresql-dev \
  && rm -rf /var/cache/apk/* && bundle config build.nokogiri --use-system-libraries

# end nokogiri

RUN bundle config --global frozen 1 && bundle install
RUN mkdir -p /usr/src/app && ln -s /lib/libcrypto.so.1.0.0 /lib/libcrypto.so.1.1 && ln -s /lib/libssl.so.1.0.0 /lib/libssl.so.1.1

EXPOSE 3000
