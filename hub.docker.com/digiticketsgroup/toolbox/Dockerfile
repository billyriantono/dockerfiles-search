FROM node:10.13.0-alpine as node

FROM digiticketsgroup/php-dev:7.2

MAINTAINER Warrick Hill <warrick.hill@digitickets.co.uk>

RUN apk add --update \
    bash \
    bash-completion \
    mysql-client \
    ncurses \
    openssh \
    && rm -f /var/cache/apk/*

# add compsoer
COPY ./composer-install.sh /composer-install.sh
RUN . /composer-install.sh

RUN composer global require hirak/prestissimo

# add node
COPY --from=node /usr/local/bin /usr/local/bin
COPY --from=node /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node /opt /opt

RUN npm install -g \
    grunt-cli \
    gulp-cli

WORKDIR /var/www/app

RUN chmod +x /usr/local/bin/entrypoint

CMD tail -f /dev/null
