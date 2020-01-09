FROM clonm/php:7.2

ENV PHPPGADMIN_HOST pgsql
ENV PHPPGADMIN_PORT 5432

RUN apt-get update -q -q && \
 apt-get install phppgadmin --yes && \
 apt-get install postgresql-client --no-install-recommends --yes && \
 sed -i 's/.*<h1>.*<\/h1>.*//' /usr/share/phppgadmin/intro.php

COPY ./etc /etc
