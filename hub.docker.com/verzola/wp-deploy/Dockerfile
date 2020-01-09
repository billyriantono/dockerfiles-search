FROM alpine:3
RUN apk add openssh \
  wget \
  curl \
  git \
  php7 \
  php7-curl \
  php7-openssl \
  php7-json \
  php7-mbstring \
  php7-phar \
  nodejs \
  --no-cache
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer 
