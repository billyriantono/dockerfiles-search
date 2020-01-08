FROM pdouble16/autopilotpattern-base:1.4.0
FROM pdouble16/kafkacat:1.3.1-r1

FROM maven:3-jdk-8
RUN git clone -b replica-adjust https://github.com/double16/doctorkafka.git
RUN cd doctorkafka && mvn package -pl kafkastats,drkafka -am -Dmaven.test.skip=true >/dev/null

FROM wurstmeister/kafka:2.11-2.0.0

ARG SOURCE_REF
ARG SOURCE_TYPE
ARG DOCKERFILE_PATH

# libcrypto1.0 libssl1.0 is required for kafkacat
RUN apk add --no-cache nginx jq curl procps libcrypto1.0 libssl1.0 &&\
    rm -rf /tmp/* /var/cache/apk/* &&\
    JMX_PROM_VER=0.3.1 &&\
    mkdir /opt/prometheus &&\
    wget -O /opt/prometheus/jmx_prometheus_javaagent.jar https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JMX_PROM_VER}/jmx_prometheus_javaagent-${JMX_PROM_VER}.jar &&\
    wget -O /opt/prometheus/jmx_prometheus_httpserver-jar-with-dependencies.jar https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/${JMX_PROM_VER}/jmx_prometheus_httpserver-${JMX_PROM_VER}-jar-with-dependencies.jar &&\
    mkdir /run/nginx /var/lib/nginx/cache

RUN mkdir -p /var/lib/consul /etc/consul /opt/doctorkafka
COPY --from=0 /usr/local/bin/* /usr/local/bin/
COPY --from=0 /etc/consul/* /etc/consul/
COPY --from=1 /usr/local/bin/kafkacat /usr/bin/kafkacat
COPY --from=2 /doctorkafka/drkafka/target/doctorkafka-0.2.3-jar-with-dependencies.jar /opt/doctorkafka/doctorkafka-jar-with-dependencies.jar
COPY --from=2 /doctorkafka/kafkastats/target/kafkastats-0.2.3-jar-with-dependencies.jar /opt/doctorkafka/kafkastats-jar-with-dependencies.jar
COPY opt/doctorkafka/* /opt/doctorkafka/
RUN echo "enable_script_checks = true" >> /etc/consul/consul.hcl.orig

# Fix for create-topics.sh to wait for enough brokers
COPY opt/kafka/bin/create-topics.sh /usr/bin/create-topics.sh 

ENV _JAVA_OPTIONS="-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap" \
    KAFKA_JMX_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.rmi.port=5000" \
    JMX_PORT="5000" \
    HOSTNAME_COMMAND="/opt/kafka/bin/kafka-manage hostname" \
    PORT_COMMAND="/opt/kafka/bin/kafka-manage outsideport" \
    RACK_COMMAND="/opt/kafka/bin/kafka-manage rack" \
    KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
    KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://:9092,OUTSIDE://_{HOSTNAME_COMMAND}:_{PORT_COMMAND},BROKER://:9093 \
    KAFKA_LISTENERS=PLAINTEXT://:9092,OUTSIDE://:9094,BROKER://:9093 \
    KAFKA_LISTENER_SECURITY_PROTOCOL_MAP="PLAINTEXT:PLAINTEXT,OUTSIDE:SSL,BROKER:PLAINTEXT" \
    KAFKA_INTER_BROKER_LISTENER_NAME=BROKER \
    KAFKA_INTER_BROKER_PORT=9093 \
    CONTAINERPILOT="/etc/containerpilot.json5"

COPY nginx.conf /etc/nginx/

COPY kafka-prometheus.yml /opt/prometheus/
COPY opt/kafka/bin/* /opt/kafka/bin/
COPY opt/kafka/bin/ec2metadata /usr/bin/ec2metadata

COPY etc/containerpilot.json5 ${CONTAINERPILOT}

CMD ["/usr/local/bin/containerpilot"]

EXPOSE 9092 9093 9094 9090 5000 8301 8301/udp 8302 8302/udp 8090
HEALTHCHECK --interval=120s --timeout=10s --retries=3 CMD /usr/bin/test "$(cat /var/run/kafka-healthcheck)" = "0" || exit 1

LABEL maintainer="Patrick Double (pat@patdouble.com)" \
      org.label-schema.license="MPL-2.0" \
      org.label-schema.vendor="https://bitbucket.org/double16" \
      org.label-schema.name="Autopilot Pattern for Kafka Broker with full Prometheus Telemetry" \
      org.label-schema.url="https://bitbucket.org/double16/autopilotpattern-kafka" \
      org.label-schema.docker.dockerfile="${DOCKERFILE_PATH}/Dockerfile" \
      org.label-schema.vcs-ref=$SOURCE_REF \
      org.label-schema.vcs-type=$SOURCE_TYPE \
      org.label-schema.vcs-url="https://bitbucket.org/double16/autopilotpattern-kafka.git"
