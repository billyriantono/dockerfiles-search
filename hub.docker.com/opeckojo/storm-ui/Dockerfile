FROM opeckojo/storm:0.9.2-incubating
MAINTAINER opeckojo

RUN /usr/bin/config-supervisord.sh ui

EXPOSE 8080
CMD /usr/bin/start-supervisor.sh

