FROM alpine

MAINTAINER ZhiFeng Hu "hufeng1987@gmail.com"

RUN apk update
RUN apk add nginx 


RUN mkdir /tmp/nginx

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx", "/etc/nginx"]

CMD ["nginx", "-g", "daemon off;"]
