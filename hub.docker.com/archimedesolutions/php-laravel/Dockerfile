# ModeSec Build
FROM ubuntu:18.04 as modsecurity-build
LABEL maintainer="Salvatore BROSIO <tools@archimedesolutions.it>"

# ENV
ENV DEBIAN_FRONTEND noninteractive
# Install Prereqs
RUN apt-get update -qq && \
    apt install -qq -y --no-install-recommends --no-install-suggests \
        apt-transport-https \
        apt-utils \
        autoconf \
        automake \
        build-essential \
        ca-certificates \
        dirmngr \
        git \
        libcurl4-openssl-dev \
        libgd-dev \
        libgeoip-dev \
        liblmdb-dev \
        libpcre++-dev \
        libssl-dev \
        libtool \
        libxml2-dev \
        libyajl-dev \
        lsb-release \
        lua5.2-dev \
        openssl \
        pkgconf \
        software-properties-common \
        tree \
        wget \
        zlib1g-dev
RUN cd /opt && \
    git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity && \
    cd ModSecurity && \
    git submodule init && \
    git submodule update && \
    ./build.sh && \
    ./configure && \
    make && \
    make install
RUN cd /opt && \
    git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git
RUN cd /opt && \
    wget http://nginx.org/download/nginx-1.17.1.tar.gz && \
    tar zxvf nginx-1.17.1.tar.gz && \
    cd nginx-1.17.1 && \
    ./configure --with-compat --add-dynamic-module=../ModSecurity-nginx && \
    make modules

# Final Step
FROM ubuntu:18.04
# Add wait-for-it
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /bin/wait-for-it.sh
# Add S6 supervisor (for graceful stop)
ADD https://github.com/just-containers/s6-overlay/releases/download/v1.22.1.0/s6-overlay-amd64.tar.gz /tmp/
RUN chmod 700 /bin/wait-for-it.sh && \
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && \
    rm /tmp/s6-overlay-amd64.tar.gz
ENTRYPOINT ["/init"]
CMD []
# Disable frontend dialogs
ENV DEBIAN_FRONTEND noninteractive
ENV PHP_VERSION 7.2
ENV PATH $PATH:/root/composer/vendor/binf
# Add packages
RUN apt-get update && apt-get install -qq --no-install-recommends --no-install-suggests \
    ca-certificates \
    software-properties-common \
    curl \
    gpg-agent \
    lsb-release \
    inetutils-syslogd && \
    echo "deb http://nginx.org/packages/mainline/ubuntu `lsb_release -cs` nginx" | tee /etc/apt/sources.list.d/nginx.list && \
    curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add - && \
    LC_ALL=C.UTF-8 apt-add-repository ppa:ondrej/php -y && \
    apt-get update && apt-get install -y \
    cron \
    git \
    gnupg2 \
    libgeoip-dev \
    libyajl-dev \
    lua5.2-dev \
    locales \
    nginx \
    php${PHP_VERSION}-apcu \
    php${PHP_VERSION}-bcmath \
    php${PHP_VERSION}-cli \
    php${PHP_VERSION}-curl \
    php${PHP_VERSION}-fpm \
    php${PHP_VERSION}-gd \
    php${PHP_VERSION}-intl \
    php${PHP_VERSION}-json \
    php${PHP_VERSION}-mysql \
    php${PHP_VERSION}-mbstring \
    php${PHP_VERSION}-opcache \
    php${PHP_VERSION}-soap \
    php${PHP_VERSION}-sqlite3 \
    php${PHP_VERSION}-xml \
    php${PHP_VERSION}-zip \
    php-ast \
    php-gettext \
    unzip \
    htop \
    mc \
    nano \
    zip && \
    apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* && \
    locale-gen it_IT.UTF-8 && \
    dpkg-reconfigure locales && \
    mkdir -p /run/php && chmod -R 750 /run/php && \
    sed -i 's|.*expose_php =.*|expose_php = Off|g' /etc/php/${PHP_VERSION}/fpm/php.ini && \
    sed -i 's|.*max_input_vars =.*|max_input_vars = 3000|g' /etc/php/${PHP_VERSION}/fpm/php.ini && \
    sed -i 's|.*memory_limit =.*|memory_limit = 256M|g' /etc/php/${PHP_VERSION}/fpm/php.ini && \
    sed -i 's|.*post_max_size =.*|post_max_size = 256M|g' /etc/php/${PHP_VERSION}/fpm/php.ini && \
    sed -i 's|.*upload_max_filesize =.*|upload_max_filesize = 256M|g' /etc/php/${PHP_VERSION}/fpm/php.ini && \
    sed -i 's|.*variables_order =.*|variables_order = GPCS|g' /etc/php/${PHP_VERSION}/fpm/php.ini && \
    sed -i 's|.*error_log =.*|error_log=/proc/self/fd/2|g' /etc/php/${PHP_VERSION}/fpm/php-fpm.conf && \
    sed -i 's|.*listen.mode =.*|listen.mode = 0660|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*pm.max_children =.*|pm.max_children = 150|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*pm.start_servers =.*|pm.start_servers = 10|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*pm.min_spare_servers =.*|pm.min_spare_servers = 4|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*pm.max_spare_servers =.*|pm.max_spare_servers = 24|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*pm.max_requests =.*|pm.max_requests = 1000|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*listen =.*|listen=9000|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*access.log =.*|access.log=/proc/self/fd/2|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*user\s*=.*|user = www-data|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*group\s*=.*|group = www-data|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i "s|.*catch_workers_output\s*=\s*yes|catch_workers_output = no|g" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed -i 's|.*clear_env\s*=.*|clear_env = no|g' /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY --from=modsecurity-build /usr/local/modsecurity/ /usr/local/modsecurity/
COPY --from=modsecurity-build /opt/nginx-1.17.1/objs/ngx_http_modsecurity_module.so /etc/nginx/modules
COPY --from=modsecurity-build /opt/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsecurity.d/modsecurity.conf
COPY --from=modsecurity-build /opt/ModSecurity/unicode.mapping /etc/nginx/modsecurity.d

# Apply cron job / NGINX
COPY cron/laravel /tmp/laravel
COPY config/nginx.modsec.conf /etc/nginx/nginx.conf

# Copy CRON PHP-FPM NGINX service script
COPY config/start-cron.sh /etc/services.d/cron/run
COPY config/start-env-cron.sh /etc/services.d/env/run
COPY config/start-fpm.sh /etc/services.d/php_fpm/run
COPY config/start-nginx.sh /etc/services.d/nginx/run
COPY config/start-queue.sh /etc/services.d/queue/run
RUN ln -s $(composer config --global home) /root/composer && \
    usermod -u 1000 www-data && \
    crontab -l -u www-data | cat - /tmp/laravel | crontab -u www-data - && \
    rm /tmp/laravel && \
    chmod 750 /etc/services.d/cron/run && \
    chmod 750 /etc/services.d/env/run && \
    chmod 750 /etc/services.d/php_fpm/run && \
    chmod 750 /etc/services.d/nginx/run && \
    chmod 750 /etc/services.d/queue/run && \
    chmod 644 /etc/nginx/modules/ngx_http_modsecurity_module.so && \
    echo "include /etc/nginx/modsecurity.d/modsecurity.conf" >> /etc/nginx/modsecurity.d/include.conf && \
    cd /tmp && \
    ## Get ModSecurity CRS
    git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git && \
    ## Install ModSecurity CRS
    touch /etc/nginx/modsecurity.d/crs.conf && \
    cat /tmp/owasp-modsecurity-crs/crs-setup.conf.example /tmp/owasp-modsecurity-crs/rules/*.conf >> /etc/nginx/modsecurity.d/crs.conf && \
    cp /tmp/owasp-modsecurity-crs/rules/*.data /etc/nginx/modsecurity.d/ && \
    rm -rf /tmp/owasp-modsecurity-crs && \
    echo "include /etc/nginx/modsecurity.d/crs.conf" >> /etc/nginx/modsecurity.d/include.conf && \
    sed -i -e 's/SecRuleEngine DetectionOnly/SecRuleEngine On/g' /etc/nginx/modsecurity.d/modsecurity.conf