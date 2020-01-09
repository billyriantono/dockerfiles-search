FROM library/python:3.7.0-alpine3.8

RUN apk add build-base && \
    apk add portaudio-dev  && \
    apk add sqlite

RUN pip install webob

COPY anki-sync-server /app/anki-sync-server

WORKDIR /app/anki-sync-server

RUN \
    cd anki-bundled && \
    pip install -r requirements.txt && \
    mkdir /app/data && \
    cd /app/anki-sync-server

EXPOSE 27701
CMD python -m ankisyncd
