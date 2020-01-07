FROM alpine:3.7

ARG MONGODB_VERSION="3.5"
ARG MONGODB_HOST="localhost"
ARG MONGODB_PORT="27017"
ARG PGP_FILE="/run/secrets/pgp-key"
ARG CRON_TIME="0 4 */2 * *"

ARG VERSION="0.0.1"

ENV \
  MONGODB_VERSION=${MONGODB_VERSION} \
  MONGODB_HOST=${MONGODB_HOST} \
  MONGODB_PORT=${MONGODB_PORT} \
  MONGODB_USER= \
  MONGODB_PASS= \
  MONGODB_DATABASE= \
  EXTRA_OPTS= \
  BACKUP_NAME= \
  PGP_FILE=${PGP_FILE} \
  CRON_TIME=${CRON_TIME} \
  AWS_ACCESS_KEY_ID= \
  AWS_SECRET_ACCESS_KEY= \
  S3_BUCKET_URL= \
  AWS_DEFAULT_REGION=

LABEL \
  se.vimla.version=${VERSION} \
  vendor="vimla.se"

RUN \
  apk -Uuv add python py-pip "mongodb-tools<${MONGODB_VERSION}" bash gnupg file \
    && pip install awscli \
    && apk --purge -v del py-pip \
    && rm /var/cache/apk/*

COPY ./entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
