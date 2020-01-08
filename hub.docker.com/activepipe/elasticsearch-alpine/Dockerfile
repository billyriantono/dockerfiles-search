FROM library/elasticsearch:2.4.6-alpine

RUN bin/plugin install delete-by-query

COPY elasticsearch.yml ./config/elasticsearch.yml
