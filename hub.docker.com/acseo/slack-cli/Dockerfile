FROM alpine:3.3

RUN apk add --no-cache  wget openssl php-phar php-json php-ctype php-openssl

# Fix for weird SSL issue
# https://github.com/composer/composer/issues/3346#issuecomment-76593763
WORKDIR /
RUN wget --no-check-certificate http://curl.haxx.se/ca/cacert.pem
RUN mv cacert.pem /etc/ssl/cert.pem

RUN php -r "readfile('http://cleentfaar.github.io/slack-cli/installer');" | php

ENTRYPOINT ["php", "slack.phar"]
CMD []
