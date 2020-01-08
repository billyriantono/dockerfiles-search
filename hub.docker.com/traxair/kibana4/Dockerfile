FROM traxair/oracle-java7:latest

ADD entrypoint.sh /opt/entrypoint.sh

RUN apt-get update && \
    apt-get install -y ca-certificates wget && \
    cd /opt && \
    wget https://download.elasticsearch.org/kibana/kibana/kibana-4.0.0-linux-x64.tar.gz && \
    tar -xzvf ./kibana-4.0.0-linux-x64.tar.gz && \
    mv kibana-4.0.0-linux-x64 kibana && \
    rm kibana-4.0.0-linux-x64.tar.gz && \
    apt-get clean && \
    apt-get purge && \
    chmod +x /opt/entrypoint.sh

ADD conf/kibana.yml /opt/kibana/config/kibana.yml

ENTRYPOINT ["/opt/entrypoint.sh"]