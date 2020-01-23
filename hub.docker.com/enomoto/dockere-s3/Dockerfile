FROM alpine:3.9
LABEL maintainer="Enigma Algorithms"

RUN apk update \
  && apk add -qU --no-cache \
    coreutils \
    postgresql-client \
    openssl \
    python \
    py2-pip \
  && pip install awscli \
  && apk del py2-pip \
  && rm -r /root/.cache

ENV POSTGRES_DB **None**
ENV POSTGRES_DB_FILE **None**
ENV POSTGRES_HOST **None**
ENV POSTGRES_PORT 5432
ENV POSTGRES_USER **None**
ENV POSTGRES_USER_FILE **None**
ENV POSTGRES_PASSWORD **None**
ENV POSTGRES_PASSWORD_FILE **None**
ENV POSTGRES_EXTRA_OPTS ''
ENV S3_ACCESS_KEY_ID **None**
ENV S3_ACCESS_KEY_ID_FILE **None**
ENV S3_SECRET_ACCESS_KEY **None**
ENV S3_SECRET_ACCESS_KEY_FILE **None**
ENV S3_BUCKET **None**
ENV S3_REGION us-west-1
ENV S3_PREFIX 'backup'
ENV S3_ENDPOINT **None**
ENV S3_S3V4 no
ENV ENCRYPTION_PASSWORD **None**
ENV ENCRYPTION_PASSWORD_FILE **None**
ENV DROP_PUBLIC 'no'

ADD restore.sh restore.sh

CMD ["sh", "restore.sh"]
