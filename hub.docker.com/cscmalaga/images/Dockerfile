FROM drupal:8.2-apache
MAINTAINER Juan M. Sosso <jsossoprieto@csc.com>

RUN apt-get update && apt-get install --no-install-recommends -y \
    cron \
    ssmtp \
    mysql-client \
    libxml2-dev \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/www/html

RUN { \
    echo '@reboot root     chmod a+w /var/www/private /var/www/web/files'; \
    echo '@hourly www-data /var/www/vendor/bin/drush -r /var/www/web cron -q'; \
  } | tee --append "/etc/crontab" \
  && sed 's/exec apache2/cron\napache2/' /usr/local/bin/apache2-foreground -i

RUN docker-php-ext-install soap

COPY 000-default.conf /etc/apache2/sites-enabled/

ENV PATH /var/www/scripts/container:/var/www/vendor/bin:$PATH
ENV HOME /home/user

WORKDIR /var/www/web
