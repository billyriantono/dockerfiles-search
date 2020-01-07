FROM python:2.7

RUN apt-get update && apt-get install -y \
        gcc \
        gettext \
        mysql-client libmysqlclient-dev \
        postgresql-client libpq-dev \
        sqlite3 \
        git \
        ssh-client \
    --no-install-recommends && rm -rf /var/lib/apt/lists/*

ENV DJANGO_VERSION 1.9

RUN pip install mysqlclient psycopg2 django=="$DJANGO_VERSION"

ADD install.sh ./

