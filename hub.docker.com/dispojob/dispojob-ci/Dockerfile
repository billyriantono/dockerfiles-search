FROM dispojob/dispojob

ENV COMPOSER_ALLOW_SUPERUSER 1

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
 && apt-get install -y git jq nodejs openvpn
