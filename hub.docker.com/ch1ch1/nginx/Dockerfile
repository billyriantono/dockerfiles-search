FROM nginx:1.17.3
RUN apt-get update && apt install wget -y
ENV NGINX_VERSION 1.17.3
#Install nginx-opentracing module
RUN wget -O - \
  https://github.com/opentracing-contrib/nginx-opentracing/releases/download/v0.9.0/linux-amd64-nginx-$NGINX_VERSION-ngx_http_module.so.tgz | \
  tar zxf - -C /usr/lib/nginx/modules
RUN apt-get remove wget -y

RUN touch /var/run/nginx.pid \
&& mkdir -p /var/cache/nginx \
&& chown -R 1001:1001 /etc/nginx /var/log/nginx /var/cache/nginx /var/run/nginx.pid

EXPOSE 8080 8443

USER 1001

WORKDIR /etc/nginx
