# docker run -dt -p 8111:8111 mkaduchka/centos6-teamcity-server

FROM mkaduchka/centos6-oracle-jdk7

MAINTAINER Mikhail Kaduchka <mikhail.kaduchka@gmail.com>

# TeamCity data is stored in a volume to facilitate container upgrade
VOLUME  ["/data/teamcity"]
ENV TEAMCITY_DATA_PATH /data/teamcity

ENV TEAMCITY_PACKAGE TeamCity-9.1.7.tar.gz
ENV TEAMCITY_DOWNLOAD http://download.jetbrains.com/teamcity

# Download and install TeamCity to /opt
RUN yum -y install tar wget && \
    wget $TEAMCITY_DOWNLOAD/$TEAMCITY_PACKAGE && \
    tar zxf $TEAMCITY_PACKAGE -C /opt && \
    rm -rf $TEAMCITY_PACKAGE && \
    yum -y remove wget tar

EXPOSE 8111
CMD ["/opt/TeamCity/bin/teamcity-server.sh", "run"]
