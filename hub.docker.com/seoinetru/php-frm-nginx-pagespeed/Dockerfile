FROM richarvey/nginx-php-fpm:latest

RUN apk add --no-cache \
    nano \
    php-pdo \
    jpeg-dev \
    php7-bcmath \
    jpegoptim \
    optipng \
    pngquant\
    gifsicle\
    freetype-dev \
    php7-imagick 
    
       
COPY   conf/supervisord.conf /etc/supervisord.conf

RUN apk --no-cache upgrade && \
    scanelf --needed --nobanner --format '%n#p' /usr/sbin/nginx /usr/lib/nginx/modules/*.so /usr/local/bin/envsubst \
            | tr ',' '\n' \
            | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
            | xargs apk add --no-cache \
    && \
    apk add --no-cache tzdata

RUN install -g www-data -o www-data -d /var/cache/ngx_pagespeed && \
    mkdir -p /var/cache/nginx/{client_temp,fastcgi_temp,proxy_temp} && \
    mkdir -p /var/log/nginx
     

ADD conf/nginx-site.conf /var/www/html/nginx/default.conf
ADD conf/docker-vars.ini /usr/local/etc/php/conf.d/docker-vars.ini


# Copy our nginx config
RUN rm -Rf /etc/nginx/nginx.conf
ADD conf/nginx.conf /etc/nginx/nginx.conf

RUN pip install supervisor

CMD ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
#CMD ["/start.sh"] 
