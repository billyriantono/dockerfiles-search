FROM centos:7

# http://nginx.org/packages/mainline/centos/7/x86_64/RPMS/
ARG NGINX_VERSION=1.15.8-1.el7_4.ngx

ADD nginx.repo /etc/yum.repos.d/nginx.repo

RUN curl -sO http://nginx.org/keys/nginx_signing.key && \
    rpm --import ./nginx_signing.key && \
    yum install -y nginx-${NGINX_VERSION} && \
    yum clean all && \
    rm -f ./nginx_signing.key && \
    # change permissions
    chmod -R 770 /var/cache/nginx/  && \
    # listen on 8080 as well as 80
    sed -i -e '/listen/!b' -e '/80;/!b' -e 's/80;/8080;/' /etc/nginx/conf.d/default.conf && \
    sed -i -e '/user/!b' -e '/nginx/!b' -e '/nginx/d' /etc/nginx/nginx.conf && \
    # place pid file under /var/cache/nginx
    sed -i 's!/var/run/nginx.pid;!/var/cache/nginx/nginx.pid;!g' /etc/nginx/nginx.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]
VOLUME ["/var/log/nginx"]

EXPOSE 80 8080 443

USER nginx:0

CMD ["nginx", "-g", "daemon off;"]
