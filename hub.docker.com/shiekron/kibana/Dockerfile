FROM dockerfile/java:oracle-java7

# info
MAINTAINER Joe Ortiz version: 0.1

RUN wget https://download.elasticsearch.org/kibana/kibana/kibana-4.0.0-BETA2.tar.gz -O /tmp/kibana.tar.gz && \
    tar zxf /tmp/kibana.tar.gz -C /data --strip-components=1 && \
    rm /tmp/kibana.tar.gz

EXPOSE 5601
CMD ["/data/bin/kibana"]
