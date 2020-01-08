FROM nesneros/elasticsearch-auth:5.3.0

USER root
RUN echo "xpack.security.enabled: false" >> /usr/share/elasticsearch/config/elasticsearch.yml
USER elasticsearch
