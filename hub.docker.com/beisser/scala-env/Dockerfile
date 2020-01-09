
FROM ubuntu
MAINTAINER beisser

ENV LAST_UPDATE 2015-07-28
ENV SBT_VERSION 0.13.8

RUN apt-get update

# install jdk
RUN apt-get install -yqq default-jdk

# install scala
RUN apt-get install -yqq scala

# install sbt
RUN apt-get install -yqq wget
RUN wget http://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb
RUN dpkg -i sbt-$SBT_VERSION.deb

RUN mkdir -p /home/scala-user/scala
WORKDIR /home/scala-user/scala

CMD ["/bin/bash"] 