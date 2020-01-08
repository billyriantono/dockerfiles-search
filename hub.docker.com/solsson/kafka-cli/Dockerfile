FROM solsson/kafka:latest as kafka

FROM oracle/graalvm-ce:19.0.2@sha256:684ba0e822eb2f569ffef96abb315f5b66550c4e7d5d38ad6570b72f0ce06c35 as graal-dist
RUN gu install native-image

RUN yum -y install snappy libzstd lz4 && yum clean all

RUN ls /opt/graalvm-ce-19.0.2/jre/lib/amd64/libnative-image-agent.so

WORKDIR /opt/kafka
COPY --from=kafka /opt/kafka .
COPY --from=kafka /usr/local/bin/docker-help /usr/local/bin/docker-help

ENV KAFKA_OPTS="-agentlib:native-image-agent=config-merge-dir=/graalvm-native-config-dir"
RUN mkdir /graalvm-native-config-dir \
  && echo '[]' > /graalvm-native-config-dir/jni-config.json \
  && echo '[]' > /graalvm-native-config-dir/reflect-config.json \
  && echo '[]' > /graalvm-native-config-dir/proxy-config.json \
  && echo '{}' > /graalvm-native-config-dir/resource-config.json

ENTRYPOINT ["docker-help"]
