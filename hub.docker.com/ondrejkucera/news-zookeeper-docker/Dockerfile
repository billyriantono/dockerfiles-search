FROM openjdk:8u151-jre-stretch
MAINTAINER Ondrej Kucera

ENV ZOOKEEPER_VERSION     3.4.11
ENV ZOOKEEPER_HOME        /usr/local/zookeeper-${ZOOKEEPER_VERSION}
ENV ZOOKEEPER_DATA_DIR    /zookeeper
ENV ZOOKEEPER_DATALOG_DIR /var/log/zookeeper
ENV ZOOKEEPER_CONF_DIR    ${ZOOKEEPER_HOME}/conf

ENV PATH       $JAVA_HOME/bin:$ZOOKEEPER_HOME/bin:$PATH

RUN set -x && \
    apt-get -yqq update && \ 
    mirror_url=$( \
        wget -q -O - "http://www.apache.org/dyn/closer.cgi/?as_json=1" \
        | grep "preferred" \
        | sed -n 's#.*"\(http://*[^"]*\)".*#\1#p' \
        ) && \
    wget -q -O - ${mirror_url}zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz \
        | tar -xzf - -C /usr/local && \
    ## user/dir/permmsion
    adduser --disabled-login --disabled-password -shell /usr/sbin/nologin -uid 1000 --gecos docker docker && \
    adduser --disabled-login --disabled-password -shell /usr/sbin/nologin --gecos zookeeper zookeeper && \
    mkdir -p \
        ${ZOOKEEPER_DATA_DIR} \
        ${ZOOKEEPER_DATALOG_DIR} && \
    chown -R zookeeper:zookeeper \
        ${ZOOKEEPER_HOME} \
        ${ZOOKEEPER_DATA_DIR} \
        ${ZOOKEEPER_DATALOG_DIR} && \
    ## remove unnecessary files
    rm -rf ${ZOOKEEPER_HOME}/src ${ZOOKEEPER_HOME}/docs

COPY entrypoint.sh /usr/local/bin/ 
COPY zoo.cfg       ${ZOOKEEPER_CONF_DIR}/

VOLUME ["${ZOOKEEPER_DATA_DIR}", "${ZOOKEEPER_DATALOG_DIR}"]

WORKDIR ${ZOOKEEPER_HOME}

EXPOSE 2181 2888 3888

ENTRYPOINT ["entrypoint.sh"]
CMD ["-server", "1", "1" ]
