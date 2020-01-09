# Apache Storm for Ubuntu 14.04
#
# GitHub - http://github.com/dalekurt/docker-storm-supervisor
# Docker Hub - http://hub.docker.com/u/dalekurt/storm-supervisor
# Twitter - http://www.twitter.com/dalekurt

FROM aviata/storm-2
MAINTAINER jmarsh.ext@aviatainc.com "jmarsh.ext@aviatainc.com"

EXPOSE 6700
EXPOSE 6701
EXPOSE 6702
EXPOSE 6703
EXPOSE 8000

COPY resources/storm.yaml /tmp/storm.yaml
RUN cp /tmp/storm.yaml $STORM_HOME/conf/storm.yaml

RUN /usr/bin/config-supervisord.sh supervisor
RUN /usr/bin/config-supervisord.sh logviewer

CMD /usr/bin/start-supervisor.sh
