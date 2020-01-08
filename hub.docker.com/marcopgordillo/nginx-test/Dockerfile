FROM alpine:latest
MAINTAINER Marco Gordillo <marcopgordillo@gmail.com>
LABEL description="This is a Docker file that installs NGINX"
ONBUILD RUN apk update && apk upgrade && rm -rf /var/cache/apk/*
RUN apk add --update nginx && \
	rm -rf /var/cache/apk/* && \
	mkdir -p /tmp/nginx/
COPY files/nginx.conf /etc/nginx/nginx.conf
COPY files/default.conf /etc/nginx/conf.d/default.conf
ADD files/html.tar.gz /usr/share/nginx/
EXPOSE 80/tcp
ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]

