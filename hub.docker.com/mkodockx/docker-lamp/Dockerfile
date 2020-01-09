FROM l3iggs/archlinux
MAINTAINER Markus Kosmal <code@m-ko-x.de>

## preparation
# update resources
RUN pacman -Sy

# dependencies
RUN mkdir /run/httpd
RUN ln -s /usr/bin/true /usr/bin/systemd-tmpfiles
RUN pacman -S --noconfirm --needed mariadb
RUN rm /usr/bin/systemd-tmpfiles
RUN pacman -S --noconfirm --needed apache php php-apache php-ldap php-gd php-intl php-mcrypt php-xcache exiv2 sqlite php-sqlite perl-dbd-mysql
# RUN yaourt -Syyua --noconfirm --needed mod_xsendfile
# handle no systemd and info
RUN mkdir -p /opt/php
ADD content/index.php /opt/php/

## configuration
# apache configuratopn
RUN sed -i '$a ServerName ${HOSTNAME}' /etc/httpd/conf/httpd.conf && \
    sed -i 's,LoadModule rewrite_module modules/mod_rewrite.so,LoadModule rewrite_module modules/mod_rewrite.so\nLoadModule php5_module modules/libphp5.so,g' /etc/httpd/conf/httpd.conf && \
    sed -i 's,LoadModule mpm_event_module modules/mod_mpm_event.so,LoadModule mpm_prefork_module modules/mod_mpm_prefork.so,g' /etc/httpd/conf/httpd.conf && \
    sed -i '$a Include conf/extra/php5_module.conf' /etc/httpd/conf/httpd.conf

# php extension activation
RUN sed -i 's,;extension=iconv.so,extension=iconv.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=xmlrpc.so,extension=xmlrpc.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=zip.so,extension=zip.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=bz2.so,extension=bz2.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=curl.so,extension=curl.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=ftp.so,extension=ftp.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=ldap.so,extension=ldap.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=gd.so,extension=gd.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=intl.so,extension=intl.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=mcrypt.so,extension=mcrypt.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=exif.so,extension=exif.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=sqlite3.so,extension=sqlite3.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=pdo_sqlite.so,extension=pdo_sqlite.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=pdo_mysql.so,extension=pdo_mysql.so,g' /etc/php/php.ini && \
    sed -i 's,;extension=mysql.so,extension=mysql.so,g' /etc/php/php.ini

# mariadb config with mysql ctrlr
RUN mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

## tuning
# php xcache
RUN sed -i 's,;extension=xcache.so,extension=xcache.so,g' /etc/php/conf.d/xcache.ini && \
    sed -i 's,xcache.size=64M,xcache.size=512M,g' /etc/php/conf.d/xcache.ini && \
    sed -i 's,xcache.var_size=64M,xcache.var_size=512M,g' /etc/php/conf.d/xcache.ini && \
    echo "xcache.admin.enable_auth = Off" >> /etc/php/conf.d/xcache.ini && \
    echo "xcache.stat = Off" >> /etc/php/conf.d/xcache.ini 

# mysql 
RUN sed -i 's,key_buffer_size = 16M,key_buffer_size = 512M,g' /etc/mysql/my.cnf && \
    sed -i 's,# Point the following paths to different dedicated disks,query_cache_type = 1\nquery_cache_limit = 64M\nquery_cache_size = 64M\ntable_cache = 512,g' /etc/mysql/my.cnf
    
# if changed to "show", index.php with php-infos will be in root
ENV LAMP_INFO "noshow"

# just 80
EXPOSE 80

# start script
ADD script/boot.sh /opt/boot.sh
RUN chmod a+rx /opt/boot.sh
CMD ["/opt/boot.sh"]