FROM gocd/gocd-agent-ubuntu-16.04:v19.2.0
MAINTAINER Jemstep Dev <dev@jemstep.com>

# How to install oracle JDK
#  - https://supermarket.chef.io/cookbooks/java
#  - https://docs.docker.com/develop/develop-images/multistage-build/

ENV JAVA_VER 8
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

RUN apt-get -y update && \
        apt-get -y install gnupg2 apt-transport-https openjdk-8-jdk git

RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list && \
        apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 && \
        apt-get -y update && \
        apt-get -y install sbt

RUN git clone https://github.com/jemstep-edward/todo-http4s-doobie.git && \
        chown -R go todo-http4s-doobie

USER go

RUN cd todo-http4s-doobie && \
        sbt test:compile

USER root

RUN cd / && \
        rm -r todo-http4s-doobie
