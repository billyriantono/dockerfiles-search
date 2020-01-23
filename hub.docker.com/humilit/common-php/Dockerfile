FROM humilit/common:1.0.1
LABEL maintainer="robert.brendler+github@gmail.com"

ENV PHP_TIME_LIMIT=10
ENV PHP_MEMORY_LIMIT=64M
ENV PHP_POST_SIZE_LIMIT=8M
ENV PHP_UPLOAD_SIZE_LIMIT=8M

COPY content /
RUN common-php-setup

