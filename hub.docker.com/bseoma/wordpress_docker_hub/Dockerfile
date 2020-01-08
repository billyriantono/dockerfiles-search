# Coger la imagen de Ubuntu
FROM ubuntu:16.04
MAINTAINER John Doe john@doe.es
RUN     apt update && \
        apt -y upgrade && \
        apt install -y apache2 libapache2-mod-php php-common php-gd php-mysql coreutils && \
        cd /var/www/ && \
        rm -f html/index.html && \
        rm -rf /var/lib/apt /var/lib/dpkg /var/cache/apt /usr/share/doc /usr/share/man /usr/share/info
# Porque esto no se descomprime...puta bida TT
ADD     https://wordpress.org/latest.tar.gz /var/www/
RUN     cd /var/www/ && \
        tar -zxvf latest.tar.gz -C /var/www/ && \
        rm -rf latest.tar.gz html && \
        mv wordpress html && \
        chown -R www-data:www-data html
EXPOSE 80
# Pereza infinita crear un entrypoint
#CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
ENTRYPOINT ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
