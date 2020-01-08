FROM ubuntu

MAINTAINER devopspoints

RUN apt-get update

RUN apt-get install -y vim wget dialog net-tools

RUN apt-get install -y nginx

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

ADD index.html /var/www/html/

EXPOSE 80

CMD ["nginx"]
