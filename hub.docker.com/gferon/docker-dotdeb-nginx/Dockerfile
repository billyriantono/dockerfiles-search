FROM debian:jessie

MAINTAINER Gabriel Feron "feron.gabriel@gmail.com"

RUN apt-get update && apt-get install -yq curl ca-certificates \
    && echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list \
    && curl http://www.dotdeb.org/dotdeb.gpg | apt-key add -
RUN apt-get update \
    && apt-get install -yq nginx-extras \
    && rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
