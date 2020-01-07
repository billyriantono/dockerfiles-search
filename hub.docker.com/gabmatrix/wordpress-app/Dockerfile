FROM cloudron/base:0.10.0
MAINTAINER Girish Ramakrishnan <girish@cloudron.io>

# this can be removed in next base image update
RUN apt-get update && \
    apt-get install -y php-mbstring php-zip crudini php-soap php-imap zip && \
    rm -rf /var/cache/apt /var/lib/apt/lists

RUN mkdir -p /app/code
WORKDIR /app/code
RUN curl -L http://wordpress.org/wordpress-4.9.6.tar.gz | tar -xz --strip-components 1 -f -
RUN rm readme.html wp-admin/install.php wp-config-sample.php
RUN mv /app/code/wp-content /app/code/wp-content-vanilla && ln -s /app/data/wp-content /app/code/wp-content
RUN ln -s /app/data/htaccess /app/code/.htaccess
ADD wp-config.php.template /app/code/wp-config.php.template

RUN ln -sf /run/wordpress/wp-config.php /app/code/wp-config.php

RUN curl -L -o /app/code/wp https://github.com/wp-cli/wp-cli/releases/download/v1.4.1/wp-cli-1.4.1.phar
RUN chmod +x /app/code/wp
RUN /bin/echo -e "apache_modules:\n  - mod_rewrite" > /app/code/wp-cli.yml

# Get the plugins
RUN curl -L -o /app/code/authLdap.zip https://github.com/heiglandreas/authLdap/archive/1.5.1.zip
# https://plugins.svn.wordpress.org/disable-wordpress-core-update/
RUN curl -L -o /app/code/disable-wordpress-core-update.zip https://downloads.wordpress.org/plugin/disable-wordpress-core-update.zip
# https://plugins.svn.wordpress.org/wp-mail-smtp/
RUN curl -L -o /app/code/wp-mail-smtp.zip https://downloads.wordpress.org/plugin/wp-mail-smtp.0.10.1.zip

RUN chown -R www-data:www-data /app/code

# configure apache
RUN rm /etc/apache2/sites-enabled/*
RUN sed -e 's,^ErrorLog.*,ErrorLog "|/bin/cat",' -i /etc/apache2/apache2.conf
COPY apache/mpm_prefork.conf /etc/apache2/mods-available/mpm_prefork.conf.template
RUN ln -sf /run/wordpress/mpm_prefork.conf /etc/apache2/mods-available/mpm_prefork.conf

RUN a2disconf other-vhosts-access-log
ADD apache/wordpress.conf /etc/apache2/sites-enabled/wordpress.conf
RUN echo "Listen 8000" > /etc/apache2/ports.conf

# configure mod_php. apache2ctl -M can be used to list enabled modules
RUN a2enmod rewrite && \
    a2enmod expires && \
    a2enmod headers && \
    a2enmod cache
RUN crudini --set /etc/php/7.0/apache2/php.ini PHP upload_max_filesize 500M && \
    crudini --set /etc/php/7.0/apache2/php.ini PHP post_max_size 500M && \
    crudini --set /etc/php/7.0/apache2/php.ini PHP max_input_vars 1800 && \
    crudini --set /etc/php/7.0/apache2/php.ini Session session.save_path /run/wordpress/sessions && \
    crudini --set /etc/php/7.0/apache2/php.ini Session session.gc_probability 1 && \
    crudini --set /etc/php/7.0/apache2/php.ini Session session.gc_divisor 100

RUN cp /etc/php/7.0/apache2/php.ini /etc/php/7.0/cli/php.ini

# Hack to stop sendmail/postfix to keep retrying sending emails because of rofs
RUN rm -rf /var/spool

ADD start.sh cron.sh /app/code/

CMD [ "/app/code/start.sh" ]
