FROM    debian
MAINTAINER Wellington Silva <wsilva@usp.br>

# Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# installing wget and creating /src path
RUN apt-get update && apt-get install -y wget && mkdir /src

# add dotdeb source list
RUN echo "deb http://packages.dotdeb.org wheezy all" > /etc/apt/sources.list.d/dotdeb.list \
    && echo "deb-src http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list.d/dotdeb.list \
    && wget -O - http://www.dotdeb.org/dotdeb.gpg |apt-key add -

# installing php stuff
RUN apt-get update && apt-get install -y php5-cli php5-fpm php5-mysql php5-intl php5-xdebug php5-recode \
    php5-snmp php5-mcrypt php5-memcache php5-memcached php5-imagick php5-curl php5-xsl php5-snmp \
    php5-dev php5-tidy php5-xmlrpc php5-gd php5-pspell php-pear php-apc nginx

# setting up php.ini, fpm pool conf and nginx.conf
RUN sed -i "s/;date.timezone =/date.timezone = America\/Sao_Paulo/" /etc/php5/cli/php.ini \
    && sed -i "s/;date.timezone =/date.timezone = America\/Sao_Paulo/" /etc/php5/fpm/php.ini \
    && sed -i "s/short_open_tag = On/short_open_tag = Off/" /etc/php5/cli/php.ini \
    && sed -i "s/short_open_tag = On/short_open_tag = Off/" /etc/php5/fpm/php.ini \
    && sed -i "s/error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT/error_reporting = E_ALL/" /etc/php5/cli/php.ini \
    && sed -i "s/error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT/error_reporting = E_ALL/" /etc/php5/fpm/php.ini \
    && sed -i "s/display_errors = Off/display_errors = On/" /etc/php5/cli/php.ini \
    && sed -i "s/display_errors = Off/display_errors = On/" /etc/php5/fpm/php.ini \
    && sed -i "s/display_startup_errors = Off/display_startup_errors = On/" /etc/php5/cli/php.ini \
    && sed -i "s/display_startup_errors = Off/display_startup_errors = On/" /etc/php5/fpm/php.ini \
    && sed -i "s/www-data;/www-data;\\ndaemon off;/g" /etc/nginx/nginx.conf

COPY run.sh /run.sh
RUN chmod a+x /run.sh

# virtualhosts configuration
COPY teste.dev.conf /etc/nginx/sites-available/teste.dev.conf

RUN ln -sf /etc/nginx/sites-available/teste.dev.conf /etc/nginx/sites-enabled/teste.dev.conf

# removing deb files
RUN apt-get clean

EXPOSE 80:80

ENTRYPOINT ["/run.sh"]
