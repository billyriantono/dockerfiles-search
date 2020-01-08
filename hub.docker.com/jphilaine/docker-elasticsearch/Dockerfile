FROM elasticsearch:latest

RUN /usr/share/elasticsearch/bin/plugin install license
RUN /usr/share/elasticsearch/bin/plugin install marvel-agent
RUN chown -R elasticsearch:elasticsearch /usr/share/elasticsearch
