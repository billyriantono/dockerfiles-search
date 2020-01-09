FROM alpine:latest
LABEL maintainer="Russ McKendrick <russ@mckendrick.io>"
LABEL description="This example Dockerfile installs NGINX."
RUN apk add --update nginx && \
        rm -rf /var/cache/apk/* && \
        mkdir -p /tmp/nginx/


RUN wget -q -O /etc/nginx/nginx.conf  https://github.com/eacatalyst/Mastering-Docker-Third-Edition/tree/master/chapter02/dockerfile-example/files/nginx.conf
RUN wget -q -O /etc/nginx/conf.d/default.conf  https://github.com/eacatalyst/Mastering-Docker-Third-Edition/tree/master/chapter02/dockerfile-example/files/default.conf

RUN mkdir -p /usr/share/nginx

RUN wget -q -O /usr/share/nginx/html  https://github.com/eacatalyst/Mastering-Docker-Third-Edition/tree/master/chapter02/dockerfile-example/files/html

# ADD ./files/html.tar.gz /usr/share/nginx/

EXPOSE 80/tcp

ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
