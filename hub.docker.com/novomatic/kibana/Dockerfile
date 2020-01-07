FROM docker.elastic.co/kibana/kibana:5.4.3

ENV XPACK_GRAPH_ENABLED=false
ENV XPACK_MONITORING_ENABLED=false
ENV XPACK_REPORTING_ENABLED=false
ENV XPACK_SECURITY_ENABLED=false

COPY config/kibana/kibana.yml /usr/share/kibana/config/kibana.yml

RUN kibana-plugin remove x-pack && \
    kibana-plugin install https://github.com/novomatic-tech/keycloak-kibana/releases/download/1.0.1/keycloak-kibana-1.0.1_5.4.3.zip