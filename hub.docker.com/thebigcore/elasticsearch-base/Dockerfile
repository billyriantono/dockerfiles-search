FROM elasticsearch:latest

RUN plugin install elasticsearch/marvel/latest
RUN plugin install lmenezes/elasticsearch-kopf/latest
RUN plugin install polyfractal/elasticsearch-segmentspy/latest
RUN plugin install xyu/elasticsearch-whatson/latest
RUN plugin install royrusso/elasticsearch-HQ

COPY docker-entrypoint.sh /
RUN  chmod +x ./docker-entrypoint.sh


