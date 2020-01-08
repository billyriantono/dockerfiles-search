FROM php:cli-alpine

MAINTAINER Dmytro Sychevsky <sych@pdffiller.com>

ENV SELENOID_STATUS_URL="http://localhost:4444/status"

COPY selenoid-exporter.php selenoid-exporter.php

EXPOSE 9600

CMD php -S 0.0.0.0:9600 selenoid-exporter.php