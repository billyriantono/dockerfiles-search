FROM binhnv/openjdk:8
LABEL maintainer="Binh Van Nguyen<binhnv80@gmail.com>"

# The following environment variables are required at runtime unless user uses
# his/her own custom configuration template and that template doesn't require
# these variables
#
# - KAFKA_ZOOKEEPER_CONNECT: Zookeeper connection string. Check Kafka documentation for the format


ENV KAFKA_VERSION="0.8.2.1" \
    KAFKA_SCALA_VERSION="2.10" \
    KAFKA_HOME="${MY_APP_DIR}/kafka" \
    KAFKA_LOG_DIR="${MY_APP_LOG_DIR}/kafka" \
    KAFKA_DATA_DIR="${MY_APP_DATA_DIR}/kafka" \
    KAFKA_HEAP_OPTS="-Xmx128m -Xms64m"

WORKDIR ${KAFKA_HOME}
COPY files/share/scripts/build /my_build
RUN chmod +x /my_build/install.sh && \
    /my_build/install.sh && \
    rm -rf /my_build


COPY files/share/services ${MY_SERVICE_DIR}/
COPY files/0.8/templates ${MY_TEMPLATE_DIR}/
COPY files/0.8/scripts/init ${MY_INIT_DIR}/

