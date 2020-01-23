FROM fedora
MAINTAINER 01e0e1 <gediminas.z@outlook.com>

RUN yum -y update && yum clean all
RUN yum -y install php-fpm php-cli php-common php-mysql php-pdo php-mcrypt php-gd php-soap php-curl php-json php-xml && yum clean all

ADD ./php.ini /etc/php.ini
ADD ./www.conf /etc/php-fpm.d/www.conf

RUN usermod -u 1000 nginx

EXPOSE 9000

CMD [ "/usr/sbin/php-fpm", "--nodaemonize" ]
