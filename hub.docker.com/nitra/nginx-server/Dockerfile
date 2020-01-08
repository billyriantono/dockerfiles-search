FROM nitra/nginx

# Версія образу
ENV VER 3

VOLUME ["/etc/nginx/certs", "/etc/nginx/dhparam", "/etc/nginx/conf.d", "/root/.acme.sh"]

RUN apk add --no-cache openssl

COPY start.sh .

CMD ["/start.sh"]