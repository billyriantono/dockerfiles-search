FROM mvwestendorp/spark-base:latest
ENV ZEPPELIN_HOME=/zeppelin \
    ZEPPELIN_VERSION=0.7.0  \
    Z_VERSION=0.8.2 \
    LOG_TAG="[ZEPPELIN_${Z_VERSION}]:" \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

RUN echo "$LOG_TAG Download Zeppelin binary" && \
    wget -O /tmp/zeppelin-${Z_VERSION}-bin-all.tgz http://archive.apache.org/dist/zeppelin/zeppelin-${Z_VERSION}/zeppelin-${Z_VERSION}-bin-all.tgz && \
    tar -zxvf /tmp/zeppelin-${Z_VERSION}-bin-all.tgz && \
    rm -rf /tmp/zeppelin-${Z_VERSION}-bin-all.tgz && \
    mv /zeppelin-${Z_VERSION}-bin-all ${ZEPPELIN_HOME}

RUN apt-get install curl
RUN  mkdir -p ${ZEPPELIN_HOME}/interpreter/mongodb && \
    curl -SL -o ${ZEPPELIN_HOME}/interpreter/mongodb/zeppelin-mongodb-${ZEPPELIN_VERSION}.jar \
      https://github.com/bbonnin/zeppelin-mongodb-interpreter/releases/download/${ZEPPELIN_VERSION}/zeppelin-mongodb-${ZEPPELIN_VERSION}.zip


RUN wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc |  apt-key add - && \
apt-get install -y apt-transport-https && \
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-4.2.list && \
apt-get update && \
apt-get install -y mongodb-org-shell mongodb-org-tools

WORKDIR ${ZEPPELIN_HOME}
CMD ["bin/zeppelin.sh"]

