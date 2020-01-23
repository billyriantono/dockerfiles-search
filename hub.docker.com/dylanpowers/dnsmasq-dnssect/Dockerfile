FROM centos:latest
MAINTAINER robert.cuadra@dws.la

## Add repos
RUN wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN curl -O http://rpms.famillecollet.com/RPM-GPG-KEY-remi; rpm --import RPM-GPG-KEY-remi
RUN rpm -Uvh remi-release-6*.rpm epel-release-6*.rpm

## Install php. Requires httpd so that gets installed too.
RUN yum -y --enablerepo=epel,remi install php

RUN service httpd stop

# allow .htaccess overrides. needed for rewrites.
RUN sed -i 's/AllowOverride None/AllowOverride All/' /etc/httpd/conf/httpd.conf

# docroot
RUN mkdir -p /srv/www
RUN sed -i 's#DocumentRoot "/var/www/html"#DocumentRoot "/srv/www"#' /etc/httpd/conf/httpd.conf

# turn up!
RUN sed -i 's/error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT/error_reporting = E_ALL/' /etc/php.ini

# its dev, you want to see the horrible errors you've caused dont you?
RUN sed -i 's/display_errors = Off/display_errors = On/' /etc/php.ini

# so php doeasnt complain...
RUN sed -i 's/;date.timezone =/date.timezone = America\/Los_Angeles/' /etc/php.ini

EXPOSE 80
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]