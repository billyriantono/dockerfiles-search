FROM python:2.7.15-alpine3.8

RUN apk update && \ 
    apk add git && \
    git clone https://github.com/oliverlorenz/mqtt-watchdir.git && \
    cd mqtt-watchdir && \
    python setup.py develop && \
    rm -rf /var/cache/apk/*

CMD python mqtt-watchdir/mqtt-watchdir.py