FROM  debian:stretch-slim as builder
LABEL maintainer="NGINX with NGX_PGCOPY <rba765@gmail.com>"
RUN              apt-get update                \
        && yes | apt-get install libc6-dev     \
                                 libpqxx3-dev  \
                                 libpcre3-dev  \
                                 zlib1g-dev    \
                                 libssh-dev    \
                                 git           \
                                 gcc           \
                                 make          \
        && git clone https://github.com/nginx/nginx /root/nginx                     && \
           git clone https://github.com/AntonRiab/ngx_pgcopy /root/nginx/ngx_pgcopy && \ 
	   cd /root/nginx                                                              \
	&& CONFIG="\
                --prefix=/etc/nginx                       \
                --sbin-path=/usr/sbin/nginx               \
                --conf-path=/etc/nginx/nginx.conf         \
                --error-log-path=/var/log/nginx/error.log \
                --http-log-path=/var/log/nginx/access.log \
                --pid-path=/var/run/nginx.pid             \
                --lock-path=/var/run/nginx.lock           \
                --http-client-body-temp-path=/var/lib/postgresql/data/import          \
                --http-proxy-temp-path=/var/lib/postgresql/data/import/proxy_temp     \
                --http-fastcgi-temp-path=/var/lib/postgresql/data/import/fastcgi_temp \
                --http-uwsgi-temp-path=/var/lib/postgresql/data/import/uwsgi_temp     \
                --http-scgi-temp-path=/var/lib/postgresql/data/import/scgi_temp       \
                --user=nginx                    \
                --group=nginx                   \
                --with-http_realip_module       \
                --with-http_addition_module     \
                --with-http_sub_module          \
                --with-http_gunzip_module       \
                --with-http_gzip_static_module  \
                --with-http_stub_status_module  \
                --with-http_auth_request_module \
                --with-http_ssl_module          \
                --with-threads                  \
                --with-file-aio                 \
                --add-module=ngx_pgcopy         \
	" \
	&& ./auto/configure $CONFIG \
	&& make                     \
        #
        && mkdir -p /root/minimal_nginx/etc/            \
        && cp -r conf /root/minimal_nginx/etc/nginx     \
        && mkdir -p /root/minimal_nginx/var/log/nginx   \
        && touch /root/minimal_nginx/var/log/nginx/error.log           \
        && touch /root/minimal_nginx/var/log/nginx/access.log          \
        && mkdir -p /root/minimal_nginx/var/cache/nginx                \
        && mkdir -p /root/minimal_nginx/var/lib/postgresql/data/import \
	&& mkdir -p /root/minimal_nginx/etc/nginx/conf.d/              \
	&& mkdir -p /root/minimal_nginx/usr/share/nginx/html/          \
        && mkdir -p /root/minimal_nginx/usr/sbin/                      \
        && cp -r docs/html/ /root/minimal_nginx/usr/share/nginx/       \
        && cp objs/nginx /root/minimal_nginx/usr/sbin/                 \
        #
        && for i in `ldd objs/nginx | awk '$0!~/linux-vdso.so.1/{if ( $3 == "") print $1; else print $3}'`; do \
               cp --parents $i /root/minimal_nginx ; done

FROM debian:stretch-slim
COPY --from=builder /root/minimal_nginx/ /
RUN    groupadd -r nginx \
    && useradd --system --home /var/cache/nginx -s /sbin/nologin -g nginx nginx \
    #  forward request and error logs to docker log collector
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log
EXPOSE 80
STOPSIGNAL SIGTERM
CMD ["nginx", "-g", "daemon off;"]
