FROM openresty/openresty:1.11.2.5-alpine-fat

# Add OpenResty stuff to path
ENV PATH=/usr/local/openresty/luajit/bin:/usr/local/openresty/nginx/sbin:/usr/local/openresty/bin:$PATH
ARG ECS_GEN_RELEASE=0.4.0-custom

RUN apk update && \
    apk add --no-cache openssl-dev git bash \
    python py-setuptools py-pip ca-certificates && \
    pip install --upgrade pip && \
    pip install supervisor==3.3.1 && \
    luarocks install lua-resty-openidc && \
    apk del py-pip openssl-dev git && \
    curl -LOk https://github.com/madhu1512/ecs-gen/releases/download/$ECS_GEN_RELEASE/ecs-gen-linux-amd64.zip && \
    unzip ecs-gen-linux-amd64.zip && \
    cp ecs-gen-linux-amd64 /usr/local/bin/ecs-gen && \
    rm -rf ecs-gen-linux-amd64* 

COPY nginx/nginx.conf /usr/local/openresty/nginx/conf/nginx.conf
COPY nginx/default.conf /usr/local/openresty/nginx/conf/sites/default.conf
COPY bootstrap.sh /usr/local/openresty/bootstrap.sh
COPY supervisord.conf /etc/supervisor/
COPY nginx.tmpl nginx.tmpl
RUN chmod +x /usr/local/openresty/bootstrap.sh
ENTRYPOINT ["supervisord", "--configuration", "/etc/supervisor/supervisord.conf"]
