FROM phosfato/php7.2-fpm AS builder

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -yq && \
    apt-get upgrade -yq &&  \
    apt-get install -yq \
        composer && \
    # remove files left by `apt-get update`
    rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/magento2

COPY ./magento2 .

ARG COMPOSER_ALLOW_SUPERUSER=1
RUN composer install


FROM phosfato/php7.2-fpm

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -yq && \
    apt-get upgrade -yq &&  \
    apt-get install -yq \
        lsof \
        mysql-client-5.7 && \
    # remove files left by `apt-get update`
    rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/magento2

COPY --from=builder /var/www/magento2 .

# setup a MTA (mail trasnsport agent) see if we need one
# maybe it's using an online service
