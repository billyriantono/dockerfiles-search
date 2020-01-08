FROM python:3-alpine

WORKDIR /curator
RUN ln -s /curator /root/.curator
RUN pip install elasticsearch-curator==5.5.2

COPY curator.yml /curator
COPY curator-actions.yml /curator

ENV ELASTICSEARCH_HOST=localhost 
ENV INDEX_TO_DELETE=filebeat 
ENV OLDER_THAN_IN_DAYS=30

CMD ["/usr/local/bin/curator","--config","/curator/curator.yml","/curator/curator-actions.yml"]
