FROM dataplatform/hive
MAINTAINER Binh Van Nguyen

ENV SPARK_VERSION=1.6.0

ARG SPARK_MASTER=local
ARG SPARK_DRIVER_MEMORY=512m
ARG SPARK_EXECUTOR_MEMORY=512m
ARG SPARK_HOME=/usr/local/spark
ARG SPARK_SOURCE=/tmp/spark/src
ARG SPARK_SRC_URL=https://github.com/apache/spark/archive/v${SPARK_VERSION}.tar.gz

ENV SPARK_MASTER=${SPARK_MASTER} \
    SPARK_DRIVER_MEMORY=${SPARK_DRIVER_MEMORY} \
    SPARK_EXECUTOR_MEMORY=${SPARK_EXECUTOR_MEMORY} \
    SPARK_CONF_DIR=${SPARK_HOME}/conf \
    SPARK_CONF_TPL_DIR=${SPARK_HOME}/templates

RUN mkdir -p ${SPARK_SOURCE} \
    && curl -sL ${SPARK_SRC_URL} | tar -xz -C ${SPARK_SOURCE} --strip-component=1 \
    && cd ${SPARK_SOURCE} \
    && ./make-distribution.sh -Phadoop-provided -Phive -Phive-thriftserver -Pyarn \
    && rm -rf ${SPARK_HOME} && mv dist ${SPARK_HOME} && rm -rf ${SPARK_SOURCE} \
    && rm -rf ${USER_HOME}/.m2

ARG PYHOCON_VERSION=0.3.30
ARG KAFKA_PYTHON_VERSION=1.2.3
ARG MYSQL_PYTHON_VERSION=1.2.5
ARG VERTICA_PYTHON_VERSION=0.6.5
ARG ISO8601_VERSION=0.1.11

RUN apt-get install -y python-pip python-dev libsasl2-dev libmysqlclient-dev rsync \
    && pip install pyhocon==${PYHOCON_VERSION} impyla snakebite cheetah redis \
    && pip install SQLAlchemy MySQL-python==${MYSQL_PYTHON_VERSION} \
    && pip install kafka-python==${KAFKA_PYTHON_VERSION} \
    && pip install vertica-python==${VERTICA_PYTHON_VERSION} \
    && pip install iso8601==${ISO8601_VERSION} \
    && apt-get clean

COPY templates/spark ${SPARK_CONF_TPL_DIR}

CMD dhcmd config \
    # Need ssh to run ingestion
    && service ssh restart \
    && dockerize \
        -template "${SPARK_CONF_TPL_DIR}/spark-env.sh.tmpl:${SPARK_CONF_DIR}/spark-env.sh" \
        -template "${SPARK_CONF_TPL_DIR}/spark-defaults.conf.tmpl:${SPARK_CONF_DIR}/spark-defaults.conf" \
    && tail -f /dev/null
