FROM bazaglia/nginx-php

RUN apk add --update nodejs && \
    curl -sS https://getcomposer.org/installer --insecure | php && \
    mv composer.phar /usr/bin/composer && \
    composer global require "fxp/composer-asset-plugin:~1.3" && \
    rm -rf /var/cache/apk/*
ENV PATH /root/.composer/vendor/bin:$PATH
RUN npm install -g bower
