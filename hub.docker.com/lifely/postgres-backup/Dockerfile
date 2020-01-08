FROM ubuntu:16.04
LABEL maintainer="Dirk Kok dirk@lifely.nl"

ENV AWS_ACCESS_KEY_ID **None**
ENV AWS_SECRET_ACCESS_KEY **None**
ENV AWS_SSE_KEY **None**
ENV AWS_S3_BUCKET **None**
ENV AWS_S3_PREFIX backup
ENV AWS_S3_BACKUP_NAME **None**
ENV AWS_REGION eu-central-1
ENV SCHEDULE **None**

ENV POSTGRES_DB **None**
ENV POSTGRES_HOST "postgres"
ENV POSTGRES_PORT 5432
ENV POSTGRES_USER **None**
ENV POSTGRES_PASSWORD **None**
ENV POSTGRES_EXTRA_OPTS ''

ENV AWS_S3_ENABLE_VERSIONING **None**
ENV AWS_S3_LIFECYLCE_CONFIGURATION **None**
    
# Install everything and remove the bits we don't need anymore
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        wget \
        ca-certificates \
        curl \
        cron \
        python3-pip \
        python3-setuptools \
        python3-dev \
        python3-wheel \
    && pip3 install --upgrade pip \
    && pip install awscli \
    && echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
    && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
    && apt-get update && apt-get install -y --no-install-recommends postgresql-client-10 \
\
    && apt-get remove -y --purge --auto-remove \
        wget \
        curl \
        python3-setuptools \
        python3-dev \
        python3-wheel \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

# Add
ADD run.sh run.sh
ADD backup.sh backup.sh

CMD ["bash", "run.sh"]