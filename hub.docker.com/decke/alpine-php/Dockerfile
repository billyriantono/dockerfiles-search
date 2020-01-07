FROM php:alpine

LABEL maintainer="Bernhard Froehlich <decke@bluelife.at>"

RUN apk add --no-cache composer gnupg make sassc

# manually install phive since there is no alpine package yet
RUN apk add --no-cache wget \
    && wget https://phar.io/releases/phive.phar \
    && wget https://phar.io/releases/phive.phar.asc \
    && gpg --yes --keyserver pool.sks-keyservers.net --recv-keys 0x9D8A98B29B2D5D79 \
    && gpg --yes --verify phive.phar.asc phive.phar \
    && chmod +x phive.phar \
    && mv phive.phar /usr/local/bin/phive
