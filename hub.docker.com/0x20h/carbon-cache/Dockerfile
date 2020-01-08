FROM python:2-alpine

MAINTAINER Jan Kohlhof <kohj@informatik.uni-marburg.de>

RUN apk --update add gcc musl-dev && \
    pip install https://github.com/graphite-project/whisper/tarball/master https://github.com/graphite-project/carbon/tarball/master && \
    apk del gcc musl-dev

COPY carbon.conf /opt/graphite/conf/carbon.conf
COPY storage-schemas.conf /opt/graphite/conf/storage-schemas.conf
COPY startup.sh /startup.sh

ENTRYPOINT ["/startup.sh"]
