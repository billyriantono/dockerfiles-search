FROM picoded/ubuntu-openjdk-8-jdk


RUN \
  curl -L -o sbt-1.2.8.deb http://dl.bintray.com/sbt/debian/sbt-1.2.8.deb && \
  dpkg -i sbt-1.2.8.deb && \
  rm sbt-1.2.8.deb && \
  apt-get update && \
  apt-get install sbt && \
  sbt sbtVersion &&\
  apt-get install -y sfst && \
  dpkg --listfiles sfst

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales

RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8

ENV SBT_OPTS="-Xmx2G -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xss2M"


RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y sfst


RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y git

RUN apt-get install -y bash-completion

CMD /bin/bash
