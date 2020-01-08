ARG PHPCS_VERSION=3.3.2

FROM composer:latest AS composer

ARG PHPCS_VERSION
RUN composer require "squizlabs/php_codesniffer="${PHPCS_VERSION}""


FROM php:7.2-alpine

ARG BUILD_DATE
ARG VCS_REF
ARG PHPCS_VERSION

LABEL maintainer="Marco Gilbert <marco.gilbert@gmail.com>" \
    org.label-schema.build-date="${BUILD_DATE}" \
    org.label-schema.name="Docker image for PHP_CodeSniffer" \
    org.label-schema.description="PHP_CodeSniffer tokenizes PHP, JavaScript and CSS files and detects violations of a defined set of coding standards." \
    org.label-schema.vcs-url="https://github.com/ma-gi/docker-phpcs" \
    org.label-schema.vcs-ref="${VCS_REF}" \
    org.label-schema.version="${PHPCS_VERSION}" \
    org.label-schema.schema-version="1.0"

COPY --from=composer /app /app
COPY entrypoint.sh /sbin/entrypoint.sh

ENV PATH /app/vendor/bin:$PATH

# Install tools and configure phpcs
RUN apk --no-cache add bash patch \
    # use colors in output by default
    && phpcs --config-set colors 1 \
    # reports should fill the entire terminal width
    && phpcs --config-set report_width auto \
    && chmod a+x /sbin/entrypoint.sh

# Set the working directory to /mnt
WORKDIR /mnt
VOLUME /mnt

ENTRYPOINT ["/sbin/entrypoint.sh"]
CMD ["phpcs", "--version"]
