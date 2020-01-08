FROM versantus/webserver-dev:latest

RUN apt update \
	&& apt install -y --no-install-recommends \
    ca-certificates \
    openssh-client \
    rsync \
    wget \
    gzip \
    tar \
    patch \
    perl \
    php-pear \
    libpcre3-dev \
    imagemagick \
    php-imagick \
    php7.3-bcmath \
    mysql-client\
    php-curl\
    sendmail \
    inetutils-ping \
    telnet \
    php-mongodb\
    php-ssh2\
    php-soap\
    php-memcached\
    memcached \
    && rm -r /var/lib/apt/lists/* \
    && ln -sf /usr/bin/php7.3 /usr/bin/php

# Turn on all error reporting
RUN echo 'error_reporting = E_ALL' >> /etc/php/7.3/apache2/php.ini
RUN echo 'display_errors = On' >> /etc/php/7.3/apache2/php.ini

# Increase memory / execution time
RUN echo 'max_execution_time = 120' >> /etc/php/7.3/apache2/php.ini
RUN echo 'max_input_time = 120' >> /etc/php/7.3/apache2/php.ini
RUN echo 'memory_limit = 256M' >> /etc/php/7.3/apache2/php.ini
RUN echo 'upload_max_filesize = 50M' >> /etc/php/7.3/apache2/php.ini
RUN echo 'post_max_size = 50M' >> /etc/php/7.3/apache2/php.ini



RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
#RUN cat go1.8.3.linux-amd64.tar.gz  | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php/7.3/cli/php.ini
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php/7.3/apache2/php.ini

# make the terminal prettier
COPY .bash_profile /root/.bash_profile
RUN cat /root/.bash_profile >>/root/.bashrc

# Pass the VERSANTUS_ENV env var from the host (developer's) machine to the container
ENV VERSANTUS_ENV=local

# Copy versantus global drush commands
RUN mkdir /var/www/drush
COPY drush/drushrc.php /var/www/drush/drushrc.php
RUN mkdir /var/www/drush/Commands
COPY drush/versantus_global_commands.drush.inc /var/www/drush/versantus_global_commands.drush.inc
COPY drush/Commands/versantus_global_commands_shared.inc /var/www/drush/Commands/versantus_global_commands_shared.inc
#COPY drush/Commands/versantus_globalCommands.php /var/www/drush/Commands/versantus_globalCommands.php


# Install nvm BEGIN

# replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# update the repository sources list
# and install dependencies
RUN apt-get update \
    && apt-get install -y curl \
    && apt-get -y autoclean

RUN curl --silent -o- /usr/local/nvm https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash

# install node and npm
RUN source /root/.nvm/nvm.sh \
    && nvm install --lts \
    && nvm alias default lts/* \
    && nvm use default

ENV SHELL=/bin/bash

# Install nvm END


# Install wkhtmltopdf patched binary and libxrender dependency
COPY bin/wkhtmltopdf /usr/bin/wkhtmltopdf
RUN apt update && apt install -y libxrender1

WORKDIR /var/www/html
RUN groupadd -g 1000 versantus && \
    useradd -r -u 1000 -g versantus versantus -d /var/www/html
COPY apache.conf /etc/apache2/sites-available/000-default.conf
COPY apache-envvars /etc/apache2/envvars
RUN ln -sf /dev/stdout /var/log/apache2/other_vhosts_access.log \
    && ln -sf /dev/stderr /var/log/apache2/default_error_log

RUN set -ex \
	&& buildDeps=' \
		libpng-dev \
		libpq-dev \
	' \
	&& apt update && apt install -y --no-install-recommends ca-certificates $buildDeps && rm -rf /var/lib/apt/lists/* \
	&& apt-mark manual \
		libpq5 \
	&& apt purge -y --auto-remove $buildDeps

WORKDIR /var/www/html
RUN chown -R versantus:versantus /var/www

# Install drush
RUN php7.3 -r "readfile('https://github.com/drush-ops/drush/releases/download/8.1.17/drush.phar');" > drush && chmod +x drush && mv drush /usr/bin/

# Install drupal console
RUN php7.3 -r "readfile('https://drupalconsole.com/installer');" > drupal.phar && chmod +x drupal.phar && mv drupal.phar /usr/local/bin/drupal

# Install WP-cli (for wordpress sites)
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && chmod +x wp-cli.phar && mv wp-cli.phar /usr/local/bin/wp

#USER versantus

# Install drupal-check
RUN curl -O -L https://github.com/mglaman/drupal-check/releases/latest/download/drupal-check.phar && mv drupal-check.phar /usr/local/bin/drupal-check && chmod +x /usr/local/bin/drupal-check

# Install PHP code sniffer
RUN curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar && curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar && mv phpcs.phar /usr/local/bin/phpcs && chmod +x /usr/local/bin/phpcs && mv phpcbf.phar /usr/local/bin/phpcbf && chmod +x /usr/local/bin/phpcbf

# Install PHPCompatibility extension for code sniffer
RUN curl -OL https://github.com/PHPCompatibility/PHPCompatibility/archive/9.3.4.tar.gz && tar -xvzf 9.3.4.tar.gz -C /opt && phpcs --config-set installed_paths /opt/PHPCompatibility-9.3.4

