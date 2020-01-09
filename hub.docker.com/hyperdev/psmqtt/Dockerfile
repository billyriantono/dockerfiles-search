FROM python:2.7-alpine

RUN apk add --no-cache --virtual .build-deps linux-headers make gcc g++ \
    && pip install recurrent paho-mqtt python-dateutil psutil jinja2 \
    && apk del .build-deps

WORKDIR /usr/src/app
ADD . .

ENTRYPOINT [ "python" ]
CMD [ "psmqtt.py" ]