FROM ubuntu:14.04

MAINTAINER Eric G. Miller <eric.miller@spirent.com>
# Based on tianon/apache2 https://registry.hub.docker.com/u/tianon/apache2/dockerfile
# Other references
##  Kimbro Staken (http://www.kstaken.com/blog/2013/07/06/how-to-run-apache-under-docker/). Used Docker 0.4.8
##  Glenn Y. Rolland (glenux/database, https://registry.hub.docker.com/u/glenux/database/). Supervisord from basebox

RUN apt-get update && apt-get install -y apache2

# Settings from /etc/init.d/apache2
ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_ENVVARS $APACHE_CONFDIR/envvars
# Settings from $APACHE_CONFDIR/envvars itself
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_PID_FILE $APACHE_RUN_DIR/apache2.pid
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C

# Make sure referenced directories exist
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

# Make CustomLog (access log) go to stdout instead of files
#  and ErrorLog to stderr
RUN find "$APACHE_CONFDIR" -type f -exec sed -ri ' \
    s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; \
    s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g; \
' '{}' ';'

EXPOSE 80
EXPOSE 443

CMD ["apache2", "-DFOREGROUND"]

