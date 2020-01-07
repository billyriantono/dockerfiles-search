FROM alpine:latest

MAINTAINER alex alexwhen@gmail.com

RUN apk --update add nginx

RUN ln -sf /dev/stdout /var/log/nginx/access.log

RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
