FROM ubuntu:16.04
MAINTAINER arnv
RUN apt-get update && apt-get install -y nginx && service nginx start
COPY index.nginx-debian.html /var/www/html/index.nginx-debian.html
EXPOSE 8080 8082
VOLUME ["/var/log/nginx"]
CMD nginx -g 'daemon off;'
