FROM nginx:alpine
 
COPY nginx.conf /etc/nginx/nginx.conf

COPY out/ops.hebe.ch/ops.hebe.ch.cer out/ops.hebe.ch/ops.hebe.ch.key out/ops.hebe.ch/ca.cer out/ops.hebe.ch/fullchain.cer /etc/nginx/
RUN apk add --update curl openssl netcat-openbsd && \
    rm -rf /var/cache/apk/*

EXPOSE 443
EXPOSE 80
