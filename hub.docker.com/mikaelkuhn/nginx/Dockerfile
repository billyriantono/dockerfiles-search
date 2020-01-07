FROM mikaelkuhn/ubuntu

ENV NGINX_VERSION 1.6.2-1~trusty

# Please note your docker version must be ie 1.4.1+ to build this image

RUN export DEBIAN_FRONTEND=noninteractive && \
	apt-key adv --fetch-keys "http://nginx.org/keys/nginx_signing.key" &&  \
	echo "deb http://nginx.org/packages/ubuntu/ trusty nginx" >> /etc/apt/sources.list && \
	echo "deb-src http://nginx.org/packages/ubuntu/ trusty nginx" >> /etc/apt/sources.list && \
	apt-get update && \
	apt-get install -y nginx=${NGINX_VERSION}

VOLUME ["/data"]

EXPOSE 80 443

CMD ["nginx", "-c", "/data/nginx.conf", "-g", "daemon off;"]