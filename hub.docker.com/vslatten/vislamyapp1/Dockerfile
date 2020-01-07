# Use the ubuntu 14.04 base image
FROM ubuntu:14.04

MAINTAINER Vidar <visla@statoil.com>

# Set timezone
RUN ln -sf /usr/share/zoneinfo/Europe/Oslo /etc/localtime

# Use Statoil HTTP proxy
#ENV http_proxy http://www-proxy.statoil.no:80/
#ENV https_proxy http://www-proxy.statoil.no:80/

# Install required packages
RUN apt-get update && apt-get install -y \
    supervisor \
    nodejs \
    npm

ADD . /myapp/

WORKDIR /myapp

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN npm install

CMD npm start

EXPOSE 80
