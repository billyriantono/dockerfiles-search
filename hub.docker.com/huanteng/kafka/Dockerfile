FROM bitnami/kafka:1.0.0-r5

RUN curl --silent --remote-time --output /opt/bitnami/kafka/libs/jmx_prometheus_javaagent-0.3.1.jar \
      https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.3.1/jmx_prometheus_javaagent-0.3.1.jar \
      && chmod 0644 /opt/bitnami/kafka/libs/jmx_prometheus_javaagent-0.3.1.jar
COPY run.sh /run.sh
