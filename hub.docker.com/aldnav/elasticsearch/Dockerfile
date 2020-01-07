FROM docker.elastic.co/elasticsearch/elasticsearch:6.4.2
RUN bin/elasticsearch-keystore create
RUN chown -R elasticsearch:elasticsearch /usr/share/elasticsearch/config/
RUN chmod g+ws /usr/share/elasticsearch
RUN chmod 755 /usr/share/elasticsearch/config/elasticsearch.keystore
RUN yes | bin/elasticsearch-plugin install repository-s3