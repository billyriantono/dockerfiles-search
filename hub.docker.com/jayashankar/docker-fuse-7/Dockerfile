FROM jayashankar/centos-jdk:latest 

MAINTAINER Jayashankar <jshankarc1@gmail.com>

ENV FUSE_VERSION 7.0.0.fuse-000199

ENV FUSE_USER fuse
ENV FUSE_UID 8181
ENV JAVA_HOME /usr/lib/jvm/java 
ENV JAVA_MAX_MEM 256m
ENV FUSE_EXEC exec


COPY install.sh /opt/fuse/install.sh
RUN  /opt/fuse/install.sh

EXPOSE 8181 8101 1099 44444

VOLUME /opt/fuse/etc
VOLUME /opt/fuse/data
VOLUME /opt/fuse/deploy

WORKDIR /opt/fuse/

USER $FUSE_USER

CMD ["/opt/fuse/bin/fuse", "run"]

