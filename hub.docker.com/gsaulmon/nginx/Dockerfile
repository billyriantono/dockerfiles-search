FROM fedora

RUN yum install yum-fastestmirror -y
RUN yum update -y
RUN yum -y install nginx

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["nginx"]