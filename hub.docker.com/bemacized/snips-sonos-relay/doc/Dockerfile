FROM ubuntu 
MAINTAINER beisser 

ENV LAST_UPDATE 2015-08-20
ENV ACTIVATOR_VERSION 1.3.5
ENV SBT_VERSION 0.13.8
ENV USER_HOME /home/play

RUN apt-get update

# adding a user 
RUN adduser --disabled-password play
RUN echo 'play ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers
RUN mkdir $USER_HOME/source
RUN chown -R play:play $USER_HOME/source

# apt-get installations 
RUN apt-get install -yqq wget
RUN apt-get install -yqq unzip

# java 8 is required 
#RUN apt-get install -yqq default-jdk

RUN apt-get install -yqq software-properties-common
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -yqq oracle-java8-installer  
RUN apt-get install -yqq oracle-java8-set-default
RUN apt-get install -yqq scala

WORKDIR $USER_HOME

# manual installations 
RUN wget http://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb
RUN dpkg -i sbt-$SBT_VERSION.deb

RUN wget http://downloads.typesafe.com/typesafe-activator/$ACTIVATOR_VERSION/typesafe-activator-$ACTIVATOR_VERSION.zip
RUN unzip -qq typesafe-activator-$ACTIVATOR_VERSION 
RUN mv $USER_HOME/activator-dist-$ACTIVATOR_VERSION $USER_HOME/activator
RUN echo 'export PATH=$PATH:$USER_HOME/activator' >> $USER_HOME/.bashrc
RUN chown -R play:play $USER_HOME/activator

# clean up downloads
RUN rm -rf typesafe-activator-$ACTIVATOR_VERSION.zip
RUN rm -rf sbt-$SBT_VERSION.deb

USER play
VOLUME ["$USER_HOME/source"]
EXPOSE 9000
CMD ["/bin/bash"]
