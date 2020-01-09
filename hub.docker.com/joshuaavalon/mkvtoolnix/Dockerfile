FROM python:alpine

RUN mkdir /data && \
    apk add --no-cache mkvtoolnix && \
    pip install pysubs2

WORKDIR /data

CMD ["/bin/sh"]
