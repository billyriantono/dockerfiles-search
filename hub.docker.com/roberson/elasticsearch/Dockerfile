FROM elasticsearch

MAINTAINER Roberson Faria <roberson.faria@gmail.com>

# Install plugins
RUN bin/elasticsearch-plugin install x-pack --batch


EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
