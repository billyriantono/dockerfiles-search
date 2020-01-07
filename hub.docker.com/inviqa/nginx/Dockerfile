FROM inviqa/base
MAINTAINER Mike Simons <msimons@inviqa.com>

RUN yum install -y nginx && yum clean all

RUN echo -e "\ndaemon off;" >> /etc/nginx/nginx.conf

ADD files/ /

EXPOSE 80 443
