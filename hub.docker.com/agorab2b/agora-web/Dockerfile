FROM python:2.7

RUN mkdir /agora \
 && mkdir -p /agora-web/static \
 && mkdir -p /agora-web/media

COPY ./entrypoint.sh /entrypoint.sh
COPY ./entrypoint-lite.sh /entrypoint-lite.sh
COPY ./entrypoint-test.sh /entrypoint-test.sh
COPY requirements.txt /agora/requirements.txt

RUN apt-get update \
 && apt-get install gettext -y \
 && pip install django==1.6.11 \
 && pip install -r /agora/requirements.txt

WORKDIR /agora

CMD ["./entrypoint.sh"]
