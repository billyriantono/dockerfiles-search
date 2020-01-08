FROM selenium/standalone-firefox:3.10.0

USER root
RUN apt-get update &&  apt-get -y install python && apt-get clean

COPY http_server.sh /opt/bin/
USER seluser
CMD ["/opt/bin/http_server.sh"]
EXPOSE 8080 4444