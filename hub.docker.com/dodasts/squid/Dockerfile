FROM dodasts/centos:7-grid
LABEL maintainer="diego.ciangottini@pg.infn.it"
LABEL Version=1.0

RUN rpm -Uvh http://frontier.cern.ch/dist/rpms/RPMS/noarch/frontier-release-1.1-1.noarch.rpm

RUN yum install -y frontier-squid

COPY scripts/launch_squid.sh /launch_squid.sh

RUN chmod +x /launch_squid.sh

ENTRYPOINT [ "/etc/init.d/frontier-squid", "start" ]
