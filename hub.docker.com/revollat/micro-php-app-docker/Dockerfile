FROM alpine:3.1
RUN apk add --update php-cli && rm -rf /var/cache/apk/*
ADD index.php /var/www/index.php
EXPOSE 80
CMD ["php", "-S", "0.0.0.0:80", "-t", "/var/www"]
