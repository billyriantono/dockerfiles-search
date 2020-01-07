FROM srdc/java:oraclejdk-8
MAINTAINER SRDC Corp. <technical@srdc.com.tr>

ARG kafka_version=0.10.1.1
ARG scala_version=2.11
COPY start-kafka.sh /usr/bin/start-kafka.sh

RUN \
       mkdir /kafka && curl http://www-eu.apache.org/dist/kafka/$kafka_version/kafka_$scala_version-$kafka_version.tgz | tar xvzf - -C /kafka --strip-components=1 && \
       sed -i 's/#delete.topic.enable/delete.topic.enable/g' /kafka/config/server.properties && \
       sed -i 's/#listeners=PLAINTEXT:\/\/:9092/listeners=PLAINTEXT:\/\/0.0.0.0:9092/g' /kafka/config/server.properties && \
       chmod a+x /usr/bin/start-kafka.sh


CMD ["start-kafka.sh"]
