FROM ubuntu:16.04

MAINTAINER thomas@lauerbach.de

ENV CONTAINER_VERSION 1.0

# ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib

ADD customisation /opt/customisation/
ADD customisation/scripts /opt/scripts/

RUN ["/opt/customisation/init.sh"]

VOLUME /volumes/workspace
VOLUME /volumes/target

CMD ["/bin/bash"]
