FROM python:3-slim

RUN pip install 'mongo-connector[elastic5]==2.5.1'

VOLUME /data
WORKDIR /data

ENTRYPOINT ["/usr/local/bin/mongo-connector"]
CMD ["--help"]
