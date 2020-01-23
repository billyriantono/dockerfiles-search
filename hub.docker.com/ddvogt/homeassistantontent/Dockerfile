# See https://github.com/docker-library/php/blob/master/7.1/fpm/Dockerfile
FROM ddall/docker-php-ms

RUN apt-get update && apt-get install --no-install-recommends -y \
    apt-transport-https \
    libmcrypt-dev \
    g++ \
    unixodbc-dev \
    libxml2-dev \
    libssl-dev \
    openssl \
    openvpn \
    locales \
    supervisor

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen

# Install PHP extensions
RUN pecl install sqlsrv-4.3.0 \
    && pecl install pdo_sqlsrv-4.3.0 \
    && docker-php-ext-install \
        iconv \
        mbstring \
        intl \
        mcrypt \
        sockets \
        zip \
        xsl \
        json \
    && docker-php-ext-enable \
        sqlsrv \
        pdo_sqlsrv
			
ENV DEBIAN_FRONTEND=noninteractive
#  mssql
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/debian/8/prod.list | tee /etc/apt/sources.list.d/mssql-tools.list && \
    apt-get update && \
    ACCEPT_EULA=Y  apt-get install -y mssql-tools=14.0.7.0-1 msodbcsql=13.1.9.2-1 && touch /tmp/dawapsqlsrv

WORKDIR /var/www/symfony
