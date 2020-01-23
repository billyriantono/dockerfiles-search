FROM php:latest

RUN apt-get update && apt-get install vim git -y
RUN docker-php-ext-install pdo tokenizer mbstring mysqli pdo pdo_mysql ctype
RUN apt-get clean

ADD . /app

EXPOSE 80:8000

VOLUME ["/app"]
WORKDIR /app
