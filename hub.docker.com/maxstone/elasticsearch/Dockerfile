FROM elasticsearch
MAINTAINER rainer@nts.at

RUN /usr/share/elasticsearch/bin/plugin install license
RUN /usr/share/elasticsearch/bin/plugin install marvel-agent

EXPOSE 9200 9300
