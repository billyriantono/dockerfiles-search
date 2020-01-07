# Builds and generates from scratch the static API, served with nginx

# FROM itsjavi/veekun-pokedex-data:2018 as pokedata_db
FROM python:2.7-slim as pokedata_db

RUN apt-get update > /dev/null && \
    apt-get upgrade -y > /dev/null && \
    apt-get install -y --no-install-recommends git gcc libpq-dev python-dev python-distribute > /dev/null && \
    pip install --upgrade pip && \
    pip install --no-cache-dir virtualenv psycopg2 pymysql > /dev/null

WORKDIR /app

# The following conditional runs make this stage separately (--target=pokedata_db) with a mounted /app dir
# and also compatible running this step standalone.

RUN git clone https://github.com/veekun/pokedex.git /app; \
    cd /app && git checkout 18925edcd3ad71dd912a94ce4b1bc1435943937a

RUN echo "Building the bin/pokedex executable ..."; \
    virtualenv /app --python=python2; \
    cd /app; \
    bin/python setup.py develop;

RUN bin/pokedex load

ENTRYPOINT [ "bin/pokedex", "help" ]

# ---

FROM php:7.3.0-cli-stretch as pokedata_generator

RUN apt-get update -qq && apt-get install -qqy --no-install-recommends \
    apt-utils gettext-base pandoc \
    build-essential make \
    apt-transport-https ca-certificates \
    curl git unzip sqlite sqlite3 libsqlite3-dev \
    libzip-dev zip \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip

WORKDIR /app
ADD . /app

RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && composer --version \
    && mkdir -p /app/var/data/pokedata

COPY --from=pokedata_db /app/pokedex/data/pokedex.sqlite /app/var/data/pokedata
COPY --from=pokedata_db /app/pokedex/data/csv /app/var/data/pokedata/csv

RUN mv /app/var/data/pokedata/pokedex.sqlite /app/var/data/pokedata/db.sqlite && \
    ls -lh /app/var/data/pokedata

RUN cd /app && make install && make api && make api-docs

RUN echo "<!DOCTYPE html><html lang=\"en\">" > /app/build/index.html && \
    echo "<head><meta charset=\"UTF-8\"><title>PokéData</title></head><body>" >> /app/build/index.html && \
    pandoc -f markdown /app/README.md >> /app/build/index.html && \
    echo "</body></html>" >> /app/build/index.html

# ---

FROM nginx:1.15-alpine as pokedata_api

WORKDIR /usr/share/nginx/html

RUN rm -rf /usr/share/nginx/html/*
COPY --from=pokedata_generator /app/build .

RUN ls -lh ./ && ls -lh ./api && ls -lh ./docs

EXPOSE 80
