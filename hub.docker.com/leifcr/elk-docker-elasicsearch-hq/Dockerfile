FROM sebp/elk
ENV KIBANA_HOME /opt/kibana
ENV ES_HOME /usr/share/elasticsearch
WORKDIR ${ES_HOME}
RUN gosu elasticsearch bin/plugin install royrusso/elasticsearch-HQ
RUN gosu elasticsearch bin/plugin install polyfractal/elasticsearch-inquisitor
RUN gosu elasticsearch bin/plugin install mobz/elasticsearch-head
WORKDIR ${KIBANA_HOME}
RUN gosu kibana bin/kibana plugin --install elastic/sense
