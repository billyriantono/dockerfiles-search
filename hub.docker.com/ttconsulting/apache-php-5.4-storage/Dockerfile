FROM centos:centos6

RUN useradd apache --uid 48 --home-dir /usr/share/httpd --shell /sbin/nologin --user-group --system --no-create-home

# Apache config dir
VOLUME /etc/httpd/conf

# PHP config dir
VOLUME /etc/php.d

# HTML document root
VOLUME /var/www

ENTRYPOINT exec chown -R apache:apache /var/www
