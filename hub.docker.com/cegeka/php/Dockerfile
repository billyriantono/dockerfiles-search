FROM debian:stretch

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y apt-transport-https lsb-release ca-certificates wget apt-utils locales gnupg make

# Add sources
RUN wget -q -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN wget -qO- https://deb.nodesource.com/setup_8.x | bash -
RUN wget -qO- https://github.com/wodby/gotpl/releases/download/0.1.5/gotpl-linux-amd64-0.1.5.tar.gz | tar xz -C /usr/local/bin
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -y curl git apache2 && \
    apt-get autoremove --purge php5-*

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        mysql-client \
        ssmtp \
        imagemagick \
        ghostscript \
        nodejs \
        nano \
        vim \
    	php7.2 \
    	php7.2-cli \
    	php7.2-common \
    	php7.2-bcmath \
    	php7.2-gd \
    	php7.2-imap \
    	php7.2-intl \
    	php7.2-mbstring \
    	php7.2-mysql \
    	php7.2-soap \
    	php7.2-tidy \
    	php7.2-xml \
    	php7.2-gmp \
    	php-redis \
    	php-mongodb \
    	php7.2-sqlite3 \
    	php7.2-curl \
    	php7.2-zip \
    	php7.2-xdebug \
    	php7.2-apc \
	    php-imagick \
    && rm -rf /var/lib/apt/lists/*

RUN echo "FromLineOverride=YES" >> /etc/ssmtp/ssmtp.conf

RUN sed -i 's/^# *\(nl_BE.UTF-8\)/\1/' /etc/locale.gen
RUN locale-gen nl_BE.UTF-8
ENV LANG nl_BE.UTF-8
ENV LANGUAGE nl_BE
ENV LC_ALL nl_BE.UTF-8

RUN a2enmod rewrite

RUN npm install -g eslint@3.5.0
RUN npm install -g less
RUN npm install -g less-plugin-clean-css
RUN npm install -g gulp

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir -p /var/www/project && \
    chown -R www-data:www-data /var/www/project && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log

COPY templates /etc/gotpl/

WORKDIR /var/www/project
EXPOSE 80

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
