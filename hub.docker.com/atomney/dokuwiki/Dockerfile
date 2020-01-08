FROM alpine:latest

ADD start-dokuwiki.sh /start-dokuwiki.sh

RUN apk update && \
    apk add bash wget tar lighttpd php5-common php5-iconv php5-json php5-gd php5-curl \
    php5-xml php5-pgsql php5-imap php5-cgi fcgi php5-pdo php5-pdo_pgsql php5-soap php5-xmlrpc \
    php5-posix php5-mcrypt php5-gettext php5-ldap php5-ctype php5-dom php5-openssl php5-zip php5-zlib ssmtp && \
    mkdir /data && \
    rm -r /var/www/localhost/htdocs && \
    chown -R lighttpd:www-data /data && \
    ln -s /data /var/www/localhost/htdocs && \
    mkdir /run/lighttpd && \
    chown -R lighttpd:lighttpd /run/lighttpd && \
    chmod +x /start-dokuwiki.sh && \
    sed -i 's/\#\ \  include\ "mod_fastcgi.conf"/include "mod_fastcgi.conf"/' /etc/lighttpd/lighttpd.conf

# Expose Port 80
EXPOSE 80

# Volume for keeping WiKi Data.
VOLUME ["/data"]

# Command executed on container start.
#CMD ["/usr/sbin/lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
ENTRYPOINT ["/start-dokuwiki.sh"]
