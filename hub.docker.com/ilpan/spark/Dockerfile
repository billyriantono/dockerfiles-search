FROM ilpan/jdk:8-alpine3.8

LABEL maintainer=ilpan:<pna.dev@outlook.com>

ENV SPARK_HOME=/spark \
    SPARK_VERSION=spark-2.3.2 \
    HADOOP_VERSION=without-hadoop \
    MIRROR=https://archive.apache.org/dist/

ENV PATH=${PATH}:${SPARK_HOME}/bin:${SPARK_HOME}/sbin \
    SPARK_DOWURL=${MIRROR}/spark/${SPARK_VERSION}/${SPARK_VERSION}-bin-${HADOOP_VERSION}.tgz

RUN \
    cd /tmp \
    && wget -qc ${SPARK_DOWURL} -O spark.tgz \
    && mkdir -p ${SPARK_HOME} \
    && tar -xzf spark.tgz -C ${SPARK_HOME} --strip-components=1 \
    && rm -rf /tmp/*

WORKDIR ${SPARK_HOME}

COPY ./spark-standalone-env.sh ./conf/spark-env.sh
COPY ./docker-entrypoint.sh ./

EXPOSE 7077 8080 8081

ENTRYPOINT [ "./docker-entrypoint.sh" ]
