FROM nginx:stable
MAINTAINER Egor Zyuskin <ezyuskin@codenetix.com>

ADD ./etc/ /etc/
ADD ./container-entrypoint.sh /container-entrypoint.sh

EXPOSE 80 443

VOLUME ["/etc/nginx/conf.d/", "/etc/nginx/ssl"]

ENTRYPOINT ["/container-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
