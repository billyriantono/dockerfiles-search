FROM php:5.6-fpm-alpine

ENV PHPEXT_CURL_DEPS curl-dev
ENV PHPEXT_DOM_DEPS libxml2-dev
ENV PHPEXT_SOAP_DEPS libxml2-dev
ENV PHPEXT_ENCHANT_DEPS enchant-dev
ENV PHPEXT_GD_DEPS \
        freetype \
        freetype-dev \
        libpng \
        libpng-dev \
        libjpeg-turbo \
        libjpeg-turbo-dev
ENV PHPEXT_GMP_DEPS gmp-dev
ENV PHPEXT_IMAP_DEPS imap-dev
ENV PHPEXT_INTL_DEPS icu-dev
ENV PHPEXT_GETTEXT_DEPS gettext-dev
ENV PHPEXT_LDAP_DEPS openldap-dev
ENV PHPEXT_MCRYPT_DEPS libmcrypt-dev
ENV PHPEXT_PDO_SQLITE_DEPS sqlite-dev
ENV PHPEXT_READLINE_DEPS libedit-dev
ENV PHPEXT_RXSLT_DEPS libxslt-dev
ENV PHPEXT_PHAR_DEPS openssl-dev
ENV PHPEXT_ZIP_DEPS libxml2-dev

# ------------------------------------------------------------------------------------------------------------------------------

# Affecting PHP's Behaviour
# http://php.net/manual/en/refs.basic.php.php

## http://php.net/manual/en/book.opcache.php
RUN docker-php-ext-install opcache

# ------------------------------------------------------------------------------------------------------------------------------

# Command Line Specific Extensions
# http://php.net/manual/en/refs.utilspec.cmdline.php

## http://php.net/manual/de/function.readline.php
#RUN apk add --no-cache $PHPEXT_READLINE_DEPS
#RUN docker-php-ext-install readline # already loaded

# ------------------------------------------------------------------------------------------------------------------------------

# Compression and Archive Extensions
# http://php.net/manual/en/refs.compression.php

## http://php.net/manual/en/book.phar.php
#RUN apk add --no-cache $PHPEXT_PHAR_DEPS
#RUN docker-php-ext-install phar # already loaded

# http://php.net/manual/en/book.zip.php
RUN apk add --no-cache $PHPEXT_ZIP_DEPS
RUN docker-php-ext-install zip

# ------------------------------------------------------------------------------------------------------------------------------

# Cryptography Extensions
# http://php.net/manual/en/refs.crypto.php

## http://php.net/manual/en/function.hash.php
#RUN docker-php-ext-install hash # already loaded

## http://php.net/manual/en/book.mcrypt.php
RUN apk add --no-cache $PHPEXT_MCRYPT_DEPS
RUN docker-php-ext-install mcrypt

# ------------------------------------------------------------------------------------------------------------------------------

# Database Extensions
# http://php.net/manual/en/refs.database.php

##  http://php.net/manual/en/ref.pdo-sqlite.php
#RUN apk add --no-cache $PHPEXT_PDO_SQLITE_DEPS
#RUN docker-php-ext-install pdo_sqlite # already loaded

## http://php.net/manual/en/ref.pdo-mysql.php
RUN docker-php-ext-install pdo_mysql

# ------------------------------------------------------------------------------------------------------------------------------

# Date and Time Related Extensions
# http://php.net/manual/en/refs.calendar.php

## http://php.net/manual/en/book.calendar.php
RUN docker-php-ext-install calendar

# ------------------------------------------------------------------------------------------------------------------------------

# File System Related Extensions
# http://php.net/manual/en/refs.fileprocess.file.php

## http://php.net/manual/en/book.fileinfo.php
#RUN docker-php-ext-install fileinfo # already loaded

# ------------------------------------------------------------------------------------------------------------------------------

# Human Language and Character Encoding Support
# http://php.net/manual/en/refs.international.php

##  http://php.net/manual/en/book.enchant.php
#RUN apk add --no-cache $PHPEXT_ENCHANT_DEPS
#RUN docker-php-ext-install enchant

## http://php.net/manual/en/book.gettext.php
RUN apk add --no-cache $PHPEXT_GETTEXT_DEPS
RUN docker-php-ext-install gettext

## http://php.net/manual/en/book.iconv.php
#RUN docker-php-ext-install iconv # already loaded

## http://php.net/manual/de/book.intl.php
RUN apk add --no-cache $PHPEXT_INTL_DEPS
RUN docker-php-ext-install intl

## http://php.net/manual/en/book.mbstring.php
# RUN docker-php-ext-install mbstring # already loaded

# ------------------------------------------------------------------------------------------------------------------------------

# Image Processing and Generation
# http://php.net/manual/en/refs.utilspec.image.php

## http://php.net/manual/en/book.exif.php
RUN docker-php-ext-install exif

## http://php.net/manual/en/book.image.php
RUN apk add --no-cache $PHPEXT_GD_DEPS
RUN docker-php-ext-install gd

# ------------------------------------------------------------------------------------------------------------------------------

# Mail Related Extensions
# http://php.net/manual/en/refs.remote.mail.php

## http://php.net/manual/en/book.imap.php
RUN apk add --no-cache $PHPEXT_IMAP_DEPS
RUN docker-php-ext-install imap

# ------------------------------------------------------------------------------------------------------------------------------

# Mathematical Extensions
# http://php.net/manual/en/refs.math.php

## http://php.net/manual/en/book.bc.php
RUN docker-php-ext-install bcmath

## http://php.net/manual/en/book.gmp.php
RUN apk add --no-cache $PHPEXT_GMP_DEPS
RUN docker-php-ext-install gmp

# ------------------------------------------------------------------------------------------------------------------------------

# Process Control Extensions
# http://php.net/manual/en/refs.fileprocess.process.php

## http://php.net/manual/en/book.pcntl.php
#RUN docker-php-ext-install pcntl

## http://php.net/manual/en/book.posix.php
#RUN docker-php-ext-install posix

## Semaphore, Shared Memory and IPC
## http://php.net/manual/en/book.sem.php
#RUN docker-php-ext-install sysvmsg
#RUN docker-php-ext-install sysvsem
#RUN docker-php-ext-install sysvshm

## http://php.net/manual/de/book.shmop.php
#RUN docker-php-ext-install shmop

# ------------------------------------------------------------------------------------------------------------------------------

# http://php.net/manual/en/refs.basic.other.php
# Other Basic Extensions

## http://php.net/manual/en/book.json.php
#RUN docker-php-ext-install json # already loaded

## http://php.net/manual/en/book.tokenizer.php
#RUN docker-php-ext-install tokenizer # already loaded

## http://php.net/manual/en/book.geoip.php
# RUN pecl install geoip # cannot install

# ------------------------------------------------------------------------------------------------------------------------------

# Other Services
# http://php.net/manual/en/refs.remote.other.php

# http://php.net/manual/en/book.curl.php
#RUN apk add --no-cache $PHPEXT_CURL_DEPS
#RUN docker-php-ext-install curl # already loaded

## http://php.net/manual/en/book.ftp.php
# RUN docker-php-ext-install ftp # already loaded

## http://php.net/manual/en/book.ldap.php
RUN apk add --no-cache $PHPEXT_LDAP_DEPS
RUN docker-php-ext-install ldap

## http://php.net/manual/en/book.sockets.php
RUN docker-php-ext-install sockets

# ------------------------------------------------------------------------------------------------------------------------------

# Session Extensions
# http://php.net/manual/en/refs.basic.session.php

## http://php.net/manual/en/book.session.php
# RUN docker-php-ext-install session # already loaded

# ------------------------------------------------------------------------------------------------------------------------------

# Variable and Type Related Extensions
# http://php.net/manual/en/refs.basic.vartype.php

## http://php.net/manual/en/book.ctype.php
#RUN docker-php-ext-install ctype # already loaded

# ------------------------------------------------------------------------------------------------------------------------------

# Web Services
# http://php.net/manual/en/refs.webservice.php

## http://php.net/manual/en/book.soap.php
RUN apk add --no-cache $PHPEXT_SOAP_DEPS
RUN docker-php-ext-install soap

# http://php.net/manual/en/book.xmlrpc.php
RUN docker-php-ext-install xmlrpc

# ------------------------------------------------------------------------------------------------------------------------------

# XML Manipulation
# http://php.net/manual/en/refs.xml.php

## http://php.net/manual/en/book.dom.php
#RUN apk add --no-cache $PHPEXT_DOM_DEPS
#RUN docker-php-ext-install dom # already loaded

## http://php.net/manual/en/book.libxml.php
# RUN docker-php-ext-install xml # already loaded

## http://php.net/manual/en/book.simplexml.php
# RUN docker-php-ext-install simplexml # already loaded

## http://php.net/manual/en/book.wddx.php
RUN docker-php-ext-install wddx

## http://php.net/manual/en/book.xmlwriter.php
#RUN docker-php-ext-install xmlwriter # already loaded

## http://php.net/manual/en/book.xsl.php
RUN apk add --no-cache $PHPEXT_RXSLT_DEPS
RUN docker-php-ext-install xsl
