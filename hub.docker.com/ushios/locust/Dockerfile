FROM python:3.6-alpine
LABEL maintainer "UshioShugo<ushio.s@gmail.com>"

ENV SOURCE_DIR="/opt/locust"

EXPOSE 5557 5558 8089

RUN apk update && \
    apk add --no-cache --virtual .zeromqbuild gcc g++ pkgconfig && \
    apk add --no-cache zeromq-dev musl-dev && \
    pip install pyzmq --install-option="--zmq=bundled" && \
    pip install locustio==0.8a2 && \
    apk del .zeromqbuild


WORKDIR $SOURCE_DIR

RUN chmod -R 755 $SOURCE_DIR

ENTRYPOINT ["locust"]
