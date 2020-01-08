FROM miko2u/web56
MAINTAINER miko@cafelounge.net

# packages
COPY setup/* /tmp/
RUN yum -y install --enablerepo=remi,remi-php56 openssh-server sudo patch tar php-pecl-ssh2 php-pecl-apcu \
 && yum -y --enablerepo=remi,remi-php56 clean all \
 && rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && sed -i 's/UsePAM yes/UsePAM no/' /etc/ssh/sshd_config \
 && mv /tmp/createdb.sql /boot

RUN cd /tmp \
 && curl -sOL https://ja.wordpress.org/wordpress-4.4.2-ja.tar.gz \
 && curl https://api.wordpress.org/secret-key/1.1/salt/ > /tmp/salt \
 && groupadd -g 500 staff \
 && useradd -u 500 -g 500 staff \
 && echo -e "staff\tALL=(ALL)\tNOPASSWD:ALL" > /etc/sudoers.d/staff \
 && mkdir -p /var/www/wordpress/public \
 && chown staff:staff /var/www/wordpress \
 && cd /usr/share/ \
 && tar zxf /tmp/wordpress-4.4.2-ja.tar.gz \
 && cd /usr/share/wordpress \
 && patch -p0 < /tmp/wordpress-4.1-utf8mb4.patch \
 && mv /tmp/wp-config-template.php /usr/share/wordpress \
 && touch /usr/share/wordpress/.gitignore \
 && chown -R staff:staff /usr/share/wordpress \
 && chkconfig nginx on \
 && chkconfig php-fpm on \
 && rm -rf /tmp/*

# extra modules
ADD optimizer-7.8.tar.gz /

# configure
COPY nginx/* /etc/nginx/conf.d/

# startup
COPY prepare /boot/

# bootstrap
EXPOSE 80
