FROM fedora
MAINTAINER 01e0e1 <gediminas.z@outlook.com>

RUN yum -y update && yum clean all
RUN yum -y install nginx && yum clean all

ADD ./nginx.conf /etc/nginx/nginx.conf
ADD ./symfony.conf /etc/nginx/conf.d/symfony.conf

RUN usermod -u 1000 nginx

EXPOSE 80

CMD [ "/usr/sbin/nginx" ]
