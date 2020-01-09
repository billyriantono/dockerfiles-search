FROM abiosoft/caddy:php

RUN apk update
# Upgrade system to make sure new package version matching
RUN apk upgrade

# Install some needed packages
RUN apk add --update --no-cache php7-pdo_pgsql \
        php7-ldap
