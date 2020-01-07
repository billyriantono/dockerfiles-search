# Nginx Image using host shared conf files
#
# VERSION               0.0.1

FROM nginx:latest

MAINTAINER Mateus Miranda <mateusmiranda@gmail.com>

RUN apt-get update \
	&& apt-get -y install vim curl net-tools

COPY ./nginx.conf /etc/nginx/
COPY ./conf.d/ /etc/nginx/conf.d/

EXPOSE 80
