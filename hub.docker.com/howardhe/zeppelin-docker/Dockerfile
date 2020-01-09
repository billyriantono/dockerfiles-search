FROM java:8
MAINTAINER Howard He "howard.he0329@gmail.com"

ARG VERSION=0.7.1

ENV ZEPPELIN_HOME=/zeppelin
ADD http://mirrors.tuna.tsinghua.edu.cn/apache/zeppelin/zeppelin-${VERSION}/zeppelin-${VERSION}-bin-all.tgz /tmp

RUN cd /tmp && \
    tar zxvf zeppelin-${VERSION}-bin-all.tgz -C /tmp && \
    mv zeppelin-${VERSION}-bin-all ${ZEPPELIN_HOME}

EXPOSE 8080

VOLUME ${ZEPPELIN_HOME}/logs \
    ${ZEPPELIN_HOME}/notebook

WORKDIR ${ZEPPELIN_HOME}
ENTRYPOINT ["bin/zeppelin.sh"]