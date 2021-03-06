FROM benyanke/php7:7.2

MAINTAINER "Ben Yanke" <ben@benyanke.com>

# Laravel container command controls
# Set to '1' to run these commands from running on container start
ENV CMD_ROOT /var/www
ENV RUN_PERMISSION_FIX 0
ENV RUN_COMPOSER 0
ENV RUN_WEBPACK 0
ENV RUN_MIGRATIONS 0
ENV RUN_DB_SEED 0
ENV RUN_VENDOR_PUBLISH 0

WORKDIR /tmp

# Install dumb-init
RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 && chmod +x /usr/local/bin/dumb-init

# Install Nginx
RUN apt-get update && DEBIAN_FRONTEND=noninteractive \
    apt-get install -y \
      nginx \
      php7.2-fpm \
      php7.2-bcmath \
      npm \
      libpng-dev \
      supervisor \
    && apt-get clean && rm -rf /var/lib/apt/lists/* && \
    npm install npm@latest -g

RUN mkdir -p /etc/nginx /var/run/php /var/log/supervisor

# Copy in config files
COPY nginx.conf /etc/nginx/nginx.conf
#COPY nginx-supervisor-7.2.conf /etc/supervisor/conf.d/nginx.conf
COPY nginx-supervisor-7.2.conf /etc/supervisor/conf.d/nginx-72.conf
COPY www.conf /etc/php/7.2/fpm/pool.d/www.conf
COPY startup.sh /opt/startup/startup.sh

# Log nginx to STDOUT and STDERR
RUN ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log

# Copy enabled modules from CLI dir to the new FPM module, so that any modules added and enabled to
# CLI in the parent image are now available to FPM as well
RUN cp -a /etc/php/7.2/cli/conf.d/* /etc/php/7.2/fpm/conf.d

VOLUME ["/var/www", "/etc/nginx/sites-enabled", "/opt/startup"]

EXPOSE 80

# Set workdir back to www dir so that console users are in right position
WORKDIR /var/www

# Add composer bin path
ENV PATH="/var/www/vendor/bin:${PATH}"

ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]

CMD ["/bin/bash", "-c", "/bin/bash /opt/startup/startup.sh && /usr/bin/supervisord -c /etc/supervisor/supervisord.conf"]
