FROM debian:jessie


# Set environment.
ENV \
  DEBIAN_FRONTEND=noninteractive \
  TERM=xterm-color

# Install packages.
RUN apt-get update && apt-get -y install \
  build-essential \
  curl \
  libreadline-dev \
  libncurses5-dev \
  libpcre3-dev \
  libssl-dev \
  nano \
  perl \
  wget 

# Compile openresty from source.
RUN \
  wget https://openresty.org/download/openresty-1.9.7.4.tar.gz && \
  tar -xzvf openresty-*.tar.gz && \
  rm -f openresty-*.tar.gz && \
  cd openresty-* && \
  ./configure --with-pcre-jit --with-ipv6 && \
  make && \
  make install && \
  make clean && \
  cd .. && \
  rm -rf openresty-*&& \
  ln -s /usr/local/openresty/nginx/sbin/nginx /usr/local/bin/nginx && \
  ldconfig
RUN \
  mkdir /etc/nginx && \
  cp /usr/local/openresty/nginx/conf/* /etc/nginx/

# Set the working directory.
WORKDIR /home/openresty

# Add files to the container.
ADD start.sh  /home/openresty/start.sh

# Expose volumes.
VOLUME ["/etc/nginx"]

#Install Consul Template
ADD consul-template /usr/local/bin/consul-template
ADD dumb-init_1.0.2_amd64 /usr/local/bin/dumb-init

#Setup Consul Template Files
RUN mkdir /etc/consul-templates
ADD t_nginx.conf /etc/consul-templates/nginx.conf
ENV CT_FILE /etc/consul-templates/nginx.conf

#Setup Nginx File
ADD nginx.conf /etc/nginx/nginx.conf
ENV NX_FILE /etc/nginx/app.conf

#Default Variables
ENV CONSUL consul:8500
ENV SERVICE nginx-demo

CMD dumb-init /bin/bash start.sh 
