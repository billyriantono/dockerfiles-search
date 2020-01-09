FROM php:7.2-fpm
RUN apt-get update
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        zlib1g-dev \
        libxml2 \
        libxml2-dev \
        git

RUN docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install soap \
    && docker-php-ext-install sockets \
    && docker-php-ext-install pdo_mysql

RUN pecl install mcrypt-1.0.1 && docker-php-ext-enable mcrypt

RUN /usr/local/bin/php -r "readfile('https://getcomposer.org/installer');" | /usr/local/bin/php && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer
RUN composer self-update
RUN composer global require "laravel/lumen-installer"
RUN ln -s ~/.composer/vendor/bin/lumen /usr/local/bin/lumen
RUN composer global require zircote/swagger-php
RUN ln -s ~/.composer/vendor/bin/swagger /usr/local/bin/swagger
RUN pecl install xdebug && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so\nxdebug.overload_var_dump=1" > /usr/local/etc/php/conf.d/xdebug.ini
RUN apt-get install -y ghostscript
RUN apt-get install -y poppler-utils
RUN apt-get install -y supervisor
RUN apt-get install -y procps
RUN apt-get install -y cron

RUN apt-get install -y gnupg &&\
    curl -sL https://deb.nodesource.com/setup_8.x | bash -&&\
    apt-get install -yq gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 \
    libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 \
    libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 \
    libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 \
    fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-kacst ttf-freefont \
    ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils&&\
    apt-get install -y nodejs&&\
    export NODE_PATH=/usr/lib/node_modules&&\
    npm install -g puppeteer --unsafe-perm=true --allow-root&&\
    npm install -g request&&\
    npm install -g async-redis&&\
    chown -R www-data:www-data /usr/lib/node_modules

ADD ./ssh_keys /root/.ssh
RUN chown root:root /root/.ssh \
    && chmod 700 /root/.ssh \
    && chmod 600 /root/.ssh/*

ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 /usr/local/bin/dumb-init
RUN chmod +x /usr/local/bin/dumb-init

RUN curl "https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz" -L -o "wkhtmltopdf.tar.xz" &&\
        tar Jxvf wkhtmltopdf.tar.xz &&\
        mv wkhtmltox/bin/wkhtmltopdf /usr/local/bin/wkhtmltopdf &&\
        mv wkhtmltox/include/wkhtmltox /usr/local/include/ &&\
        mv wkhtmltox/lib/* /usr/local/lib/ &&\
        rm -rf wkhtmltox*

ADD start.sh /start.sh

ENTRYPOINT ["dumb-init", "--"]
CMD /start.sh
EXPOSE 9000
