FROM ubuntu:16.04

# update
RUN apt-get update

# install nginx
RUN apt-get install -y nginx

WORKDIR /data

EXPOSE 80
EXPOSE 443

CMD /usr/sbin/nginx -g 'daemon off;'
