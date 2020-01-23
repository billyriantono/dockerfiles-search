FROM wordpress:php7.1-apache

RUN set -x \
    && apt-get update \
    && apt-get install -y libldap2-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && apt-get purge -y --auto-remove libldap2-dev
	
COPY /ldap-login-for-intranet-sites /var/www/html/wp-content/plugins/ldap-login-for-intranet-sites/
RUN mkdir /var/www/html/testing
COPY /testingDirectory /var/www/html/testing

RUN /bin/sh -c 'echo "<Directory /var/testing/>" >> /etc/apache2/apache2.conf'
RUN /bin/sh -c 'echo "Options Indexes FollowSymlinks" >> /etc/apache2/apache2.conf'
RUN /bin/sh -c 'echo "AllowOverride All" >> /etc/apache2/apache2.conf'
RUN /bin/sh -c 'echo "Require all granted" >> /etc/apache2/apache2.conf'
RUN /bin/sh -c 'echo "</Directory>" >> /etc/apache2/apache2.conf'
	