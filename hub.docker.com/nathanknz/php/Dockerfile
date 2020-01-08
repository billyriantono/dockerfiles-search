FROM nathanknz/php:7-snmpd-alpine-ext

RUN apk add --no-cache \
        git \
        openssh-client \
        zip \
    && sed -i 's/^# Host \*$/Host \*/g' /etc/ssh/ssh_config \
    && echo "    StrictHostKeyChecking no" >> /etc/ssh/ssh_config \
    && echo "    SendEnv LANG LC_*" >> /etc/ssh/ssh_config \
    && echo "    HashKnownHosts yes" >> /etc/ssh/ssh_config \
    && echo "    UserKnownHostsFile=/dev/null" >> /etc/ssh/ssh_config \
    && php -r "readfile('https://getcomposer.org/composer.phar');" > /usr/bin/composer \
    && chmod 755 /usr/bin/composer
