FROM donaldsimpson/centos-jdk-devel:latest

MAINTAINER DonaldSimpson<at>GMail<dot>com

RUN  mkdir -p /app/selenium

EXPOSE 4444

ENV GRID_NEW_SESSION_WAIT_TIMEOUT -1
ENV GRID_JETTY_MAX_THREADS -1
ENV GRID_NODE_POLLING  5000
ENV GRID_CLEAN_UP_CYCLE 5000
ENV GRID_TIMEOUT 30000
ENV GRID_BROWSER_TIMEOUT 0
ENV GRID_MAX_SESSION 5
ENV GRID_UNREGISTER_IF_STILL_DOWN_AFTER 30000

COPY generate_config /app/selenium/generate_config
COPY config.json /app/selenium/config.json
COPY entry_point.sh /opt/bin/entry_point.sh
COPY selenium-server-standalone-2.53.1.jar /app/selenium/selenium-server-standalone.jar
COPY tini /bin/
RUN chmod +x /bin/tini
RUN chmod +x /opt/bin/entry_point.sh


### Entry point:
ENTRYPOINT ["/bin/tini", "--", "/opt/bin/entry_point.sh"]
