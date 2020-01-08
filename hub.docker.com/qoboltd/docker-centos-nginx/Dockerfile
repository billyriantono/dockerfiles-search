FROM qoboltd/docker-centos-php:7.1

# Install PHP and Tools 
RUN yum -y install --setopt=tsflags=nodocs php-fpm \
    nginx \
    && yum clean all \
    && rm -rf /var/cache/yum

COPY www.conf /etc/php-fpm.d/
COPY nginx.conf /etc/nginx/
COPY default.conf /etc/nginx/conf.d/
COPY php.ini /etc/

RUN USER=nginx && \
    GROUP=nginx && \
    curl -SsL https://github.com/boxboat/fixuid/releases/download/v0.4/fixuid-0.4-linux-amd64.tar.gz | tar -C /usr/bin -xzf - && \
    chown root:root /usr/bin/fixuid && \
    chmod 4755 /usr/bin/fixuid && \
    mkdir -p /etc/fixuid && \
    printf "user: $USER\ngroup: $GROUP\npaths:\n  - /run/php-fpm\n  - /var/www/html\n  - /var/cache/nginx\n  - /var/lib/php\n  - /var/log/php-fpm\n  - /var/log/nginx\n  - /var/lib/nginx\n" > /etc/fixuid/config.yml

RUN mkdir -p /run/php-fpm \
    && mkdir -p /var/www/html \
    && mkdir -p /var/cache/nginx \
    && mkdir -p /run/nginx \
    && chown nginx:nginx /run/php-fpm -R \
    && chown nginx:nginx /run/nginx -R \
    && chmod a+rwX /run/nginx -R \
    && chown nginx:nginx /var/lib/php -R \
    && chown nginx:nginx /var/www -R \
    && chown nginx:nginx /var/log/php-fpm -R \
    && chown nginx:nginx /var/cache/nginx -R

COPY run.sh /opt/

EXPOSE 80

USER nginx:nginx
CMD ["/opt/run.sh"]
