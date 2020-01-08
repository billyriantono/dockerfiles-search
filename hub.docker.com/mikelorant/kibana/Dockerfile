FROM docker.elastic.co/kibana/kibana:6.5.1

RUN export NODE_OPTIONS="--max-old-space-size=1536" && \
    bin/kibana-plugin install https://github.com/pjhampton/kibana-prometheus-exporter/releases/download/6.5.1/kibana-prometheus-exporter-6.5.1.zip
