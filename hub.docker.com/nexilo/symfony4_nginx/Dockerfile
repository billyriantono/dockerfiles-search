FROM debian:jessie

MAINTAINER Kamil Bednarek <kamil@nexilo.uk>

RUN apt-get update && apt-get install -y \
    nginx

ADD config/nginx.conf /etc/nginx/
RUN rm /etc/nginx/sites-enabled/default

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
