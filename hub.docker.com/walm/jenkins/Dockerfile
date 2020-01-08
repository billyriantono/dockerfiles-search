FROM walm/java:0.2.0
MAINTAINER Andreas Wålm "andreas@walm.net"

RUN \
  echo "# Installing Jenkins" ;\
  mkdir -p /opt/jenkins ;\
  curl http://ftp-nyc.osuosl.org/pub/jenkins/war/1.568/jenkins.war -o /opt/jenkins/jenkins.war ;\
  \
  echo "# Cleaning up" ;\
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /setup /build

ADD jenkins.sh /etc/service/jenkins/run

EXPOSE 8080
