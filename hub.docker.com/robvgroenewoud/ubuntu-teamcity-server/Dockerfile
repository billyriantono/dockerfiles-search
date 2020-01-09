FROM            robvgroenewoud/ubuntu-jdk7

MAINTAINER      Rob van Groenewoud <docker@robvangroenewoud.com>

RUN apt-get -qq update && apt-get -qq -y install tar

VOLUME ["/data/teamcity"]
ENV TEAMCITY_DATA_PATH /data/teamcity

ENV TEAMCITY_PACKAGE TeamCity-9.0.4.tar.gz
ENV TEAMCITY_DOWNLOAD http://download.jetbrains.com/teamcity
RUN wget $TEAMCITY_DOWNLOAD/$TEAMCITY_PACKAGE && \
    tar zxf $TEAMCITY_PACKAGE -C /opt && \
    rm -rf $TEAMCITY_PACKAGE

EXPOSE 8111

CMD ["/opt/TeamCity/bin/teamcity-server.sh", "run"]
