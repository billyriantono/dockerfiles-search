FROM debian:stretch

ARG SCALA_VERSION
ENV SCALA_VERSION ${SCALA_VERSION:-2.13.0}
ARG SBT_VERSION
ENV SBT_VERSION ${SBT_VERSION:-1.2.8}
ARG KAFKA_MANAGER_VERSION
ENV KAFKA_MANAGER_VERSION ${KAFKA_MANAGER_VERSION:-2.0.0.2}
ARG KAFKA_MANAGER_REVISION
ENV KAFKA_MANAGER_REVISION ${KAFKA_MANAGER_REVISION:-9f82c0f}

RUN apt-get update \
  && apt-get install -y openjdk-8-jdk wget gnupg2 unzip apt-transport-https

RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list \
  && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 \
  && apt-get update \
  && apt-get install -y sbt \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /tmp
RUN pwd \
  && wget https://api.github.com/repos/yahoo/kafka-manager/tarball/${KAFKA_MANAGER_VERSION} -O - | tar -xz \
  && cd yahoo-kafka-manager-${KAFKA_MANAGER_REVISION} \
  && sbt clean dist \
  && unzip -d /opt/ /tmp/yahoo-kafka-manager-${KAFKA_MANAGER_REVISION}/target/universal/kafka-manager-${KAFKA_MANAGER_VERSION}.zip \
  && mv /opt/kafka-manager-${KAFKA_MANAGER_VERSION} /opt/kafka-manager

WORKDIR /opt 

ENTRYPOINT [ "./kafka-manager/bin/kafka-manager" ]