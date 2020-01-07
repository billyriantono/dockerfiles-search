FROM library/ubuntu:xenial
LABEL maintainer="vasilevici777@gmail.com"

ENV         SCALA_VERSION 2.12.3-1
#ENV         DEBIAN_FRONTEND noninteractive

# User root user to install software
USER root

# Setup play-framework user
RUN groupadd -r play -g 40218
RUN useradd -u 40218 -r -g play -m -d /home/play -s /bin/bash -c "Play Framework user" play
RUN chmod 755 /home/play
RUN passwd -d -u play
#RUN echo "play ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/play
#RUN chmod 0440 /etc/sudoers.d/play
RUN mkdir /home/play/App
RUN chown play:play /home/play/App

# INSTALL OS DEPENDENCIES
RUN apt-get update; apt-get install -y locales build-essential software-properties-common wget curl zip unzip tar
RUN apt-get install -y apt-transport-https apt-utils nano bc

# Set locales
RUN locale-gen en_GB.UTF-8
ENV LANG en_GB.UTF-8
ENV LC_CTYPE en_GB.UTF-8

# INSTALL JDK
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    apt-get install -y oracle-java8-installer

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /var/cache/oracle-jdk8-installer

# INSTALL SCALA
#RUN sudo apt-get remove scala-library scala
RUN wget http://www.scala-lang.org/files/archive/scala-${SCALA_VERSION}.deb
RUN dpkg -i scala-${SCALA_VERSION}.deb
RUN rm scala-${SCALA_VERSION}.deb

# INSTALL SBT
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
RUN apt-get update && apt-get install sbt -y && apt-get clean

# Java env vars
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
RUN echo "export PATH=$PATH:/opt/activator/bin" >> /home/play/.bashrc
RUN echo "export _JAVA_OPTIONS='-Duser.home=/home/play/App'" >> /home/play/.bashrc
#-Dsbt.global.base=/home/play/sbt

# Switch to our user, launch bash
USER play
WORKDIR /home/play
CMD ["/bin/bash"]


# Expose App volume and play ports 9000 default 9999 debug VOLUME "/home/play/App"
EXPOSE 9000
EXPOSE 9999
WORKDIR /home/play/App
