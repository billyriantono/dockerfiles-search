FROM alpine:latest
MAINTAINER Alexis Vuillaume <alexis.vuillaume@gmail.com>

RUN apk update \
    && apk add  --no-cache git build-base \
    && apk add python python-dev py-pip \
    && git clone https://github.com/xyrodileas/trape.git

RUN cat trape/requirements.txt
RUN pip install -r trape/requirements.txt

CMD python trape.py

WORKDIR /trape
