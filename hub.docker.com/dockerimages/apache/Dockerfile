FROM dockerimages/ubuntu-core:14.04
MAINTAINER Frank Lemanschik @ B8G Datentechnik
RUN apt-get -y update && \
    apt-get -y -q --no-install-recommends install \
    apache2 && \
    apt-get -y clean

# let's copy a few of the settings from /etc/init.d/apache2
ENV VIRTUAL_DOMAIN examplle.com
ENV VIRTUAL_PORT 80
ENV DOCKER_RUN docker run -d -e VIRTUAL_DOMAIN=example.com -v /var/www/${1}:/var/www/html dockerimages/apache2
ENV DOCKER_BUILD docker build -t dockerimages/apache2 git://github.com/dockerimages/apache2
ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_ENVVARS $APACHE_CONFDIR/envvars
# and then a few more from $APACHE_CONFDIR/envvars itself
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_PID_FILE $APACHE_RUN_DIR/apache2.pid
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C

# ...
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

# make CustomLog (access log) go to stdout instead of files
#  and ErrorLog to stderr
RUN find "$APACHE_CONFDIR" -type f -exec sed -ri ' \
	s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; \
	s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g; \
' '{}' ';'

EXPOSE 80

CMD ["apache2", "-DFOREGROUND"]
