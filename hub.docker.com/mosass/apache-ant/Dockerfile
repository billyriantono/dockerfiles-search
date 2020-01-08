FROM ticketfly/java:6

WORKDIR /project

ENV ANT_VERSION 1.9.13
ENV ANT_HOME /opt/apache-ant-${ANT_VERSION}

RUN cd /tmp && \
    wget http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar zxf /tmp/apache-ant-${ANT_VERSION}-bin.tar.gz -C /opt/ && \
    rm -f /tmp/*.gz

ENV PATH ${PATH}:${ANT_HOME}/bin