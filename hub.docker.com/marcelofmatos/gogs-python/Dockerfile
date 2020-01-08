FROM gogs/gogs


RUN apk add --update python python-dev py-pip build-base \
    && pip install --upgrade pip \
    && pip install websocket-client \
    && pip install gdapi-python

