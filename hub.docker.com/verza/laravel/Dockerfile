FROM ubuntu

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -yq --no-install-recommends \
    # Install mysql
    mysql-server \
    mysql-client \
    libmysqlclient-dev \
    curl \
    # Install git
    git \
    # Install apache
    apache2 \
    # Install php
    libapache2-mod-php \
    php-cli \
    php-json \
    php-curl \
    php-gd \
    php-mbstring \
    php-mysql \
    php-soap \
    php-xml \
    php-zip \
    php-intl \
    php-imagick \
    php-bcmath \
    php-ctype \
    php-tokenizer \
    # Install tools
    openssl \
    nano \
    wget \
    nodejs \
    npm \
    ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install mysql
RUN echo yes
VOLUME /var/lib/mysql        #change

RUN mkdir -p /var/run/mysqld   #change
RUN usermod -d /var/lib/mysql/ mysql
RUN find /var/lib/mysql -type f -exec touch {} \;        #change
RUN chown -R mysql:mysql /var/lib/mysql /var/run/mysqld  #change

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel
RUN composer global require laravel/installer

# Clear default index from apache2
RUN rm /var/www/html/index.html

# Add rewrite mode
RUN a2enmod rewrite

# Add Directory permission in 000-default.conf
RUN sed -i 's!/var/www/html!/var/www/html/public\n\t<Directory /var/www/html/public>\n\t    Options Indexes FollowSymLinks MultiViews\n\t    AllowOverride all\n\t    Order allow,deny\n\t    allow from all\n\t</Directory>!g' /etc/apache2/sites-available/000-default.conf

CMD mysqld
