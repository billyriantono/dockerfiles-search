############################################################
# Dockerfile to build Nginx Installed Containers
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM fedora:20

# File Author / Maintainer
MAINTAINER Oleksandr Lishchynskyy

#Install git, wget, make
RUN yum install git wget gcc make -y

#Install PCRE, zlib
RUN yum install pcre.x86_64 pcre-devel.x86_64 zlib.x86_64 zlib-devel.x86_64 -y

#Install OPENSSL
RUN yum install openssl.x86_64 openssl-devel.x86_64 -y

#Clone nginx-push-stream-module
RUN git clone https://github.com/wandenberg/nginx-push-stream-module.git

RUN NGINX_PUSH_STREAM_MODULE_PATH=$PWD/nginx-push-stream-module

# get desired nginx version (works with 1.2.0+)
RUN wget http://nginx.org/download/nginx-1.2.0.tar.gz

# unpack, configure and build
RUN ls
RUN tar xzvf nginx-1.2.0.tar.gz
RUN ls
WORKDIR /nginx-1.2.0
RUN ls
RUN ./configure --add-module=../nginx-push-stream-module
RUN make
# install and finish
RUN make install
RUN rm -v /usr/local/nginx/conf/nginx.conf
# Copy a configuration file from the current directory
ADD nginx.conf /usr/local/nginx/conf/


RUN mkdir -p /var/log/nginx

# Expose ports
EXPOSE 80

ENTRYPOINT /usr/local/nginx/sbin/nginx
# Set the default command to execute
# when creating a new container
#CMD /usr/local/nginx/sbin/nginx


