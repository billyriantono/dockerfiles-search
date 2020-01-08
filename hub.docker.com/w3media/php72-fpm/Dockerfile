FROM php:7.2-fpm

ENV DEBIAN_FRONTEND noninteractive

# Set default date.timezone
RUN echo "date.timezone=UTC" > /usr/local/etc/php/conf.d/00-default.ini
RUN echo "memory_limit=-1" > /usr/local/etc/php/php-cli.ini

# Non-root user uid:1000 / gid:1000
RUN \
    groupadd -g 1000 www &&  \
    useradd -u 1000 -g 1000 -ms /bin/bash www && \
    echo "alias ll='ls -la'" >> /home/www/.bashrc && \
    mkdir -p /app

# PHP Configuration
RUN echo "LANG=\"en_US.UTF-8\"" > /etc/default/locale && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen

# Install dependencies
RUN \
    apt-get update --fix-missing && \
    # required packages for further setup
    apt-get install -y \
        libsqlite3-dev \
        libmcrypt-dev \
        libz-dev \
        libmemcached-dev \
        libcurl4-openssl-dev \
        libxslt1-dev \
        libffi-dev \
        openssl \
        libssl-dev \
        libxml2-dev \
        libicu-dev \
        libxslt-dev \
        gnupg2 \
        imagemagick \
        python3-sphinx \
        g++ && \
    # default tools
    apt-get install -y git zip sudo locales vim nano telnet xvfb yarn wget ssh-client && \
    which convert

# SSH-server / supervisord
RUN apt-get install -y openssh-server supervisor

# PHP Configuration
RUN \
    # intl
    docker-php-ext-configure intl && \
    docker-php-ext-install intl && \
    # dom/xml/xsl
    docker-php-ext-install dom xmlrpc xsl && \
    # gd/exif
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libgd-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd exif && \
    # database
    docker-php-ext-install mysqli pdo pdo_mysql && \
    # string
    docker-php-ext-install gettext mbstring && \
    # math
    apt-get install -y libgmp-dev && \
    ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h && \
    docker-php-ext-install gmp bcmath && \
    # compression
    apt-get install -y libbz2-dev zlib1g-dev && \
    docker-php-ext-install zip bz2 && \
    # ftp
    docker-php-ext-install ftp && \
    # ssh2
    apt-get install -y libssh2-1 libssh2-1-dev && \
    pecl install ssh2-1.1.2 && \
    docker-php-ext-enable ssh2 && \
    # other extensions
    docker-php-ext-install iconv curl soap && \
    pecl install xdebug-2.6.0 && \
    echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini && \
    echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini && \
    pecl install memcached-3.0.4 && docker-php-ext-enable memcached && \
    pecl install apcu-5.1.11 apcu_bc-1.0.4 && \
    docker-php-ext-enable --ini-name docker-php-ext-apcu.ini apcu apc && \
    # Allow extension enable for the user "www"
    chown www:www -vR /usr/local/etc/php/conf.d/

RUN \
    # Node packages
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
    node --version && \
    npm --version && \
    npm install -g grunt grunt-cli gulp

# Download and install wkhtmltopdf
RUN \
    apt-get install -y build-essential xorg libxrender-dev && \
    wget -qq 'https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz' && \
    tar -xf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz && \
    rm -f wkhtmltox-0.12.4_linux-generic-amd64.tar.xz && \
    ls -lah && \
    cd wkhtmltox/bin && \
    mv wkhtmltopdf /usr/local/bin/wkhtmltopdf && \
    mv wkhtmltoimage /usr/local/bin/wkhtmltoimage && \
    wkhtmltopdf --version && \
    wkhtmltoimage --version && \
    cd - && \
    rm -Rf wkhtmltox/

ENV TERM xterm

# Image optim libraries
RUN \
    apt-get install -y optipng pngquant pngcrush jpegoptim gifsicle && \
    mkdir -p /tmp/pngout && cd /tmp/pngout && wget -qq -O pngout.tar.gz http://static.jonof.id.au/dl/kenutils/pngout-20150319-linux.tar.gz && tar -xzvf pngout.tar.gz && mv pngout-20150319-linux/x86_64/pngout /usr/local/bin/pngout && which pngout && rm -Rf /tmp/pngout && \
    mkdir -p /tmp/jpegtran && cd /tmp/jpegtran && wget -qq -O jpegtran.tar.gz http://www.ijg.org/files/jpegsrc.v9b.tar.gz && tar -xzvf jpegtran.tar.gz && cd /tmp/jpegtran/jpeg-9b/ && ./configure && make && make test && make install && which jpegtran && rm -Rf /tmp/jpegtran

# Mailhog sendmail helper
ENV PATH $PATH:/home/www/go/bin
ENV GOPATH /home/www/go
RUN apt-get install -y golang-go && go get github.com/mailhog/mhsendmail && ln -s $(which mhsendmail) /usr/local/bin/mhsendmail && which mhsendmail

# Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer && \
    mkdir -p /home/www/.composer && \
    chown 1000:1000 -R /home/www/.composer

# Cleanup
RUN apt-get -y clean && apt-get -y purge && rm -rf /var/lib/apt/lists/* && rm -Rf /tmp/pear
RUN systemctl enable ssh && service ssh start

# ENV
VOLUME /app
WORKDIR /app
ENV TERM xterm

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
