FROM php:5.6-fpm

ENV DEBIAN_FRONTEND noninteractive

# Set default date.timezone
RUN echo "date.timezone=UTC" > /usr/local/etc/php/conf.d/00-default.ini

# Non-root user uid:1000 / gid:1000
RUN \
    groupadd -g 1000 www &&  \
    useradd -u 1000 -g 1000 -ms /bin/bash www && \
    echo "alias ll='ls -lah'" >> /home/www/.bashrc && \
    mkdir -p /app

# PHP Configuration
RUN echo "LANG=\"en_US.UTF-8\"" > /etc/default/locale && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen

# Install dependencies
RUN \
    apt-get update && \
    # required packages for further setup
    apt-get install -y libsqlite3-dev zlib1g-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev libicu-dev libz-dev libmemcached-dev libcurl4-openssl-dev libxslt1-dev libffi-dev libssl-dev g++ gnupg2 imagemagick && \
    # default tools
    apt-get install -y git zip sudo locales vim nano telnet xvfb wget && \
    # Node packages
    wget -qO- https://deb.nodesource.com/setup_6.x | sudo bash - && \
    apt-get install -y nodejs && \
    node --version && \
    npm --version && \
    npm install -g grunt grunt-cli yarn gulp && \
    # Ruby
    apt-get install -y ruby ruby-dev && \
    ruby --version && \
    gem install --no-ri --no-rdoc sass && \
    which convert

# Download and install wkhtmltopdf
RUN \
    apt-get install -y build-essential xorg libssl-dev libxrender-dev wget && \
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
RUN apt-get install -y wget optipng pngquant pngcrush jpegoptim gifsicle
RUN mkdir -p /tmp/pngout && cd /tmp/pngout && wget -qq -O pngout.tar.gz http://static.jonof.id.au/dl/kenutils/pngout-20150319-linux.tar.gz && tar -xzvf pngout.tar.gz && mv pngout-20150319-linux/x86_64/pngout /usr/local/bin/pngout && which pngout
RUN mkdir -p /tmp/jpegtran && cd /tmp/jpegtran && wget -qq -O jpegtran.tar.gz http://www.ijg.org/files/jpegsrc.v9b.tar.gz && tar -xzvf jpegtran.tar.gz && cd /tmp/jpegtran/jpeg-9b/ && ./configure && make && make test && make install && which jpegtran

# Mailhog sendmail helper
ENV PATH $PATH:/home/www/go/bin
ENV GOPATH /home/www/go
RUN apt-get install -y golang-go && go get github.com/mailhog/mhsendmail && ln -s $(which mhsendmail) /usr/local/bin/mhsendmail && which mhsendmail

# PHP Configuration
RUN \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install -j$(nproc) mcrypt zip mbstring intl bcmath curl pdo_mysql mysql xsl soap && \
    pecl install xdebug-2.5.5 memcached-2.2.0 apcu-4.0.11 && \
    docker-php-ext-enable apcu && \
    docker-php-ext-enable memcached && \
    # Allow extension enable for the user "www"
    chown www:www -vR /usr/local/etc/php/conf.d/

# Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer && \
    mkdir -p /home/www/.composer && \
    chown 1000:1000 -R /home/www/.composer

# Cleanup
RUN apt-get -y clean && apt-get -y purge && rm -rf /var/lib/apt/lists/*

# ENV
VOLUME /app
WORKDIR /app
USER www
ENV TERM xterm
