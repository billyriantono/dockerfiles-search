FROM debian:jessie

RUN apt update && apt install -y php5-fpm php5 libapache2-mod-php5 \
                                curl apache2 vim php5-tidy php5-imagick \
                                php5-gmp php5-mysql php5-curl dos2unix git gcc make \
                                ruby-dev rubygems mysql-client locales

RUN gem install bundle

RUN mkdir -p /var/www/project

RUN sed -i 's/^# *\(fr_FR.UTF-8\)/\1/' /etc/locale.gen && locale-gen
RUN sed -i 's/^# *\(en_GB.UTF-8\)/\1/' /etc/locale.gen && locale-gen
RUN sed -i 's/^# *\(de_DE.UTF-8\)/\1/' /etc/locale.gen && locale-gen
RUN sed -i 's/^# *\(es_ES.UTF-8\)/\1/' /etc/locale.gen && locale-gen

COPY pool.conf /etc/php5/fpm/pool.d/www.conf
COPY php-fpm.conf /etc/php5/fpm/php-fpm.conf

COPY php.ini /etc/php5/fpm/php.ini
COPY php.ini /etc/php5/cli/php.ini
COPY php.ini /etc/php5/apache2/php.ini

RUN a2enmod headers
RUN a2enmod rewrite

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer --install-dir=/usr/local/bin
RUN php -r "unlink('composer-setup.php');"


ENV APACHE_RUN_SERVER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# AUTHORIZE SSH HOSTdocker

RUN mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh && \
    ssh-keyscan github.com > /root/.ssh/known_hosts



COPY apache_config.conf /etc/apache2/sites-enabled/000-default.conf
COPY run.sh /bin/run.sh

RUN dos2unix /bin/run.sh /bin/run.sh

WORKDIR /var/www/project

CMD ["/bin/run.sh"]
