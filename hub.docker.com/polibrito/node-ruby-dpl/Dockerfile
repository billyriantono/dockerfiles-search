FROM mhart/alpine-node:8.11.3

RUN apk add --no-cache make gcc g++ python linux-headers libc6-compat bind-tools imagemagick ruby ruby-dev ruby-io-console \
    && echo 'gem: --no-document' > /etc/gemrc \
    && rm -rf /var/lib/apt/lists/*

RUN gem install dpl
