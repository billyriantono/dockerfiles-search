FROM binhnv/hive:1.2.1
LABEL maintainer="Binh Van Nguyen<binhnv80@gmail.com>"

ENV SPARK_VERSION="1.6.3" \
    SPARK_HOME="${MY_APP_DIR}/spark" \
    SPARK_MASTER="local" \
    SPARK_DRIVER_MEMORY="512m" \
    SPARK_EXECUTOR_MEMORY="512m" \
    SQOOP_VERSION="1.4.6" \
    SQOOP_HOME="${MY_APP_DIR}/sqoop" \
    FLINK_VERSION="1.1.3" \
    FLINK_HOME="${MY_APP_DIR}/flink" \
    PYENV_HOME="${MY_APP_DIR}/pyenv" \
    HIVE_START_HIVE_SERVER="false"

ENV SPARK_CONF_DIR="${SPARK_HOME}/conf" \
    SPARK_BIN_URL="https://github.com/binhnv/spark-binaries/releases/download/v${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop-${HD_VERSION}.tgz" \
    SQOOP_BIN_URL="http://archive.apache.org/dist/sqoop/${SQOOP_VERSION}/sqoop-${SQOOP_VERSION}.bin__hadoop-2.0.4-alpha.tar.gz" \
    FLINK_BIN_URL="http://archive.apache.org/dist/flink/flink-1.1.3/flink-1.1.3-bin-hadoop27-scala_2.10.tgz" \
    PYENV_ROOT="${PYENV_HOME}" \
    PATH="${PYENV_HOME}/shims:${PYENV_HOME}/bin:${PATH}"
COPY files/share/scripts/build /my_build
RUN chmod +x /my_build/install.sh && \
    /my_build/install.sh && \
    rm -rf /my_build


COPY files/share/templates ${MY_TEMPLATE_DIR}/

