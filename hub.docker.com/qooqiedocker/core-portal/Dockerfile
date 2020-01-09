# Build caddy
FROM abiosoft/caddy:builder as builder

ARG version="0.10.14"
ARG plugins="cors,realip,expires,cache,prometheus"

# process wrapper
RUN go get -v github.com/abiosoft/parent

RUN VERSION=${version} PLUGINS=${plugins} /bin/sh /usr/bin/builder.sh

# Build php-image
FROM php:7.1-fpm-alpine

# Add build dependencies to virtual group
RUN apk --no-cache --virtual temp add build-base \
                       autoconf && \
    apk --no-cache add zeromq-dev \
                       libxml2-dev \
                       composer \
                       sox \
                       git && \
    pecl install zmq-beta && \
    docker-php-ext-enable zmq && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install soap && \
    docker-php-ext-install pcntl && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install opcache && \
    apk del temp

ENV TZ=Europe/Amsterdam

RUN apk --update add \
    tzdata \
  && cp /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Fix iconv on alpinelinux
RUN apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/community gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

# Merge caddy build into container
COPY --from=builder /install/caddy /usr/bin/caddy

# Validate install
RUN /usr/bin/caddy -version
RUN /usr/bin/caddy -plugins

# Add caddy configuration
# ADD ./Caddyfile /etc/Caddyfile

# Copy caddy from parent image
COPY --from=builder /go/bin/parent /bin/parent

# Let's Encrypt Agreement
ENV ACME_AGREE="false"

# Telemetry Stats
ENV ENABLE_TELEMETRY="false"

EXPOSE 80
WORKDIR /srv

ENTRYPOINT ["/bin/parent", "caddy"]
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout", "--agree=$ACME_AGREE"]