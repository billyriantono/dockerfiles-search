FROM ubuntu:18.04

LABEL maintainer="Rodrigo Stadler <rstadler@smthdiff.com>"

RUN apt update && apt full-upgrade -y && apt install -y \
    apache2; \
    apt-get autoremove \
    && apt-get autoclean; \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mv /etc/apache2/ports.conf /etc/apache2/ports.conf.default \
    && echo "Listen 7080\n\
    <IfModule ssl_module>\n\
        Listen 7081\n\
    </IfModule>\n\
    <IfModule mod_gnutls.c>\n\
        Listen 7081\n\
    </IfModule>" > /etc/apache2/ports.conf \
    && echo "<VirtualHost *:7080>\n\
        ServerAdmin webmaster@localhost\n\
        DocumentRoot /var/www/html/public\n\
        <Directory /var/www/html/public>\n\
            <Files ~ (\.php$)>\n\
                SetHandler "proxy:fcgi://php:9000"\n\
            </Files>\n\
            Options -Includes -ExecCGI\n\
        </Directory>\n\
        <Directory /var/www>\n\
            AllowOverride AuthConfig FileInfo Indexes Limit Options=Indexes,SymLinksIfOwnerMatch,MultiViews,FollowSymLinks,ExecCGI,Includes,IncludesNOEXEC\n\
        </Directory>\n\
        ErrorLog ${APACHE_LOG_DIR}/error.log\n\
        CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
    </VirtualHost>" > /etc/apache2/sites-available/001-default.conf \
    && a2dissite 000-default && a2ensite 001-default && a2enmod rewrite proxy proxy_fcgi && service apache2 restart

COPY apache2-foreground /usr/local/bin/
WORKDIR /var/www/html/

EXPOSE 7080
CMD ["/usr/local/bin/apache2-foreground"]
