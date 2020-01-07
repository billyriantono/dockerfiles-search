FROM ubuntu:14.04
MAINTAINER Alex King "core2duoe6420@gmail.com"

RUN apt-get update \
        && apt-get install -y vim software-properties-common openssh-client \
        && add-apt-repository -y ppa:nginx/stable \
        && apt-get update \
        && apt-get install -y nginx

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

CMD ["nginx", "-g", "daemon off;"]
