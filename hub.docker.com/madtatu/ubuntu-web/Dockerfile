FROM ubuntu:14.04.1

ENV DEBIAN_FRONTEND noninteractive

RUN locale-gen en_US.utf8

ENV LC_All en_US.utf8

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main restricted universe" > /etc/apt/sources.list ;\
    echo "deb http://security.ubuntu.com/ubuntu precise-security main restricted universe" >> /etc/apt/sources.list ;\
    echo "deb http://ppa.launchpad.net/ondrej/php5/ubuntu precise main" >> /etc/apt/sources.list ;\
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E5267A6C ;\
    apt-get update -q ;\
    apt-get upgrade -y -q ;\
    apt-get dist-upgrade -y -q

RUN apt-get install -y -q php5-mcrypt php5-curl php5-pgsql php5-memcached php-apc php5-imagick php5-gd php5-geoip apache2 libapache2-mod-php5 libapache2-mod-xsendfile gzip wget ;\
    a2enmod rewrite ;\
    a2enmod xsendfile ;\
    apt-get clean

ADD etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf

RUN sed -i -e 's/^post_max_size.*/post_max_size = 118M/' /etc/php5/apache2/php.ini ;\
    sed -i -e 's/^upload_max_filesize.*/upload_max_filesize = 110M/' /etc/php5/apache2/php.ini ;\
    echo "pgsql.auto_reset_persistent" = On >> /etc/php5/apache2/php.ini

# Update PHP timezone
RUN sed -i -e 's/^;\(date\.timezone\s*=\s*\).*$/\1 Europe\/Budapest/' /etc/php5/apache2/php.ini

RUN apt-get install -y -q nodejs

RUN chmod 0777 /var/lib/php5

ENV DEBIAN_FRONTEND dialog

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_RUN_DIR /var/run
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]
