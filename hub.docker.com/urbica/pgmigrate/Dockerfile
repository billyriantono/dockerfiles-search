FROM python:3.6
LABEL maintainer="Stepan Kuzmin <to.stepan.kuzmin@gmail.com>"

RUN set -ex && apt-get update && apt-get install -y --no-install-recommends \
  libpq-dev \
  && rm -rf /var/lib/apt/lists/* \
  && pip install psycopg2-binary yandex-pgmigrate

ENTRYPOINT ["pgmigrate"]