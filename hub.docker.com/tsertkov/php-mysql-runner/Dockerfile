FROM php:latest

RUN apt-get update && apt-get install -y \
  mysql-client \
  less \
  vim \
  --no-install-recommends && rm -r /var/lib/apt/lists/* \
  && docker-php-ext-install pdo_mysql

CMD ["bash"]
