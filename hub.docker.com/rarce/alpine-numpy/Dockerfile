FROM python:3.6-alpine3.8

RUN set -ex ;\
  # install build dependencies
  apk add --no-cache \
    --virtual .build-deps \
    git gcc g++ make libffi-dev openssl-dev;\
  # install numpy
  pip install numpy;\
  # remove dependencies
  apk del --no-cache --purge .build-deps ;\
    rm -rf /var/cache/apk/*

CMD ["python"]
