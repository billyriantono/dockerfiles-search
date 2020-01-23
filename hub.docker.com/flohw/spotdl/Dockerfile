FROM python:3.6-alpine

RUN apk add --no-cache ffmpeg
RUN pip install --no-cache-dir spotdl

WORKDIR /music
VOLUME /music

ENTRYPOINT ["spotdl", "-f", "/music"]

