FROM resin/armv7hf-debian-qemu
MAINTAINER Jimmy Yang <gankkank@gmail.com>

RUN [ "cross-build-start" ]

RUN apt-get update && \
  apt-get install -y nginx git vim 

# Clean up APT 
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

#VOLUMES

EXPOSE 80 443 
CMD [ "nginx", "-g", "daemon off;"]

RUN [ "cross-build-end" ]
