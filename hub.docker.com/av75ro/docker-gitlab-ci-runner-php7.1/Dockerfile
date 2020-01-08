FROM debian:jessie
MAINTAINER apostol victor
ENV LAST_UPDATED 2017-07-04
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y wget apt-transport-https lsb-release ca-certificates curl
RUN echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.org.list && \
	echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.org.list
RUN wget http://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y php7.1-fpm php7.1-cli php7.1-mysql php7.1-mcrypt php7.1-curl php7.1-gd php7.1-mbstring php7.1-zip php7.1-sqlite php-xml php-xdebug git

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"
ENV COMPOSER_VERSION 1.4.2

# Install Composer
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} && rm -rf /tmp/composer-setup.php
RUN composer global require "hirak/prestissimo:^0.3"
RUN mkdir -p /tmp/php-opcache

RUN sed -i 's/;opcache.enable=1/opcache.enable=1/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.enable_cli=1/opcache.enable_cli=1/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.memory_consumption=128/opcache.memory_consumption=512/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.interned_strings_buffer=8/opcache.interned_strings_buffer=64/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.max_accelerated_files=10000/opcache.max_accelerated_files=7963/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.validate_timestamps=1/opcache.validate_timestamps=0/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.save_comments=1/opcache.save_comments=1/g' /etc/php/7.1/cli/php.ini
RUN sed -i 's/;opcache.fast_shutdown=0/opcache.fast_shutdown=0/g' /etc/php/7.1/cli/php.ini
#RUN sed -i 's#;opcache.file_cache=#opcache.file_cache=/tmp/php-opcache#g' /etc/php/7.1/cli/php.ini
RUN apt-get install xz-utils
RUN apt-get clean -y && apt-get autoclean -y && apt-get autoremove -y

RUN wget -O /tmp/ffmpeg-release-64bit-static.tar.xz https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz
RUN cd /tmp && tar xf ffmpeg-release-64bit-static.tar.xz
RUN cd /tmp/ffmpeg-3.3.2-64bit-static && cp ffmpeg /usr/bin/ffmpeg && cp ffprobe /usr/bin/ffprobe && chmod +x /usr/bin/ffmpeg && chmod +x /usr/bin/ffprobe

RUN mkdir -p /run/php

EXPOSE 9000

CMD ["php-fpm7.1", "-F"]