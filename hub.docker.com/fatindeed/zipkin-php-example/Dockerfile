FROM php:alpine

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL maintainer="James Zhu <168262+fatindeed@users.noreply.github.com>" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="fatindeed/zipkin-php-example" \
      org.label-schema.description="See how much time php services spend on an http request" \
      org.label-schema.url="https://hub.docker.com/r/fatindeed/zipkin-php-example" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/fatindeed/zipkin-php-example" \
      org.label-schema.vendor="James Zhu" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

ENV HTTP_REPORTER_URL="http://zipkin:9411/api/v2/spans"

COPY *.php composer.json /var/www/html/
WORKDIR /var/www/html

RUN set -e; \
    curl -sSL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    composer install --no-dev; \
    { \
        echo '#!/bin/sh'; \
        echo 'cd /var/www/html'; \
        echo 'php -S localhost:9000 backend.php &'; \
        echo 'php -S 0.0.0.0:8081 frontend.php'; \
    } | tee /usr/local/bin/run-example.sh; \
    chmod a+x /usr/local/bin/run-example.sh;

CMD [ "/usr/local/bin/run-example.sh" ]