FROM python:3.7-alpine

RUN pip install elasticsearch-curator

COPY ./curator.yml /
COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["curator", "--config", "/curator.yml"]
