FROM nginx:1.15.6-alpine
RUN apk add --no-cache --update openssl \
    && mkdir -p /etc/nginx/ssl/localhost \
    && openssl req -new -x509 -days 365 -nodes -out /etc/nginx/ssl/localhost/cert.crt -keyout /etc/nginx/ssl/localhost/private.key -subj "/C=RU/ST=Moscow/L=Korolev/O=Dev/OU=IT/CN=localhost" \
    && openssl dhparam -out /etc/nginx/ssl/localhost/dhparam.pem 2048 \
    && rm -rf /var/cache/apk/*
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80 443
