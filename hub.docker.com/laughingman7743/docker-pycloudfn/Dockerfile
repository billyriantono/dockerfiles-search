FROM python:3.5-jessie

RUN set -ex && \
    apt-get update && \
    apt-get install -y --no-install-recommends gettext-base && \
    pip install virtualenv pipenv pycloudfn
