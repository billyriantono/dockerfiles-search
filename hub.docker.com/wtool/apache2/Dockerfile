from   wtool/php:latest

run apt-get update; \
	apt-get -y --force-yes upgrade; \
	apt-get -y --force-yes install apache2 apache2-mpm-event libapache2-mod-fastcgi; \
	apt-get autoclean;

add   ./apache-php5-fpm.conf /etc/apache2/conf-enabled/php5-fpm.conf
add   ./php-fpm.conf /opt/php/5.6/etc/php-fpm.conf
add   ./php-fpm.conf /opt/php/5.5/etc/php-fpm.conf
add   ./php-fpm.conf /opt/php/5.4/etc/php-fpm.conf
add   ./php-fpm.conf /opt/php/5.3/etc/php-fpm.conf
run    sed -i -e"s/pm = ondemand/pm = dynamic/" /opt/php/5.3/etc/php-fpm.conf; \
    sed -i -e "s/varPHP/5\.3/" /opt/php/5.3/etc/php-fpm.conf; \
    sed -i -e "s/varPHP/5\.4/" /opt/php/5.4/etc/php-fpm.conf; \
    sed -i -e "s/varPHP/5\.5/" /opt/php/5.5/etc/php-fpm.conf; \
    sed -i -e "s/varPHP/5\.6/" /opt/php/5.6/etc/php-fpm.conf; \
    chown www-data:www-data /srv -R; \
    a2enmod rewrite actions;

# let's copy a few of the settings from /etc/init.d/apache2
env    APACHE_CONFDIR /etc/apache2
env    APACHE_ENVVARS $APACHE_CONFDIR/envvars
env    APACHE_RUN_USER www-data
env    APACHE_RUN_GROUP www-data
env    APACHE_RUN_DIR /var/run/apache2
env    APACHE_PID_FILE $APACHE_RUN_DIR/apache2.pid
env    APACHE_LOCK_DIR /var/lock/apache2
env    APACHE_LOG_DIR /var/log/apache2
env    LANG C

run    mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

# make CustomLog (access log) go to stdout instead of files
#  and ErrorLog to stderr
run    find "$APACHE_CONFDIR" -type f -exec sed -ri ' \
	s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; \
	s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g; \
' '{}' ';'

add   ./php-start /opt/php-start 
add   ./Procfile /Procfile

expose 80
volume ["/srv"]

cmd ["forego", "start"]
