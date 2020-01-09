FROM python:alpine

WORKDIR /app

RUN apk add --no-cache --virtual deps alpine-sdk

RUN apk add --no-cache graphviz-dev && \
        pip install eralchemy && \
        apk del deps

CMD [ "eralchemy" ]
