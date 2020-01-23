FROM python:3.7-alpine

RUN set -ex \
  ; BLACK_VERSION="19.3b0" \
  ; pip install --no-cache-dir --disable-pip-version-check black==$BLACK_VERSION \
  ; black --version
