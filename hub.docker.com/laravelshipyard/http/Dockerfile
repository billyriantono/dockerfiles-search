FROM alpine:latest

RUN apk add --no-cache gnupg bash tini \
    && wget -O - https://getcaddy.com | bash -s personal http.authz,http.cgi,http.cors,http.filebrowser,http.filter,http.forwardproxy,http.grpc,http.ipfilter,http.jwt,http.locale,http.login,http.minify,http.nobots,http.ratelimit,http.upload \
    && apk del --no-cache bash gnupg

RUN addgroup -S caddy \
    && adduser -D -S -h /var/cache/caddy -s /sbin/nologin -G caddy caddy

COPY Caddyfile.default Caddyfile.webguis /

USER caddy

ENTRYPOINT [ "tini", "caddy", "-log", "stderr", "-conf", "/Caddyfile.default" ]