FROM treillage/base-php:latest
LABEL maintainer="Meraj Sahebdar <itsdrewstiles@gmail.com>" \
    com.treillage.name="bedrock" \
    com.treillage.vendor="treillage" \
    com.treillage.vcs-url="https://github.com/treillage/images" \
    com.treillage.version="1.0.0" \
    com.treillage.license="MIT"

ENV WP_ENV="development" \
    DB_PREFIX="wp_"

COPY add-on/ /opt/

RUN set -x \
    # Download and Install bedrock
    && su-exec app curl -sSL "https://github.com/roots/bedrock/archive/1.12.7.tar.gz" | su-exec app tar -xzC /www --strip-components 1 \
    && su-exec app composer install --no-interaction --working-dir /www \
    && image-build \
    && image-clean
