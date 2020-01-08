FROM elasticsearch:2.4.4-alpine
MAINTAINER Andrew Usov "andrew.usov@youdowell.com"

RUN plugin install --batch io.fabric8/elasticsearch-cloud-kubernetes/2.4.4

ADD elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml
ADD docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
