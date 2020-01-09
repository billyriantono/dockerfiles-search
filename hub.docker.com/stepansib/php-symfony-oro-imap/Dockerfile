FROM stepansib/php-symfony-oro:7.1
MAINTAINER Stepan Yudin <stepan.sib@gmail.com>

# Install PHP IMAP dependencies
RUN apt-get update && apt-get install -y \
  libc-client-dev \
  libkrb5-dev

# Install and configure PHP IMAP extension
RUN docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos
RUN docker-php-ext-install imap

# Install and configure PHP Mailparse extension
RUN pecl install mailparse \
    && docker-php-ext-enable mailparse