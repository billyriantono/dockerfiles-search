FROM centos:7

RUN yum update -y && yum install -y epel-release
RUN yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum-config-manager --enable remi-php70
RUN yum install -y php-fpm php-php-gettext php-mysqlnd php-pdo php-mbstring php-gd php-xml php-process php-mcrypt php-cli

ADD php-fpm.conf /etc/php-fpm.conf

EXPOSE 9000

CMD [ "php-fpm" ]
