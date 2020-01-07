FROM defektive/alpine-ruby-node:latest
RUN apk add --no-cache --virtual .build-deps \
       binutils-gold \
       curl \
       g++ \
       gcc \
       gnupg \
       libgcc \
       linux-headers \
       make \
       python \
       sqlite-dev \
    && gem install rails \
    && rails new --skip-turbolinks --skip-spring ./tmpapp \
    && rm -rf tmpapp
