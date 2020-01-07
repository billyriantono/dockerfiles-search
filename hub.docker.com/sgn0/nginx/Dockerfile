FROM sgn0/baseimage
MAINTAINER Jesus Lopez, jesus@sgn.com

# nginx
RUN set -ex; \
    apk --no-cache -q add nginx

COPY conf /etc/nginx/
COPY bin /usr/sbin/

RUN set -ex; \
    ln -s /usr/sbin/nginx_ensite /usr/sbin/nginx_dissite; \
    nginx_ensite default

EXPOSE 80

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
