FROM php:7.1.8-fpm-alpine

RUN docker-php-ext-install \
  pdo_mysql \
  bcmath

RUN apk add --update openssh && rm -rf /var/cache/apk/*

RUN sed -i s/www-data/root/g /usr/local/etc/php-fpm.d/www.conf

RUN mkdir /root/.ssh && chmod 700 /root/.ssh

RUN { \
  echo 'Host *'; \
  echo '  ForwardAgent yes'; \
  echo '  StrictHostKeyChecking no'; \
  echo '  UserKnownHostsFile /dev/null'; \
  echo '  IdentitiesOnly yes'; \
  echo '  LogLevel QUIET'; \
} | tee /root/.ssh/config

RUN chmod 600 /root/.ssh/config

CMD ["php-fpm", "--allow-to-run-as-root"]
