#
# PHP-FPM 7.1 Dockerfile
#
# https://github.com/phalcon/dockerfiles
# https://gitlab.com/boxedcode/alpine-nginx-php-fpm
#

FROM boxedcode/alpine-nginx-php-fpm:v1.7.5

ENV PHALCON_VERSION=3.4.0

RUN apk add --update --no-cache curl && \
 	curl -sSL "https://codeload.github.com/phalcon/cphalcon/tar.gz/v${PHALCON_VERSION}" | tar -xz \
    && cd cphalcon-${PHALCON_VERSION}/build \
    && ./install \
    && cp ../tests/_ci/phalcon.ini $(php-config --configure-options | grep -o "with-config-file-scan-dir=\([^ ]*\)" | awk -F'=' '{print $2}') \
    && cd ../../ \
    && rm -r cphalcon-${PHALCON_VERSION}