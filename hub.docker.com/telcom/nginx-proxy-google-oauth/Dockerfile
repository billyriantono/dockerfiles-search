FROM jwilder/nginx-proxy:latest

# Install libnginx-mod-http-lua + lua-cjson + lua-resty-http
RUN echo "deb http://ftp.debian.org/debian stretch-backports main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get -t stretch-backports install -y --no-install-recommends -o Dpkg::Options::="--force-confold" nginx-extras lua-cjson git ca-certificates && \
    rm -rf /var/lib/apt/lists/* && \
    git clone -c transfer.fsckobjects=true https://github.com/pintsized/lua-resty-http.git /tmp/lua-resty-http && \
    cd /tmp/lua-resty-http && \
    git checkout v0.12 && \
    mkdir -p /etc/nginx/lua && \
    cp -aR /tmp/lua-resty-http/lib/resty /etc/nginx/lua/resty && \
    rm -rf /tmp/lua-resty-http

# Load modules + set lua path
RUN sed -i "1s#^#load_module /usr/lib/nginx/modules/ndk_http_module.so;\nload_module /usr/lib/nginx/modules/ngx_http_lua_module.so;\n#" /etc/nginx/nginx.conf
COPY lua.conf /etc/nginx/conf.d/lua.conf

# Install google auth from https://github.com/cloudflare/nginx-google-oauth
RUN git clone -c transfer.fsckobjects=true https://github.com/cloudflare/nginx-google-oauth.git /tmp/nginx-google-oauth && \
    cd /tmp/nginx-google-oauth && \
    mkdir -p /etc/nginx/lua/nginx-google-oauth && \
    mv access.lua /etc/nginx/lua/nginx-google-oauth/access.lua

# Apply google auth via lua by default
COPY location.conf /etc/nginx/vhost.d/default_location

# Disable the ipv6 resolver (hopfully this is temp)
RUN sed -i 's/resolver {{ $.Env.RESOLVERS }};/resolver {{ $.Env.RESOLVERS }} ipv6=off;/' /app/nginx.tmpl

ENTRYPOINT ["/app/docker-entrypoint.sh"]

CMD ["forego", "start", "-r"]
