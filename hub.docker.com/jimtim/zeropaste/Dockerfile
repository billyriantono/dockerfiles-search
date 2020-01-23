FROM alpine:3.5
MAINTAINER nerdware <info@jimtim.de>
RUN apk add --update php5 \
      php5-dom \
      php5-json \
      php5-xml \
      php5-zlib \
      apache2 \
      apache2-utils \
      php5-apache2 \
      git \
      && rm -rf /var/cache/apk/* \
      && rm -rf /etc/apache2/conf.d/default.conf \
      && rm -rf /etc/apache2/conf.d/info.conf \
      && rm -rf /etc/apache2/conf.d/languages.conf \
      && rm -rf /etc/apache2/conf.d/mpm.conf \
      && rm -rf /etc/apache2/conf.d/userdir.conf \
      && echo "ServerSignature Off" >> "/etc/apache2/httpd.conf" \
      && echo "ServerTokens Prod" >> "/etc/apache2/httpd.conf" \
      && sed -i -e 's#Listen 80#Listen 8000#g' /etc/apache2/httpd.conf \
      && sed -i -e 's#ErrorLog "logs/error_log"#ErrorLog "|/bin/cat"#g' /etc/apache2/httpd.conf \
      && sed -i -e 's#CustomLog "logs/access_log" combined#CustomLog "|/bin/cat" combined#g' /etc/apache2/httpd.conf \
      && sed -i '/^#ServerName/cServerName localhost' /etc/apache2/httpd.conf \
      && mkdir -p /opt/session \
      && sed -i -e 's#;session.save_path = "/tmp"#session.save_path = "/opt/session"#g' /etc/php5/php.ini \
      && echo  "log_errors = On">>/etc/php5/php.ini \
      && echo "error_log = /dev/stderr">>/etc/php5/php.ini \
      && echo "zlib.output_compression = On">>/etc/php5/php.ini \
      && chmod -R 777 /opt/session \
      && rm -rf /var/www/localhost/htdocs/* \
      && mkdir -p /opt/zeropaste \
      && git clone https://JimTim89@bitbucket.org/nerdware/zeropaste.git /opt/zeropaste \
      && chown apache:apache -R /opt/zeropaste \
      && apk del git \
      && rm -rf /var/www/html/docker \
      && rm -rf /var/cache/apk/* \
      && mkdir -p /run/apache2
COPY zeropaste.conf /etc/apache2/conf.d/zeropaste.conf
WORKDIR /opt/zeropaste
EXPOSE 8000 443
CMD rm -rf /run/apache2/* || true && /usr/sbin/httpd -DFOREGROUND
