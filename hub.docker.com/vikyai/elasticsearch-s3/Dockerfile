# docker build -t vikyai/elasticsearch-s3:7.4.1 .
# docker push vikyai/elasticsearch-s3:7.4.1

ARG ELASTICSEARCH_VERSION=7.4.1
FROM elasticsearch:${ELASTICSEARCH_VERSION}

RUN bin/elasticsearch-plugin install -b repository-s3
