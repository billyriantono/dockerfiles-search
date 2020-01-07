FROM ubuntu:16.04

RUN echo 'deb http://nginx.org/packages/ubuntu/ xenial nginx' >>  /etc/apt/sources.list.d/nginx.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 \ 
 && apt-get update
 
RUN apt install -y --no-install-recommends --no-install-suggests --allow-unauthenticated \
    ca-certificates \
    nginx \
    nginx-module-xslt \
    nginx-module-geoip \
    nginx-module-image-filter \
    nginx-module-perl \
    nginx-module-njs \
    gettext-base \
 && mkdir /etc/nginx/certs

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log


EXPOSE 80 443

VOLUME ["/etc/nginx/conf.d/", "/etc/nginx/certs/"]

CMD ["nginx", "-g", "daemon off;"]

