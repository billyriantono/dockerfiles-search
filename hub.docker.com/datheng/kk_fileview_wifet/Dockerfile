FROM dataplatform/docker-base:1.0.2
MAINTAINER MZ

ENV KAFKA_VERSION="0.10.2.1" \
    KAFKA_HOME="${MY_APP_DIR}/kafka" \
    KAFKA_LOG_DIR="${MY_APP_LOG_DIR}/kafka" \
    KAFKA_DATA_DIR="${MY_APP_DATA_DIR}/kafka" \
    KAFKA_INITIAL_TOPICS="" \
    KAFKA_ADVERTISED_HOST_NAME="kafka" \
    KAFKA_SERVICE_NAME="kafka" \
    KAFKA_SECURITY_PROTOCOL="SASL_PLAINTEXT" \
    KAFKA_SECURITY_MECHANISM="GSSAPI" \
    KAFKA_OPTS="-Djava.security.auth.login.config=/usr/local/kafka/config/jaas.conf" \
    KAFKA_LOG4J_OPTS="-Dkafka.logs.dir=${MY_APP_LOG_DIR}/kafka"

# User need to provide the following environment variable
# - ZOOKEEPER_HOST: Zookeeper hostname in format of "zk1","zk2"

WORKDIR ${KAFKA_HOME}

COPY scripts/build /my_build
RUN /my_build/install.sh && rm -rf /my_build

COPY services ${MY_SERVICE_DIR}
COPY templates ${MY_TEMPLATE_DIR}
COPY config/jaas.conf ${KAFKA_HOME}/config/jaas.conf
COPY scripts/startup ${MY_STARTUP_DIR}
COPY files/kafka-graphite-1.0.4.jar ${KAFKA_HOME}/libs
