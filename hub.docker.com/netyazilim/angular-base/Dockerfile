FROM netyazilim/alpine-base:3.9
LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"
EXPOSE 80
RUN apk add --upgrade --no-cache nginx && \
    mkdir -p /run/nginx

COPY default.conf /etc/nginx/conf.d/default.conf
COPY app/ /var/lib/nginx/html/
ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["-g", "daemon off;"]