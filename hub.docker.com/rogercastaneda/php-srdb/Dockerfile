FROM alpine:3.4

LABEL version="0.1"
LABEL description="PHP 5.6.x for Search replace database utility"
LABEL maintainer="rogercastanedag@gmail.com"

RUN \
  apk update && apk add git php php5-ctype php5-pdo php5-pdo_mysql php5-pdo php5-pdo_mysql php5-common php5-mysqli

RUN git clone https://github.com/interconnectit/Search-Replace-DB.git /srdb

WORKDIR /srdb

