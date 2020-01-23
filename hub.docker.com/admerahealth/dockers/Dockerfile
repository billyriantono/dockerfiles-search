FROM admerahealth/centos:6.8
MAINTAINER "Ryan Mank" ryan.mank@admerahealth.com
RUN yum -y update && yum -y install \
    httpd \
    mod_ssl \
    php \
    php-mysql
RUN yum clean all
COPY /login.php /var/www/html/
COPY /index.php /var/www/html/
COPY /httpd.conf /etc/httpd/conf/httpd.conf
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]
EXPOSE 80
