FROM kibana:7.1.1

ENV PATH /usr/share/kibana/bin:$PATH

# Documentation https://www.elastic.co/blog/elasticsearch-docker-plugin-management
RUN kibana-plugin install \
"https://github.com/fbaligand/kibana-enhanced-table/releases/download/v1.2.0/enhanced-table-1.2.0_7.1.1.zip"
