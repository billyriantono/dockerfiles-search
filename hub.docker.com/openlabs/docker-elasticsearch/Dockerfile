FROM dockerfile/elasticsearch
MAINTAINER Sharoon Thomas <sharoon.thomas@openlabs.co.in>

ADD nicknames.txt /config/synonyms/nicknames.txt
ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml

# Install the required plugins
RUN /elasticsearch/bin/plugin -install elasticsearch/elasticsearch-analysis-phonetic/2.3.0
RUN /elasticsearch/bin/plugin -install polyfractal/elasticsearch-inquisitor
RUN /elasticsearch/bin/plugin -install elasticsearch/elasticsearch-cloud-aws/2.3.0
RUN /elasticsearch/bin/plugin -install mobz/elasticsearch-head
RUN /elasticsearch/bin/plugin -install royrusso/elasticsearch-HQ

EXPOSE 9200 9300
ENTRYPOINT ["/elasticsearch/bin/elasticsearch"]
CMD ["-Des.config=/elasticsearch/config/elasticsearch.yml"]
