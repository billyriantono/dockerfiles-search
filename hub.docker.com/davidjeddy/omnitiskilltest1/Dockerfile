FROM php:7.2.9-cli-stretch
RUN apt-get update -y
RUN apt-get install -y iputils-ping
RUN apt-get clean
COPY ./ /app
CMD ["php", "/app/index.php"]