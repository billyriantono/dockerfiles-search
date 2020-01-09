FROM tonyzhang/ioc-base:jessie

WORKDIR /root

ENV ARCHIVERAP "archappl_v0.0.1_SNAPSHOT_22-June-2017T14-44-56.tar.gz"
ENV TOMCAT "apache-tomcat-7.0.81.tar.gz"

ADD http://mirror.cogentco.com/pub/apache/tomcat/tomcat-7/v7.0.81/bin/$TOMCAT .
ADD https://github.com/slacmshankar/epicsarchiverap/releases/download/v0.0.1_SNAPSHOT_22-June-2017/$ARCHIVERAP .

COPY jdk-8u144-linux-x64.tar.gz .

RUN tar zxf $ARCHIVERAP && \
    tar zxf jdk-8u144-linux-x64.tar.gz && \
    rm -rf jdk-8u144-linux-x64.tar.gz $ARCHIVERAP

ENV EPICS_CA_AUTO_ADDR_LIST "NO"
ENV EPICS_CA_ADDR_LIST "172.17.255.255"
ENV PATH "/root/jdk1.8.0_144/bin":$PATH

EXPOSE 17665
CMD ["/root/quickstart.sh", "apache-tomcat-7.0.81.tar.gz"]
