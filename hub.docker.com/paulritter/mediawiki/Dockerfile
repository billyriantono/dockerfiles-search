FROM mediawiki:1.33

# Hardening
RUN a2enmod headers \
    && sed -i "s/ServerSignature On/ServerSignature Off/" /etc/apache2/conf-available/security.conf \
    && sed -i "s/ServerTokens OS/ServerTokens Prod/" /etc/apache2/conf-available/security.conf \
    && sed -i "s/#Header set X/Header set X/" /etc/apache2/conf-available/security.conf \
    && sed -i "s/Options Indexes FollowSymLinks/Options -Indexes/" /etc/apache2/apache2.conf

# System Dependencies. No ssmtp in buster
RUN apt-get update && apt-get install -y \
		libapache2-mod-auth-mellon \
		liblasso3 \
		libxmlsec1 \
		libxmlsec1-openssl \
		libxslt1.1 \
	--no-install-recommends && rm -r /var/lib/apt/lists/*

RUN a2enmod auth_mellon \
	&& a2enmod ldap \
	&& a2enmod authnz_ldap

RUN echo "sendmail_path=sendmail -t" > /usr/local/etc/php/conf.d/php-sendmail.ini

RUN mkdir -p /etc/apache2/site-config \
    && mkdir -p /etc/apache2/saml

ADD config/mellon.conf /etc/apache2/site-config/mellon.conf
ADD config/ldap.conf /etc/apache2/site-config/ldap.conf
ADD config/htpasswd.conf /etc/apache2/site-config/htpasswd.conf
ADD config/000-default.conf /etc/apache2/sites-available/000-default.conf

ADD config/mellon_create_metadata.sh /opt/mellon_create_metadata.sh
ADD config/firstrun.sh /opt/firstrun.sh
RUN chmod +x /opt/mellon_create_metadata.sh \
    && chmod +x /opt/firstrun.sh

ADD extensions/MinervaNeue.tar.gz /var/www/html/skins/
ADD extensions/MobileFrontend.tar.gz /var/www/html/extensions/
ADD extensions/Kartographer.tar.gz /var/www/html/extensions/
ADD extensions/PluggableAuth.tar.gz /var/www/html/extensions/
ADD extensions/YouTube.tar.gz /var/www/html/extensions/
ADD extensions/Auth_remoteuser.tar.gz /var/www/html/extensions/
ADD extensions/JsonConfig.tar.gz /var/www/html/extensions/

WORKDIR /var/www/html

VOLUME /etc/apache2/site-config
VOLUME /etc/apache2/saml
VOLUME /etc/ssmtp
