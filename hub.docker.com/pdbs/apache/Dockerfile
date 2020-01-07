FROM ubuntu:latest
LABEL build="201910111515"
LABEL maintainer "marc.jakob@bs.ch"

COPY dpkg-excludes /etc/dpkg/dpkg.cfg.d/excludes
COPY start.sh /

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get install locales && \
    locale-gen en_US.UTF-8 && \
    locale-gen de_CH.UTF-8 && \
    apt-get install apache2 libapache2-mod-php php php-pgsql php-mysql php-bz2 php-curl php-gd \
        php-imagick php-intl php-mbstring php-xml php-zip libphp-phpmailer php-ldap \
        libapache2-mod-auth-kerb libapache2-mod-security2 libapache2-mod-svn libapache2-mod-auth-openidc -y && \
    sed -i "s/Options Indexes FollowSymLinks/Options -Indexes/" /etc/apache2/apache2.conf && \
    sed -i "s/ServerSignature On/ServerSignature Off/"          /etc/apache2/conf-enabled/security.conf && \
    sed -i "s/ServerTokens OS/ServerTokens ProductOnly/"        /etc/apache2/conf-enabled/security.conf && \
    mv /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/ssl.conf && \
    /usr/sbin/a2enmod rewrite && \
    /usr/sbin/a2enmod ssl && \
    /usr/sbin/a2enmod security2 && \
    /usr/sbin/a2enmod headers && \
    /usr/sbin/a2enmod xml2enc && \
    /usr/sbin/a2enmod authnz_ldap && \
    /usr/sbin/a2enmod auth_openidc && \
    mv /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf && \
    rm -rf /var/lib/apt/lists/*
	
#ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8' TZ='Europe/Zurich'

COPY security2.conf /etc/apache2/mods-enabled/security2.conf

RUN tar -cf /apache.tar /var/www /etc/apache2 && \
    rm -rf /var/www /etc/apache2 && \
    chmod 0750 /start.sh

EXPOSE 80 443
VOLUME  ["/var/www", "/etc/apache2", "/var/log/apache2"]
ENTRYPOINT ["/start.sh"]
