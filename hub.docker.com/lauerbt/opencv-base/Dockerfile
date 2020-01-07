FROM ubuntu:16.04

MAINTAINER thomas@lauerbach.de

ENV CONTAINER_VERSION 1.0
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib

ADD customisation /opt/customisation/

USER root
RUN ["/opt/customisation/root-init.sh"]

USER opencv
RUN ["/opt/customisation/opencv-build.sh"]
ADD deployments/test /home/opencv/test

VOLUME /volumes/video

CMD ["/bin/bash"]
