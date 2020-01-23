FROM ubuntu:16.10

RUN apt-get update \
    && apt-get install -y nginx nginx-extras \
    && apt-get clean \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY ./nginx /etc/nginx
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
