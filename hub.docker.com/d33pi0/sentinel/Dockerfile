FROM debian:stable

RUN set -x \
  && apt-get update \
  && apt-get install -yq \
    python3 \
    python3-pip \
    vim

COPY ./Sentinel /code/Sentinel
RUN set -x \
  && pip3 install -r /code/Sentinel/requirements/api_v1.txt

COPY ./scripts/start.sh /code/start
RUN set -x \
  && chmod +x /code/start

COPY ./scripts/start-celery.sh /code/start-celery
RUN set -x \
  && chmod +x /code/start-celery