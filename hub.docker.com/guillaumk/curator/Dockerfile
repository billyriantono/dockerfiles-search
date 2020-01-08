# Docker Definition for ElasticSearch Curator

FROM python:2.7.8-slim

RUN pip install --quiet elasticsearch-curator==5.4.1

ENTRYPOINT [ "/usr/local/bin/curator" ]
