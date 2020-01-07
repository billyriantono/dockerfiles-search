FROM openjdk:8u212-b04-jdk-stretch

ENV DAEMON_RUN=true
ENV SPARK_VERSION=2.4.4
ENV HADOOP_VERSION=2.7
ENV SCALA_VERSION=2.12.4
ENV SCALA_HOME=/usr/share/scala
ENV SPARK_HOME=/spark

ENV SPARK_MASTER_HOST="spark-master"
ENV SPARK_MASTER_PORT=7077
ENV SPARK_WEBUI_PORT=8080
ENV SPARK_LOG=/spark/logs
ENV PYTHONHASHSEED 1

# Update & Install packages
RUN apt-get update && \
    apt-get install -y curl vim wget software-properties-common ssh net-tools ca-certificates jq

# Install Scala
RUN cd "/tmp" && \
    wget --no-verbose "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
    tar xzf "scala-${SCALA_VERSION}.tgz" && \
    mkdir "${SCALA_HOME}" && \
    rm "/tmp/scala-${SCALA_VERSION}/bin/"*.bat && \
    mv "/tmp/scala-${SCALA_VERSION}/bin" "/tmp/scala-${SCALA_VERSION}/lib" "${SCALA_HOME}" && \
    ln -s "${SCALA_HOME}/bin/"* "/usr/bin/" && \
    rm -rf "/tmp/"*

# Install Python3
RUN apt-get install -y python3 python3-pip python3-numpy python3-matplotlib python3-scipy python3-pandas python3-simpy && \
    update-alternatives --install "/usr/bin/python" "python" "$(which python3)" 1

# Install Spark
RUN wget --no-verbose http://apache.mirror.iphh.net/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    tar xzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} "${SPARK_HOME}" && \
    rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz


EXPOSE 8080 7077 6066

COPY root /

CMD ["/bin/bash", "/start-spark.sh"]
