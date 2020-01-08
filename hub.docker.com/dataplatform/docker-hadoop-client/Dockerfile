FROM dataplatform/docker-hive-base:1.0.2
MAINTAINER MZ

ENV SPARK_VERSION="2.2.0" \
    SPARK_HOME="${MY_APP_DIR}/spark" \
    SPARK_MASTER="local" \
    SPARK_DRIVER_MEMORY="512m" \
    SPARK_EXECUTOR_MEMORY="512m" \
    SQOOP_VERSION="1.4.6" \
    SQOOP_HOME="${MY_APP_DIR}/sqoop" \
    FLINK_VERSION="1.1.3" \
    FLINK_HOME="${MY_APP_DIR}/flink" \
    VERTICA_CLIENT_VERSION="8.0.1"

ENV SPARK_CONF_DIR="${SPARK_HOME}/conf" \
    SPARK_BIN_URL="https://github.com/thaiphamquoc/spark/releases/download/v${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop-2.7.3.tgz" \
    SQOOP_BIN_URL="http://archive.apache.org/dist/sqoop/${SQOOP_VERSION}/sqoop-${SQOOP_VERSION}.bin__hadoop-2.0.4-alpha.tar.gz" \
    FLINK_BIN_URL="http://archive.apache.org/dist/flink/flink-${FLINK_VERSION}/flink-${FLINK_VERSION}-bin-hadoop27-scala_2.10.tgz" \
    VSQL_BIN_URL="https://github.com/thaiphamquoc/vsql/releases/download/v${VERTICA_CLIENT_VERSION}/vertica-client-${VERTICA_CLIENT_VERSION}-0.x86_64.tar.gz"

COPY scripts/build /my_build
RUN /my_build/install.sh && rm -rf /my_build

COPY templates ${MY_TEMPLATE_DIR}
COPY scripts/init ${MY_INIT_DIR}
