FROM composer:latest AS magento-composer
WORKDIR /magento
COPY *.json ./

RUN composer install --ignore-platform-reqs

FROM alpine AS magento-files

RUN apk update
RUN apk add zip

WORKDIR /magento
COPY --from=magento-composer /magento ./
RUN zip -r /magento.zip ./

FROM alpine AS magento-zip
COPY --from=magento-files /magento.zip /