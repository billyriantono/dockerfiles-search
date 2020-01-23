FROM busybox

COPY jmx_prometheus_javaagent-0.12.0.jar.md5 /
RUN wget https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.12.0/jmx_prometheus_javaagent-0.12.0.jar && \
    md5sum -c jmx_prometheus_javaagent-0.12.0.jar.md5
