###
# Bootstrap image
#
FROM php:7.0-fpm AS builder

# Prepare build environment
ARG ARTIFACT_DIR=/artifacts
ARG BUILD_DIR=/build
RUN set -x && \
    mkdir -p ${ARTIFACT_DIR} ${BUILD_DIR} && \
    apt-get update

# Install aws-env
ARG AWS_ENV_VERSION=f6b72b9a61602f60b161590516dac2226e0cf197
ADD https://github.com/Droplr/aws-env/raw/${AWS_ENV_VERSION}/bin/aws-env-linux-amd64 ${ARTIFACT_DIR}/aws-env
RUN chmod +x ${ARTIFACT_DIR}/aws-env

# Install dockerize
ARG DOCKERIZE_VERSION=v0.6.1
ADD https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz ${BUILD_DIR}/dockerize.tar.gz
RUN tar -C ${ARTIFACT_DIR} -xzvf ${BUILD_DIR}/dockerize.tar.gz

# Install composer
ADD https://getcomposer.org/installer ${BUILD_DIR}/composer-setup.php
RUN set -x && \
    EXPECTED_SIGNATURE=$(php -r "echo file_get_contents('https://composer.github.io/installer.sig');") && \
    ACTUAL_SIGNATURE=$(php -r "echo hash_file('SHA384', '${BUILD_DIR}/composer-setup.php');") && \
    if [ "${EXPECTED_SIGNATURE}" != "${ACTUAL_SIGNATURE}" ]; then \
        echo 'ERROR: Invalid installer signature' >&2 && \
        exit 1; \
    fi; \
    \
    apt-get install -y --no-install-recommends git unzip  && \
    php ${BUILD_DIR}/composer-setup.php \
        --quiet \
        --install-dir=${ARTIFACT_DIR} \
        --filename=composer


###
# Final image
#
FROM php:7.0-fpm

COPY --from=builder /artifacts /usr/local/bin/
COPY bin /usr/local/bin/

# Install template for FPM configuration
ENV EXTRAS_PATH=/opt
COPY templates ${EXTRAS_PATH}/templates/

ARG DEPS_BZ2="libbz2-dev"
ARG DEPS_COMPOSER="git unzip"
ARG DEPS_INTL="g++ libicu-dev zlib1g-dev"
ARG DEPS_MCRYPT="libmcrypt-dev"
ARG EXT_VER_APCU=5.1.8
ARG EXT_VER_XDEBUG=2.5.0
ARG EXTS_SRC="bz2 intl mcrypt pdo_mysql"

RUN set -x && \
    apt-get update && \
    \
# Install package dependencies
    apt-get install -y --no-install-recommends \
        ${DEPS_BZ2} \
        ${DEPS_COMPOSER} \
        ${DEPS_INTL} \
        ${DEPS_MCRYPT} \
    && \
    \
# Install PHP extensions
    docker-php-ext-install -j$(nproc) ${EXTS_SRC} && \
    docker-php-pecl-install apcu-${EXT_VER_APCU} && \
    docker-php-pecl-install xdebug-${EXT_VER_XDEBUG} && \
    docker-php-ext-enable apcu opcache && \
    \
# Cleanup
    apt-get purge -y --auto-remove \
        -o APT::AutoRemove::RecommendsImportant=false \
        -o APT::AutoRemove::SuggestsImportant=false \
        g++ \
    && \
    rm -rf /var/lib/apt/lists/*
