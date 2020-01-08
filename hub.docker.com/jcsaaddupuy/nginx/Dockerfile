FROM debian:jessie
MAINTAINER Jc Saad-Dupuy "jc.saaddupuy@fsfe.org"

# install base packages
RUN apt-get update -qq && apt-get upgrade -y
RUN apt-get install -y wget
RUN wget http://nginx.org/keys/nginx_signing.key && apt-key add nginx_signing.key
RUN echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list
RUN apt-get update -qq
RUN apt-get install -y nginx
RUN rm nginx_signing.key


# Copy custom config
ADD nginx/nginx.conf /etc/nginx/nginx.conf
ADD nginx/conf.d/ /etc/nginx/conf.d/

# Clean useless config
RUN rm /etc/nginx/conf.d/example_ssl.conf

RUN mkdir -p /var/www


EXPOSE 80

CMD ["nginx"]

