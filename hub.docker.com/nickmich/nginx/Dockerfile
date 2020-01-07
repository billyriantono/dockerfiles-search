FROM centos:latest
MAINTAINER nickmich

RUN yum -y update
RUN yum -y upgrade
RUN yum -y install epel-release
RUN yum -y install nginx
RUN echo "nginx -c /opt/nginx/nginx.conf && tail -f /var/log/nginx/access.log" > /start.sh

EXPOSE 8777
VOLUME /opt/nginx/
VOLUME /var/nginx/

ENTRYPOINT ["bash", "/start.sh"]
