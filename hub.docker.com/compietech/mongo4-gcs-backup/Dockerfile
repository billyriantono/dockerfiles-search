FROM alpine:3.8

RUN apk update

RUN apk add libssl1.1 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/main
RUN apk add mongodb-tools --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community
RUN apk add --update \
#  mongodb-tools \
  curl \
  python \
  py-pip \
  py-cffi \
  && pip install --upgrade pip \
  && apk add --virtual build-deps \
  gcc \
  libffi-dev \
  python-dev \
  linux-headers \
  musl-dev \
  openssl-dev \
  && pip install gsutil \
  && apk del build-deps \
  && rm -rf /var/cache/apk/*

ADD ./backup.sh /mongodb-gcs-backup/backup.sh
ADD ./initialize.sh /mongodb-gcs-backup/initialize.sh
WORKDIR /mongodb-gcs-backup

RUN chmod +x /mongodb-gcs-backup/backup.sh
RUN chmod +x /mongodb-gcs-backup/initialize.sh

CMD ["/mongodb-gcs-backup/initialize.sh"]