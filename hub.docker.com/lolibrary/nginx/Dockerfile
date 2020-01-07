FROM amelia/dhparam:latest as dh
FROM nginx:mainline-alpine

LABEL maintainer="amelia@lolibrary.org"

COPY --from=dh /etc/ssl/dhparam.pem /etc/nginx/dhparam.pem
COPY --from=dh /etc/ssl/snakeoil-cert.pem /etc/nginx/certs/certificate.pem
COPY --from=dh /etc/ssl/snakeoil-key.pem /etc/nginx/certs/privkey.pem

COPY nginx.conf /etc/nginx/nginx.conf

RUN apk --update add ca-certificates \
    && update-ca-certificates \
    && rm -rf /var/cache/apk/* \
    && nginx -t

CMD ["/usr/sbin/nginx"]
