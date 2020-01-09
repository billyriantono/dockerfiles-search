FROM php:7.3-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    mariadb-client \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    zlib1g-dev \
    libicu-dev \
    g++ \
    supervisor \
    apt-transport-https \
    gnupg2 \
    apt-utils \
    libzip-dev


# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql zip exif pcntl pdo bcmath
RUN docker-php-ext-configure gd
RUN docker-php-ext-configure intl
RUN docker-php-ext-install gd
RUN docker-php-ext-install intl

RUN touch /etc/apt/sources.list.d/nginx.list

RUN echo "deb http://nginx.org/packages/debian/ stretch nginx" > /etc/apt/sources.list.d/nginx.list
RUN echo "deb-src http://nginx.org/packages/debian/ stretch nginx" >> /etc/apt/sources.list.d/nginx.list

RUN curl -L https://nginx.org/keys/nginx_signing.key | apt-key add -
RUN apt-get update
RUN apt-get install nginx -y

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

COPY supervisor.conf /etc/supervisor/conf.d/supervisor.conf
COPY nginx.conf /etc/nginx/nginx.conf

# Forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log \
	&& ln -sf /dev/stderr /var/log/php7.2-fpm.log

# Create the directory for the app files
RUN mkdir -p /var/www/app

# Run supervisor (PHP-FPM and NGINX)
CMD ["/usr/bin/supervisord"]