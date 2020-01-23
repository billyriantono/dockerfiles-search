# Apache Storm UI for Ubuntu 14.04

FROM aviata/storm-2

MAINTAINER jmarsh.ext@aviatainc.com "jmarsh.ext@aviatainc.com"

COPY resources/storm.yaml /tmp/storm.yaml
RUN cp /tmp/storm.yaml $STORM_HOME/conf/storm.yaml

RUN /usr/bin/config-supervisord.sh ui

EXPOSE 8080
CMD /usr/bin/start-supervisor.sh
