FROM phpmyadmin/phpmyadmin:4.8.4

RUN apk --update add --no-cache \
    ca-certificates \
    wget \
    unzip

# Install consul-template
ENV CONSUL_TEMPLATE_VERSION=0.19.4 \
    CONSUL_TEMPLATE_SHA256=5f70a7fb626ea8c332487c491924e0a2d594637de709e5b430ecffc83088abc0 \
    CONSUL_TEMPLATE_LOG_LEVEL=info

RUN wget -q -O /tmp/consul-template.zip https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip \
    && echo "${CONSUL_TEMPLATE_SHA256}  /tmp/consul-template.zip" | sha256sum -c - \
    && unzip -d /usr/local/bin /tmp/consul-template.zip \
    && chmod +x /usr/local/bin/consul-template \
    && rm /tmp/consul-template.zip

ENV PHP_REDIS=4.2.0 \
    PHP_REDIS_SHA256=73a8f99e6594b8114d7ee5627000097797077e26f78e33963fe31908ac31e8f8

RUN wget https://github.com/phpredis/phpredis/archive/${PHP_REDIS}.tar.gz -O /tmp/php-redis.tar.gz && \
    echo "${PHP_REDIS_SHA256}  /tmp/php-redis.tar.gz" | sha256sum -c - && \
    cd /tmp && tar xvf php-redis.tar.gz && \
    docker-php-ext-configure || true && \
    mv /tmp/phpredis-4.2.0 /usr/src/php/ext/redis && \
    docker-php-ext-install redis && \
    rm /tmp/php-redis.tar.gz

COPY etc/supervisor.d/consul-template.ini /etc/supervisor.d/consul-template.ini
COPY consul-template/ /srv
