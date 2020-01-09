# Alpine ARM32v7 image with the 'qemu-arm-static' already included
FROM balenalib/armv7hf-alpine:3.10

# Get build arguments (Version)
ARG VERSION=2.3.8
ARG BUILD_DATE=unknown
ARG BUILD_REF=unknown

# Set labels
LABEL build_version=$VERSION \
      build_date=$BUILD_DATE \
      build_reference=$BUILD_REF

# Fix iconv/musl 
RUN apk add --no-cache gnu-libiconv --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

# Copy configuration files
COPY root /

WORKDIR /var/www/wallabag

# Size improvement: removed 'mysql' related packages and all Python2 dependencies
# TODO: get rid of 'ansible' package (another 90MB+)
RUN set -ex \
     && apk add --no-cache ansible libwebp nginx pcre \
          php7 php7-amqp php7-bcmath php7-ctype php7-curl php7-dom php7-fpm php7-gd php7-gettext php7-iconv php7-json \
          php7-mbstring php7-openssl php7-pdo_pgsql php7-pdo_sqlite php7-phar php7-session php7-simplexml php7-sockets \
          php7-tidy php7-tokenizer php7-xml php7-xmlreader php7-zlib \
          py3-psycopg2 py3-simplejson rabbitmq-c s6 tzdata \
     # Install build dependencies
     && apk add --no-cache --virtual .build-dep git composer \
     # Create symbolic link to python3 to fix ansible error
     && ln -sf /usr/bin/python3 /usr/bin/python \
     # Disable detachedHead MASSIVE warning message
     && git -c advice.detachedHead=false clone --branch $VERSION --depth 1 https://github.com/wallabag/wallabag.git /var/www/wallabag \
     # Move parameters.yml to checkout (can only be done after clone)
     && mv /parameters.yml /var/www/wallabag/app/config/ \
     # Run composer
     && SYMFONY_ENV=prod composer install --no-dev --no-suggest --optimize-autoloader --prefer-dist --no-progress \
     && chown -R nobody:nobody /var/www/wallabag \
     # Clear composer cache
     && composer clear-cache \
     # Remove build dependencies
     && apk del --purge .build-dep

EXPOSE 80
ENTRYPOINT ["/entrypoint.sh"]
CMD ["wallabag"]
