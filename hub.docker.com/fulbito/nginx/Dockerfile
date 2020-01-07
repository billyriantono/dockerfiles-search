FROM nginx:1.11

MAINTAINER Zeta <zetahernandez@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ADD config/nginx.crt /etc/nginx/ssl/nginx.crt
ADD config/nginx.key /etc/nginx/ssl/nginx.key


EXPOSE 80
EXPOSE 443

CMD service nginx start
