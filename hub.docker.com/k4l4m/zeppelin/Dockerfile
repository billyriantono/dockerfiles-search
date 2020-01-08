FROM k4l4m/spark

ARG ZEPPELIN_VERSION=0.7.1

ENV ZEPPELIN_HOME="/opt/zeppelin"
ENV PATH="${ZEPPELIN_HOME}/bin:${PATH}"

ENV MESOS_NATIVE_JAVA_LIBRARY="/usr/local/lib/libmesos.so"


WORKDIR /opt

ADD http://apache.lauf-forum.at/zeppelin/zeppelin-${ZEPPELIN_VERSION}/zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz .
RUN tar xzvf zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz \
    && rm zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz \
    && mv zeppelin-${ZEPPELIN_VERSION}-bin-all zeppelin

WORKDIR /opt/zeppelin

CMD zeppelin-daemon.sh start && tail -F ${ZEPPELIN_HOME}/logs/*.log