# leoontheearth/elasticsearch:5.5
# https://www.docker.elastic.co/
FROM docker.elastic.co/elasticsearch/elasticsearch:5.5.3
MAINTAINER Leo "leo.on.the.earth@gmail.com"

RUN elasticsearch-plugin remove x-pack --purge

USER elasticsearch

CMD ["/bin/bash", "bin/es-docker"]
