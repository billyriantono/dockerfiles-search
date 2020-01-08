FROM svlentink/psycopg2

RUN echo "http://mirror.leaseweb.com/alpine/edge/testing" >> /etc/apk/repositories \
    && echo "http://dl-8.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && apk update && apk add --no-cache geos-dev gfortran openblas-dev \
    && pip install shapely numpy scipy \
    && rm -rf /var/cache/apk/*
