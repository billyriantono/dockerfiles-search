FROM python:3.7.0-alpine3.8

RUN pip install --no-cache-dir schedule subliminal

RUN mkdir /.cache /tvshows \
 && chmod 777 /.cache /tvshows

COPY startup.sh /
COPY job.py /

VOLUME /tvshows /.cache

CMD ["/startup.sh"]

