FROM elasticsearch:5.5.0
MAINTAINER Gururaj Jeerge <gururaj@orangepro.in>

RUN bin/elasticsearch-plugin install x-pack --batch

EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
