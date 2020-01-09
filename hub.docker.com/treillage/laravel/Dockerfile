FROM treillage/base-php:latest
LABEL maintainer="Meraj Sahebdar <itsdrewstiles@gmail.com>" \
    com.treillage.name="laravel" \
    com.treillage.vendor="treillage" \
    com.treillage.vcs-url="https://github.com/treillage/images" \
    com.treillage.version="1.0.0" \
    com.treillage.license="MIT"

COPY add-on/ /opt/

RUN set -x \
    # Download and Install laravel
    && su-exec app curl -sSL "https://github.com/laravel/laravel/archive/v5.8.16.tar.gz" | su-exec app tar -xzC /www --strip-components 1 \
    && su-exec app composer install --no-interaction --working-dir /www \
    && image-build \
    && image-clean
