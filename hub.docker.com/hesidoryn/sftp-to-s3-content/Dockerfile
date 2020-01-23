FROM elasticsearch:1.6

ADD ./elasticsearch.yml /data/

ENTRYPOINT ["elasticsearch", "-Des.config=/data/elasticsearch.yml"]
