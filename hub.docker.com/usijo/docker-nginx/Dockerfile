FROM usijo/docker-alpine
MAINTAINER Hongshun Yang<ojisucom@gmail.com>

RUN echo "@edge_main http://dl-4.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories

#nginx-mod-http-image-filter@edge_main \
#nginx-mod-http-xslt-filter@edge_main \
#nginx-mod-stream@edge_main \
#nginx-mod-mail@edge_main \
RUN apk add --no-cache nginx@edge_main \
                       nginx-mod-http-lua@edge_main  \
                       nginx-mod-http-upload-progress@edge_main \
                       nginx-mod-devel-kit@edge_main \
                       nginx-mod-http-echo@edge_main \
                       nginx-mod-http-fancyindex@edge_main \
                       nginx-mod-http-geoip@edge_main \
                       nginx-mod-http-headers-more@edge_main \
&& rm -rf /var/cache/apk/*

COPY rootfs/_var_www_html /var/www/html
COPY tmpl/_etc_nginx_conf.d_default.conf.tmpl /etc/nginx/conf.d/default.conf.tmpl
RUN mkdir -p /run/nginx

EXPOSE 80 443

CMD ["dockerize","-template","/etc/nginx/conf.d/default.conf.tmpl:/etc/nginx/conf.d/default.conf","nginx", "-g", "daemon off;"]

