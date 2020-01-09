FROM php:7-alpine

WORKDIR /app
COPY yourip.php ./

EXPOSE 80

CMD ["php", "-S", "0.0.0.0:80", "yourip.php"]