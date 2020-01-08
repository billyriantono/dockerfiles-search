FROM postgres:9.2

RUN apt-get update && apt-get install -y python-pip \
    python-dev \
    postgresql \
    python-psycopg2 \
    libpq-dev

RUN pip install --upgrade psycopg2
RUN pip install pgcli
