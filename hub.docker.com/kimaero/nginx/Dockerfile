FROM alpine:latest
MAINTAINER Denis Kim <denis@kim.aero>

RUN apk --update add nginx nginx-mod-stream

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log
RUN mkdir /run/nginx
RUN chown -R nobody /var/lib/nginx

EXPOSE 80 443

VOLUME ["/etc/nginx", "/www", "/var/log/nginx"]
WORKDIR /etc/nginx

CMD ["nginx", "-g", "daemon off;"]