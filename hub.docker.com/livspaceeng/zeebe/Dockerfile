# Bundle Hazelcast with Zeebe

FROM camunda/zeebe:0.22.0-alpha2
ADD https://github.com/zeebe-io/zeebe-hazelcast-exporter/releases/download/0.6.0/zeebe-hazelcast-exporter-0.6.0-jar-with-dependencies.jar /usr/local/zeebe/lib/zeebe-hazelcast-exporter.jar
RUN chmod 644 /usr/local/zeebe/lib/zeebe-hazelcast-exporter.jar
