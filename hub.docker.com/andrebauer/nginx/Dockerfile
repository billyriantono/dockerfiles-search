FROM ubuntu:16.04
MAINTAINER André Bauer <andre.bauer@posteo.de>
LABEL  architecture="amd64" \
       provides=www
RUN apt-get update && apt-get install -y nginx && apt-get clean
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
EXPOSE 80
ENTRYPOINT ["nginx"]