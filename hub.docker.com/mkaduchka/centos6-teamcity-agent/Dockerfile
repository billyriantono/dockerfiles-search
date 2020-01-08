# docker run -e TEAMCITY_SERVER=http://buildserver:8111 -dt -p 9090:9090 mkaduchka/centos6-teamcity-agent

FROM mkaduchka/centos6-oracle-jdk7

MAINTAINER Mikhail Kaduchka <mikhail.kaduchka@gmail.com>

ADD setup-agent.sh /setup-agent.sh
RUN yum -y install wget unzip zip sudo freetype fontconfig && \
    yum clean all && \
    adduser teamcity

EXPOSE 9090
CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"
