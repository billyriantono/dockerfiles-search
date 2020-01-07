FROM progrium/busybox:latest
MAINTAINER Alan LaMielle <alan.lamielle+github@gmail.com>

EXPOSE 80 443
VOLUME ["/data"]
ENTRYPOINT ["nginx"]
CMD ["-c", "/data/nginx.conf"]

RUN mkdir /var/log/nginx /var/lib/nginx

RUN opkg-install nginx
