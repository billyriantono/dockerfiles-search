FROM php:5.6-apache

MAINTAINER Simon Dubois <simon@dubandubois.com>

RUN sed -i 's!/var/www/html!/var/www/html/public!g' /etc/apache2/sites-enabled/000-default.conf

RUN a2enmod rewrite

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs build-essential

RUN apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    && echo "sv_SE.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen \
    && /usr/sbin/update-locale LANG=en_US.UTF-8

RUN apt-get install -y bash-completion

RUN apt-get install -y nano

RUN apt-get install -y git

RUN apt-get install -y mysql-client \
    && docker-php-ext-install pdo pdo_mysql

RUN apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip

RUN apt-get install -y libxml2-dev \
    && docker-php-ext-install soap

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.var_display_max_depth = 5" >> /usr/local/etc/php/php.ini \
    && echo "xdebug.max_nesting_level = 500" >> /usr/local/etc/php/php.ini

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && php /tmp/composer-setup.php -- --install-dir=/usr/local/bin --filename=composer \
    && rm /tmp/composer-setup.php

RUN pear install PHP_CodeSniffer

RUN echo "log_errors = On" >> /usr/local/etc/php/php.ini \
    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/php.ini \
    && echo "error_log = /dev/stderr" >> /usr/local/etc/php/php.ini \
    && echo "upload_max_filesize = 16M" >> /usr/local/etc/php/php.ini \
    && echo "post_max_size = 16M" >> /usr/local/etc/php/php.ini

ADD https://raw.githubusercontent.com/jamesob/desk/master/desk /usr/local/bin/desk
RUN chmod a+rx /usr/local/bin/desk

ADD https://raw.githubusercontent.com/jamesob/desk/master/shell_plugins/bash/desk /usr/share/bash-completion/completions/desk
RUN chmod a+r /usr/share/bash-completion/completions/desk

RUN groupadd -r -g 1000 docker \
    && useradd -r -u 1000 -g 1000 -d /home/docker -s /bin/bash docker \
    && mkdir /home/docker \
    && chmod 755 /home/docker \
    && chown 1000:1000 /home/docker

ADD https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh /home/docker/.bash_gitprompt
RUN chmod a+r /home/docker/.bash_gitprompt

ENV APACHE_RUN_USER docker
ENV APACHE_RUN_GROUP docker
