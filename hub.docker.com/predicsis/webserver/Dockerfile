FROM ubuntu:14.04
MAINTAINER wnkz

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get -qy dist-upgrade
RUN apt-get install -qy software-properties-common
RUN add-apt-repository -y ppa:nginx/stable
RUN apt-get update
RUN apt-get install -qy nginx

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
