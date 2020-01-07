FROM gsol/nginx:1.14.0-alpine-lua

LABEL maintainer="Global-Solutions co. ltd."

ENV LUA_REDIS_VERSION=0.26 \
    LUA_RESTY_REDIS_DIR=/opt/nginx/lua-resty-redis

RUN apk --update add --no-cache --virtual .deps curl tar && \
    mkdir $LUA_RESTY_REDIS_DIR -p && \
    curl -fSL https://github.com/openresty/lua-resty-redis/archive/v$LUA_REDIS_VERSION.tar.gz | tar -zxC $LUA_RESTY_REDIS_DIR --strip-components 1 && \
    apk del .deps && \
    rm -rf /var/cache/apk/* && \
    echo "lua_package_path '$LUA_RESTY_REDIS_DIR/lib/?.lua;;';" > /etc/nginx/conf.d/lua_resty_redis.conf
