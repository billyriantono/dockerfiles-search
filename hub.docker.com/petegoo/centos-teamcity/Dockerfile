
FROM petegoo/centos-jre8

MAINTAINER Peter Goodman <docker@petegoo.com>

# TeamCity data is stored in a volume to facilitate container upgrade
VOLUME  ["/data/teamcity"]
ENV TEAMCITY_DATA_PATH /data/teamcity

# Download and install TeamCity to /opt
RUN yum -y install tar wget unzip sudo python-setuptools
RUN easy_install supervisor
ENV TEAMCITY_PACKAGE TeamCity-9.0.3.tar.gz
ENV TEAMCITY_DOWNLOAD http://download.jetbrains.com/teamcity
RUN wget -qO- $TEAMCITY_DOWNLOAD/$TEAMCITY_PACKAGE | tar xz -C /opt
#ADD TeamCity-9.0.2.tar.gz /opt

EXPOSE 8111

# Setup the build-agent
RUN adduser teamcity

COPY supervisord.conf /etc/supervisord.conf

CMD /usr/bin/supervisord -c /etc/supervisord.conf
