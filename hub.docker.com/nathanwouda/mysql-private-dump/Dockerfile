FROM php:cli-alpine
LABEL maintainer="contact@nathanwouda.nl" \
      version="0.0.7" \
      description="Private Dump is a CLI tool which can create an anonymised dump of your MySQL database."
RUN docker-php-ext-install pdo_mysql
RUN curl -Lo private-dump https://github.com/ashleyhindle/private-dump/releases/download/v0.0.7/private-dump && chmod a+x private-dump
ENTRYPOINT ["/private-dump"]
